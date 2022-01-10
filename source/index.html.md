---
title: مستندات API والکس

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript
  - php

toc_footers:
  - <a href='https://wallex.ir/login'>عضویت در والکس</a>

search: false

code_clipboard: false
---

# مفاهیم اولیه

وب‌سرویس‌های والکس به صورت REST در اختیار کاربران قرار گرفته است.

# احراز هویت

متد ها یا خصوصی یا عمومی هستند. برای دسترسی به متد های خصوصی باید ابتدا یک Token دریافت کنید اما برای استفاده از متد های عمومی بدون احراز هویت و دریافت Token هم قادر به استفاده خواهید بود.

> برای دریافت Token از متد زیر استفاده کنید :

```python
import requests
import json

url = "https://api.wallex.ir/auth/login"

payload = json.dumps({
  "mobile_number": "09121111111",
  "password": "your-password"
})
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request POST 'https://api.wallex.ir/auth/login' \
--header 'Content-Type: application/json' \
--data-raw '{
    "mobile_number":"09121111111",
    "password":"your-password"
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Content-Type", "application/json");

var raw = JSON.stringify({
  mobile_number: "09121111111",
  password: "your-password",
});

var requestOptions = {
  method: "POST",
  headers: myHeaders,
  body: raw,
  redirect: "follow",
};

fetch("https://api.wallex.ir/auth/login", requestOptions)
  .then((response) => response.text())
  .then((result) => console.log(result))
  .catch((error) => console.log("error", error));
```

```php
<?php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.wallex.ir/auth/login');
$request->setMethod(HTTP_Request2::METHOD_POST);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'Content-Type' => 'application/json'
));
$request->setBody('{\n    "mobile_number":"09121111111",\n    "password":"your-password"\n}');
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
    "token": "ODca212Wkc1dA123D54c5t5tDh9wsDvdsgf4w3w",
    "stream_key": "WjdeidAdsa32HN23D3r2jrasdfasd",
    "two_step": {
      "status": true, // true means you're okay
      "type": "off", // two step type
      "channel": null // sent from where (example : 09123456790)
    }
  },
  "message": "با موفقیت وارد شدید",
  "success": true
}
```

HTTP Request

`POST https://api.wallex.ir/auth/login`

Query Parameters

| Parameter     | Type   | Default  | Description        | Sample        |
| ------------- | ------ | -------- | ------------------ | ------------- |
| mobile_number | String | required | شماره موبایل کاربر | 09121111111   |
| password      | String | required | رمز عبور کاربر     | your-password |

نکته :

<aside class="info">

قبل از استفاده از API ورود دو مرحله ای را غیرفعال کنید.
<br>
با استفاده از رشته <code>stream_key</code> می توانید به private socket اکانت کانکت شوید.

</aside>

#بازارها

##لیست بازار ها و وضعیتشان (عمومی)

با این درخواست لیست بازار ها را دریافت کنید.

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

> خروجی

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

##آمار بازار جهانی (عمومی)

با این درخواست آخرین آمار بازار های جهانی ارز های مختلف را دریافت کنید.

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

> خروجی

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

نکته :

<aside class="info">
مقادیر <code>ath_date</code>, <code>created_at</code>, <code>updated_at</code> با فرمت ZULU نمایش داده میشود.
</aside>

##لیست سفارشات بازار (عمومی)

با این درخواست لیست سفارشات (orderbook) را دریافت کنید.

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

HTTP Request

`GET https://api.wallex.ir/v1/depth`

Query Parameters

| Parameter | Type   | Default  | Description | Sample |
| --------- | ------ | -------- | ----------- | ------ |
| symbol    | String | required | نام بازار   | BTCTMN |

نکته :

<aside class="info">
برای مشاهده توضیحات درباره market Symbol های والکس میتوانید به درخواست لیست بازار ها مراجعه کنید
</aside>

##لیست آخرین معاملات بازار (عمومی)

با این درخواست لیست آخرین معاملات بازار های والکس را دریافت کنید.

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

> خروجی

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
| symbol    | String | required | نام بازار   | BTCTMN |

نکته :

<aside class="info">
<code>timestamp</code>  با فرمت ZULU نمایش داده میشود.
</aside>

##آمار OHLC بازار والکس (عمومی)

با این درخواست آمار OHLC بازار والکس را دریافت کنید.

<a href="https://en.wikipedia.org/wiki/Open-high-low-close_chart" target="_blank">آمار OHLC چیست ؟‌</a>

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

> خروجی

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
| symbol     | String  | required | نام بازار          | BTCTMN     |
| resolution | String  | required | بازه زمانی هر کندل | D          |
| from       | Integer | required | زمان ابتدا بازه    | 1624841423 |
| to         | Integer | required | زمان پایان بازه    | 1624841423 |

لیست resolution های قابل قبول :

| Resolution | Description |
| ---------- | ----------- |
| 60         | یک ساعت     |
| 180        | سه ساعت     |
| 360        | شش ساعت     |
| 720        | دوازده ساعت |
| D          | یک روز      |
| 2D         | دو روز      |
| 3D         | سه روز      |

نکته :

<aside class="info">
مقادیر <code>from</code> و <code>to</code> فرمت timestamp است.
</aside>

#پروفایل

##دریافت اطلاعات پروفایل کاربر (خصوصی)

با این درخواست اطلاعات پروفایل خود را دریافت کنید.

```python
import requests

url = "https://api.wallex.ir/v1/account/profile"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/profile' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

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

#حساب بانکی

##دریافت لیست شماره کارت های حساب (خصوصی)

با این درخواست لیست شماره کارت های حسابتان را دریافت کنید.

```python
import requests

url = "https://api.wallex.ir/v1/account/card-numbers"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/card-numbers' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

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

##ایجاد شماره کارت جدید (خصوصی)

با این درخواست یک شماره کارت جدید به حسابتان اضافه کنید.

```python
import requests
import json

url = "https://api.wallex.ir/v1/account/card-numbers"

payload = json.dumps({
  "card_number": "6037991895454444"
})
headers = {
  'Authorization': 'Bearer your-token',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request POST 'https://api.wallex.ir/v1/account/card-numbers' \
--header 'Authorization: Bearer your-token' \
--header 'Content-Type: application/json' \
--data-raw '{
    "card_number":"6037991895454444"
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");
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
  'Authorization' => 'Bearer your-token',
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

> خروجی

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
| card_number | String | required | شماره کارت  | 6037991895454444 |

##حذف شماره کارت (خصوصی)

با این درخواست یک شماره کارت خاص را از حسابتان حذف کنید.

```python
import requests

url = "https://api.wallex.ir/v1/account/card-numbers/{cardNumberID}"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("DELETE", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location -g --request DELETE 'https://api.wallex.ir/v1/account/card-numbers/{cardNumberID}' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

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
  "result": [],
  "message": "Deleted successfully",
  "success": true
}
```

HTTP Request

`DELETE https://api.wallex.ir/v1/account/card-numbers/{cardNumberID}`

##دریافت لیست شماره شبا های حساب (خصوصی)

با این درخواست لیست شماره شبا های حسابتان را دریافت کنید.

```python
import requests

url = "https://api.wallex.ir/v1/account/ibans"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/ibans' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

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

##ایجاد شماره شبا جدید (خصوصی)

با این درخواست یک شماره شبا جدید به حسابتان اضافه کنید.

```python
import requests
import json

url = "https://api.wallex.ir/v1/account/ibans"

payload = json.dumps({
  "iban": "520000000000000000000000"
})
headers = {
  'Authorization': 'Bearer your-token',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request POST 'https://api.wallex.ir/v1/account/ibans' \
--header 'Authorization: Bearer your-token' \
--header 'Content-Type: application/json' \
--data-raw '{
    "iban":"520000000000000000000000"
}'
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");
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
  'Authorization' => 'Bearer your-token',
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

> خروجی

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
| iban      | String | required | شماره شبا بدون IR | 520000000000000000000000 |

##حذف شماره شبا (خصوصی)

با این درخواست یک شماره شبا خاص را از حسابتان حذف کنید.

```python
import requests

url = "https://api.wallex.ir/v1/account/ibans/{ibanID}"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("DELETE", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location -g --request DELETE 'https://api.wallex.ir/v1/account/ibans/{ibanID}' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

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
  "result": [],
  "message": "Deleted successfully",
  "success": true
}
```

HTTP Request

`DELETE https://api.wallex.ir/v1/account/ibans/{ibanID}`

#کیف پول

##دریافت کیف پول ارز دیجیتال (خصوصی)

با این درخواست کیف پول ارز دیجیتال مورد نظرتان در والکس را دریافت کنید.

```python
import requests

url = "https://api.wallex.ir/v1/account/wallets/usdt"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/wallets/usdt' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

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

##دریافت موجودی (خصوصی)

با این درخواست موجودی حساب را برای تمام ارز ها دریافت کنید.

```python
import requests

url = "https://api.wallex.ir/v1/account/balances"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/balances' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

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

##دریافت سطح و میزان کارمزد (خصوصی)

با این درخواست سطح و میزان کارمزد حسابتان را دریافت کنید.

```python
import requests

url = "https://api.wallex.ir/v1/account/fee"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/fee' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

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

#سفارشات و معاملات

##ایجاد سفارش جدید (خصوصی)

با این درخواست یک سفارش جدید در بازار مورد نظرتان ثبت کنید.

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
  'Authorization': 'Bearer your-token',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request POST 'https://api.wallex.ir/v1/account/orders' \
--header 'Authorization: Bearer your-token' \
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
myHeaders.append("Authorization", "Bearer your-token");
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
  'Authorization' => 'Bearer your-token',
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

> خروجی

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
| price     | String          | required | قیمت واحد                                                                    | 24828                  |
| quantity  | String          | required | مقدار                                                                        | 10                     |
| side      | String          | required | طرف سفارش (buy-sell)                                                         | sell                   |
| symbol    | String          | required | نام بازار                                                                    | USDTTMN                |
| type      | String          | required | نوع سفارش (limit,market)                                                     | limit                  |
| client_id | String (Unique) | optional | شناسه یکتا معامله (در صورت ارسال نشدن یک شناسه به صورت رندوم ایجاد خواهد شد) | myUniqueRandomClientID |

##لغو سفارش (خصوصی)

با این درخواست سفارشتان را لغو کنید.

```python
import requests
import json

url = "https://api.wallex.ir/v1/account/orders"

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
curl --location --request DELETE 'https://api.wallex.ir/v1/account/orders' \
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
| clientOrderId | String (Unique) | required | شناسه یکتا سفارش | LIMIT-93c76637-9742-466d-b30a-89926d2cf11c |

##دریافت لیست سفارشات فعال حساب (خصوصی)

با این درخواست لیست سفارشات فعال حسابتان را دریافت کنید.

```python
import requests

url = "https://api.wallex.ir/v1/account/openOrders?symbol=USDTTMN"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/openOrders?symbol=USDTTMN' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

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
| symbol    | String | required | نام بازار   | USDTTMN |

##دریافت لیست معاملات اخیر حساب (خصوصی)

با این درخواست لیستی از آخرین معاملات حسابتان دریافت کنید.

```python
import requests

url = "https://api.wallex.ir/v1/account/trades?symbol=USDTTMN&side=sell&active=false"

payload = ""
headers = {
  'Authorization': 'Bearer your-token'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```shell
curl --location --request GET 'https://api.wallex.ir/v1/account/trades?symbol=USDTTMN&side=sell&active=false' \
--header 'Authorization: Bearer your-token' \
--data-raw ''
```

```javascript
var myHeaders = new Headers();
myHeaders.append("Authorization", "Bearer your-token");

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
| symbol    | String  | optional | نام بازار                | USDTTMN |
| side      | String  | optional | سمت معامله (buy, sell)   | sell    |
| active    | Boolean | optional | فعال ها یا غیر فعال ها ؟ | false   |
