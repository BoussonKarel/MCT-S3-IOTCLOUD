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
``
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc5MjM0Mzc2NywyMDIxMjUxMDA1LDEwOT
k5NzY4MzldfQ==
-->