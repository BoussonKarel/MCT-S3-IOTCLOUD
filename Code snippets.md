# IoT Cloud - Handy code
## Python: HTTP requests
**GET**
```python
import requests

url = "..."
ret = requests.get(url)
print(ret.status_code)
print(ret.text)
```
> 200
> "Hello again Python"

**POST**
```python
import requests
import json

payload = { 'getal1': 4, 'getal2': 2 }
url = "..."
json = json.dumps(payload)
ret = requests.post(url, data=json)
print(ret.status_code)
print(ret.text)
```
> 200
> {"quotient": 2}

**JSON inladen en opvragen**
```python
jsonstring = ret.text
obj = json.loads(jsonstring)
print("Het resultaat is {}".format(obj["quotient"]))
```

## Azure Functions - basics
Sending information in the **body** using **POST**
```csharp
[FunctionName("HelloWorld")] // azure function name
public static async Task<IActionResult> HelloWorld( // c# function name
            [HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "helloworld")] HttpRequest req,
            ILogger log)

{
	log.LogInformation("C# HTTP trigger function processed a request.");

	// Body (bytes) inlezen en omvormen naar een json string die je terugkrijgt
	string requestBody = await new 	StreamReader(req.Body).ReadToEndAsync();
	// Declareren een variabele v type SomRequest
	// Roepen JsonConvert.DeserializeObject
	// Parameter: jsonString
	// Omzetten naar een C# object, welk? Geef je mee tussen <>
	SomRequest somRequest = JsonConvert.DeserializeObject<SomRequest>(requestBody);

	// OkObjectResult gaat het automatisch serializen
	return new OkObjectResult(new SomResponse() { Resultaat = somRequest.Getal1 + somRequest.Getal2 });
}
```
Parameters meegeven in de URL
```csharp
[FunctionName("HelloWorld")] // azure function name
public static async Task<IActionResult> HelloWorld( // c# function name
	[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "helloworld/{parameterNaam}")] HttpRequest req,
	string parameterNaam,
	ILogger log)
{
	// Nu kan je parameterNaam gebruiken
	return new OkObjectResult("");
}
```
## SQL Server
### Instellen van de SQL Server Connectionstring
In **local.settings.json**:
```csharp
{
	"IsEncrypted": false,
	"Values": {
		"AzureWebJobsStorage": "UseDevelopmentStorage=true",
		"FUNCTIONS_WORKER_RUNTIME": "dotnet",
		"SQLServer": "Server=xxxxxxxxxxxxxxxxxxxxxxxx";
	}
}
```
### GET (SELECT statement)
```csharp
try
{
	List<Visit> visits = new List<Visit>();

	string connectionString = Environment.GetEnvironmentVariable("SQLServer");

	using (SqlConnection connection = new SqlConnection(connectionString))
	{
		using (SqlCommand command = new SqlCommand())
		{
			await connection.OpenAsync();

			command.Connection = connection;
			command.CommandText = "SELECT * FROM Bezoekers WHERE DagVanDeWeek = @day";
			command.Parameters.AddWithValue("@day", day);

			SqlDataReader dataReader = await command.ExecuteReaderAsync();

			while (await dataReader.ReadAsync())
			{
				Visit v = new Visit()
				{
					Tijdstip = int.Parse(dataReader["TijdstipDag"].ToString()),
					AantalBezoekers = int.Parse(dataReader["AantalBezoekers"].ToString()),
					Dag = dataReader["DagVanDeWeek"].ToString()
				};
				visits.Add(v);
			}
		}
	}

	return new OkObjectResult(visits);
}
catch(Exception ex)
{
	log.LogError(ex.Message);
	return new StatusCodeResult(500);
}
```
### POST (INSERT statement)
```csharp
try
{
	List<Visit> visits = new List<Visit>();

	string connectionString = Environment.GetEnvironmentVariable("SQLServer");

	using (SqlConnection connection = new SqlConnection(connectionString))
	{
		await connection.OpenAsync();
		using (SqlCommand command = new SqlCommand())
		{
			command.Connection = connection;
			command.CommandText = "INSERT INTO registrations VALUES ...";
			command.Parameters.AddWithValue("@parameter1", value);

			await command.ExecuteNonQueryAsync();
		}
	}

	return new OkObjectResult(visits);
}
catch(Exception ex)
{
	log.LogError(ex.Message);
	return new StatusCodeResult(500);
}
```
## Azure Table Storage
### Instellen van de Connectionstring
Zoals SQL

### GET (data ophalen)
```csharp
try
{
	string connectionString = Environment.GetEnvironmentVariable("ConnectionStringStorage");
	CloudStorageAccount storageAccount = 	CloudStorageAccount.Parse(connectionString);
	CloudTableClient cloudTableClient = storageAccount.CreateCloudTableClient();
	CloudTable table = cloudTableClient.GetTableReference("registrations");
	await table.CreateIfNotExistsAsync();

	TableQuery<RegistrationEntity> rangeQuery = new TableQuery<RegistrationEntity>()
	.Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, zipcode));

	var queryResult = await table.ExecuteQuerySegmentedAsync<RegistrationEntity>(rangeQuery, null);
	List<Registration> registrations = new List<Registration>();

	foreach (var reg in queryResult.Results)
	{
		registrations.Add(new Registration()
		{
			RegistrationId = Guid.Parse(reg.RowKey),
			Age = reg.Age,
			Email = reg.EMail,
			FirstName = reg.FirstName,
			IsFirstTimer = reg.IsFirstTimer,
			LastName = reg.LastName,
			Zipcode = reg.PartitionKey
		});
	}

	return new OkObjectResult(registrations);
}
catch (Exception ex)
{
	log.LogError(ex.Message);
	return new StatusCodeResult(500);
}
```
### POST (data opslaan)
```csharp
try
{
	string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
	Registration reg = JsonConvert.DeserializeObject<Registration>(requestBody);

	reg.RegistrationId = Guid.NewGuid();

	RegistrationEntity entity = new RegistrationEntity(reg.Zipcode, reg.RegistrationId.ToString())
	{
		EMail = reg.Email,
		Age = reg.Age,
		FirstName = reg.FirstName,
		LastName = reg.LastName,
		IsFirstTimer = reg.IsFirstTimer,
		Zipcode = reg.Zipcode
	};

	string connectionString = Environment.GetEnvironmentVariable("ConnectionStringStorage");
	
	// We willen praten met een account
	CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
	
	// Binnen dat account: Met welke dienst willen we precies communiceren? Cloud Table Storage
	CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
	
	// Nu willen we een specifieke table
	CloudTable table = tableClient.GetTableReference("registrations");
	await table.CreateIfNotExistsAsync();

	TableOperation insertOperation = TableOperation.Insert(entity);
	await table.ExecuteAsync(insertOperation);
	// GEEN EMAIL STUREN MAAR BERICHT OP QUEUE PLAATSEN
	await SendEmailMessage(reg);

	return new OkObjectResult(reg);
}
catch (Exception ex)
{
	log.LogError(ex.Message);
	return new StatusCodeResult(500);
}
```
## Message Queue
### Bericht plaatsen
```csharp
private static async Task SendEmailMessage(Registration reg)
{
	try
	{
		string connectionString = Environment.GetEnvironmentVariable("ConnectionStringStorage");
		QueueClient queueClient = new QueueClient(connectionString, "registrations");
		await queueClient.CreateIfNotExistsAsync();
		// Omzetten naar Json string
		string json = JsonConvert.SerializeObject(reg);
		// Omzetten naar bytes
		var valueBytes = Encoding.UTF8.GetBytes(json);
		// Omzetten naar Base64
		await queueClient.SendMessageAsync(Convert.ToBase64String(valueBytes));
	}
	...
}
```
### Message Queue Trigger (bericht inlezen)
```csharp
...
Registration reg = JsonConvert.DeserializeObject<Registration>(myQueueItem);
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg0NjU2NTkzMCwyMDIxMjUxMDA1LDEwOT
k5NzY4MzldfQ==
-->