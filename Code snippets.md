# IoT Cloud - Handy things
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
[FunctionName("GratisMode")]
public static IActionResult GratisMode(
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

## IoTHub Connection string
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NzY3MjYxNDcsLTEzODUxNzU0MCwxOD
E5NjIyMzc5LDIwMjEyNTEwMDUsMTA5OTk3NjgzOV19
-->