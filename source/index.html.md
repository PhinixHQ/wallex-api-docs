---
title: قیمت لحظه ای و نرخ ارزهای دیجیتال | صرافی والکس api

language_tabs: # must be one of https://git.io/vQNgJ
- shell
- python
- javascript
- php

toc_footers:
- <a href='https://wallex.ir/app/auth/register'>عضویت در والکس</a>


search: false

code_clipboard: false
---

# مفاهیم اولیه

<ul style="direction: rtl;padding-right: 80px">
<li>وب‌سرویس‌های والکس به صورت REST در اختیار کاربران قرار گرفته است.</li>
<li>دقت شود در هدر تمامی در خواست ها دو هدر زیر ارسال شود تا پاسخ مناسب دریافت شود :
  <ul>
    <li>Accept: application/json</li>
    <li>Content-Type: application/json</li>
  </ul>
</li>
</ul>

# احراز هویت

متد ها یا خصوصی یا عمومی هستند. برای دسترسی به متد های خصوصی باید ابتدا یک Token دریافت کنید اما برای استفاده از متد های عمومی بدون احراز هویت و دریافت Token هم قادر به استفاده خواهید بود.

> برای دریافت Token از متد زیر استفاده کنید :


```python
import requests
import json

url = "https://wallex.ir/api/v2/login"

payload = json.dumps({
  "email": "your@email.com",
  "password": "your-password"
})
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request POST 'https://wallex.ir/api/v2/login' \
--header 'Content-Type: application/json' \
--data-raw '{
    "email":"your@email.com",
    "password":"your-password"
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
 "email":"your@email.com",
  "password": "your-password"
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://wallex.ir/api/v2/login", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://wallex.ir/api/v2/login');
$request->setMethod(HTTP_Request2::METHOD_POST);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'Content-Type' => 'application/json'
));
$request->setBody('{\n    "email":"your@email.com",\n    "password":"your-password"\n}');
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

> در خروجی پایین token را مشاهده میکنید که باید در هدر درخواست های خصوصی ارسال شود.

```json
{
  "result": {
    "token": "ODca212Wkc1dA123D54c5t5tDh9wsDvdsgf4w3w.........."
  },
  "success": true
}
```



<p class="title">HTTP Request</p>

<p class="url">
<span>POST https://wallex.ir/api/v2/login</span>
</p>

<p class="title">Query Parameters</p>

Parameter | Type | Default | Description | Sample |
--------- | ---- | ------- | ----------- | ------ |
email | String | required | ایمیل کاربر | your@email.com
password | String | required | رمز عبور کاربر| your-password

نکته :
<aside class=“info”>
توکن صادر شده بعد از ۲۴ ساعت منقضی می شود . در صورت نیاز به توکن بلند مدت می توانید پارامتر remember را true ارسال نمایید .
توکن صادر شده به این روش  به مدت یک ماه اعتبار دارد .
</aside>

#بازارها

##لیست بازار ها و وضعیتشان (عمومی)

با این درخواست لیست بازار ها را دریافت کنید.


```python
import requests

url = "https://wallex.ir/api/v2/markets"

payload = ""
headers = {}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://wallex.ir/api/v2/markets' \
--data-raw ''
```

```javascript
var raw = "";

var requestOptions = {
  method: 'GET',
  body: raw,
  redirect: 'follow'
};

fetch("https://wallex.ir/api/v2/markets", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://wallex.ir/api/v2/markets');
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

> خروجی

```json
{
  "result": {
    "symbols": {
      "BTC-TMN": {
        "symbol": "BTC-TMN",
        "baseAsset": "BTC",// Source currency
        "baseAssetPrecision": 8,// Source currency precision count
        "quoteAsset": "TMN",// Destination currency
        "quotePrecision": 0,// Destination currency precision count
        "faName": "بیت کوین - تومان",
        "faBaseAsset": "بیت کوین",
        "faQuoteAsset": "تومان",
        "stepSize": 6, //max quantity precision
        "tickSize": 0, //max price precision
        "minQty": 0.000001,// Minimum quantity that is acceptable
        "maxQty": 100000,// Maximum quantity that is acceptable
        "minNotional": 100000,// Minimum trade sum that is acceptable
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



<p class="title">HTTP Request</p>

<p class="url"><span>GET https://wallex.ir/api/v2/markets</span></p>


##لیست سفارشات بازار (عمومی)

با این درخواست لیست سفارشات (orderbook) را دریافت کنید.

```python
import requests

url = "https://wallex.ir/api/v2/depth?symbol=BTC-TMN"

payload = ""
headers = {}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://wallex.ir/api/v2/depth?symbol=BTC-TMN' \
--data-raw ''
```

```javascript
var raw = "";

var requestOptions = {
  method: 'GET',
  body: raw,
  redirect: 'follow'
};

fetch("https://wallex.ir/api/v2/depth?symbol=BTC-TMN", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://wallex.ir/api/v2/depth?symbol=BTC-TMN');
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

> خروجی

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



<p class="title">HTTP Request</p>

<p class="url"><span>GET https://wallex.ir/api/v2/depth</span></p>

<p class="title">Query Parameters</p>

<p class='one-item'></p>

Parameter | Type | Default | Description | Sample |
--------- | ---- | ------- | ----------- | ------ |
symbol | String | required | نام بازار | BTC-TMN

نکته :

<aside class="info">
برای مشاهده توضیحات درباره market Symbol های والکس میتوانید به درخواست لیست بازار ها مراجعه کنید
</aside>

<aside class="info">
  برای دریافت لیست کل سفارشات در همه بازار ها کافیست درخواست را به آدرس زیر ارسال کنید
</aside>

<p class='one-item'></p>

Request Type  |  Path
---------     | ----------- 
GET           | https://wallex.ir/api/v2/depth/all


##لیست آخرین معاملات بازار (عمومی)

با این درخواست لیست آخرین معاملات بازار های والکس را دریافت کنید.


```python
import requests

url = "https://wallex.ir/api/v2/latestTrades?symbol=BTC-TMN"

payload = ""
headers = {}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://wallex.ir/api/v2/latestTrades?symbol=BTC-TMN' \
--data-raw ''
```

```javascript
var raw = "";

var requestOptions = {
  method: 'GET',
  body: raw,
  redirect: 'follow'
};

fetch("https://wallex.ir/api/v2/latestTrades?symbol=BTC-TMN", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://wallex.ir/api/v2/latestTrades?symbol=BTC-TMN');
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

> خروجی

```json
{
  "result": {
    "latestTrades": [
      {
        "symbol": "BTC-TMN",
        "quantity": "0.0017700000000000",
        "price": "852231321.0000000000000000",
        "sum": "1508449.4381700000000000",
        "isBuyOrder": false,
        "timestamp": "2021-06-28T00:02:15Z"
      },
      {
        "symbol": "BTC-TMN",
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



<p class="title">HTTP Request</p>

<p class="url"><span>GET https://wallex.ir/api/v2/latestTrades</span></p>

<p class="title">Query Parameters</p>

<p class='one-item'></p>

Parameter | Type | Default | Description | Sample |
--------- | ---- | ------- | ----------- | ------ |
symbol | String | required | نام بازار | BTC-TMN

نکته :

<aside class="info">
<code>timestamp</code>  با فرمت ZULU نمایش داده میشود.
</aside>


#کیف پول

##دریافت موجودی (خصوصی)

با این درخواست موجودی حساب را برای تمام ارز ها دریافت کنید.

```python
import requests

url = "https://wallex.ir/api/v2/account/balances"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://wallex.ir/api/v2/account/balances' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

var raw = "";

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://wallex.ir/api/v2/account/balances", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://wallex.ir/api/v2/account/balances');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'Authorization' => 'Bearer your-token'
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

> خروجی

```json
{
  "result": {
    "balances": {
      "BCH": {
        "asset": "BCH",
        "faName": "بیت کوین کش",
        "fiat": false,// Fiat is sort of real money types (like toman or dollar)
        "value": "0.00000000",// Total balance
        "locked": "0.00000000"// Locked balance
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


<p class="title">HTTP Request</p>

<p class="url"><span>GET https://wallex.ir/api/v2/account/balances</span></p>



##دریافت سطح و میزان کارمزد (خصوصی)

با این درخواست سطح و میزان کارمزد حسابتان را دریافت کنید.

```python
import requests

url = "https://wallex.ir/api/v2/account/fee"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://wallex.ir/api/v2/account/fee' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

var raw = "";

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://wallex.ir/api/v2/account/fee", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://wallex.ir/api/v2/account/fee');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'Authorization' => 'Bearer your-token'
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

> خروجی

```json
{
  "result": {
    "BTC-TMN": {
      "makerFeeRate": "0.00300000",// Seller fee
      "takerFeeRate": "0.00400000",// Buyer fee
      "recent_days_sum": 240448// Recent trade value sum
    },
    "ETH-TMN": {
      "makerFeeRate": "0.00300000",
      "takerFeeRate": "0.00400000",
      "recent_days_sum": 240448
    },
    ...,
    
    "DOGE-USDT": {
      "makerFeeRate": "0.00200000",
      "takerFeeRate": "0.00200000",
      "recent_days_sum": 0
    },
    "default": [],
    "metaData": {
      "levels": [
        0,
        5000000,
        20000000,
        50000000,
        100000000,
        500000000,
        2000000000,
        10000000000,
        50000000000,
        100000000000
      ],
      "coin_levels": [
        0,
        1000,
        3000,
        10000,
        50000,
        100000,
        500000,
        1000000
      ],
      "latestTradesSum": 240448
    }
  },
  "message": "The operation was successful",
  "success": true
}
```


<p class="title">HTTP Request</p>

<p class="url"><span>GET https://wallex.ir/api/v2/account/fee</span></p>




#سفارشات و معاملات

##ایجاد سفارش جدید (خصوصی)

با این درخواست یک سفارش جدید در بازار مورد نظرتان ثبت کنید.

```python
import requests
import json

url = "https://wallex.ir/api/v2/account/orders"

payload = json.dumps({
  "price": "24828",
  "quantity": "10",
  "side": "sell",
  "symbol": "USDT-TMN",
  "type": "limit",
  "client_id": "myUniqueRandomClientID"
})
headers = {
  'Authorization': 'Bearer your-token',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request POST 'https://wallex.ir/api/v2/account/orders' \
--header 'Authorization: Bearer your-token' \
--header 'Content-Type: application/json' \
--data-raw '{
    "price":"24828",
    "quantity":"10",
    "side":"sell",
    "symbol":"USDT-TMN",
    "type":"limit",
    "client_id":"myUniqueRandomClientID"
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  "price": "24828",
  "quantity": "10",
  "side": "sell",
  "symbol": "USDT-TMN",
  "type": "limit",
  "client_id": "myUniqueRandomClientID"
});

var requestOptions = {
  method: 'POST',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://wallex.ir/api/v2/account/orders", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://wallex.ir/api/v2/account/orders');
$request->setMethod(HTTP_Request2::METHOD_POST);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'Authorization' => 'Bearer your-token',
  'Content-Type' => 'application/json'
));
$request->setBody('{\n    "price":"24828",\n    "quantity":"10",\n    "side":"sell",\n    "symbol":"USDT-TMN",\n    "type":"limit",\n    "client_id":"myUniqueRandomClientID"\n}');
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

> خروجی

```json
{
  "result": {
    "symbol": "USDT-TMN",
    "type": "LIMIT",// Available -> LIMIT, MARKET
    "side": "SELL",// Available -> BUY, SELL
    "clientOrderId": "LIMIT-93c76637-9742-466d-b30a-89926d2cf11c",
    "transactTime": 1624846226,
    "price": "24828.0000000000000000",
    "origQty": "10.0000000000000000",// Original quantity
    "executedQty": "0.0000000000000000",// Traded quantity
    "status": "NEW",
    "active": true,// Active means this order is still in orderbook
    "fills": []
  },
  "message": "The operation was successful",
  "success": true
}
```

<p class="title">HTTP Request</p>

<p class="url"><span>POST https://wallex.ir/api/v2/account/orders</span></p>

<p class="title">Query Parameters</p>

Parameter | Type | Default | Description | Sample |
--------- | ---- | ------- | ----------- | ------ |
price | String | required | قیمت واحد | 24828
quantity | String | required | مقدار | 10
side | String | required | طرف سفارش (buy-sell) | sell
symbol | String | required | نام بازار | USDT-TMN
type | String | required | نوع سفارش (limit,market) | limit
client_id | String (Unique) | optional | شناسه یکتا معامله (در صورت ارسال نشدن یک شناسه به صورت رندوم ایجاد خواهد شد) | myUniqueRandomClientID


##لغو سفارش (خصوصی)

با این درخواست سفارشتان را لغو کنید.

```python
import requests
import json

url = "https://wallex.ir/api/v2/account/orders"

payload = json.dumps({
  "clientOrderId": "LIMIT-93c76637-9742-466d-b30a-89926d2cf11c"
})
headers = {
  'Authorization': 'Bearer your-token',
  'Content-Type': 'application/json'
}

response = requests.request("DELETE", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request DELETE 'https://wallex.ir/api/v2/account/orders' \
--header 'Authorization: Bearer your-token' \
--header 'Content-Type: application/json' \
--data-raw '{
    "clientOrderId":"LIMIT-93c76637-9742-466d-b30a-89926d2cf11c"
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  "clientOrderId": "LIMIT-93c76637-9742-466d-b30a-89926d2cf11c"
});

var requestOptions = {
  method: 'DELETE',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://wallex.ir/api/v2/account/orders", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://wallex.ir/api/v2/account/orders');
$request->setMethod(HTTP_Request2::METHOD_DELETE);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'Authorization' => 'Bearer your-token',
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

> خروجی

```json
{
  "result": {
    "symbol": "USDT-TMN",
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

<p class="title">HTTP Request</p>

<p class="url"><span>DELETE https://wallex.ir/api/v2/account/orders</span></p>

<p class="title">Query Parameters</p>

<p class='one-item'></p>

Parameter | Type | Default | Description | Sample |
--------- | ---- | ------- | ----------- | ------ |
clientOrderId | String (Unique) | required | شناسه یکتا سفارش | LIMIT-93c76637-9742-466d-b30a-89926d2cf11c


##دریافت لیست سفارشات فعال حساب (خصوصی)

با این درخواست لیست سفارشات فعال حسابتان را دریافت کنید.

```python
import requests

url = "https://wallex.ir/api/v2/account/openOrders?symbol=USDT-TMN"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://wallex.ir/api/v2/account/openOrders?symbol=USDT-TMN' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

var raw = "";

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://wallex.ir/api/v2/account/openOrders?symbol=USDT-TMN", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://wallex.ir/api/v2/account/openOrders?symbol=USDT-TMN');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'Authorization' => 'Bearer your-token'
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

> خروجی

```json
{
  "result": {
    "orders": [
      {
        "symbol": "BTC-TMN",
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

<p class="title">HTTP Request</p>

<p class="url"><span>GET https://wallex.ir/api/v2/account/openOrders</span></p>

<p class="title">Query Parameters</p>

<p class='one-item'></p>

Parameter | Type | Default | Description | Sample |
--------- | ---- | ------- | ----------- | ------ |
symbol | String | required | نام بازار | USDT-TMN



##دریافت لیست معاملات اخیر حساب (خصوصی)

با این درخواست لیستی از آخرین معاملات حسابتان دریافت کنید.

```python
import requests

url = "https://wallex.ir/api/v2/account/trades?symbol=USDT-TMN&side=sell&active=false"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://wallex.ir/api/v2/account/trades?symbol=USDT-TMN&side=sell&active=false' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

var raw = "";

var requestOptions = {
  method: 'GET',
  headers: myHeaders,
  body: raw,
  redirect: 'follow'
};

fetch("https://wallex.ir/api/v2/account/trades?symbol=USDT-TMN&side=sell&active=false", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://wallex.ir/api/v2/account/trades?symbol=USDT-TMN&side=sell&active=false');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'Authorization' => 'Bearer your-token'
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

> خروجی

```json
{
  "result": {
    "AccountLatestTrades": [
      {
        "symbol": "LTC-TMN",
        "quantity": "0.0253800000000000",
        "price": "4343723.0000000000000000",
        "sum": "110243.0000000000000000",// Quantity * Price
        "fee": "0.0000000000000000",
        "feeCoefficient": "0.0000000000000000",// Fee percentage
        "feeAsset": "LTC",
        "isBuyer": true,
        "timestamp": "2021-05-29T07:55:06Z"
      },
      {
        "symbol": "LTC-TMN",
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

<p class="title">HTTP Request</p>

<p class="url"><span>GET https://wallex.ir/api/v2/account/trades</span></p>

<p class="title">Query Parameters</p>

Parameter | Type | Default | Description | Sample |
--------- | ---- | ------- | ----------- | ------ |
symbol | String | optional | نام بازار | USDT-TMN
side | String | optional | سمت معامله (buy, sell) | sell
active | Boolean | optional | فعال ها یا غیر فعال ها ؟ | false


#محدودیت فراخوانی

##ای‌پی‌ای‌های عمومی 

محدودیت در این ای پی ای ها براساس هر ای پی اعمال میشود

|   Method  | URL                   | Rate Limit      |
|-----------|-----------------------|-----------------|
|    POST   | api/v2/login          | 5 req/min
|    GET    | api/v2/markets        | 60 req/min
|    GET    | api/v2/depth          | 1800 req/min
|    GET    | api/v2/latestTrades   | 60 req/min
|    GET    | api/v2/stats          | 60 req/min
|    GET    | api/v1/stats          | 60 req/min
|    GET    | api/v1/coins          | 60 req/min


##ای‌پی‌ای‌های خصوصی
 
محدودیت در این ای پی ای ها براساس هر کاربر اعمال میشود
‍‍‍

|   Method  | URL                   | Rate Limit      |
|-----------|-----------------------|-----------------|
|    GET    | api/v2/account/orders/{clientOrderId} |  60 req/min
|    GET    | api/v2/account/balances               |  60 req/min
|    GET    | api/v2/account/orders                 |  60 req/min
|    GET    | api/v2/account/openOrders             |  60 req/min
|    GET    | api/v2/account/trades                 |  60 req/min
|    GET    | api/v2/account/fee                    |  60 req/min
|    POST   | api/v2/account/orders                 |  60 req/min
|    DELETE | api/v2/account/orders                 |  60 req/min
