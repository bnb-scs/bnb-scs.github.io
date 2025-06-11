---
title: API Reference

language_tabs: # must be one of https://github.com/rouge-ruby/rouge/wiki/List-of-supported-languages-and-lexers
  - shell
  - go
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Welcome to the HashDit API! You can use our API to access HashDit service, which provides various security capabilities including address security, token security, transaction securitiy, ...

We have language bindings in Shell, Go, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

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
  --url https://api.diting.pro/v2/hashdit/transaction-security \
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

HashDit uses API keys to allow access to the API. You can apply a new HashDit API key by contacting **support@hashdit.io**. It will be much appreciated if you could provide the following information in your email:

* Some background of your project, business scenario, etc.. for example: DeFi wallet Dex
* When will your business be fully in production?
* What’s your rollout plan in production?
  * like 10% on Dec 10th, 50% on Dec 15th, ...
* What’s the estimated QPS you will put on our API when fully roll out?

Then HashDit expects for the API key to be included in all API requests to the server in a header that looks like the following:

`X-API-Key: ****`

<aside class="notice">
  You must replace <code>****</code> with your real API key.
</aside>

<aside class="notice">
  We will grant you the QA environment permission first, if everything works fine on QA we will proceed the production integration
</aside>

# Domain

Env        | domain
---------- | ---------
QA         | api.diting.pro
Production | service.hashdit.io

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
    url := "https://api.diting.pro/v2/hashdit/transaction-security"
    method := "POST"

    payload := []byte(`{
	"from": "0xf977814e90da44bfa03b6295a0616a897441acec",
	"to": "0x55d398326f99059fF775485246999027B3197955",
	"data": "0x095ea7b3000000000000000000000000d99d1c33f9fc3444f8101754abc46c52416550d1ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
	"dappUrl": "https://claim-linea.com",
	"chainId": 56
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

url = "https://api.diting.pro/v2/hashdit/transaction-security"
payload = {
	"from": "0xf977814e90da44bfa03b6295a0616a897441acec",
	"to": "0x55d398326f99059fF775485246999027B3197955",
	"data": "0x095ea7b3000000000000000000000000d99d1c33f9fc3444f8101754abc46c52416550d1ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
	"dappUrl": "https://claim-linea.com",
	"chainId": 56
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
  --url https://api.diting.pro/v2/hashdit/transaction-security \
  --header 'Content-Type: application/json' \
  --header 'X-API-Key: ****' \
  --data '{
	"from": "0xf977814e90da44bfa03b6295a0616a897441acec",
	"to": "0x55d398326f99059fF775485246999027B3197955",
	"data": "0x095ea7b3000000000000000000000000d99d1c33f9fc3444f8101754abc46c52416550d1ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
	"dappUrl": "https://claim-linea.com",
	"chainId": 56
}'
```

```javascript
const url = "https://api.diting.pro/v2/hashdit/transaction-security";
const payload = {
	from: "0xf977814e90da44bfa03b6295a0616a897441acec",
	to: "0x55d398326f99059fF775485246999027B3197955",
	data: "0x095ea7b3000000000000000000000000d99d1c33f9fc3444f8101754abc46c52416550d1ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
	dappUrl: "https://claim-linea.com",
	chainId: 56
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
	"tx_hash": "",
	"chain": "bsc",
	"url": "https://bscscan.com/tx/None",
	"from": "0xF977814e90dA44bFA03b6295A0616a897441aceC",
	"to": "0x55d398326f99059fF775485246999027B3197955",
	"value": "0x0",
	"value_in_eth": 0,
	"gas_used": "0x0",
	"status": true,
	"method": "approve(address,uint256)",
	"transaction_fee": 0,
	"overall_risk": 5,
	"risk_description": "High Risk",
	"risk_details": [
		{
			"name": "unlimited_EOA_approval",
			"value": "0xD99D1c33F9fC3444f8101754aBC46c52416550D1",
			"value_type": "address",
			"risk": 4,
			"risk_name": "High Risk",
			"description": "Using 'approve' for unlimited tokens to an EOA address: 0xD99D1c33F9fC3444f8101754aBC46c52416550D1.\nYou are using 'approve' for unlimited tokens to a personal wallet (EOA) rather than a contract. This is unusual and potentially risky as EOAs are controlled by individuals."
		},
		{
			"name": "dapp_risk",
			"value": "https://claim-linea.com",
			"value_type": "url",
			"risk": 5,
			"risk_name": "Critical Risk",
			"description": "There are potential risks in the dApp based on the threat intelligence."
		}
	]
}
```

This endpoint returns the risk level and risk details about the requested transaction.

### HTTP Request

`POST https://api.diting.pro/v2/hashdit/transaction-security`

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

### HTTP Response

Parameter | Description
--------- | -----------
status    | "ok"
data      | the address analysis result, see the right side for details
urlData   | the url analysis result, see the right side for details

### Parameters in data

Field       | Description
----------- | -----------
risk_level  | -1: unknown risk, 0 ~ 5: the bigger the number, the higher the risk
risk_detail | the result data, see the right side for details

### Parameters in urlData

Field       | Description
----------- | -----------
risk_level  | -1: unknown risk, 0 ~ 5: the bigger the number, the higher the risk
risk_detail | the result data, see the right side for details

<aside class="notice">
Discuss with us about an appropriate `risk_level` if you need to take certain actions based on it
</aside>

## Address Security

```go
package main

import (
    "bytes"
    "fmt"
    "net/http"
)

func main() {
    url := "https://api.diting.pro/v2/hashdit/address-security"
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

url = "https://api.diting.pro/v2/hashdit/address-security"
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
  --url https://api.diting.pro/v2/hashdit/address-security \
  --header 'Content-Type: application/json' \
  --header 'X-API-Key: ****' \
  --data '{
  "chainId": 56,
  "to": "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
}'
```

```javascript
const url = "https://api.diting.pro/v2/hashdit/address-security";
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

This endpoint returns the risk level and risk details about the requested transaction.

### HTTP Request

`POST https://api.diting.pro/v2/hashdit/address-security`

### Post Parameters

Parameter | Required? | Default | Description
--------- | --------- | ------- | -----------
chainId   | Yes       | 56      | The chain you want to check againt
address   | Yes       |         | the target address of the transaction

### HTTP Response

Parameter | Description
--------- | -----------
status    | "ok"
data      | the address analysis result, see the right side for details

### Parameters in data

Field       | Description
----------- | -----------
risk_level  | -1: unknown risk, 0 ~ 5: the bigger the number, the higher the risk
risk_detail | the result data, see the right side for details

<aside class="notice">
Discuss with us about an appropriate `risk_level` if you need to take certain actions based on it
</aside>

## Batch Address Security

```go
package main

import (
    "bytes"
    "fmt"
    "net/http"
)

func main() {
    url := "https://api.diting.pro/v2/hashdit/batch-address-security"
    method := "POST"

    payload := []byte(`[
        {
            "chainId": 56,
            "address": "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
        },
        {
            "address": "0xfa7fee97951fb46675410aef89c9f3f6dd93f042"
        }
    ]`)

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

url = "https://api.diting.pro/v2/hashdit/batch-address-security"
payload = [
    {
        "chainId": 56,
        "address": "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
    },
    {
        "address": "0xfa7fee97951fb46675410aef89c9f3f6dd93f042"
    }
]
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
  --url https://api.diting.pro/v2/hashdit/batch-address-security \
  --header 'Content-Type: application/json' \
  --header 'X-API-Key: ****' \
  --data '[{
  "chainId": 56,
  "address": "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
},{"address": "0xfa7fee97951fb46675410aef89c9f3f6dd93f042"}]'
```

```javascript
const url = "https://api.diting.pro/v2/hashdit/batch-address-security";
const payload = [{
    chainId: 56,
    address: "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
}, {
    address: "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
}];

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
	"data": [
		{
			"request_id": "bc95bfb7-7936-4cb1-a863-2ceff394a5a4",
			"has_result": true,
			"polling_interval": 0,
			"risk_level": 4,
			"risk_detail": [
				{
					"name": "is_in_blist",
					"value": "There are potential risks in the contract based on the threat intelligence."
				}
			]
		},
		{
			"request_id": "bc95bfb7-7936-4cb1-a863-2ceff394a5a4",
			"has_result": true,
			"polling_interval": 0,
			"risk_level": 1,
			"risk_detail": []
		},
		{
			"request_id": "bc95bfb7-7936-4cb1-a863-2ceff394a5a4",
			"has_result": true,
			"polling_interval": 0,
			"risk_level": 4,
			"risk_detail": [
				{
					"name": "is_in_blist",
					"value": "There are potential risks in the contract based on security analysis model."
				}
			]
		},
		{
			"request_id": "bc95bfb7-7936-4cb1-a863-2ceff394a5a4",
			"has_result": true,
			"polling_interval": 0,
			"risk_level": 1,
			"risk_detail": []
		},
		{
			"request_id": "bc95bfb7-7936-4cb1-a863-2ceff394a5a4",
			"has_result": true,
			"polling_interval": 0,
			"risk_level": 1,
			"risk_detail": []
		}
	]
}
```

This endpoint returns the risk level and risk details about the requested transaction.

### HTTP Request

`POST https://api.diting.pro/v2/hashdit/batch-address-security`

### Post Parameters

The array of:

Parameter | Required? | Default | Description
--------- | --------- | ------- | -----------
chainId   | No       |       | if not specified, we will run against all of the chains we supported, which are: bnbchain, ethereum, opbnb, polygon these 4 chains ATM
address   | Yes       |         | the target address of the transaction

### HTTP Response

Parameter | Description
--------- | -----------
status    | "ok"
data      | the address analysis result, see the right side for details

### Parameters in data

Field       | Description
----------- | -----------
risk_level  | -1: unknown risk, 0 ~ 5: the bigger the number, the higher the risk
risk_detail | the result data, see the right side for details

<aside class="notice">
Discuss with us about an appropriate `risk_level` if you need to take certain actions based on it
</aside>


## Token Security

```go
package main

import (
    "bytes"
    "fmt"
    "net/http"
)

func main() {
    url := "https://api.diting.pro/v2/hashdit/token-security"
    method := "POST"

    payload := []byte(`{
        "chainId": 56,
        "address": "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
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

url = "https://api.diting.pro/v2/hashdit/token-security"
payload = {
    "chainId": 56,
    "address": "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
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
  --url https://api.diting.pro/v2/hashdit/token-security \
  --header 'Content-Type: application/json' \
  --header 'X-API-Key: ****' \
  --data '{
  "chainId": 56,
  "address": "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
}'
```

```javascript
const url = "https://api.diting.pro/v2/hashdit/token-security";
const payload = {
    chainId: 56,
    address: "0xa7a5db3d94810ac366ab663f6fd71e6b795d8538"
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
		"proxy": {
			"is_proxy": "0",
			"proxy_admin_type": "",
			"proxy_admin_address": "",
			"proxy_implementation_address": "",
			"proxy_implementation_verified": ""
		},
		"status": 200,
		"buy_gas": "-1",
		"buy_tax": "-1",
		"holders": [
			{
				"token_balance": "1292648065000000000000",
				"account_address": "0xdBD3fa3469A67876f530b94f2f6C6800202434ca"
			},
			{
				"token_balance": "400000000000000000000",
				"account_address": "0xf823034616585049c0f9f9b6761c31A383F2DbBf"
			},
			{
				"token_balance": "314541160000000000000",
				"account_address": "0x747DBB91f4d19DDD311D24B2Ff8EB207e7ce10E2"
			},
			{
				"token_balance": "139152693933746153812",
				"account_address": "0xf25B3fa015f33c9d8D760069091150709516004A"
			},
			{
				"token_balance": "100000000000000000000",
				"account_address": "0x9fAC90FC6a339E093fEB32D6F0aBFcefb28bCc75"
			},
			{
				"token_balance": "60462512000000000000",
				"account_address": "0xa47dCC127BD2487B01477D8e381dCEd5de5e5033"
			},
			{
				"token_balance": "50000000000000000000",
				"account_address": "0xBe1e9EA516Ac20DD300358224Ae0a75e42150E1C"
			},
			{
				"token_balance": "45000000000000000000",
				"account_address": "0x1d2B16cfbd9128F1EC0BBe3E3b08299A9ecA3EE7"
			},
			{
				"token_balance": "27090220000000000000",
				"account_address": "0x6a3FfA5C2F13898848295C3D2920614735069CE3"
			},
			{
				"token_balance": "20600000000000000000",
				"account_address": "0xC1F80A92AfBBb299844fDc41B3194F0437E050e2"
			}
		],
		"dex_info": [],
		"sell_gas": "-1",
		"sell_tax": "-1",
		"verified": "1",
		"is_in_dex": "0",
		"cannot_buy": "0",
		"fake_token": {
			"is_fake": "0",
			"mimic_token_name": "",
			"mimic_token_symbol": "",
			"mimic_token_address": ""
		},
		"owner_type": "contract",
		"token_name": "USDe",
		"cannot_sell": "0",
		"dev_address": "0xaa439fb33e55306c7c79841f20121b4c4139f3dc",
		"is_mintable": "1",
		"address_type": "ERC20",
		"hidden_owner": "0",
		"token_symbol": "USDe",
		"total_supply": "2586985396000000000000",
		"transfer_gas": "-1",
		"transfer_tax": "-1",
		"holders_count": "110",
		"is_anti_whale": "0",
		"owner_address": "0xc9647361742Eb964965B461C44Bdf5c4Bc3c406d",
		"self_destruct": "0",
		"diting_version": "v1.2.7",
		"token_decimals": "18",
		"cannot_transfer": "0",
		"token_price_usd": "0.9996",
		"code_obfuscation": "0",
		"dev_token_balance": "0",
		"dev_token_percent": "0.0",
		"transfer_cooldown": "0",
		"transfer_pausable": "0",
		"transfer_blacklist": "0",
		"transfer_whitelist": "0",
		"unlimited_mintable": "0",
		"bad_function_encode": "0",
		"owner_token_balance": "0",
		"owner_token_percent": "0.0",
		"owner_change_balance": "0",
		"anti_whale_modifiable": "0",
		"balance_external_call": "0",
		"low_level_external_call": "0"
	}
}
```

This endpoint returns all of the risk info about the requested token.

### HTTP Request

`POST https://api.diting.pro/v2/hashdit/token-security`

### Post Parameters

Parameter | Required? | Default | Description
--------- | --------- | ------- | -----------
chainId   | Yes       | 56      | the chain you want to check againt
address   | Yes       |         | the token address to be analyzed

### HTTP Response

Parameter | Description
--------- | -----------
status    | "ok" - if the result is update to date, "in progress" - if the result is temporarily unavailable
pollAfter | poll after `pollAfter` seconds again if the result was unavailable
data      | the result data, see the right side for details


## Domain Security

```go
package main

import (
    "bytes"
    "fmt"
    "net/http"
)

func main() {
    url := "https://api.diting.pro/v2/hashdit/domain-security"
    method := "POST"

    payload := []byte(`{
        "url": "example.com"
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

url = "https://api.diting.pro/v2/hashdit/domain-security"
payload = {
    "url": "example.com"
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
  --url https://api.diting.pro/v2/hashdit/domain-security \
  --header 'Content-Type: application/json' \
  --header 'X-API-Key: ****' \
  --data '{
  "url": "example.com"
}'
```

```javascript
const url = "https://api.diting.pro/v2/hashdit/domain-security";
const payload = {
    url: "example.com"
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
    "risk_level": 5,
    "risk_detail": [
      {
        "name": "is_in_blist",
        "value": "There are potential risks in the dApp based on the threat intelligence."
      },
      {
        "name": "red_alarm",
        "value": "This dApp was marked as red alarm on: https://dappbay.bnbchain.org/detail/movai"
      }
    ]
  }
}
```

This endpoint returns all of the risk info about the requested url.

### HTTP Request

`POST https://api.diting.pro/v2/hashdit/domain-security`

### Post Parameters

Parameter | Required? | Default | Description
--------- | --------- | ------- | -----------
url       | Yes       |         | the url to be analyzed

### HTTP Response

Parameter | Description
--------- | -----------
status    | "ok" - if the request is successful
data      | the result data, see the right side for details

### Parameters in result data

Field       | Description
----------- | -----------
risk_level  | -1: unknown risk, 0 ~ 5: the bigger the number, the higher the risk
risk_detail | the result data, see the right side for details

<aside class="notice">
Discuss with us about an appropriate `risk_level` if you need to take certain actions based on it
</aside>
