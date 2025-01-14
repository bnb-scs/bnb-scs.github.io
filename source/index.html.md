---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - go
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Welcome to the Kittn API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```go
import "net/http"

client := &http.Client{}
req, err := http.NewRequest(method, url, bytes.NewBuffer(payload))
if err != nil {
    fmt.Println(err)
    return
}
req.Header.Add("Content-Type", "application/json")
req.Header.Add("X-API-Key", "****")
```

```python
import requests

headers = {
    "Content-Type": "application/json",
    "X-API-Key": "****"
}

response = requests.post(url, json=payload, headers=headers)
```

```shell
# With shell, you can just pass the correct header with each request
curl --request POST \
  --url https://service.hashdit.io/v2/hashdit/transaction-security \
  --header 'Content-Type: application/json' \
  --header 'X-API-Key: ****' \
  --data '{
  "chainId": 56,
  "to": "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
}'
```

```javascript
const headers = {
    "Content-Type": "application/json",
    "X-API-Key": "****"
};

fetch(url, {
    method: "POST",
    headers: headers,
    body: JSON.stringify(payload)
})
```

> Make sure to replace `****` with your API key.

HashDit uses API keys to allow access to the API. You can apply a new HashDit API key by contacting support@hashdit.io.

HashDit expects for the API key to be included in all API requests to the server in a header that looks like the following:

`X-API-Key: ****`

<aside class="notice">
You must replace <code>****</code> with your real API key.
</aside>

# Security APIs

## Transaction Security

```go
package main

import (
    "bytes"
    "fmt"
    "net/http"
)

func main() {
    url := "https://service.hashdit.io/v2/hashdit/transaction-security"
    method := "POST"

    payload := []byte(`{
        "chainId": 56,
        "to": "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
    }`)

    client := &http.Client{}
    req, err := http.NewRequest(method, url, bytes.NewBuffer(payload))
    if err != nil {
        fmt.Println(err)
        return
    }
    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("X-API-Key", "****")

    res, err := client.Do(req)
    if err != nil {
        fmt.Println(err)
        return
    }
    defer res.Body.Close()

    fmt.Println("Response Status:", res.Status)
}
```

```python
import requests

url = "https://service.hashdit.io/v2/hashdit/transaction-security"
payload = {
    "chainId": 56,
    "to": "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
}
headers = {
    "Content-Type": "application/json",
    "X-API-Key": "****"
}

response = requests.post(url, json=payload, headers=headers)

print("Response Status:", response.status_code)
print("Response Body:", response.text)
```

```shell
curl --request POST \
  --url https://service.hashdit.io/v2/hashdit/transaction-security \
  --header 'Content-Type: application/json' \
  --header 'X-API-Key: ****' \
  --data '{
  "chainId": 56,
  "to": "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
}'
```

```javascript
const url = "https://service.hashdit.io/v2/hashdit/transaction-security";
const payload = {
    chainId: 56,
    to: "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
};

const headers = {
    "Content-Type": "application/json",
    "X-API-Key": "****"
};

fetch(url, {
    method: "POST",
    headers: headers,
    body: JSON.stringify(payload)
})
.then(response => response.json())
.then(data => {
    console.log("Response Data:", data);
})
.catch(error => {
    console.error("Error:", error);
});
```

> The above command returns JSON structured like this:

```json
{
	"code": "0",
	"status": "ok",
	"data": {
		"has_result": true,
		"polling_interval": 0,
		"risk_level": 0,
		"risk_detail": [
			{
				"name": "is_in_wlist",
				"value": "The contract is relatively safe based on the threat intelligence."
			}
		]
	}
}
```

This endpoint retrieves all kittens.

### HTTP Request

`POST https://service.hashdit.io/v2/hashdit/transaction-security`

### Post Parameters

Parameter | Required? | Default | Description
--------- | --------- | ------- | -----------
chainId   | Yes       | 56      | The chain you want to check againt
to        | Yes       |         | the target address of the transaction
from      | Optional  |         | the sender address of the transaction
data      | Optional  |         | the transaction data
value     | Optional  |         | the transaction value
gas       | Optional  |         | the transaction gasLimit
gasPrice  | Optional  |         | the transaction gasPrice
maxFeePerGas  | Optional  |         | EIP1559 max fee per gas
maxPriorityFeePerGas  | Optional  |         | EIP1559 tip fee per gas
nonce     | Optional  |         | the transaction nonce
dappUrl   | Optional  |         | the URL of the dapp initiated the transaction

<aside class="success">
</aside>
