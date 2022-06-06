---
title: Wallex API Documentation 
meta_description: Official Documentation for the Wallex APIs and Streams
sidebar_header: API Documentation 

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript
  - php

toc_footers:
  - <a href='https://wallex.ir/login' id='signup-api'>Sign Up</a>

language_switcher: <a href='/' class='lang'>Farsi</a>

search: false

code_clipboard: false
---
# Change Log
<h3>2022-04-04</h3>
New API Management process.


<h3>2022-03-07</h3>
Adding WebSocket docs for the matkets.


# Introduction

Wallex provides users with RESTful API and in some cases with WebSocket.

## Authentication
Methods are either private or public. To access private methods, you must first get a Token, but you will also be able to use public methods without authentication and getting Tokens. 


You should place your API key on HTTP Header like:
```
x-api-key: YouHaveToPlaceYourKeyHere
```

```
x-api-key: YouHaveToPlaceYourKeyHere
```


## Get a new API Key:
You can create a new API key, by referring to <a href="https://wallex.ir/app/my-account/api-management" target="_blank">API Management</a>
 section in your profile.

In order to create a new API key, you will need to enter required information as below:

<h3> API name (mandatory)</h3>
You have to set a name for your API key.


<h3>Valid to </h3>


the default validation date is up to 90 days; however, you can shorten the time of expiration to 60, 30 or 15 days, if you wish.


<h3>Permissions </h3>
All API keys have “read access” as a default; however you can grant the access of trade and withdraw if you wish. Please note that in case you allow withdraw access, you will have to enter permitted IPs for your operations’ security


<h3>Permitted IPs (Mandatory if withdraw is allowed) </h3>
After all information are given, you will have to pass the two-step verification by entering the OTP sent to you Email and then to you phone number. Please make sure you keep the API key somewhere safe as you will be able to view and copy the API key once.


## EDIT API keys:
You can edit your API keys by referring to the list in API management section. Please note you will not be able to edit expiration date; For this purpose, you will need to create a new API key.
In order to make changes in your API key, you need to pass the two-step verification for your own security.


## Expiry of API keys:
All API keys will be deactivated in the expiration date and will not be in use any longer. To prevent any malfunction in users’ operation, we will notify you 48 hours before expiration and also once the API key is deactivated, through Emails and in-app messages.


## Limitations in API keys:
 Please be noted that you cannot have more than 3 active API keys. 
 
 
 ## Delete API keys:
 In order to have your API keys deleted, you will have to pass the two-step verification after confirming your operation.


#Markets

##List of market and status (Public)

Get Wallex markets and status lists.  

```python
import requests

url = "https://api.wallex.ir/v1/markets"

payload = ""
headers = {}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/markets' \
--data-raw ''
```

```javascript
var raw = "";

var requestOptions = {
  method: "GET",
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/markets", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/markets');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "symbols": {
      "BTCTMN": {
        "symbol": "BTCTMN",
        "baseAsset": "BTC", // Source currency
        "baseAssetPrecision": 8, // Source currency precision count
        "quoteAsset": "TMN", // Destination currency
        "quotePrecision": 0, // Destination currency precision count
        "faName": "بیت کوین - تومان",
        "faBaseAsset": "بیت کوین",
        "faQuoteAsset": "تومان",
        "stepSize": 6,
        "tickSize": 0,
        "minQty": 0.000001, // Minimum quantity that is acceptable
        "maxQty": 100000, // Maximum quantity that is acceptable
        "minNotional": 100000, // Minimum trade sum that is acceptable
        "stats": {
          "bidPrice": "1323000001",
          "askPrice": "1324135008",
          "24h_ch": "-3.04",
          "24h_volume": "0.18734400",
          "24h_quoteVolume": "251943031.0000000000000000",
          "24h_highPrice": "1375000000.00000000",
          "24h_lowPrice": "1310925535.00000000",
          "lastPrice": "1323000001.00000000",
          "lastQty": "0.00009200"
        }
      }
    }
  },
  "message": "The operation was successful",
  "success": true
}
```

HTTP Request

`GET https://api.wallex.ir/v1/markets`



##Global markets statistics (Public)

Get the latest statistics of global markets.

```python
import requests

url = "https://api.wallex.ir/v1/currencies/stats"

payload = ""
headers = {}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/currencies/stats' \
--data-raw ''
```

```javascript
var raw = "";

var requestOptions = {
  method: "GET",
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/currencies/stats", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/currencies/stats');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": [
    {
      "key": "BTC",
      "name": "بیت کوین",
      "name_en": "Bitcoin",
      "rank": 1,
      "dominance": 45.749428044724,
      "volume_24h": 32181710761.492,
      "market_cap": 613868313928.44,
      "ath": 64805,
      "ath_change_percentage": -49.09243,
      "ath_date": "2021-04-14T11:54:46Z",
      "price": 32750.734991767,
      "daily_high_price": 33599,
      "daily_low_price": 31042,
      "weekly_high_price": 35787.077405232,
      "weekly_low_price": 31711.935467727,
      "percent_change_1h": -0.0584588,
      "percent_change_24h": 4.59022,
      "percent_change_7d": -7.3306,
      "percent_change_14d": -7.55017,
      "percent_change_30d": -14.67178,
      "percent_change_60d": -40.03963,
      "percent_change_200d": 79.82314,
      "percent_change_1y": 259.71576,
      "price_change_24h": 897.95079613191,
      "price_change_7d": -2740.555003737,
      "price_change_14d": -2825.0625147781,
      "price_change_30d": -5801.8082903472,
      "price_change_60d": -22150.727578626,
      "price_change_200d": 14504.572682697,
      "price_change_1y": 23674.600903579,
      "max_supply": 21000000,
      "total_supply": 18743650,
      "circulating_supply": 18743650,
      "created_at": "2021-02-01T10:46:09Z",
      "updated_at": "2021-06-27T20:05:37Z"
    },
    ...
  ],
  "message": "The operation was successful",
  "success": true
}
```

HTTP Request

`GET https://api.wallex.ir/v1/currencies/stats`

Note:

<aside class="info">
The values of <code>ath_date</code>, <code>created_at</code>, <code>updated_at</code> are displayed in ZULU format.
</aside>

## Order Book (Public) 

Get the Order book for each market.

```python
import requests

url = "https://api.wallex.ir/v1/depth?symbol=BTCTMN"

payload = ""
headers = {}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/depth?symbol=BTCTMN' \
--data-raw ''
```

```javascript
var raw = "";

var requestOptions = {
  method: "GET",
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/depth?symbol=BTCTMN", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/depth?symbol=BTCTMN');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "ask": [
      {
        "price": "1317505698.00000000",
        "quantity": "0.13471800"
      },
      {
        "price": "1317783488.00000000",
        "quantity": "0.69433100"
      }
    ],
    "bid": [
      {
        "price": "1311752950.00000000",
        "quantity": "0.00076300"
      },
      {
        "price": "1309100000.00000000",
        "quantity": "0.00076300"
      }
    ]
  },
  "message": "The operation was successful",
  "success": true
}
```

HTTP Request

`GET https://api.wallex.ir/v1/depth`

Query Parameters

| Parameter | Type   | Default  | Description | Sample |
| --------- | ------ | -------- | ----------- | ------ |
| symbol    | String | required | Market Name   | BTCTMN |

Note:

<aside class="info">
To see the description of the market symbols of Wallex, you can refer to the market list. 
</aside>

## Latest market trades list

List of the latest trades in Wallex markets.

```python
import requests

url = "https://api.wallex.ir/v1/trades?symbol=BTCTMN"

payload = ""
headers = {}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/trades?symbol=BTCTMN' \
--data-raw ''
```

```javascript
var raw = "";

var requestOptions = {
  method: "GET",
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/trades?symbol=BTCTMN", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/trades?symbol=BTCTMN');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "latestTrades": [
      {
        "symbol": "BTCTMN",
        "quantity": "0.0017700000000000",
        "price": "852231321.0000000000000000",
        "sum": "1508449.4381700000000000",
        "isBuyOrder": false,
        "timestamp": "2021-06-28T00:02:15Z"
      },
      {
        "symbol": "BTCTMN",
        "quantity": "0.0007040000000000",
        "price": "852231321.0000000000000000",
        "sum": "599970.8499840000000000",
        "isBuyOrder": false,
        "timestamp": "2021-06-27T23:56:36Z"
      },
      ...
    ]
  },
  "message": "The operation was successful",
  "success": true
}

```

HTTP Request

`GET https://api.wallex.ir/v1/trades`

Query Parameters

| Parameter | Type   | Default  | Description | Sample |
| --------- | ------ | -------- | ----------- | ------ |
| symbol    | String | required | Market Name   | BTCTMN |

Note:

<aside class="info">
The displayed <code>timestamp</code> is in ZULU format.
</aside>

##OHLC statistics of Wallex market

Get the OHLC statistics of the Wallex market. 

<a href="https://en.wikipedia.org/wiki/Open-high-low-close_chart" target="_blank">What are OHLC statistics?</a>

```python
import requests

url = "https://api.wallex.ir/v1/udf/history?symbol=BTCTMN&resolution=D&from=1624841423&to=1624841423"

payload = ""
headers = {}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/udf/history?symbol=BTCTMN&resolution=D&from=1624841423&to=1624841423' \
--data-raw ''
```

```javascript
var raw = "";

var requestOptions = {
  method: "GET",
  body: raw,
  redirect: "follow",
};

fetch(
  "https://api.wallex.ir/v1/udf/history?symbol=BTCTMN&resolution=D&from=1624841423&to=1624841423",
  requestOptions
)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/udf/history?symbol=BTCTMN&resolution=D&from=1624841423&to=1624841423');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "s": "ok",
  "t": [1562182200],
  "c": ["134000000.0000000000"],
  "o": ["130578000.0000000000"],
  "h": ["123863600.0000000000"],
  "l": ["120732000.0000000000"],
  "v": ["8.3238723141"]
}
```

HTTP Request

`GET https://api.wallex.ir/v1/udf/history`

Query Parameters

| Parameter  | Type    | Default  | Description        | Sample     |
| ---------- | ------- | -------- | ------------------ | ---------- |
| symbol     | String  | required | Market Name          | BTCTMN     |
| resolution | String  | required | The time interval of each candle
 | D          |
| from       | Integer | required | The starting time of the interval
    | 1624841423 |
| to         | Integer | required | The finishing time of the interval    | 1624841423 |

Acceptable resolutions :

| Resolution | Description |
| ---------- | ----------- |
| 60         | 1 Hour     |
| 180        | 3 Hour     |
| 360        | 6 Hour     |
| 720        | 12 Hour |
| D          | 1 Day      |
| 2D         | 2 Days     |
| 3D         | 3 Days     |

Note:

<aside class="info">
Values of <code>from</code> & <code>to</code> in timestamp formats.
</aside>
# Market and trade WebSocket
### Using the WebSocket

Methods are either private or public. To access WebSocket, you must use the socket.io client. You’ll need to send and receive your requests to <code>https://api.wallex.ir/socket.io</code>


You’ll also need these data objects for your requestes:

You should <code>emit</code > on the <code>subscribe</code> event.

## Order Book
The order book for each market


WebSocket


`{“channel” : “symbol@buyDepth”}`  

<aside class="info">
To see the description of the market symbols of Wallex, you can refer to the market list.
</aside>

> Output

```json
{
   "quantity":0.0058,
   "price":"1018259534.0000000000000000",
   "sum":5905905.2972
}
```

WebSocket


`{“channel” : “symbol@sellDepth”}`
<aside class="info">
To see the description of the market symbols of Wallex, you can refer to the market list.
</aside>

## Latest Trade

WebSocket


`{“channel” : “symbol@trade”}`

<aside class="info">
To see the description of the market symbols of Wallex, you can refer to the market list.
</aside>
> Output

```json
{
   "isBuyOrder":true,
   "quantity":"0.0012000000000000",
   "price":"1018259534.0000000000000000",
   "…"
}
```
## List of market and status
Get Wallex markets and status lists.  


WebSocket

`{“channel” : “symbol@marketCap}`

> Output

```
7d_ch: -0.86
7d_volume: "11.6699390000000000"
24h_ch: -1.19
24h_highPrice: "39670.9800000000000000"
24h_lowPrice: "37172.6400000000000000"
24h_quoteVolume: "43259.1354590400000000"
24h_volume: "1.1240740000000000"
askCount: 117
askPrice: "38505.1700000000000000"
askVolume: "1.4295580000000000"
bidCount: 163
bidPrice: "38274.5900000000000000"
bidVolume: "4.5113380000000000"
createdAt: "2020-04-01T00:00:00.000000Z"
direction: {SELL: 37, BUY: 63}
lastPrice: "38451.3300000000000000"
lastQty: "0.0005740000000000"
lastTradeSide: "SELL"
socket: null
symbol: "BTCUSDT"

```
## Private Methods
To receive private account data like updates, balance, orders, and trades you’ll need to use <code>Outputs</code> on the <code>stream_key</code>.

After you’ve logged in to your account you should <code>emit</code> on the <code>Output </code>.


WebSocket


`{“channel” : stream_key}`


 Output will contain all of account activity updates.
# Profile

## Profile Info (Private)

Get your profile information.

```python
import requests

url = "https://api.wallex.ir/v1/account/profile"

payload = ""
headers = {
  'x-api-key': 'your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/profile' \
--header 'x-api-key: your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");

var raw = "";

var requestOptions = {
  method: "GET",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/account/profile", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/profile');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token'
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "client_id": 123,
    "first_name": "محمد",
    "last_name": "محمدی",
    "national_code": "0123456789",
    "birthday": "1997-03-10T00:00:00Z", // In zulu format
    "address": {
      "city": "تهران",
      "country": "ایران",
      "location": "سعادت آباد - بلوار سعادت آباد",
      "province": "تهران",
      "postal_code": "1234567890",
      "house_number": "10"
    },
    "phone_number": {
      "area_code": "021",
      "main_number": "12345678"
    },
    "mobile_number": "09123456789",
    "email": "something@something.com",
    "verification": "VERIFIED", // Available status -> VERIFIED, UNVERIFIED
    "invite_code": "oX2sym",
    "avatar": "jpeg/adwra8ec-dsq2-4e2d-8da2-d2dffaq2123d",
    "commission": 25, // Commission in invite friend profit
    "settings": {
      "mode": "pro",
      "theme": "dark",
      "logins": true,
      "coin_deposit": true,
      "default_mode": true,
      "coin_withdraw": true,
      "money_deposit": true,
      "money_withdraw": true,
      "order_delete_confirm": false,
      "order_submit_confirm": false
    },
    "status": {
      "first_name": "ACCEPTED",
      "last_name": "ACCEPTED",
      "national_code": "ACCEPTED",
      "national_card_image": "ACCEPTED",
      "birthday": "ACCEPTED",
      "address": "ACCEPTED",
      "phone_number": "ACCEPTED",
      "mobile_number": "ACCEPTED",
      "email": "ACCEPTED"
    },
    "created_at": "2020-11-22T18:47:27Z",
    "updated_at": "2021-05-16T10:38:07Z"
  },
  "message": "The operation was successful",
  "success": true
}
```

HTTP Request

`GET https://api.wallex.ir/v1/account/profile`

# Bank Account

## List of user credit card numbers (Private)

Get a list of user credit card numbers.

```python
import requests

url = "https://api.wallex.ir/v1/account/card-numbers"

payload = ""
headers = {
  'x-api-key': 'your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/card-numbers' \
--header 'x-api-key: your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");

var raw = "";

var requestOptions = {
  method: "GET",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/account/card-numbers", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/card-numbers');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token'
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": [
    {
      "id": 12,
      "card_number": "6037991895454444",
      "owners": ["محمد محمدی"],
      "status": "ACCEPTED" // Available status, ACCEPTED, UNACCEPTED, PENDING
    },
    {
      "id": 14,
      "card_number": "6037991895453333",
      "owners": ["محمد محمدی"],
      "status": "ACCEPTED" // Available status, ACCEPTED, UNACCEPTED, PENDING
    }
  ],
  "message": "The operation was successful",
  "success": true,
  "result_info": {
    "page": 1,
    "per_page": 2,
    "count": 1,
    "total_count": 2
  }
}
```

HTTP Request

`GET https://api.wallex.ir/v1/account/card-numbers`

## Creating a new credit card number (private)

Add a new credit card number to the user account.

```python
import requests
import json

url = "https://api.wallex.ir/v1/account/card-numbers"

payload = json.dumps({
  "card_number": "6037991895454444"
})
headers = {
  'x-api-key': 'your-token',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request POST 'https://api.wallex.ir/v1/account/card-numbers' \
--header 'x-api-key: your-token' \
--header 'Content-Type: application/json' \
--data-raw '{
    "card_number":"6037991895454444"
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  card_number: "6037991895454444",
});

var requestOptions = {
  method: "POST",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/account/card-numbers", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/card-numbers');
$request->setMethod(HTTP_Request2::METHOD_POST);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token',
  'Content-Type' => 'application/json'
));
$request->setBody('{\n    "card_number":"6037991895454444"\n}');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "id": 12,
    "card_number": "6037991895454444",
    "owners": ["محمد محمدی"],
    "status": "PENDING" // Available status, ACCEPTED, UNACCEPTED, PENDING
  },
  "message": "The operation was successful",
  "success": true
}
```

HTTP Request

`POST https://api.wallex.ir/v1/account/card-numbers`

Query Parameters

| Parameter   | Type   | Default  | Description | Sample           |
| ----------- | ------ | -------- | ----------- | ---------------- |
| card_number | String | required | Credit card number  | 6037991895454444 |

## Removing a credit card number (private)

Remove a specific credit card number from the user account. 

```python
import requests

url = "https://api.wallex.ir/v1/account/card-numbers/{cardNumberID}"

payload = ""
headers = {
  'x-api-key': 'your-token'
}

response = requests.request("DELETE", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location -g --request DELETE 'https://api.wallex.ir/v1/account/card-numbers/{cardNumberID}' \
--header 'x-api-key: your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");

var raw = "";

var requestOptions = {
  method: "DELETE",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch(
  "https://api.wallex.ir/v1/account/card-numbers/{cardNumberID}",
  requestOptions
)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/card-numbers/{cardNumberID}');
$request->setMethod(HTTP_Request2::METHOD_DELETE);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token'
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": [],
  "message": "Deleted successfully",
  "success": true
}
```

HTTP Request

`DELETE https://api.wallex.ir/v1/account/card-numbers/{cardNumberID}`

## List of IBANs

Get the list of IBANs of the user account. 

```python
import requests

url = "https://api.wallex.ir/v1/account/ibans"

payload = ""
headers = {
  'x-api-key': 'your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/ibans' \
--header 'x-api-key: your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");

var raw = "";

var requestOptions = {
  method: "GET",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/account/ibans", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/ibans');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token'
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "id": 10,
    "iban": "IR520000000000000000000000",
    "owners": ["محمد محمدی"],
    "bank_name": "قرض الحسنه رسالت",
    "status": "PENDING" // Available status, ACCEPTED, UNACCEPTED, PENDING
  },
  "message": "The operation was successful",
  "success": true
}
```

HTTP Request

`GET https://api.wallex.ir/v1/account/ibans`

## Creating a new IBAN (Private)

Add a new IBAN to the user account.

```python
import requests
import json

url = "https://api.wallex.ir/v1/account/ibans"

payload = json.dumps({
  "iban": "520000000000000000000000"
})
headers = {
  'x-api-key': 'your-token',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request POST 'https://api.wallex.ir/v1/account/ibans' \
--header 'x-api-key: your-token' \
--header 'Content-Type: application/json' \
--data-raw '{
    "iban":"520000000000000000000000"
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  iban: "520000000000000000000000",
});

var requestOptions = {
  method: "POST",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/account/ibans", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/ibans');
$request->setMethod(HTTP_Request2::METHOD_POST);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token',
  'Content-Type' => 'application/json'
));
$request->setBody('{\n    "iban":"520000000000000000000000"\n}');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "id": 10,
    "iban": "IR520000000000000000000000",
    "owners": ["محمد محمدی"],
    "bank_name": "قرض الحسنه رسالت",
    "status": "ACCEPTED" // Available status, ACCEPTED, UNACCEPTED, PENDING
  },
  "message": "The operation was successful",
  "success": true
}
```

HTTP Request

`POST https://api.wallex.ir/v1/account/ibans`

Query Parameters

| Parameter | Type   | Default  | Description       | Sample                   |
| --------- | ------ | -------- | ----------------- | ------------------------ |
| iban      | String | required |  IBAN | 520000000000000000000000 |

## Removing the IBAN (Private)

Remove a specific IBAN from the user account.

```python
import requests

url = "https://api.wallex.ir/v1/account/ibans/{ibanID}"

payload = ""
headers = {
  'x-api-key': 'your-token'
}

response = requests.request("DELETE", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location -g --request DELETE 'https://api.wallex.ir/v1/account/ibans/{ibanID}' \
--header 'x-api-key: your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");

var raw = "";

var requestOptions = {
  method: "DELETE",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/account/ibans/{ibanID}", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/ibans/{ibanID}');
$request->setMethod(HTTP_Request2::METHOD_DELETE);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token'
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": [],
  "message": "Deleted successfully",
  "success": true
}
```

HTTP Request

`DELETE https://api.wallex.ir/v1/account/ibans/{ibanID}`

# Wallet

## Cryptocurrency wallet (Private)

.Get a cyptocurrency wallet 

```python
import requests

url = "https://api.wallex.ir/v1/account/wallets/usdt"

payload = ""
headers = {
  'x-api-key': 'your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/wallets/usdt' \
--header 'x-api-key: your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");

var raw = "";

var requestOptions = {
  method: "GET",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/account/wallets/usdt", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/wallets/usdt');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token'
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "wallets": {
      "ERC20": {
        "network": {
          "name": "ERC20",
          "message": null,
          "deposit_availability": "ENABLE",// Available -> ENABLE, DISABLE
          "withdrawal_availability": "ENABLE"// Available -> ENABLE, DISABLE
        },
        "address": "0xeee8b3730b0032354c88d59b379d7dad40fb1b3e",
        "memo": null,
        "min_confirmation": 10,// Minimum confirmations that we need to accept a deposit
        "transaction_fee": 20// Withdrawal transaction fee
        "min_withdrawal_value": 40,
        "min_deposit_value": 2
      },
      "TRC20": {
        "network": {
          "name": "TRC20",
          "message": null,
          "deposit_availability": "ENABLE",
          "withdrawal_availability": "ENABLE"
        },
        "address": "TMuywP2Xxam9ZMW93LfqzPaPUqSfrPXtap",
        "memo": null,
        "min_confirmation": 1,
        "transaction_fee": 1.5,
        "min_withdrawal_value": 5,
        "min_deposit_value": 2
      }
    },
    "coin_type": {
      "key": "USDT",
      "name": "تتر",
      "name_en": "Tether",
      "type": "ADDRESS",
      "deposit_availability": "ENABLE",// Available -> ENABLE, DISABLE
      "withdrawal_availability": "ENABLE"// Available -> ENABLE, DISABLE
    }
  },
  "message": "The operation was successful",
  "success": true
}
```

HTTP Request

`GET https://api.wallex.ir/v1/account/wallets/usdt`

## Account balance (Private)

Get account balance.

```python
import requests

url = "https://api.wallex.ir/v1/account/balances"

payload = ""
headers = {
  'x-api-key': 'your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/balances' \
--header 'x-api-key: your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");

var raw = "";

var requestOptions = {
  method: "GET",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/account/balances", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/balances');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token'
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "balances": {
      "BCH": {
        "asset": "BCH",
        "faName": "بیت کوین کش",
        "fiat": false, // Fiat is sort of real money types (like toman or dollar)
        "value": "0.00000000", // Total balance
        "locked": "0.00000000" // Locked balance
      },
      "BTC": {
        "asset": "BTC",
        "faName": "بیت کوین",
        "fiat": false,
        "value": "0.00000045",
        "locked": "0.00000000"
      },
      "DASH": {
        "asset": "DASH",
        "faName": "دش",
        "fiat": false,
        "value": "0.00000000",
        "locked": "0.00000000"
      },
      "EOS": {
        "asset": "EOS",
        "faName": "ایاس",
        "fiat": false,
        "value": "0.00000000",
        "locked": "0.00000000"
      },
      "ETH": {
        "asset": "ETH",
        "faName": "اتریوم",
        "fiat": false,
        "value": "0.00000000",
        "locked": "0.00000000"
      },
      "LTC": {
        "asset": "LTC",
        "faName": "لایت کوین",
        "fiat": false,
        "value": "0.00024310",
        "locked": "0.00000000"
      },
      "TMN": {
        "asset": "TMN",
        "faName": "تومان",
        "fiat": true,
        "value": "21051348",
        "locked": "21000000"
      },
      "TRX": {
        "asset": "TRX",
        "faName": "ترون",
        "fiat": false,
        "value": "0.00000000",
        "locked": "0.00000000"
      },
      "USDT": {
        "asset": "USDT",
        "faName": "تتر",
        "fiat": false,
        "value": "562.47946200",
        "locked": "0.00000000"
      },
      "XLM": {
        "asset": "XLM",
        "faName": "استلار",
        "fiat": false,
        "value": "0.00000000",
        "locked": "0.00000000"
      },
      "XRP": {
        "asset": "XRP",
        "faName": "ریپل",
        "fiat": false,
        "value": "0.00000000",
        "locked": "0.00000000"
      }
    }
  },
  "message": "The operation was successful",
  "success": true
}
```

HTTP Request

`GET https://api.wallex.ir/v1/account/balances`

## ACL and commission fee

Get your ACL and commission fee.

```python
import requests

url = "https://api.wallex.ir/v1/account/fee"

payload = ""
headers = {
  'x-api-key': 'your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/fee' \
--header 'x-api-key: your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");

var raw = "";

var requestOptions = {
  method: "GET",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/account/fee", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/fee');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token'
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "BTCTMN": {
      "makerFeeRate": "0.00300000", // Seller fee
      "takerFeeRate": "0.00400000", // Buyer fee
      "recent_days_sum": 240448 // Recent trade value sum
    },
    "ETHTMN": {
      "makerFeeRate": "0.00300000",
      "takerFeeRate": "0.00400000",
      "recent_days_sum": 240448
    },
    "BCHTMN": {
      "makerFeeRate": "0.00300000",
      "takerFeeRate": "0.00400000",
      "recent_days_sum": 240448
    },
    "LTCTMN": {
      "makerFeeRate": "0.00300000",
      "takerFeeRate": "0.00400000",
      "recent_days_sum": 240448
    },
    "DASHTMN": {
      "makerFeeRate": "0.00300000",
      "takerFeeRate": "0.00400000",
      "recent_days_sum": 240448
    },
    "USDTTMN": {
      "makerFeeRate": "0.00300000",
      "takerFeeRate": "0.00400000",
      "recent_days_sum": 240448
    },
    "BTCUSDT": {
      "makerFeeRate": "0.00200000",
      "takerFeeRate": "0.00200000",
      "recent_days_sum": 0
    },
    "ETHUSDT": {
      "makerFeeRate": "0.00200000",
      "takerFeeRate": "0.00200000",
      "recent_days_sum": 0
    },
    "BCHUSDT": {
      "makerFeeRate": "0.00200000",
      "takerFeeRate": "0.00200000",
      "recent_days_sum": 0
    },
    "LTCUSDT": {
      "makerFeeRate": "0.00200000",
      "takerFeeRate": "0.00200000",
      "recent_days_sum": 0
    },
    "DASHUSDT": {
      "makerFeeRate": "0.00200000",
      "takerFeeRate": "0.00200000",
      "recent_days_sum": 0
    },
    "XRPTMN": {
      "makerFeeRate": "0.00300000",
      "takerFeeRate": "0.00400000",
      "recent_days_sum": 240448
    },
    "XLMTMN": {
      "makerFeeRate": "0.00300000",
      "takerFeeRate": "0.00400000",
      "recent_days_sum": 240448
    },
    "EOSTMN": {
      "makerFeeRate": "0.00300000",
      "takerFeeRate": "0.00400000",
      "recent_days_sum": 240448
    },
    "TRXTMN": {
      "makerFeeRate": "0.00300000",
      "takerFeeRate": "0.00400000",
      "recent_days_sum": 240448
    },
    "XRPUSDT": {
      "makerFeeRate": "0.00200000",
      "takerFeeRate": "0.00200000",
      "recent_days_sum": 0
    },
    "XLMUSDT": {
      "makerFeeRate": "0.00200000",
      "takerFeeRate": "0.00200000",
      "recent_days_sum": 0
    },
    "EOSUSDT": {
      "makerFeeRate": "0.00200000",
      "takerFeeRate": "0.00200000",
      "recent_days_sum": 0
    },
    "TRXUSDT": {
      "makerFeeRate": "0.00200000",
      "takerFeeRate": "0.00200000",
      "recent_days_sum": 0
    },
    "default": [],
    "metaData": {
      "levels": [
        0, 5000000, 20000000, 50000000, 100000000, 500000000, 2000000000,
        10000000000, 50000000000, 100000000000
      ],
      "coin_levels": [0, 1000, 3000, 10000, 50000, 100000, 500000, 1000000],
      "latestTradesSum": 240448
    }
  },
  "message": "The operation was successful",
  "success": true
}
```

HTTP Request

`GET https://api.wallex.ir/v1/account/fee`

# Orders and Trades

## New order (Private)

Place a new order in your target market.

```python
import requests
import json

url = "https://api.wallex.ir/v1/account/orders"

payload = json.dumps({
  "price": "24828",
  "quantity": "10",
  "side": "sell",
  "symbol": "USDTTMN",
  "type": "limit",
  "client_id": "myUniqueRandomClientID"
})
headers = {
  'x-api-key': 'your-token',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request POST 'https://api.wallex.ir/v1/account/orders' \
--header 'x-api-key: your-token' \
--header 'Content-Type: application/json' \
--data-raw '{
    "price":"24828",
    "quantity":"10",
    "side":"sell",
    "symbol":"USDTTMN",
    "type":"limit",
    "client_id":"myUniqueRandomClientID"
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  price: "24828",
  quantity: "10",
  side: "sell",
  symbol: "USDTTMN",
  type: "limit",
  client_id: "myUniqueRandomClientID",
});

var requestOptions = {
  method: "POST",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/account/orders", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/orders');
$request->setMethod(HTTP_Request2::METHOD_POST);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token',
  'Content-Type' => 'application/json'
));
$request->setBody('{\n    "price":"24828",\n    "quantity":"10",\n    "side":"sell",\n    "symbol":"USDTTMN",\n    "type":"limit",\n    "client_id":"myUniqueRandomClientID"\n}');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "symbol": "USDTTMN",
    "type": "LIMIT", // Available -> LIMIT, MARKET
    "side": "SELL", // Available -> BUY, SELL
    "clientOrderId": "LIMIT-93c76637-9742-466d-b30a-89926d2cf11c",
    "transactTime": 1624846226,
    "price": "24828.0000000000000000",
    "origQty": "10.0000000000000000", // Original quantity
    "executedQty": "0.0000000000000000", // Traded quantity
    "status": "NEW",
    "active": true, // Active means this order is still in orderbook
    "fills": []
  },
  "message": "The operation was successful",
  "success": true
}
```

HTTP Request

`POST https://api.wallex.ir/v1/account/orders`

Query Parameters

| Parameter | Type            | Default  | Description                                                                  | Sample                 |
| --------- | --------------- | -------- | ---------------------------------------------------------------------------- | ---------------------- |
| price     | String          | required | Pricr                                                                    | 24828                  |
| quantity  | String          | required | مقدار                                                                        | 10                     |
| side      | String          | required |Side (buy-sell)                                                         | sell                   |
| symbol    | String          | required | Market Name                                                                    | USDTTMN                |
| type      | String          | required | Order Type (limit,market)                                                     | limit                  |
| client_id | String (Unique) | optional | Unique transaction ID (will be generated randomly if not sent) | myUniqueRandomClientID |

## Order cancellation (Private)

Cancel The order.

```python
import requests
import json

url = "https://api.wallex.ir/v1/account/orders"

payload = json.dumps({
  "clientOrderId": "LIMIT-93c76637-9742-466d-b30a-89926d2cf11c"
})
headers = {
  'x-api-key': 'your-token',
  'Content-Type': 'application/json'
}

response = requests.request("DELETE", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request DELETE 'https://api.wallex.ir/v1/account/orders' \
--header 'x-api-key: your-token' \
--header 'Content-Type: application/json' \
--data-raw '{
    "clientOrderId":"LIMIT-93c76637-9742-466d-b30a-89926d2cf11c"
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  clientOrderId: "LIMIT-93c76637-9742-466d-b30a-89926d2cf11c",
});

var requestOptions = {
  method: "DELETE",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/v1/account/orders", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/orders');
$request->setMethod(HTTP_Request2::METHOD_DELETE);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token',
  'Content-Type' => 'application/json'
));
$request->setBody('{\n    "clientOrderId":"LIMIT-93c76637-9742-466d-b30a-89926d2cf11c"\n}');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "symbol": "USDTTMN",
    "type": "LIMIT",
    "side": "SELL",
    "clientOrderId": "LIMIT-93c76637-9742-466d-b30a-89926d2cf11c",
    "transactTime": 1624846226,
    "price": "24828.0000000000000000",
    "origQty": "10.0000000000000000",
    "executedQty": "0.0000000000000000",
    "status": "FILLED",
    "active": false,
    "fills": []
  },
  "message": "The operation was successful",
  "success": true
}
```

HTTP Request

`DELETE https://api.wallex.ir/v1/account/orders`

Query Parameters

| Parameter     | Type            | Default  | Description      | Sample                                     |
| ------------- | --------------- | -------- | ---------------- | ------------------------------------------ |
| clientOrderId | String (Unique) | required | Unique transaction ID | LIMIT-93c76637-9742-466d-b30a-89926d2cf11c |

## Active orders (Private)

Get the list of your active orders. 

```python
import requests

url = "https://api.wallex.ir/v1/account/openOrders?symbol=USDTTMN"

payload = ""
headers = {
  'x-api-key': 'your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/openOrders?symbol=USDTTMN' \
--header 'x-api-key: your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");

var raw = "";

var requestOptions = {
  method: "GET",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch(
  "https://api.wallex.ir/v1/account/openOrders?symbol=USDTTMN",
  requestOptions
)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/openOrders?symbol=USDTTMN');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token'
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "orders": [
      {
        "symbol": "BTCTMN",
        "type": "LIMIT",
        "side": "BUY",
        "clientOrderId": "LIMIT-93b9b17b-c21b-4f34-a7b0-0b43cae08adc",
        "price": "700000000.0000000000000000",
        "origQty": "0.0500000000000000",
        "executedQty": "0.0000000000000000",
        "status": "NEW",
        "active": true
      },
      ...
    ]
  },
  "message": "The operation was successful",
  "success": true,
  "result_info": {
    "page": 1,
    "per_page": 1,
    "count": 1,
    "total_count": 1
  }
}
```

HTTP Request

`GET https://api.wallex.ir/v1/account/openOrders`

Query Parameters

| Parameter | Type   | Default  | Description | Sample  |
| --------- | ------ | -------- | ----------- | ------- |
| symbol    | String | required | Market Name   | USDTTMN |

## Recent transactions (Private)

Get a list of your latest transactions.

```python
import requests

url = "https://api.wallex.ir/v1/account/trades?symbol=USDTTMN&side=sell&active=false"

payload = ""
headers = {
  'x-api-key': 'your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/trades?symbol=USDTTMN&side=sell&active=false' \
--header 'x-api-key: your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("x-api-key", "your-token");

var raw = "";

var requestOptions = {
  method: "GET",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch(
  "https://api.wallex.ir/v1/account/trades?symbol=USDTTMN&side=sell&active=false",
  requestOptions
)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/v1/account/trades?symbol=USDTTMN&side=sell&active=false');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'your-token'
));
$request->setBody('');
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}
```

> Output

```json
{
  "result": {
    "AccountLatestTrades": [
      {
        "symbol": "LTCTMN",
        "quantity": "0.0253800000000000",
        "price": "4343723.0000000000000000",
        "sum": "110243.0000000000000000", // Quantity * Price
        "fee": "0.0000000000000000",
        "feeCoefficient": "0.0000000000000000", // Fee percentage
        "feeAsset": "LTC",
        "isBuyer": true,
        "timestamp": "2021-05-29T07:55:06Z"
      },
      {
        "symbol": "LTCTMN",
        "quantity": "0.0300000000000000",
        "price": "4340184.0000000000000000",
        "sum": "130205.0000000000000000",
        "fee": "0.0000000000000000",
        "feeCoefficient": "0.0000000000000000",
        "feeAsset": "LTC",
        "isBuyer": true,
        "timestamp": "2021-05-29T05:48:16Z"
      }
    ]
  },
  "message": "The operation was successful",
  "success": true,
  "result_info": {
    "page": 1,
    "per_page": 100,
    "count": 1,
    "total_count": 2
  }
}
```

HTTP Request

`GET https://api.wallex.ir/v1/account/trades`

Query Parameters

| Parameter | Type    | Default  | Description              | Sample  |
| --------- | ------- | -------- | ------------------------ | ------- |
| symbol    | String  | optional | Market Name                | USDTTMN |
| side      | String  | optional | Side (buy, sell)   | sell    |
| active    | Boolean | optional | Actives and inactives | false   |
