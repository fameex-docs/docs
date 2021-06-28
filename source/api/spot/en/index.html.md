---
title: FAMEEX API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - go

toc_footers:
  - <a href='https://www.fameex.com' target='blank'>FAMEEX Exchange</a>

includes:
  # - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: FAMEEX API Documentation
  - name: keywords
    content: FAMEEX,API,Documentation
---



# Update log

**2020-12-22**

- Wallet interface update:
  - Delete the withdrawal record interface of all currencies `v1/api/account/withdrawal/history`
  - Delete the withdrawal record interface of a single currency `v1/api/account/withdrawal/history/currency`
  - Delete the deposit record interface for obtaining all currencies `v1/api/account/deposit/histoty`
  - Delete the interface for querying bill flow records `v1/api/spot/bill_flow`
  - Added an interface for querying spot account transaction bills `v1/api/spot/record/trade`
  - Added an interface for querying the transfer bill of a spot account `v1/api/spot/record/chargewithdraw`
  - Added an interface for querying cash account deposit and withdrawal bills `v1/api/spot/record/trans`
  - Added an interface for querying other bills of spot accounts `v1/api/spot/record/others`
  - Modify the fund transfer interface parameter interface `v1/api/account/transfer`

**2020-11-16**

- Coin trading interface update:
  - Update obtain a list of orders `v1/api/spot/orderlist`to obtain a list of orders
  - Update get order details `v1/api/spot/orderdetail`to obtain orders details
  - Updated list of orders to obtain leverage `v1/api/lever/orders`to obtain a list of orders lever
  - Update get order details leverage `v1/api/lever/orders/detail`to acquire a lever Order details

**2020-10-30**

- Wallet interface update:
  - Modify the fund transfer function interface `v1/api/account/transfer`

**2020-10-29**

- Wallet interface update:
  - Added function interface for leveraged pending orders `v1/api/lever/orders/place`
  - Added a function interface for leveraged order cancellation `v1/api/lever/orders/cancel`
  - New interface for batch withdrawal of leveraged orders `v1/api/lever/orders/batch_cancel`
  - Added a function interface for obtaining the order list of margin accounts `v1/api/lever/orders`
  - Added a function interface for obtaining the details of a margin account order `v1/api/lever/orders/detail`
  - Added function interface for obtaining leverage configuration `v1/api/lever/pair/config`

**2020-10-28**

- Wallet interface update:
  - Added an interface for obtaining a margin account statement `v1/api/lever/ledger`
  - Added the prompt parameter interface for obtaining a specific currency pair of a margin account and repaying a currency under a specific currency `v1/api/lever/repayparam`
  - Added a new interface for obtaining specific currency pairs for margin accounts and repaying currencies under specific currencies `v1/api/lever/repay`
  - Added a new interface for obtaining specific currency pairs in a margin account, and a prompt parameter interface for borrowing currency in a specific currency `v1/api/lever/borrow`
  - Added interface for obtaining specific currency pairs in margin accounts and borrowing currency in specific currencies `v1/api/lever/borrowparam`

**2020-10-27**

- Wallet interface update:
  - Added an interface for obtaining margin account information `v1/api/lever/accounts`
  - Added an interface for obtaining the details of a specific currency pair under a margin account `v1/api/lever/accounts/{pairName}`

# Introduction

API overview

FAMEEX provides you with a simple and powerful API interface to help you obtain market information and trade quickly and efficiently.

Before using the API, please create your own API, obtain your AccessKey and SecretKey, and set the IP access restriction of the API.

API trading permissions allow you to quickly obtain the latest market quotations and timely order transactions, query your available and frozen amounts, query your current pending orders, buy or sell, and withdraw orders.

FAMEEX official website homepage: [www.fameex.com](http://www.fameex.com)

If you have any questions during use, please contact FAMEEX official customer service,

Our contact information is as follows:

Official customer service mailbox: [Service@mail.fameex.info](mailto:Service@mail.fameex.info)

Official Weibo: [https://weibo.com/fameexgroup](https://weibo.com/fameexgroup)

Official Twitter: [https://twitter.com/FameexGroup](https://twitter.com/FameexGroup)

Official Telegram: [https://t.me/fameexgroup](https://t.me/fameexgroup)

Official Facebook: [https://www.facebook.com/FameexOfficial](https://www.facebook.com/FameexOfficial)

We will make the most authoritative answer for you.

# Access instructions

## Access URLs

| Access URLs               | Remarks                 |
| ------------------------- | ----------------------- |
| `https://api.fameex.com`  | RESTFUL API             |
| `wss://www.fameex.com/ws` | WebSocket Feed (quotes) |

All requests are based on the Https protocol, and the contentType in the header information of the POST request needs to be uniformly set to:'application/json'

In view of the high latency and poor stability, it is not recommended to access FAMEEX-API through proxy.

## Restriction rules

**Limit frequency:** The limit of each interface is different.

A single API Key dimension is restricted. It is recommended to add a signature to the market API access, otherwise the frequency limit will be stricter.

| Frequency limiting rules                        | Type                  | Remarks |
| ----------------------------------------------- | ----------------------------- | ------- |
| Frequency limit for each AccessKey and each URL | 20 times/2s (most interfaces) | no      |

## Header setting

The parameters of the request header are as follows:

| parameter        | Type | Remarks                                      |
| ---------------- | ------------ | -------------------------------------------- |
| AccessKey        | string       | The Accesskey you applied for                |
| SignatureMethod  | string       | HmacSHA256                                   |
| SignatureVersion | string       | v1.0                                         |
| Timestamp        | int64        | Timestamp of the request time; unit: seconds |
| Signature        | string       | signature                                    |
| Content-Type     | string       | application/json                             |

Explanation of the parameters of the request header:

**API Access Key (AccessKey):** The AccessKey of the API you applied for.

**Signature Method (SignatureMethod):** A hash-based protocol for the user to calculate the signature. Here, HmacSHA256 is used.

**Signature Version (SignatureVersion):** the version of the signature protocol, here v1.0 is used.

**Timestamp:** The time when you made the request. For example: 2019-07-24 00:00:00 corresponds to the timestamp 1563897600. Including this value in the query request helps prevent third parties from intercepting your request.

**Signature:** The value calculated by the signature to ensure that the signature is valid and has not been tampered with.

## signature

\1. Signature description

API requests are very likely to be tampered with during transmission via the internet. In order to ensure that the request has not been changed, all private interfaces except the push service interface must use your API’s AccessKey and SecretKey for signature authentication to verify parameters or parameters Whether the value has changed during transmission.

Method request address: access server address api.fameex.com, such as api.fameex.com/v1/order/orders

**API Key contains the following two parts:**

AccessKey: API access key

SecretKey: The key used for signature authentication and encryption (only visible at the time of application)

`Signature`It is a string spliced on a `timestamp（Unit second） + method（GET OR POST） + requestPath + body`string (+ means string connection), using secretKey, encrypting it according to the HMAC SHA256 method, and outputting it through hex encoding.

Among them, `timestamp`the value of is the same as the request header, `Timestamp`and must be in the decimal seconds format of the UTC time zone Unix timestamp or the ISO8601 standard time format, accurate to the second

method is a request method, all uppercase letters: `GET/POST`.

requestPath is the request interface path. E.g:`/orders?state=1&type=2`

The body refers to the string of the request body (without blank characters, such as \n,\r,\t). If the request has no body (usually a GET request), the body can be omitted. E.g:`{"orderId":"377454671037440"}`

The secretKey is generated when the user applies for the API Key. For example: 533d6e70-21b2-eb5c-f801-c128021c70a1

# Websocket market push

## Heartbeat connection

**Description:**

Long connection heartbeat

**Request path:**

wss://[www.fameex.com/push](http://www.fameex.com/push)

**Request method:**

websocket

> **Request example:**

``` json
{
  "op": "heartBeat"
}
```

| parameter | Mandatory | Type | Remarks                    |
| --------- | -------------- | ------------ | -------------------------- |
| on        | Yes            | string       | Message type ("heartBeat") |

> **Return example:**

```json
  {
    "code": 200,
    "msg": "***",
    "type":"heartBeat"
  }
```

**Return Value:**

| Field Name | Type | Remarks                    |
| ---------- | ------------ | -------------------------- |
| type       | string       | Message type ("heartBeat") |

## login information

**Description:**

Long connection login

**Request path:**

wss://[www.fameex.com/push](http://www.fameex.com/push)

**Request method:**

websocket

> **Request example:**

``` json
{
  "op": "login",
  "AccessKey": "***",
  "sign": "***"
}
```

**Parameter:**

| parameter | Mandatory | Type | Remarks                       |
| --------- | -------------- | ------------ | ----------------------------- |
| on        | Yes            | string       | Message type ("Login")        |
| AccessKey | Yes            | string       | AccessKey applied for         |
| sign      | Yes            | string       | Unique page identifier (uuid) |

> **Return example:**

```json
{
  "code": 200,
  "msg": "***",
  "type": "login"
}
```

**Return Value:**

| Field Name | Type | Remarks                |
| ---------- | ------------ | ---------------------- |
| code       | int          | 200, normal            |
| msg        | string       | Remarks                |
| type       | string       | Message type ("login") |

## Register Kline Information

**Description:**

This interface is registered for K-line service

**Request path:**

wss://[www.fameex.com/push](http://www.fameex.com/push)

**Request method:**

websocket

> **Request example:**

```json
{
  "op": "register",
  "type": "kLineData",
  "base": "***",
  "quote": "***",
  "KTime": "***"
}
```

**Parameter:**

| parameter | Mandatory | Type | Remarks                                                |
| --------- | -------------- | ------------ | ------------------------------------------------------ |
| on        | Yes            | string       | Message type ("register")                              |
| type      | Yes            | string       | Registration type ("kLineData")                        |
| base      | Yes            | string       | Trading currency in the trading pair                   |
| quote     | Yes            | string       | Denominated currency in the trading pair               |
| Ktima     | Yes            | string       | K Line Time("1","5","15","30","60","120","240","1D","1W") |

**Return Value:**

no

## Register Home Quotes

**Description:**

This interface is used to register the homepage quotation service

**Request path:**

wss://[www.fameex.com/push](http://www.fameex.com/push)

**Request method:**

websocket

> **Request example:**

```json
{
  "op": "register",
  "type": "homemarket"
}
```

**Parameter:**

| parameter | Mandatory | Type | Remarks           |
| --------- | -------------- | ------------ | ----------------- |
| on        | Yes            | string       | Message type      |
| type      | Yes            | string       | Registration Type |

**Return Value:**

no

## Register in-depth quotes

**Description:**

This interface registers for in-depth services

**Request path:**

wss://[www.fameex.com/push](http://www.fameex.com/push)

**Request method:**

websocket

> **Request example:**

```json
{
  "op": "register",
  "type": "transDepth",
  "base": "***",
  "quote": "***",
  "percision": 0
}
```

**Parameter:**

| parameter | Mandatory | Type | Remarks                                  |
| --------- | -------------- | ------------ | ---------------------------------------- |
| on        | Yes            | string       | Message type                             |
| type      | Yes            | string       | Registration Type                        |
| base      | Yes            | string       | Trading currency in the trading pair     |
| quote     | Yes            | string       | Denominated currency in the trading pair |
| percision | Yes            | int          | Depth precision digits                   |

**Return Value:**

no

## Push coin pair depth list

**Description:**

This interface pushes homepage market data

**Request path:**

wss://[www.fameex.com/push](http://www.fameex.com/push)

**Request method:**

websocket

**Parameter:**

no

> **Return example:**

```json
 {
    "code": 200,
    "msg": "***",
    "type":"homemarket",
    "data": {
        "base_quote":{
            "base":"",
            "quote":"",
            "transactionPrice":0,
            "gain":0,
            "coinHour24OpenPrice":0,
            "coinHour24LowPrice":0,
            "coinHour24HighPrice":0,
            "hour24Volume":0,
            "tranHour24Volume":0,
            "tranByCnyPrice":0,
            "baseByCnyPrice":0
        }
    }
  }
```

**Return Value:**

| Field Name          | Type | Remarks                                  |
| ------------------- | ------------ | ---------------------------------------- |
| type                | string       | Message type                             |
| base_quote          | string       | Currency pair key                        |
| base                | string       | Trading currency in the trading pair     |
| quote               | string       | Denominated currency in the trading pair |
| transactionPrice    | float        | final price                              |
| gain                | float        | 24-hour increase                         |
| coinHour24OpenPrice | float        | Open 24 hours                            |
| coinHour24LowPrice  | float        | 24 hours minimum                         |
| coinHour24HighPrice | float        | 24 hours maximum                         |
| hour24Volume        | float        | 24-hour volume                           |
| tranHour24Volume    | float        | 24-hour turnover                         |
| tranByCnyPrice      | float        | Price in denominated currency (in RMB)   |
| baseByCnyPrice      | float        | Transaction currency price (in RMB)      |

## Push the depth list of currency pairs

**Description:**

This interface pushes the currency pair depth list data

**Request path:**

wss://[www.fameex.com/push](http://www.fameex.com/push)

**Request method:**

websocket

**Parameter:**

no

> **Return example:**

```json
{
    "code": 200,
    "msg": "***",
    "type": "transDepth",
    "data": {
        "base": "",
        "quote": "",
        "buyList": [
            {
                "price": "",
                "count": "",
                "orderCount": ""
            }
        ],
        "sellList": [
            {
                "price": "",
                "count": "",
                "orderCount": ""
            }
        ],
        "timestamp": 0
    }
}
```

**Return Value:**

| Field Name | Type | Remarks                                  |
| ---------- | ------------ | ---------------------------------------- |
| type       | string       | Message type ("transDepth")              |
| base       | string       | Trading currency in the trading pair     |
| quote      | string       | Denominated currency in the trading pair |
| buyList    | array        | Buy list                                 |
| price      | string       | unit price                               |
| count      | string       | Unit price corresponds to depth quantity |
| orderCount | int          | quantity of order                        |
| sellList   | array        | Sell list                                |
| timestamp  | int64        | Timestamp                                |

## Push K-line data

**Description:**

This interface pushes K-line data

**Request path:**

wss://[www.fameex.com/push](http://www.fameex.com/push)

**Request method:**

websocket

**Parameter:**

no

> **Return example:**

```json
{
    "code": 200,
    "msg": "***",
    "type": "kLineData",
    "data": {
        "time": 0,
        "open": 0,
        "high": 0,
        "low": 0,
        "close": 0,
        "volume": 0
    }
}
```

**Return Value:**

| Field Name | Type | Remarks                                                      |
| ---------- | ------------ | ------------------------------------------------------------ |
| type       | string       | Message type ("kLineData")                                   |
| time       | int64        | K-line timestamp (push according to registered K-line service) |
| open       | float        | Opening price                                                |
| high       | float        | Highest price                                                |
| low        | float        | Lowest price                                                 |
| close      | float        | Closing price                                                |
| volume     | float        | Volume                                                       |

## Push the latest transaction order quotation

**Description:**

This interface pushes the latest transaction order details

**Request path:**

wss://[www.fameex.com/push](http://www.fameex.com/push)

**Request method:**

websocket

**Parameter:**

no

> **Return example:**

```json
 {
    "code": 200,
    "msg": "***",
    "type": "lastTrade",
    "data": {
        "base": "",
        "quote": "",
        "price": 0,
        "count": 0,
        "time": 0,
        "buyType": 0
    }
}
```

**Return Value:**

| Field Name | Type | Remarks                                     |
| ---------- | ------------ | ------------------------------------------- |
| type       | string       | Message type                                |
| base       | string       | Trading currency in the trading pair        |
| quote      | string       | Denominated currency in the trading pair    |
| price      | float        | Transaction price                           |
| count      | float        | The number of transactions                  |
| time       | int64        | Transaction time unit: milliseconds         |
| buyType    | int          | Buying and selling direction 0, buy, 1 sell |

## Push order transaction or cancellation

**Description:**

Push buyers and sellers or own orders to complete or cancel

**Request path:**

wss://[www.fameex.com/push](http://www.fameex.com/push)

**Request method:**

websocket

**Parameter:**

no

> **Return example:**

```json
{
    "code": 200,
    "msg": "***",
    "type": "myTransDepth",
    "data": {
        "orderId": "***",
        "base": "BTC",
        "quote": "USDT",
        "state": 11,
        "price": 0.816,
        "count": 0,
        "totalCount": 0,
        "dealedCount": 1,
        "dealedMoney": 3,
        "buyType": 0,
        "buyClass": 0,
        "lossPrice": 0,
        "createTime": 0
    }
}
```

**Return Value:**

| Field Name  | Type | Remarks                                                      |
| ----------- | ------------ | ------------------------------------------------------------ |
| type        | string       | Message type ("myTransDepth")                                |
| orderId     | string       | Order id                                                     |
| base        | string       | Transaction currency                                         |
| quote       | string       | Denominated currency                                         |
| state       | int          | The status code of the order 4-taker is fully executed 8-taker is partially executed 9-maker is partially executed 10-maker is completely executed 11-cancelled |
| price       | float        | Order price                                                  |
| count       | float        | Unsold quantity                                              |
| totalCount  | float        | Number of orders                                             |
| dealedCount | float        | Number of transactions                                       |
| dealedMoney | float        | Turnover                                                     |
| buyType     | int          | Buying and Selling Direction 0-Buy1-Sell                     |
| buyClass    | int          | Transaction Type 0-Limit Price 1 Market Price 2 Take Profit and Stop Loss |
| lossPrice   | float        | Stop profit and stop loss trigger price                      |
| createTime  | int64        | order time                                                   |

## Push partial cancellation of my order

**Description:**

This interface pushes partial transaction or partial cancellation data of my order

**Request path:**

wss://[www.fameex.com/push](http://www.fameex.com/push)

**Request method:**

websocket

**Parameter:**

no

> **Return example:**

```json
 {
    "code": 200,
    "msg": "***",
    "type":"myOrderPartCancel",
    "data": {"orderId":""}
  }
```

**Return Value:**

| Field Name | Type | Remarks                            |
| ---------- | ------------ | ---------------------------------- |
| type       | string       | Message type ("myOrderPartCancel") |
| orderId    | string       | Order id                           |

## Cancel homepage quotes

**Description:**

This interface cancels the homepage quotation service

**Request path:**

wss://[www.fameex.com/push](http://www.fameex.com/push)

**Request method:**

websocket

> **Request example:**

```json
{
  "op": "unregister",
  "type": "homemarket"
}
```

**Parameter:**

| parameter | Mandatory | Type | Remarks           |
| --------- | -------------- | ------------ | ----------------- |
| on        | Yes            | string       | Message type      |
| type      | Yes            | string       | Registration Type |

**Return Value:**

no

# Basic API interface

## Get current system time

Speed limit rule: 20 times/2s

**Description:**

Get the current system time, in seconds

**Request path:**

/v1/common/timestamp

curl `https://api.fameex.com/v1/common/timestamp`

**Routing parameters:**

no

**Post Parameter:**

no

> **Return example:**

```json
{
  "code": 200,
  "ts": 1553254857,
  "data": 1553254857
}
```

**Return Value:**

| Field Name | Type | Remarks                            |
| ---------- | ------------ | ---------------------------------- |
| code       | int          | 200, normal                        |
| ts         | int64        | Request time, seconds              |
| data       | int64        | Return value, current time, second |

## Get all trading currency pairs

Speed limit rule: 20 times/2s

**Function description:**

This interface returns all trading currency pairs supported by the FAMEEX platform.

**Request path:**

/v1/common/symbols

curl `https://api.fameex.com/v1/common/symbols`

**Routing parameters:**

no

**Post Parameter:**

no

> **Return example:**

```json
{
  "code": 200,
  "ts": 1554178231,
  "msg": "",
  "total": 20,
  "data": [
    {
      "base": "ETH",
      "pair": "ETH/BTC",
      "quote": "BTC",
      "pricePercision": "6",
      "amountPercision": "2",
      "permitAmount": "0.2"
    }
  ]
}
```

**Return Value:**

| Field Name      | Type | Remarks                                                      |
| --------------- | ------------ | ------------------------------------------------------------ |
| code            | int          | 200, normal                                                  |
| ts              | int64        | Request time, seconds                                        |
| msg             | string       | Description of the return value this time                    |
| total           | int          | Total number of trading currency pairs                       |
| data            | list         | Return data: currency pair information                       |
| base            | string       | Transaction currency                                         |
| quote           | string       | Denominated currency                                         |
| pair            | string       | Trading currency pairs                                       |
| pricePercision  | string       | The precision of the denominated currency in the trading pair (digits after the decimal point) |
| amountPercision | string       | The precision of the trading currency in the trading pair (digits after the decimal point) |
| permitAmount    | string       | Minimum number of pending orders                             |

## Get all transaction currencies

Speed limit rule: 20 times/2s

**Function description:**

This interface returns all trading currencies supported by FAMEEX.

**Request path:**

/v1/common/currencys

curl `https://api.fameex.com/v1/common/currencys`

**Routing parameters:**

no

**Post Parameter:**

no

> **Return example:**

```json
{
  "code": 200,
  "data": {
    "list": [
      {
        "currency": "USDT",
        "nameZh": "泰达币",
        "nameEn": "Tether",
        "isBase": 1,
        "isQuote": 1,
        "currencyDetail": {
          "ERC20": {
            "id": 49,
            "chainType": "ERC20",
            "currencyRecharge": {
              "state": 1,
              "minChargeAmount": "1",
              "blockConfirmNumber": 10
            },
            "currencyWithdraw": {
              "state": 1,
              "onceminwithdraw": "5",
              "daymaxwithdrawtimes": 5,
              "feewithdraw": "1.5"
            },
            "warnrule": {
              "withDrawAmount": "0",
              "withDrawAmountToCny": "0",
              "withDrawTimes": 0,
              "chargeAmount": "0",
              "chargeAmountToCny": "0"
            }
          }
        }
      },
      {
        "currency": "BTC",
        "nameZh": "比特币",
        "nameEn": "Bitcoin",
        "isBase": 1,
        "isQuote": 1,
        "currencyDetail": {
          "BTC": {
            "id": 48,
            "chainType": "BTC",
            "currencyRecharge": {
              "state": 1,
              "minChargeAmount": "1",
              "blockConfirmNumber": 10
            },
            "currencyWithdraw": {
              "state": 1,
              "onceminwithdraw": "0.01",
              "daymaxwithdrawtimes": 5,
              "feewithdraw": "0.005"
            },
            "warnrule": {
              "withDrawAmount": "0",
              "withDrawAmountToCny": "0",
              "withDrawTimes": 0,
              "chargeAmount": "0",
              "chargeAmountToCny": "0"
            }
          }
        }
      }
    ]
  }
}
```

**Return Value:**

| Field Name                | Type | Remarks                                                      |
| ------------------------- | ------------ | ------------------------------------------------------------ |
| code                      | int          | 200, normal                                                  |
| msg                       | string       | Description of the return value this time                    |
| data                      | list         | Return data: currency information                            |
| currency                  | string       | Currency abbreviation                                        |
| nameEn                    | string       | English name                                                 |
| nameZh                    | string       | Chinese name                                                 |
| isBase                    | int          | 1- Can be used as transaction currency 2- Can not be used as transaction currency |
| isQuote                   | int          | 1- Can be used as a denominated currency 2- Can not be used as a denominated currency |
| minChargeAmount           | string       | Minimum deposit amount                                       |
| blockConfirmNumber        | int          | Block confirmation number                                    |
| onceminwithdraw           | string       | Maximum number of withdrawals at a time                      |
| daymaxwithdrawtimes       | int          | Maximum number of withdrawals in a single day                |
| feewithdraw               | string       | Withdrawal fee                                               |
| state in currencyRecharge | int          | Deposit status 1-open 2-close                                |
| state in currencyWithdraw | int          | Withdrawal status 1-open 2-close                             |

# Quote API interface

## Get k-line data

Speed limit rule: 20 times/2s

**Function description:**

This interface obtains historical K-line data.

**Request path:**

GET /v1/market/history/kline

curl `https://api.fameex.com/v1/market/history/kline`

**Routing parameters:**

| parameter   | Mandatory | Type | Remarks                                                     |
| ----------- | -------------- | ------------ | ----------------------------------------------------------- |
| pairName    | Yes            | string       | Currency pair, for example "ETH_BTC"                        |
| granularity | Yes            | string       | Time granularity,like（ "1","5","15","30","60","120","240","1D","1W") |
| startTime   | no             | string       | Start time, timestamp (unit: seconds)                       |
| endTime     | no             | string       | End time, timestamp (unit: seconds)                         |

**Post Parameter:**

no

> **Return example:**

```json
{
  "code": 200,
  "msg": "SUCCESS",
  "data": [
    {
      "time": 1570518900,
      "amount": 0,
      "open": 0.00481,
      "close": 0.00481,
      "low": 0.00481,
      "hight": 0.00481,
      "vol": 0
    }
  ]
}
```

**Return Value:**

| Field Name | Type | Remarks                                                |
| ---------- | ------------ | ------------------------------------------------------ |
| code       | int          | Return value status                                    |
| time       | int64        | Timestamp                                              |
| amount     | float        | Transaction volume counted in the denominated currency |
| open       | float        | Opening price                                          |
| close      | float        | Closing price                                          |
| low        | float        | Lowest price                                           |
| hight      | float        | Highest price                                          |
| vol        | float        | Transaction volume counted in transaction currency     |

## Market Depth Data

Speed limit rule: 20 times/2s

**Function description:**

This interface returns the current market depth data of the specified trading pair.

**Request path:**

/v1/market/depth

curl `https://api.fameex.com/v1/market/depth`

**Routing parameters:**

| parameter | Mandatory | Type | Remarks                                            |
| --------- | -------------- | ------------ | -------------------------------------------------- |
| pairName  | Yes            | string       | For example: BTC_USDT                              |
| size      | no             | string       | Return the number of depth gears, up to 200        |
| depth     | no             | string       | Depth price decimal places, for example: -2,-1,0,1 |

**Routing parameters:**

no

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "base": "omg",
    "quote": "usdt",
    "buyList": [
      {
        "price": "10.00",
        "count": "0.6",
        "orderCount": 1
      }
    ],
    "sellList": [
      {
        "price": "11.00",
        "count": "1",
        "orderCount": 1
      }
    ],
    "timestamp": 0
  }
}
```

**Return Value:**

| Field Name | Type | Remarks                        |
| ---------- | ------------ | ------------------------------ |
| code       | int          | 200, normal                    |
| msg        | string       | Remarks                        |
| data       | map          | Return data: market depth data |
| base       | string       | Transaction currency           |
| quote      | string       | Denominated currency           |
| price      | string       | unit price                     |
| count      | string       | Quantity                       |
| orderCount | int          | quantity of order              |
| timestamp  | int64        | Timestamp                      |

## Get transaction data

Speed limit rule: 20 times/2s

**Function description:**

This interface returns the transaction detail record of the specified trading pair.

**Request path:**

GET /v1/market/history/trade

curl `https://api.fameex.com/v1/market/history/trade`

**Routing parameters:**

| parameter | Mandatory | Type | Remarks                                                      |
| --------- | -------------- | ------------ | ------------------------------------------------------------ |
| pairName  | Yes            | string       | For example, the name of the currency pair: BTC_USDT         |
| size      | no             | string       | The maximum is 100, if not filled in, 100 will be returned by default |

**Post Parameter:**

no

> **Return example:**

```json
{
  "code": 200,
  "msg": "SUCCESS",
  "data": [
    {
      "orderId": "10401466572658466816",
      "price": "1234546",
      "count": "123456",
      "time": "1122350000000000000",
      "buyType": "0"
    }
  ]
}
```

**Return Value:**

| Field Name | Type | Remarks                                         |
| ---------- | ------------ | ----------------------------------------------- |
| code       | int          | 200, normal                                     |
| msg        | string       | Remarks                                         |
| data       | list         | Return value, latest transaction record         |
| orderId    | string       | Transaction order id                            |
| price      | string       | Transaction price                               |
| count      | string       | The number of transactions                      |
| time       | string       | Time stamp unit of transaction time: nanosecond |
| buyType    | string       | Buying and selling direction 0, buy, 1 sell     |

## Get a ticker information

Speed limit rule: 20 times/2s

**Function description:**

This interface returns a summary of the market data for the last 24 hours, and the data value time interval is 24-hour rolling.

**Request path:**

/v1/market/history/kline24h

curl `https://api.fameex.com/v1/market/history/kline24h`

**Routing parameters:**

| parameter | Mandatory | Type | Remarks                                      |
| --------- | -------------- | ------------ | -------------------------------------------- |
| pairName  | Yes            | string       | Trading currency pair, for example "ETH_BTC" |

**Post Parameter:**

no

> **Return example:**

```json
{
  "code": 200,
  "msg": "SUCCESS",
  "data": {
    "pairName": "OMG_ETH",
    "last": "0.0048",
    "buyFirst": "00477",
    "sellFirst": "00478",
    "coinHour24OpenPrice": "00479",
    "coinHour24LowPrice": "0.0048",
    "coinHour24HighPrice": "0.00482",
    "base24Volume": "10",
    "quoteHour24Volume": "0.02405",
    "timestamp": 1570523192282391200
  }
}
```

**Return Value:**

| Field Name          | Type | Remarks                                                      |
| ------------------- | ------------ | ------------------------------------------------------------ |
| code                | int          | 200, normal                                                  |
| pairName            | string       | For example, the name of the currency pair: "OMG_ETH"        |
| last                | string       | Latest transaction price                                     |
| buyFirst            | string       | Buy one price                                                |
| sellFirst           | string       | Sell one price                                               |
| coinHour24OpenPrice | string       | 24-hour opening price                                        |
| coinHour24LowPrice  | string       | Lowest price in 24 hours                                     |
| coinHour24HighPrice | string       | Highest price in 24 hours                                    |
| base24Volume        | string       | Statistics of 24-hour trading volume by trading currency     |
| quoteHour24Volume   | string       | Calculate the 24-hour trading volume in the currency of denomination |
| timestamp           | int64        | System timestamp (unit: nanosecond)                          |

## Get all ticker information

Speed limit rule: 20 times/2s

**Function description:**

This interface returns a summary of the market data for the last 24 hours, and the data value time interval is 24-hour rolling.

**Request path:**

/v1/market/history/kline24h/all

curl `https://api.fameex.com/v1/market/history/kline24h/all`

**Routing parameters:**

no

**Post Parameter:**

no

> **Return example:**

```json
{
  "code": 200,
  "msg": "SUCCESS",
  "data": [
    {
      "pairName": "BTC_USDT",
      "last": "0",
      "buyFirst": "0",
      "sellFirst": "0",
      "coinHour24OpenPrice": "0",
      "coinHour24LowPrice": "0",
      "coinHour24HighPrice": "0",
      "base24Volume": "0",
      "quoteHour24Volume": "0",
      "timestamp": 1570524123199845100
    },
    {
      "pairName": "OMG_USDT",
      "last": "0",
      "buyFirst": "0",
      "sellFirst": "0",
      "coinHour24OpenPrice": "0",
      "coinHour24LowPrice": "0",
      "coinHour24HighPrice": "0",
      "base24Volume": "0",
      "quoteHour24Volume": "0",
      "timestamp": 1570524123212810600
    }
  ]
}
```

**Return Value:**

| Field Name          | Type | Remarks                                                      |
| ------------------- | ------------ | ------------------------------------------------------------ |
| code                | int          | 200, normal                                                  |
| pairName            | string       | For example, the name of the currency pair: "OMG_ETH"        |
| last                | string       | Latest transaction price                                     |
| buyFirst            | string       | Buy one price                                                |
| sellFirst           | string       | Sell one price                                               |
| coinHour24OpenPrice | string       | 24-hour opening price                                        |
| coinHour24LowPrice  | string       | Lowest price in 24 hours                                     |
| coinHour24HighPrice | string       | Highest price in 24 hours                                    |
| base24Volume        | string       | Statistics of 24-hour trading volume by trading currency     |
| quoteHour24Volume   | string       | Calculate the 24-hour trading volume in the currency of denomination |
| timestamp           | int64        | System timestamp (unit: nanosecond)                          |

# Exchange API interface

## New order

Speed limit rule: 100 times/2s

**Function description:**

This interface provides the function of canceling all unexecuted orders of a specified currency pair or currency pairs.

**Request path:**

/v1/api/spot/orders

curl `https://api.fameex.com/v1/api/spot/orders`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                  |
| --------- | -------------- | ------------ | ---------------------------------------- |
| base      | Yes            | string       | Trading currency in the trading pair     |
| quote     | Yes            | string       | Denominated currency in the trading pair |
| buyType   | Yes            | int          | 0 buy, 1 sell                            |
| price     | Yes            | string       | Order unit price                         |
| count     | Yes            | string       | Order quantity                           |

> **Return example:**

```json
{
  "code": 200,
  "msg": "SUCCESS",
  "orderId": "10383992916667793408"
}
```

**Return Value:**

| Field Name | Type | Remarks                 |
| ---------- | ------------ | ----------------------- |
| code       | int          | 200, normal             |
| msg        | string       | Information Description |
| orderId    | string       | Pending order id        |

## Cancel Order

Speed limit rule: 100 times/2s

**Function description:**

This interface provides the function of canceling unfilled orders.

**Request path:**

/v1/api/spot/cancel_orders

curl `https://api.fameex.com/v1/api/spot/cancel_orders`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                  |
| --------- | -------------- | ------------ | ---------------------------------------- |
| orderid   | Yes            | string       | Order id                                 |
| base      | Yes            | string       | Trading currency in the trading pair     |
| quote     | Yes            | string       | Denominated currency in the trading pair |

> **Return example:**

```json
{
    "code": 200,
    "msg": "SUCCESS",
    "orderId": "10383992916667793408"
}
```

**Return Value:**

| Field Name | Type | Remarks                |
| ---------- | ------------ | ---------------------- |
| code       | int          | 200, normal            |
| msg        | string       | Remarks                |
| orderId    | string       | Id to cancel the order |

## Batch cancellation

Speed limit rule: 100 times/2s

**Function description:**

This interface provides the function of canceling all unexecuted orders of a specified currency pair or currency pairs.

**Request path:**

/v1/api/spot/cancel_orders_all

curl `https://api.fameex.com/v1/api/spot/cancel_orders_all`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                            |
| --------- | -------------- | ------------ | -------------------------------------------------- |
| buyType   | Yes            | int          | Buying and selling direction 0 buy, 1 sell, -1 all |
| base      | Yes            | string       | Trading currency in the trading pair               |
| quote     | Yes            | string       | Denominated currency in the trading pair           |
| startTime | Yes            | int64        | "0" all                                            |
| endTime   | Yes            | int64        | "0" all                                            |

> **Return example:**

```json
{
  "code": 200,
  "msg": "SUCCESS"
}
```

**Return Value:**

| Field Name | Type | Remarks     |
| ---------- | ------------ | ----------- |
| code       | int          | 200, normal |
| msg        | string       | SUCCESS     |

## Get order details

Speed limit rule: 20 times/2s

**Function description:**

This interface obtains the specified order information through the order ID.

**Request path:**

/v1/api/spot/orderdetail

curl `https://api.fameex.com/v1/api/spot/orderdetail`

`Headers Parameter`

no

**Routing parameters:**

| parameter | Mandatory | Type | Remarks                                               |
| --------- | -------------- | ------------ | ----------------------------------------------------- |
| orderId   | Yes            | string       | Order id                                              |
| pairName  | Yes            | string       | The name of the currency pair (for example: BTC_USDT) |

**Post Parameter:**

no

> **Return example:**

```json
{
  "code": 200,
  "msg": "SUCCESS",
  "data": {
    "orderId": "10403653860461117440",
    "pairName": "OMG_ETH",
    "buyType": 0,
    "buyClass": 0,
    "state": 6,
    "price": "0.00475",
    "count": "2",
    "lossPrice": "0",
    "totalCount": "3",
    "dealedCount": "1",
    "dealedMoney": "0.00475",
    "priceAvg": "0.00475",
    "createTime": 1571041467866373519,
    "endTime": 1571041467866373590
  }
}
```

**Return Value:**

| Field Name  | Type | Remarks                                                      |
| ----------- | ------------ | ------------------------------------------------------------ |
| code        | int          | Return value status                                          |
| msg         | string       | Return value description                                     |
| data        | string       | Return value, order details                                  |
| orderId     | string       | Matching task id                                             |
| pairName    | string       | The name of the currency pair (for example: BTC_USDT)        |
| buyType     | int          | Buying and Selling Direction 0-Buy1-Sell                     |
| buyClass    | int          | Order type 0-limit price1-market price2-stop profit and stop loss |
| state       | int          | Order status 1-To be matched 4-Taker is fully traded 7-In the deep queue 9-Partially traded by maker 10-Maker is fully traded 11-Canceled |
| price       | string       | Pending order unit price                                     |
| count       | string       | Unsold quantity                                              |
| lossPrice   | string       | Stop Profit and Stop Loss Trigger Price                      |
| totalCount  | string       | Total number of pending orders                               |
| dealedCount | string       | Number of transactions                                       |
| dealedMoney | string       | Transaction amount                                           |
| priceAvg    | string       | Average transaction price                                    |
| createTime  | int64        | Order creation time in nanoseconds                           |
| endTime     | int64        | Last update time of order status in nanoseconds              |

## Get a list of orders

Speed limit rule: 20 times/2s

**Function description:**

This interface obtains and lists your current order information (the order information of the last 3 months). This request supports paging, and is sorted and stored in reverse chronological order, with the latest one at the top.

**Request path:**

/v1/api/spot/orderlist

curl `https://api.fameex.com/v1/api/spot/orderlist`

`Headers Parameter`

no

**Routing parameters:**

| parameter | Mandatory | Type | Remarks                                                      |
| --------- | -------------- | ------------ | ------------------------------------------------------------ |
| type      | Yes            | string       | 0 all, 1 completed, 2 not completed, 3 cancelled, 4 cancelled and completed |
| buyType   | Yes            | string       | Trading direction: 0 buy, 1 sell, -1 all                     |
| pairName  | Yes            | string       | The name of the currency pair (for example: BTC_USDT)        |
| pageno    | Yes            | string       | Paging usage, which page                                     |
| pageSize  | Yes            | string       | Paging usage, number per page (0 <pageSize ≤ 500)            |
| startTime | no             | string       | Timestamp, query the start time of the order in seconds      |
| endTime   | no             | string       | Timestamp, query the end time of the order in seconds        |

**Post Parameter:**

no

> **Return example:**

```json
{
  "code": 200,
  "msg": "SUCCESS",
  "data": {
    "pageNum": 1,
    "pageSize": 100,
    "total": 2,
    "list": [
      {
        "id": 1,
        "orderId": "10384834938169458688",
        "userId": "11034971",
        "userType": 0,
        "userLevel": 3,
        "pairName": "omg_eth",
        "buyType": 0,
        "buyClass": 0,
        "state": 4,
        "price": "0.0001222",
        "totalPrice": "0.0001222",
        "count": "2",
        "totalCount": "0",
        "dealedCount": "2",
        "dealedMoney": "0.0002444",
        "priceAvg": "0.00475",
        "lossPrice": "120",
        "triggerGreater": true,
        "matchCount": 1,
        "createTime": 1566554687147922500,
        "endTime": 1566554687293533400,
        "isErr": 0,
        "triggered": 0
      }
    ]
  }
}
```

**Return Value:**

| Field Name     | Type | Remarks                                                      |
| -------------- | ------------ | ------------------------------------------------------------ |
| code           | int          | Return value status                                          |
| msg            | string       | Return value description                                     |
| data           | string       | Return value, order list                                     |
| id             | int64        | Data number                                                  |
| orderId        | string       | Order id                                                     |
| userId         | string       | User id                                                      |
| userType       | int          | User type 1 Ordinary user 2 api user                         |
| userLevel      | int          | user level                                                   |
| base           | string       | Trading currency in the trading pair                         |
| quote          | string       | Denominated currency in the trading pair                     |
| buyType        | int          | 0 buy 1 sell                                                 |
| buyClass       | int          | 0 limit order                                                |
| state          | int          | Order Status 1-Pending Match 4-Taker Completed Transaction 7-In the Deep Queue 8-Taker Partial Transaction 9-maker Partial Transaction 10-maker Complete Transaction 11-Canceled |
| price          | string       | Order unit price                                             |
| totalPrice     | string       | Initial commission price                                     |
| count          | string       | Unsold quantity                                              |
| lossPrice      | string       | Stop Profit and Stop Loss Trigger Price                      |
| totalCount     | string       | The total amount                                             |
| dealedCount    | string       | Number of transactions                                       |
| dealedMoney    | string       | Cumulative turnover                                          |
| priceAvg       | string       | Average transaction price                                    |
| triggerGreater | bool         | Is it greater than or equal to the trigger price of stop profit and stop loss |
| matchCount     | int          | Matches                                                      |
| createTime     | int64        | Order creation time unit: nanosecond                         |
| endTime        | int64        | The last update time unit of the order: nanosecond           |
| isErr          | int          | 0 Normal orders and other orders that failed to unlock assets |
| triggered      | int          | Whether stop profit and stop loss is triggered 0 not triggered 1 triggered |

## Get transaction details

Speed limit rule: 20 times/2s

**Function description:**

This interface gets all your current transaction order information. This request supports paging, and is sorted and stored in reverse chronological order, with the latest one at the top.

**Request path:**

/v1/api/spot/fills

curl `https://api.fameex.com/v1/api/spot/fills`

**Routing parameters:**

| parameter | Mandatory | Type | Remarks                                                      |
| --------- | -------------- | ------------ | ------------------------------------------------------------ |
| pairName  | Yes            | string       | Token name (e.g. BTC_UDST)                                   |
| orderId   | no             | string       | Order id                                                     |
| buyType   | Yes            | string       | Trading direction: 0 buy, 1 sell, -1 all                     |
| pageno    | Yes            | string       | Pagination use, the first few pages, starting from the first page |
| pageSize  | Yes            | string       | Paging usage, number per page (0 <pageSize ≤ 500)            |
| startTime | no             | string       | Timestamp, seconds                                           |
| endTime   | no             | string       | Timestamp, seconds                                           |

**Post Parameter:**

no

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "total": 8,
    "pageSize": 100,
    "pageNum": 1,
    "list": [
      {
        "orderId": "10385145101749346304",
        "pairName": "OMG_ETH",
        "base": "OMG",
        "quote": "ETH",
        "time": 1566628635843252500,
        "buyClass": 0,
        "buyType": 1,
        "price": "120",
        "count": "0.99583334",
        "fee": "0.11950001",
        "feeRate": "0.001",
        "originFeeRate": "0.001"
      }
    ]
  }
}
```

**Return Value:**

| Field Name    | Type | Remarks                                               |
| ------------- | ------------ | ----------------------------------------------------- |
| code          | int          | Return value status                                   |
| msg           | string       | Return value description                              |
| data          | string       | Return value, transaction details                     |
| pairName      | string       | The name of the currency pair (for example: BTC_USDT) |
| base          | string       | Transaction currency                                  |
| quote         | string       | Denominated currency                                  |
| orderId       | string       | Order id                                              |
| time          | int64        | Transaction time in nanoseconds                       |
| buyClass      | int          | Transaction type: 0 limit transaction                 |
| buyType       | int          | Trading direction: 0 buy, 1 sell                      |
| price         | string       | the deal price                                        |
| count         | string       | The number of transactions                            |
| fee           | string       | Handling fee                                          |
| feeRate       | string       | Actual handling fee rate                              |
| originFeeRate | string       | Original fee rate                                     |

## Get all outstanding orders

Speed limit rule: 20 times/2s

**Function description:**

This interface gets all your current transaction order information. This request supports paging, and is sorted and stored in reverse chronological order, with the latest one at the top.

**Request path:**

/v1/api/orders_pending

curl `https://api.fameex.com /v1/api/orders_pending`

**Routing parameters:**

| parameter | Mandatory | Type | Remarks                                                      |
| --------- | -------------- | ------------ | ------------------------------------------------------------ |
| pairName  | Yes            | string       | The name of the currency pair (for example: BTC_USDT)        |
| pageno    | Yes            | string       | Pagination use, the first few pages, starting from the first page |
| pageSize  | Yes            | string       | Paging usage, number per page (0< pageSize ≤ 500)            |

**Post Parameter:**

no

> **Return example:**

```json
{
  "code": 200,
  "msg": "SUCCESS",
  "data": {
    "pageNum": 1,
    "pageSize": 100,
    "list": [
      {
        "orderId": "11403650861072384000",
        "pairName": "OMG_ETH",
        "price": "0.00477",
        "count": "1",
        "buyType": 1,
        "buyClass": 0,
        "dealedCount": "0",
        "dealedMoney": "0",
        "state": 1,
        "time": 1571040752762737823
      }
    ]
  }
}
```

**Return Value:**

| Field Name  | Type | Remarks                                               |
| ----------- | ------------ | ----------------------------------------------------- |
| code        | int          | Return value status                                   |
| msg         | string       | Return value description                              |
| data        | string       | Return value, transaction details                     |
| pairName    | string       | The name of the currency pair (for example: BTC_USDT) |
| orderId     | string       | Order number                                          |
| buyClass    | int          | Transaction type: 0 limit transaction                 |
| buyType     | int          | Trading direction: 0 buy, 1 sell                      |
| price       | string       | Commission price                                      |
| count       | string       | Number of orders                                      |
| dealedCount | string       | Number of transactions                                |
| dealedMoney | string       | Transaction amount                                    |
| state       | int          | 1 Not effective 2 Not completed 3 Partially completed |
| time        | int64        | Time (unit: nanosecond)                               |

# Wallet API interface

## Get wallet info

Speed limit rule: 20 times/2s

**Function description:**

This interface obtains a list of all asset information of the wallet currency account, and queries the balance, freeze and availability information of each currency.

**Request path:**

/v1/api/account/wallet

curl `https://api.fameex.com/v1/api/account/wallet`

**Routing parameters:**

no

**Post Parameter:**

no

> **Return example:**

```json
{
    "code": 200,
    "data": [
        {
            "list": [
                {
                    "available": "0.00000000",
                    "currency": "USDT",
                    "hold": "0.00000000",
                    "total": "0.00000000"
                },
                {
                    "available": "0.00000000",
                    "currency": "BTC",
                    "hold": "0.00000000",
                    "total": "0.00000000"
                }
            ],
            "walletType": "c2c"
        }
    ],
    "userid": "85942975"
}
```

**Return Value:**

| Field Name | Type | Remarks                                                      |
| ---------- | ------------ | ------------------------------------------------------------ |
| code       | int          | 200, normal                                                  |
| data       | list         | Return value, currency account data                          |
| userid     | string       | User id                                                      |
| walletType | string       | Account type: spot-spot account otc-fiat account l2c-margin account |
| available  | string       | Available Balance                                            |
| total      | string       | Total balance                                                |
| currency   | string       | Currency example: BTC                                        |
| hold       | string       | Frozen amount                                                |

## Get the details of single currency

Speed limit rule: 20 times/2s

**Function description:**

Get wallet account details (single currency)

**Request path:**

/v1/api/account/wallet/currency

curl `https://api.fameex.com/v1/api/account/wallet/currency`

**Routing parameters:**

| parameter | Mandatory | Type | Remarks            |
| --------- | -------------- | ------------ | ------------------ |
| currency  | Yes            | string       | Currency, e.g. BTC |

**Post Parameter:**

no

> **Return example:**

```json
{
    "code": 200,
    "data": {
        "available": "20.00000000",
        "hold": "2.00000000"
    },
    "msg": "Success",
    "userid": "481"
}
```

**Return Value:**

| Field Name | Type | Remarks                                               |
| ---------- | ------------ | ----------------------------------------------------- |
| code       | int          | 200, normal                                           |
| msg        | string       | Description of the return value this time             |
| userid     | string       | User id                                               |
| data       | map          | Return value, currency account, details of a currency |
| available  | string       | Available Balance                                     |
| hold       | string       | Frozen amount                                         |

## Transfer

Speed limit rule: 1 time/2s

**Function description:**

This interface provides funds transfer between spot wallets, legal currency wallets, and leveraged wallets within the platform. [Note: Transfers between margin account currency pairs only support transfers between quoted currencies, for example, transfer USDT from BTC_USDT under the margin account to the ETH_USDT currency pair]

**Request path:**

POST /v1/api/account/transfer

curl `https://api.fameex.com/v1/api/account/transfer`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                                      |
| --------- | -------------- | ------------ | ------------------------------------------------------------ |
| currency  | Yes            | string       | Currency type                                                |
| amount    | Yes            | string       | Quantity                                                     |
| from      | Yes            | string       | Transfer account: spot spot account, otc fiat currency account, l2c margin account, swap USDT-futures account |
| to        | Yes            | string       | Transfer account: spot spot account, otc fiat currency account, l2c margin account, swap USDT-futures account |
| fromPair  | no             | string       | The outgoing currency pair during the mutual transfer between margin account currency pairs, for example: BTC_USDT |
| toPair    | no             | string       | The transferred currency pair during the mutual transfer between margin account currency pairs, for example: ETH_USDT |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "orderid": "541989259557478400",
    "userid": "72473826"
  }
}
```

**Return Value:**

| Field Name | Type | Remarks                                           |
| ---------- | ------------ | ------------------------------------------------- |
| code       | int          | 200, normal                                       |
| msg        | string       | success, normal                                   |
| data       | object       | The response object returned by the fund transfer |
| orderid    | string       | Order id                                          |
| userid     | string       | User id                                           |

## Get a transaction bill for a spot account

Speed limit rule: 20 times/2s

**Function description:**

This interface queries the spot account transaction bill.

**Request path:**

POST /v1/api/spot/record/trade

curl `https://api.fameex.com/v1/api/spot/record/trade`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                                      |
| --------- | -------------- | ------------ | ------------------------------------------------------------ |
| tradeType | no             | int          | Transaction type: 0. All; 2. Buy; 3. Sell; 4. Actual fee     |
| currency  | no             | string       | Example of currency name: ETH                                |
| pageno    | Yes            | string       | Page, 1 starts                                               |
| pageSize  | Yes            | string       | Number of pages (0 <pageSize ≤ 500)                          |
| startTime | no             | string       | Start time seconds to query records within the last 90 days at most |
| endTime   | no             | string       | End time seconds                                             |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "userId": "",
    "total": 4,
    "list": [
      {
        "tradeType": 3,
        "operateTime": 1606755600,
        "currency": "USDT",
        "amount": "1.99991550"
      },
      {
        "tradeType": 3,
        "operateTime": 1606701601,
        "currency": "USDT",
        "amount": "0.99979000"
      },
      {
        "tradeType": 3,
        "operateTime": 1606096802,
        "currency": "USDT",
        "amount": "0.99979000"
      },
      {
        "tradeType": 3,
        "operateTime": 1605492004,
        "currency": "USDT",
        "amount": "0.99979000"
      }
    ]
  }
}
```

**Return Value:**

| Field Name  | Type | Remarks                                          |
| ----------- | ------------ | ------------------------------------------------ |
| code        | int          | 200, normal                                      |
| msg         | string       | success, normal                                  |
| data        | object       | Empty string                                     |
| userId      | string       | User id                                          |
| total       | int          | Number of bill records                           |
| list        | array        | Billing record list                              |
| tradeType   | int          | Transaction type: 2. Buy; 3. Sell; 4. Actual fee |
| operateTime | int64        | Operating time                                   |
| currency    | string       | Example of currency name: ETH                    |
| amount      | string       | Quantity                                         |

## Obtain a cash account deposit and withdrawal bill

Speed limit rule: 20 times/2s

**Function description:**

This interface queries the deposit and withdrawal bills of the spot account.

**Request path:**

POST /v1/api/spot/record/chargewithdraw

curl `https://api.fameex.com/v1/api/spot/record/chargewithdraw`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                             |
| --------- | -------------- | ------------ | --------------------------------------------------- |
| tradeType | no             | int          | Transaction type: 0. All; 1. Withdrawal; 2. Deposit |
| currency  | no             | string       | Example of currency name: ETH                       |
| startTime | no             | int64        | Start time: second-level timestamp                  |
| endTime   | no             | int64        | End time time: second-level timestamp               |
| pageno    | Yes            | int          | Page number, starting from 1                        |
| pageSize  | Yes            | int          | Number of pages (0 <pageSize ≤ 500)                 |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "total": 4,
    "list": [
      {
        "tradeType": 2,
        "currency": "USDT",
        "address": "1AUVYs7LfhnZMi7DkD6FeLqsXrXaWy4P9Z",
        "amount": "4.00000000",
        "fee": "1.00000000",
        "label": "",
        "chainType": "USDT_OMNI",
        "state": 3,
        "txId": "INTERNAL",
        "operateTime": 1603784595254607137
      },
      {
        "tradeType": 2,
        "currency": "USDT",
        "address": "1AUVYs7LfhnZMi7DkD6FeLqsXrXaWy4P9Z",
        "amount": "4.00000000",
        "fee": "1.00000000",
        "label": "",
        "chainType": "USDT_OMNI",
        "state": 1,
        "txId": "",
        "operateTime": 1603423928893177788
      },
      {
        "tradeType": 2,
        "currency": "USDT",
        "address": "1AUVYs7LfhnZMi7DkD6FeLqsXrXaWy4P9Z",
        "amount": "4.00000000",
        "fee": "1.00000000",
        "label": "",
        "chainType": "USDT_OMNI",
        "state": 5,
        "txId": "",
        "operateTime": 1603335471347179187
      },
      {
        "tradeType": 2,
        "currency": "USDT",
        "address": "1AUVYs7LfhnZMi7DkD6FeLqsXrXaWy4P9Z",
        "amount": "4.00000000",
        "fee": "1.00000000",
        "label": "",
        "chainType": "USDT_OMNI",
        "state": 1,
        "txId": "",
        "operateTime": 1603334047527967315
      }
    ]
  }
}
```

**Return Value:**

| Field Name  | Type | Remarks                                                      |
| ----------- | ------------ | ------------------------------------------------------------ |
| code        | int          | 200, normal                                                  |
| msg         | string       | success, normal                                              |
| data        | object       | Empty string                                                 |
| total       | int          | Number of bill records                                       |
| list        | array        | Billing record list                                          |
| tradeType   | int          | Transaction type: 1. Withdraw coins; 2. Deposit coins        |
| operateTime | int64        | Operating time                                               |
| currency    | string       | Example of currency name: ETH                                |
| amount      | string       | Quantity                                                     |
| address     | string       | When the tradeType is 1, it represents the withdrawal address; when the tradeType is 2, it represents the deposit address |
| fee         | string       | Withdrawal fee                                               |
| label       | string       | User's label                                                 |
| chainType   | string       | Chain type of currency                                       |
| state       | int          | Bill status: When the tradeType is 1, state respectively represents: 1-Pending review; 2-Under review; 3-Completed; 4-Review failed; 5-Retracted; 6-Withdrawal failed; 7-Initial creation; 8- When the tradeType is 2 in confirmation , state respectively represents: 1-Completed |
| txId        | string       | Transaction hash                                             |

## Obtain a transfer bill from a spot account

Speed limit rule: 20 times/2s

**Function description:**

This interface queries the transfer bill of the spot account.

**Request path:**

POST /v1/api/spot/record/trans

curl `https://api.fameex.com/v1/api/spot/record/trans`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                                   |
| --------- | -------------- | ------------ | --------------------------------------------------------- |
| tradeType | no             | int          | Transaction type: 0. All; 1. Transfer in; 2. Transfer out |
| currency  | no             | string       | Example of currency name: ETH                             |
| startTime | no             | int64        | Start time: second-level timestamp                        |
| endTime   | no             | int64        | End time time: second-level timestamp                     |
| pageno    | Yes            | int          | Page number, starting from 1                              |
| pageSize  | Yes            | int          | Number of pages (0 <pageSize ≤ 500)                       |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "userId": "35856194",
    "total": 16,
    "list": [
      {
        "userId": "35856194",
        "tradeType": 2,
        "currency": "USDT",
        "fromCoinPair": "",
        "toCoinPair": "",
        "fromAccount": 0,
        "toAccount": 1,
        "amount": "500.00000000",
        "operateTime": 1600863239,
        "state": 1
      },
      {
        "userId": "35856194",
        "tradeType": 2,
        "currency": "USDT",
        "fromCoinPair": "",
        "toCoinPair": "",
        "fromAccount": 0,
        "toAccount": 1,
        "amount": "450.00000000",
        "operateTime": 1600863103,
        "state": 1
      }
    ]
  }
}
```

**Return Value:**

| Field Name   | Type | Remarks                                                      |
| ------------ | ------------ | ------------------------------------------------------------ |
| code         | int          | 200, normal                                                  |
| msg          | string       | success, normal                                              |
| data         | object       | Empty string                                                 |
| userId       | string       | User id                                                      |
| total        | int          | Number of bill records                                       |
| list         | array        | Billing record list                                          |
| tradeType    | int          | Transaction type: 1. Transfer in; 2. Transfer out            |
| operateTime  | int64        | Operating time                                               |
| currency     | string       | Example of currency name: ETH                                |
| amount       | string       | Quantity                                                     |
| fromCoinPair | string       | Transferred currency pair                                    |
| toCoinPair   | string       | Transfer out currency pair                                   |
| fromAccount  | string       | Transfer out account: 0. Spot; 1. Leverage; 3. Legal currency |
| toAccount    | string       | Transfer to account: 0. Spot; 1. Leverage; 3. Legal currency |

## Get other bills for spot accounts

Speed limit rule: 20 times/2s

**Function description:**

This interface queries other bills of spot accounts, including rebates and activities.

**Request path:**

POST /v1/api/spot/record/others

curl `https://api.fameex.com/v1/api/spot/record/others`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                            |
| --------- | -------------- | ------------ | -------------------------------------------------- |
| tradeType | no             | int          | Transaction type: 0. All; 1. Rebate; 2. Activities |
| currency  | no             | string       | Example of currency name: ETH                      |
| startTime | no             | int64        | Start time: second-level timestamp                 |
| endTime   | no             | int64        | End time time: second-level timestamp              |
| pageno    | Yes            | int          | Page number, starting from 1                       |
| pageSize  | Yes            | int          | Number of pages (0 <pageSize ≤ 500)                |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "userId": "94433127",
    "total": 14,
    "list": [
      {
        "tradeType": 1,
        "currency": "BTC",
        "amount": "0.01",
        "operateTime": 1608086059
      },
      {
        "tradeType": 1,
        "currency": "BTC",
        "amount": "0.01",
        "operateTime": 1608086059
      }
    ]
  }
}
```

**Return Value:**

| Field Name  | Type | Remarks                                    |
| ----------- | ------------ | ------------------------------------------ |
| code        | int          | 200, normal                                |
| msg         | string       | success, normal                            |
| data        | object       | Empty string                               |
| userId      | string       | User id                                    |
| total       | int          | Number of bill records                     |
| list        | array        | Billing record list                        |
| tradeType   | int          | Transaction type: 1. Rebate; 2. Activities |
| operateTime | int64        | Operation time: second-level timestamp     |
| currency    | string       | Example of currency name: ETH              |
| amount      | string       | Quantity                                   |

## Get the deposit address

Speed limit rule: 20 times/2s

**Function description:**

This interface obtains the deposit address of each currency.

**Request path:**

/v1/api/account/deposit/address

curl `https://api.fameex.com/v1/api/account/deposit/address`

**Routing parameters:**

| parameter | Mandatory | Type | Remarks            |
| --------- | -------------- | ------------ | ------------------ |
| coinType  | Yes            | string       | Currency type USDT |
| chainType | Yes            | string       | Chain type ERC20   |

**Post Parameter:**

no

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "request": {
    "userId": "66491610",
    "coinType": "btc",
    "label": ""
  },
  "data": {
    "userId": "66491610",
    "coinType": "btc",
    "code": 200,
    "address": "1DDceT2o3zQS6dYzLg3HGG9Y787DfGXMLA",
    "exportAddr": ""
  }
}
```

**Return Value:**

| Field Name | Type | Remarks           |
| ---------- | ------------ | ----------------- |
| code       | int          | 200, normal       |
| request    | map          | Request parameter |
| userId     | string       | User id           |
| coinType   | string       | Currency          |
| address    | string       | address           |

## Get margin account information

Speed limit rule: 1 time/2s

**Function description:**

This interface obtains a list of all asset information of a margin account, and queries the balance, freeze, and availability information of each currency.

**Request path:**

/v1/api/lever/accounts

curl `https://api.fameex.com/v1/api/lever/accounts`

**Routing parameters:**

no

**Post Parameter:**

no

> **Return example:**

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "walletType": "l2c",
        "list": [
            {
                "baseAvailable": "0.00000000",
                "baseBorrowed": "0.00000000",
                "baseCurrency": "ETH",
                "baseHold": "0.00000000",
                "baseInterest": "0.00000000",
                "baseTotal": "0.00000000",
                "coinpair": "ETH/USDT",
                "quoteAvailable": "0.00000000",
                "quoteBorrowed": "0.00000000",
                "quoteCurrency": "USDT",
                "quoteHold": "0.00000000",
                "quoteInterest": "0.00000000",
                "quoteTotal": "0.00000000"
            },
            {
                "baseAvailable": "0.00000000",
                "baseBorrowed": "0.00000000",
                "baseCurrency": "ADA",
                "baseHold": "0.00000000",
                "baseInterest": "0.00000000",
                "baseTotal": "0.00000000",
                "coinpair": "ADA/USDT",
                "quoteAvailable": "10.00000000",
                "quoteBorrowed": "0.00000000",
                "quoteCurrency": "USDT",
                "quoteHold": "0.00000000",
                "quoteInterest": "0.00000000",
                "quoteTotal": "10.00000000"
            }
        ]
    },
    "userid": "72473826"
}
```

**Return Value:**

| Field Name     | Type | Remarks                                                      |
| -------------- | ------------ | ------------------------------------------------------------ |
| code           | int          | 200, normal                                                  |
| data           | list         | Return value, margin account data                            |
| userid         | string       | User id                                                      |
| walletType     | string       | Account type: spot-currency account otc-fiat currency account l2c-margin account |
| coinpair       | string       | Example of currency pair name: BTC/USDT                      |
| baseCurrency   | string       | Example of transaction currency name: BTC                    |
| quoteCurrency  | string       | Example of denomination currency name: USDT                  |
| baseAvailable  | string       | Available amount of transaction currency                     |
| quoteAvailable | string       | Available amount in denominated currency                     |
| baseHold       | string       | Frozen amount of trading currency                            |
| quoteHold      | string       | Frozen amount in denominated currency                        |
| baseTotal      | string       | Total transaction currency                                   |
| quoteTotal     | string       | Total denominated currency                                   |
| baseBorrowed   | string       | Transaction currency loan amount                             |
| quote Borrowed | string       | Denominated currency loan amount                             |
| baseInterest   | string       | Transaction currency interest                                |
| quoteInterest  | string       | Denominated currency interest                                |

# Margin trading API interface

## Get the details of a currency pair under a margin account

Speed limit rule: 1 time/2s

**Function description:**

Get information about the balance, freeze, and availability of a currency pair account under a margin account

**Request path:**

/v1/api/lever/accounts

curl `https://api.fameex.com/v1/api/lever/accounts`

**Routing parameters:**

| parameter | Mandatory | Type | Remarks                         |
| --------- | -------------- | ------------ | ------------------------------- |
| pairName  | Yes            | string       | Currency pair, example BTC_USDT |

**Post Parameter:**

no

> **Return example:**

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "baseAvailable": "0.60029232",
        "baseBorrowed": "1",
        "baseCurrency": "BTC",
        "baseHold": "0",
        "baseInterest": "0.000042",
        "baseTotal": "0.60029232",
        "coinpair": "BTC/USDT",
        "quoteAvailable": "3902.45765848",
        "quoteBorrowed": "219.34",
        "quoteCurrency": "USDT",
        "quoteHold": "0",
        "quoteInterest": "0.00921228",
        "quoteTotal": "3902.45765848",
        "burstPrice": "9213.53694692",
        "riskRate": "112.25"
    },
    "userid": "72473826"
}
```

**Return Value:**

| Field Name     | Type | Remarks                                     |
| -------------- | ------------ | ------------------------------------------- |
| code           | int          | 200, normal                                 |
| data           | list         | Return value, margin account data           |
| msg            | string       | code response message                       |
| userid         | string       | User id                                     |
| coinpair       | string       | Example of currency pair name: BTC/USDT     |
| baseCurrency   | string       | Example of transaction currency name: BTC   |
| quoteCurrency  | string       | Example of denomination currency name: USDT |
| baseAvailable  | string       | Available amount of transaction currency    |
| quoteAvailable | string       | Available amount in denominated currency    |
| baseHold       | string       | Frozen amount of trading currency           |
| quoteHold      | string       | Frozen amount in denominated currency       |
| baseTotal      | string       | Total transaction currency                  |
| quoteTotal     | string       | Total denominated currency                  |
| baseBorrowed   | string       | Transaction currency loan amount            |
| quote Borrowed | string       | Denominated currency loan amount            |
| baseInterest   | string       | Transaction currency interest               |
| quoteInterest  | string       | Denominated currency interest               |
| burstPrice     | string       | Liquidation price                           |
| riskRate       | string       | Liquidation risk rate                       |

## Leverage order

Speed limit rule: 1 time/2s

**Function description:**

This interface provides leverage to place orders.

**Request path:**

/v1/api/lever/orders/place

curl `https://api.fameex.com/v1/api/lever/orders/place`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                  |
| --------- | -------------- | ------------ | ---------------------------------------- |
| base      | Yes            | string       | Trading currency in the trading pair     |
| quote     | Yes            | string       | Denominated currency in the trading pair |
| buyType   | Yes            | int          | 0 buy, 1 sell                            |
| price     | Yes            | string       | Order unit price                         |
| count     | Yes            | string       | Order quantity                           |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "orderId": "10541638782567317504"
}
```

**Return Value:**

| Field Name | Type | Remarks                 |
| ---------- | ------------ | ----------------------- |
| code       | int          | 200, normal             |
| msg        | string       | Information Description |
| orderId    | string       | Pending order id        |

## Leverage Cancellation

Speed limit rule: 1 time/2s

**Function description:**

This interface provides the function of canceling unfilled leveraged orders.

**Request path:**

/v1/api/lever/orders/cancel

curl `https://api.fameex.com/v1/api/lever/orders/cancel`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks  |
| --------- | -------------- | ------------ | -------- |
| orderId   | Yes            | string       | Order id |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "orderId": "10541638782567317504"
}
```

**Return Value:**

| Field Name | Type | Remarks                |
| ---------- | ------------ | ---------------------- |
| code       | int          | 200, normal            |
| msg        | string       | Remarks                |
| orderId    | string       | Id to cancel the order |

## Leverage batch cancellation

Speed limit rule: 1 time/2s

**Function description:**

This interface provides the function of canceling all unexecuted leveraged orders of a specified currency pair or currency pairs.

**Request path:**

/v1/api/lever/orders/batch_cancel

curl `https://api.fameex.com/v1/api/lever/orders/batch_cancel`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                            |
| --------- | -------------- | ------------ | -------------------------------------------------- |
| buyType   | Yes            | int          | Buying and selling direction 0 buy, 1 sell, -1 all |
| base      | Yes            | string       | Trading currency in the trading pair               |
| quote     | Yes            | string       | Denominated currency in the trading pair           |
| startTime | Yes            | int64        | "0" all                                            |
| endTime   | Yes            | int64        | "0" all                                            |

> **Return example:**

```json
{
  "code": 200,
  "msg": "SUCCESS"
}
```

**Return Value:**

| Field Name | Type | Remarks     |
| ---------- | ------------ | ----------- |
| code       | int          | 200, normal |
| msg        | string       | SUCCESS     |

## Get a list of leveraged orders

Speed limit rule: 1 time/2s

**Function description:**

List your current order information (the order information of the last 3 months). This request supports paging, and is sorted and stored in reverse chronological order, with the latest one at the top.

**Request path:**

/v1/api/lever/orders

curl `https://api.fameex.com/v1/api/lever/orders`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                                      |
| --------- | -------------- | ------------ | ------------------------------------------------------------ |
| pageno    | Yes            | int          | Paging usage, which page                                     |
| pageSize  | Yes            | int          | Paging usage, number per page (0 <pageSize ≤ 500)            |
| type      | Yes            | int          | 0 all, 1 completed (complete deal), 2 not completed, 3 cancelled, 4 cancelled and completed 5 partial deal has been cancelled 6 completed (complete deal) and partial deal has been cancelled 7 uncompleted deal has been cancelled |
| buyType   | no             | int          | Trading direction: 0 buy, 1 sell, -1 all                     |
| base      | no             | string       | Example of transaction currency name: BTC                    |
| quote     | no             | string       | Example of denomination currency name: USDT                  |
| startTime | no             | int64        | Timestamp, query the start time of the order in seconds      |
| endTime   | no             | int64        | Timestamp, query the end time of the order in seconds        |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "pageNum": 1,
    "pageSize": 2,
    "total": 5,
    "list": [
      {
        "id": 1,
        "orderId": "10541643424227393536",
        "userId": "72473826",
        "userType": 1,
        "userLevel": 1,
        "pairName": "btc_usdt",
        "base": "btc",
        "quote": "usdt",
        "buyType": 0,
        "buyClass": 0,
        "state": 11,
        "price": "6900",
        "totalPrice": "690",
        "count": "0.1",
        "totalCount": "0.1",
        "dealedCount": "0",
        "dealedMoney": "0",
        "priceAvg": "0",
        "lossPrice": "0",
        "triggerGreater": false,
        "matchCount": 0,
        "createTime": 1603940743588535348,
        "endTime": 1603941181672225017,
        "isErr": 0,
        "triggered": 0,
        "strategyId": "",
        "strategyName": "",
        "strategyType": 0,
        "accountFlag": 1,
        "detail": null
      }
    ]
  }
}
```

**Return Value:**

| Field Name     | Type | Remarks                                                      |
| -------------- | ------------ | ------------------------------------------------------------ |
| code           | int          | Return value status                                          |
| msg            | string       | Return value description                                     |
| data           | string       | Return value, order list                                     |
| id             | int64        | Data number                                                  |
| orderId        | string       | Order id                                                     |
| userId         | string       | User id                                                      |
| userType       | int          | User type 1 Ordinary user 2 api user                         |
| userLevel      | int          | user level                                                   |
| base           | string       | Trading currency in the trading pair                         |
| quote          | string       | Denominated currency in the trading pair                     |
| buyType        | int          | 0 buy 1 sell                                                 |
| buyClass       | int          | 0 limit order                                                |
| state          | int          | Order Status 1-Pending Match 4-Taker Completed Transaction 7-In the Deep Queue 8-Taker Partial Transaction 9-maker Partial Transaction 10-maker Complete Transaction 11-Canceled |
| price          | string       | Order unit price                                             |
| totalPrice     | string       | Initial commission price                                     |
| count          | string       | Unsold quantity                                              |
| lossPrice      | string       | Stop Profit and Stop Loss Trigger Price                      |
| totalCount     | string       | The total amount                                             |
| dealedCount    | string       | Number of transactions                                       |
| dealedMoney    | string       | Cumulative turnover                                          |
| priceAvg       | string       | Average transaction price                                    |
| triggerGreater | bool         | Is it greater than or equal to the trigger price of stop profit and stop loss |
| matchCount     | int          | Matches                                                      |
| createTime     | int64        | Order creation time unit: nanosecond                         |
| endTime        | int64        | The last update time unit of the order: nanosecond           |
| isErr          | int          | 0 Normal orders and other orders that failed to unlock assets |
| triggered      | int          | Whether stop profit and stop loss is triggered 0 not triggered 1 triggered |
| accountFlag    | int          | Order type: 1. Ordinary leveraged order; 2. Leveraged liquidation |
| detail         | object       | Details                                                      |

## Get details of leveraged orders

Speed limit rule: 1 time/2s

**Function description:**

This interface obtains the specified order information through the order ID.

**Request path:**

/v1/api/lever/orders/detail

curl `https://api.fameex.com/v1/api/lever/orders/detail`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                               |
| --------- | -------------- | ------------ | ----------------------------------------------------- |
| orderId   | Yes            | string       | Order id                                              |
| pairName  | Yes            | string       | The name of the currency pair (for example: BTC_USDT) |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "orderId": "10541703708627435520",
    "pairName": "BNB_USDT",
    "buyType": 0,
    "buyClass": 0,
    "state": 10,
    "price": "16.03205599",
    "count": "0",
    "lossPrice": "0",
    "totalCount": "1",
    "dealedCount": "1",
    "dealedMoney": "16.03205599",
    "priceAvg": "16.03205599",
    "createTime": 1603955116509568123,
    "endTime": 1603955125579079857
  }
}
```

**Return Value:**

| Field Name  | Type | Remarks                                                      |
| ----------- | ------------ | ------------------------------------------------------------ |
| code        | int          | Return value status                                          |
| msg         | string       | Return value description                                     |
| data        | string       | Return value, order details                                  |
| orderId     | string       | Matching task id                                             |
| pairName    | string       | The name of the currency pair (for example: BTC_USDT)        |
| buyType     | int          | Buying and Selling Direction 0-Buy1-Sell                     |
| buyClass    | int          | Order type 0-limit price1-market price2-stop profit and stop loss |
| state       | int          | Order status 1-To be matched 4-Taker is fully traded 7-In the deep queue 9-Partially traded by maker 10-Maker is fully traded 11-Canceled |
| price       | string       | Pending order unit price                                     |
| count       | string       | Unsold quantity                                              |
| lossPrice   | string       | Stop Profit and Stop Loss Trigger Price                      |
| totalCount  | string       | Total number of pending orders                               |
| dealedCount | string       | Number of transactions                                       |
| dealedMoney | string       | Transaction amount                                           |
| priceAvg    | string       | Average transaction price                                    |
| createTime  | int64        | Order creation time in nanoseconds                           |
| endTime     | int64        | Last update time of order status in nanoseconds              |

## Get leveraged transaction details

Speed limit rule: 1 time/2s

**Function description:**

This interface gets all your current transaction order information. This request supports paging, and is sorted and stored in reverse chronological order, with the latest one at the top.

**Request path:**

/v1/api/lever/deals

curl `https://api.fameex.com/v1/api/lever/deals`

**Routing parameters:**

no

**Post Parameter:**

| parameter   | Mandatory | Type | Remarks                                                      |
| ----------- | -------------- | ------------ | ------------------------------------------------------------ |
| pairName    | Yes            | string       | Token name (e.g. BTC_UDST)                                   |
| buyType     | Yes            | int          | Trading direction: 0 buy, 1 sell, -1 all                     |
| pageno      | Yes            | int          | Pagination use, the first few pages, starting from the first page |
| pageSize    | Yes            | int          | Paging usage, number per page (0 <pageSize ≤ 500)            |
| accountFlag | Yes            | int          | Account source (0-coin1-leverage 2-leverage liquidation)     |
| orderId     | no             | string       | Order id                                                     |
| startTime   | no             | int64        | Timestamp, seconds                                           |
| endTime     | no             | int64        | Timestamp, seconds                                           |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "total": 8,
    "pageSize": 2,
    "pageNum": 1,
    "list": [
      {
        "orderId": "10541703746694963200",
        "pairName": "BNB_USDT",
        "base": "bnb",
        "quote": "usdt",
        "time": 1603955125579079857,
        "buyClass": 0,
        "buyType": 0,
        "price": "16.03205599",
        "count": "1",
        "fee": "0.0000009",
        "feeRate": "0.0000009",
        "originFeeRate": "0.000001",
        "buyerOrderId": "10541703708627435520",
        "buyerUserId": "72473826",
        "sellerOrderId": "10541703746644606976",
        "sellerUserId": "72473826",
        "strategyId": "",
        "strategyName": "",
        "strategyType": 0,
        "accountFlag": 1
      }
    ]
  }
}
```

**Return Value:**

| Field Name    | Type | Remarks                                                   |
| ------------- | ------------ | --------------------------------------------------------- |
| code          | int          | Return value status                                       |
| msg           | string       | Return value description                                  |
| data          | string       | Return value, transaction details                         |
| pairName      | string       | The name of the currency pair (for example: BTC_USDT)     |
| base          | string       | Transaction currency                                      |
| quote         | string       | Denominated currency                                      |
| orderId       | string       | Order id                                                  |
| time          | int64        | Transaction time in nanoseconds                           |
| buyClass      | int          | Transaction type: 0 limit transaction                     |
| buyType       | int          | Trading direction: 0 buy, 1 sell                          |
| price         | string       | the deal price                                            |
| count         | string       | The number of transactions                                |
| fee           | string       | Handling fee                                              |
| feeRate       | string       | Actual handling fee rate                                  |
| originFeeRate | string       | Original fee rate                                         |
| accountFlag   | int          | Type: 1. Ordinary leverage order; 2. Leverage liquidation |

## Get leverage configuration

Speed limit rule: 1 time/2s

**Function description:**

This interface obtains the currency pair configuration information of the wallet margin account.

**Request path:**

/v1/api/lever/pair/config

curl `https://api.fameex.com/v1/api/lever/pair/config`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                 |
| --------- | -------------- | ------------ | --------------------------------------- |
| pairName  | no             | string       | Example of currency pair name: ETH_USDT |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": [
    {
      "coinPair": "TOMO/USDT",
      "leverMultiple": 10,
      "isBorrow": 0,
      "quoteLeatestBorrowAmount": "10",
      "borrowFeeRate": "0.05",
      "quoteMostBorrowAmount": "10000",
      "baseMostBorrowAmount": "10000"
    },
    {
      "coinPair": "BTC/USDT",
      "leverMultiple": 10,
      "isBorrow": 0,
      "quoteLeatestBorrowAmount": "100",
      "borrowFeeRate": "0.000021",
      "quoteMostBorrowAmount": "5000",
      "baseMostBorrowAmount": "100"
    },
    {
      "coinPair": "BNB/USDT",
      "leverMultiple": 4,
      "isBorrow": 0,
      "quoteLeatestBorrowAmount": "10",
      "borrowFeeRate": "0.000001",
      "quoteMostBorrowAmount": "1000000000",
      "baseMostBorrowAmount": "10"
    }
  ]
}
```

**Return Value:**

| Field Name               | Type | Remarks                                           |
| ------------------------ | ------------ | ------------------------------------------------- |
| code                     | int          | 200, normal                                       |
| msg                      | string       | success, normal                                   |
| data                     | array        | Return value, leverage configuration information  |
| coinPair                 | string       | Currency pair name                                |
| leverMultiple            | string       | Leverage                                          |
| quoteLeatestBorrowAmount | string       | Minimum borrowing amount of denominated currency  |
| borrowFeeRate            | string       | Loan rate                                         |
| quoteMostBorrowAmount    | string       | The maximum loanable currency in a single day     |
| baseMostBorrowAmount     | string       | Maximum loanable trading currency in a single day |

## Get leveraged currency borrowing parameters

Speed limit rule: 1 time/2s

**Function description:**

This interface obtains the prompt parameters when the user borrows coins.

**Request path:**

/v1/api/lever/borrowparam

curl `https://api.fameex.com/v1/api/lever/borrowparam`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                 |
| --------- | -------------- | ------------ | --------------------------------------- |
| pairName  | Yes            | string       | Example of currency pair name: ETH_USDT |
| currency  | Yes            | string       | Example of currency name: ETH           |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "canBorrowAmount": "15",
    "borrowedAmount": "3",
    "borrowFeeRate": "0.0001",
    "leastBorrowAmount": "0"
  }
}
```

**Return Value:**

| Field Name        | Type | Remarks                                          |
| ----------------- | ------------ | ------------------------------------------------ |
| code              | int          | 200, normal                                      |
| msg               | string       | success, normal                                  |
| data              | array        | Return value, leverage configuration information |
| canBorrowAmount   | string       | Available amount                                 |
| borrowedAmount    | string       | Amount borrowed                                  |
| borrowFeeRate     | string       | Minimum borrowing amount of denominated currency |
| leastBorrowAmount | string       | Minimum loan amount                              |

## Leveraged currency

Speed limit rule: 1 time/2s

**Function description:**

This interface is used for leveraged currency borrowing.

**Request path:**

/v1/api/lever/borrow

curl `https://api.fameex.com/v1/api/lever/borrow`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                 |
| --------- | -------------- | ------------ | --------------------------------------- |
| pairName  | Yes            | string       | Example of currency pair name: ETH_USDT |
| currency  | Yes            | string       | Example of currency name: ETH           |
| amount    | Yes            | string       | Loan amount                             |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": ""
}
```

**Return Value:**

| Field Name | Type | Remarks         |
| ---------- | ------------ | --------------- |
| code       | int          | 200, normal     |
| msg        | string       | success, normal |
| data       | array        | Empty string    |

## Get leveraged currency parameters

Speed limit rule: 1 time/2s

**Function description:**

This interface obtains the currency return prompt parameters of a specific currency under a specific currency pair.

**Request path:**

/v1/api/lever/repayparam

curl `https://api.fameex.com/v1/api/lever/repayparam`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                 |
| --------- | -------------- | ------------ | --------------------------------------- |
| pairName  | Yes            | string       | Example of currency pair name: ETH_USDT |
| currency  | Yes            | string       | Example of currency name: ETH           |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "borrowedAmount": "1.00000200",
    "interest": "0.00000401",
    "unReturnAmount": "1.00000601",
    "availAmount": "1.99999910"
  }
}
```

**Return Value:**

| Field Name     | Type | Remarks                                                      |
| -------------- | ------------ | ------------------------------------------------------------ |
| code           | int          | 200, normal                                                  |
| msg            | string       | success, normal                                              |
| data           | object       | Return value, prompt message of user returning currency      |
| borrowedAmount | string       | Unpaid principal                                             |
| interest       | string       | Unpaid interest on borrowed currency                         |
| unReturnAmount | string       | Outstanding amount                                           |
| availAmount    | string       | The available amount of the currency under the currency pair |

## Leveraged currency

Speed limit rule: 1 time/2s

**Function description:**

This interface is used for leveraged currency.

**Request path:**

/v1/api/lever/repay

curl `https://api.fameex.com/v1/api/lever/repay`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                 |
| --------- | -------------- | ------------ | --------------------------------------- |
| pairName  | Yes            | string       | Example of currency pair name: ETH_USDT |
| currency  | Yes            | string       | Currency name                           |
| amount    | Yes            | string       | Refund amount                           |

> **Return example:**

```json
{
    "code": 200,
    "msg": "success",
    "data": ""
}
```

**Return Value:**

| Field Name | Type | Remarks         |
| ---------- | ------------ | --------------- |
| code       | int          | 200, normal     |
| msg        | string       | success, normal |
| data       | array        | Empty string    |

## Get Margin Account Debit and Return Record

Speed limit rule: 1 time/2s

**Function description:**

This interface obtains the information of the leverage loan and return record.

**Request path:**

/v1/api/lever/record/borrow_repay

curl `https://api.fameex.com/v1/api/lever/record/borrow_repay`

**Routing parameters:**

no

**Post Parameter:**

| parameter | Mandatory | Type | Remarks                                 |
| --------- | -------------- | ------------ | --------------------------------------- |
| pairName  | Yes            | string       | Example of currency pair name: ETH_USDT |
| currency  | Yes            | string       | Example of currency name: ETH           |
| pageSize  | Yes            | int          | Display quantity per page               |
| pageno    | Yes            | int          | page number                             |

> **Return example:**

```json
{
    "code": 200,
    "msg": "success",
    "data": {
        "list": [
            {
                "borrowedTime": 1603959122,
                "coinPair": "BNB/USDT",
                "coinType": "BNB",
                "recordId": "1603959122152142070",
                "borrowedAmount": "1",
                "amount": "0.000002",
                "borrowFeeRate": "0.0001",
                "interest": "0.00000001",
                "refund": "0.000001",
                "state": 1
            },
            {
                "borrowedTime": 1603958809,
                "coinPair": "BNB/USDT",
                "coinType": "BNB",
                "recordId": "1603958809028866056",
                "borrowedAmount": "1",
                "amount": "0",
                "borrowFeeRate": "0.0001",
                "interest": "0",
                "refund": "0.000001",
                "state": 2
            }
        ],
        "pageNum": 1,
        "pageSize":5,
        "total": 2
    }
}
```

**Return Value:**

| Field Name     | Type | Remarks                                           |
| -------------- | ------------ | ------------------------------------------------- |
| code           | int          | 200, normal                                       |
| msg            | string       | success, normal                                   |
| data           | list         | Return value, margin account data                 |
| borrowedTime   | int64        | Borrow time                                       |
| coinPair       | string       | Example of borrowing currency pair name: BTC/USDT |
| coinType       | string       | Example of borrowing currency name: BTC           |
| recordId       | string       | Borrowing record id                               |
| borrowedAmount | string       | Number of borrowed coins                          |
| amount         | string       | Available amount of transaction currency          |
| borrowFeeRate  | string       | Hourly rate                                       |
| interest       | string       | Interest paid                                     |
| refund         | string       | Frozen amount in denominated currency             |
| state          | int          | Loan status: 1. Not repaid; 2. Repaid             |

## Get a margin account statement

Speed limit rule: 1 time/2s

**Function description:**

Use this interface to obtain leveraged bills.

**Request path:**

/v1/api/lever/ledger

curl `https://api.fameex.com/v1/api/lever/ledger`

**Routing parameters:**

no

**Post Parameter:**

| parameter  | Mandatory | Type | Remarks                                                      |
| ---------- | -------------- | ------------ | ------------------------------------------------------------ |
| pageno     | Yes            | int          | page number                                                  |
| pageSize   | Yes            | int          | Display quantity per page (0 <pageSize ≤ 500)                |
| currency   | no             | string       | Currency type, all bills will be returned if not filled      |
| ledgerType | no             | int          | Bill type 2 Buy in 3 Buy out 4 Handling fee 5 Loan currency 6 Return interest 7 Return principal 8 System buy 9 System sell 11 Liquidation fee 12 Transfer in 13 Transfer out |
| pairName   | no             | string       | Currency pair type, if not filled in, the bill of all currency pairs will be returned |

> **Return example:**

```json
{
  "code": 200,
  "message": "success",
  "data": [
    {
      "ledger_id": "10541354256305774592",
      "coinPair": "BTC/USDT",
      "currency": "BTC",
      "balance": "0.60029232",
      "amount": "0.46417600",
      "typename": "lever_trade",
      "timestamp": "2020-10-28T15:56:40Z"
    },
    {
      "ledger_id": "10541354255949258752",
      "coinPair": "BTC/USDT",
      "currency": "USDT",
      "balance": "653.25823816",
      "amount": "8.73514642",
      "typename": "lever_trade",
      "timestamp": "2020-10-28T15:56:40Z"
    }
  ],
  "total": 239,
  "operateTime": "2020-10-28T18:17:01Z"
}
```

**Return Value:**

| Field Name | Type | Remarks            |
| ---------- | ------------ | ------------------ |
| ledger_id  | string       | Bill ID            |
| coinPair   | string       | Currency pair      |
| currency   | string       | Currency           |
| balance    | string       | Balance            |
| amount     | string       | Number of changes  |
| typename   | string       | Bill type          |
| timestamp  | string       | Bill creation time |

# Error message

| code   | Remarks                                                      |
| ------ | ------------------------------------------------------------ |
| 200    | normal                                                       |
| 112002 | API single key traffic exceeds limit                         |
| 112005 | API request frequency exceeded                               |
| 112007 | API-Key creation failed                                      |
| 112008 | API-Key remark name already exists                           |
| 112009 | The number of API-Key creation exceeds the limit (a single user can create up to 5 APIs) |
| 112010 | API-Key is invalid (the time limit for a single Key is 60 natural days) |
| 112011 | API request IP access is restricted (the bound IP is inconsistent with the request IP) |
| 112015 | Signature error                                              |
| 112020 | Wrong signature                                              |
| 112021 | Wrong signature version                                      |
| 112022 | Signature timestamp error                                    |

# common problem

| common problem                                               |
| ------------------------------------------------------------ |
| 1. What is a trading currency? What is a denominated currency? Is the transaction volume counted in the transaction currency or the denominated currency? Answer: Each transaction currency pair is composed of transaction currency/denominated currency. The front of the currency pair is the transaction currency, and the back is the denominated currency. For example: In the BTC/USDT trading currency pair, BTC is the trading currency and USDT is the quotation currency. The transaction volume is calculated based on the transaction currency. The total transaction amount is calculated based on the denominated currency. |
| 2. Rest access restriction? Answer: 1. A single IP is restricted to 1200 visits per minute. If it exceeds 1200 times, it will be locked for 1 hour, and will be automatically unlocked after one hour. 2. A single user is restricted to 20 visits per second, and more than 20 requests within one second will be considered invalid. |
| 3. WebSocket access restriction? Answer: A single user is restricted to 50 visits per second, and more than 50 requests in one second will be regarded as invalid. |
| 4. What is the use of the generated key? Answer: The key is the key used to operate the API, and the API key needs to be provided when calling the API interface. The private key is only displayed once when it is just generated, and it needs to be regenerated if it is forgotten. |
| 5. Can the candlestick chart obtain data from months or one year ago? Answer: The system candlestick chart only provides 1000 pieces of data at most. If you want to obtain longer data, you need to use the unit of hour or day to obtain it. |
| 6. Does the IP of the API need to be bound? Answer: 1. The IP binding of the API effectively prevents servers other than this IP from calling their own authority for transaction operations. 2. After the IP is bound, it can only be accessed by the bound IP. If it is not bound, the access to the IP is not restricted. |
| 7. Does the API support withdrawals? Answer: No, withdrawals must be made on the FAMEEX official website. |
| 8. Can the public key and private key be provided to others? Answer: It is not recommended, it will cause asset loss. |
| 9. Frequent signature failures? • Check whether the API Key is valid, copied correctly, and whether there is a whitelist of bound IP; • Check whether the timestamp is UTC time; • Check whether the parameters are sorted alphabetically; • Check the code; • Check the signature code It should be hex; • Check whether it is submitted in a form ; • Check whether the url has a signature field, and whether the POST data format is json format; • Check whether the signature result is URI-encoded. |
| 10. Return login-required? • Check whether the parameter account-id is returned by the /v1/account/accounts interface instead of the filled UID; • Check whether the request includes the business parameters into the signature; • Check whether the request includes parameters Sort in the order of the ASCII code table. |
| 11. Return gateway-internal-error? Check whether the request declares Content-Type: application/json in the header. |