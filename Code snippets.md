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

## MQTT Trigger
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

## MQTT Send

[FunctionName("GratisMode")]
public static IActionResult GratisMode(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "parking/mode")] HttpRequest req,
ILogger log, [Mqtt] out IMqttMessage outMessage, ILogger logger)
{
            string requestBody = new StreamReader(req.Body).ReadToEnd();

            ModeObject m = JsonConvert.DeserializeObject<ModeObject>(requestBody);

            string json = "{\"isTrue\" : \"" +  m.isTrue + "\"}";


            outMessage = new MqttMessage("/lennertdefauw/mode", Encoding.ASCII.GetBytes(json), MqttQualityOfServiceLevel.AtLeastOnce, true);

            return new StatusCodeResult(200);
        }

## IoTHub Connection string
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5MDE3NzkyNiwtMTM4NTE3NTQwLDE4MT
k2MjIzNzksMjAyMTI1MTAwNSwxMDk5OTc2ODM5XX0=
-->