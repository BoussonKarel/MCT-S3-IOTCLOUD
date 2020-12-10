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
Function without parameters
```csharp
[FunctionName("GET_noParams")]
public static async Task<IActionResult> Get_noParams(
	[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getroute")] HttpRequest req,
	ILogger log)
{
	try
	{
		//Can also return the structure of a class
		return new OkObjectResult("I returned something :)");
	}
	catch (Exception e)
	{
		//Returned http status code
		return new StatusCodeResult(500);
	}
}
```
Function with 2 parameters
```csharp
[FunctionName("GET_Params")]
public static async Task<IActionResult> Get_Params(
	[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getroute/{getal1}/{getal2}")] HttpRequest req,
	int getal1, int getal2,
	ILogger log)
{
	try
	{
		//Using the parameters in the sum
		int result = getal1 + getal2;

		//Can also return the structure of a class
		return new OkObjectResult(result);
	}
	catch (Exception e)
	{
		//Returned http status code
		return new StatusCodeResult(500);
	}
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
eyJoaXN0b3J5IjpbLTYxNTE3NTkwNywyMDIxMjUxMDA1LDEwOT
k5NzY4MzldfQ==
-->