# IoT Cloud - Handy things
## IoTHub Connectionstrings
### Connectionstring voor device
**IoTHub > IoT Devices > (devicenaam):** Primary Connection String

![Connectionstring voor device](https://i.imgur.com/gmRhSun.png)

### Connectionstring voor IoT Hub Trigger
**IoTHub > Built-in endpoints:** Event-Hub compatible endpoint
![](https://i.imgur.com/4fLTxe0.png)

### Connectionstring voor IoT Hub Trigger
**IoTHub > Built-in endpoints:** Event-Hub compatible endpoint
![IoTHub Trigger connectionstring](https://i.imgur.com/4fLTxe0.png)

### Connectionstring voor IoT Hub beheer
**IoTHub > Shared access policies:** iothubowner: Primary key
![iothubowner connectionstring](https://i.imgur.com/iGXCmhy.png)

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

## MQTT
### MQTT Trigger
```csharp
[FunctionName("MQTTTrigger")]
public static void MQTTListener(
[MqttTrigger("/karelstopic")] IMqttMessage message, ILogger logger)
{
	var body = message.GetMessage();
	var bodyString = Encoding.UTF8.GetString(body);

	Registration r = JsonConvert.DeserializeObject<Registration>(bodyString);

	...
}
```
### MQTT Send
```csharp
[FunctionName("MQTTSend")]
public static IActionResult MQTTSend(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "routenaam/objects")] HttpRequest req,
ILogger log, [Mqtt] out IMqttMessage outMessage, ILogger logger)
{
	string requestBody = new StreamReader(req.Body).ReadToEnd();
	ObjectKlasse m = JsonConvert.DeserializeObject<ObjectKlasse>(requestBody);

	string json = "{\"property\" : \"" +  m.property+ "\"}";
	outMessage = new MqttMessage("/karelstopic/subtopic", Encoding.ASCII.GetBytes(json), MqttQualityOfServiceLevel.AtLeastOnce, true);

	return new StatusCodeResult(200);
}
```

## CosmosDB

## IoTHub Connection string
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc1MzM4NzkyMSwxMzcyMDczMDc1LC02OD
EyNTczNDUsLTI0NjYxODg2NywxNjIzNzM3NzczLDEyODAyNTQ4
MzEsLTEzODUxNzU0MCwxODE5NjIyMzc5LDIwMjEyNTEwMDUsMT
A5OTk3NjgzOV19
-->