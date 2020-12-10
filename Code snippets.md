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
[MqttTrigger("/lennertdefauw")] IMqttMessage message, ILogger logger)
{
	var body = message.GetMessage();
	var bodyString = Encoding.UTF8.GetString(body);

	Registration r = JsonConvert.DeserializeObject<Registration>(bodyString);

	...
}
```

## IoTHub Connection string
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkyMTQ0MjI2MywxODE5NjIyMzc5LDIwMj
EyNTEwMDUsMTA5OTk3NjgzOV19
-->