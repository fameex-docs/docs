---
title: FameEX API Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - go

toc_footers:
  - <a href='https://www.fameex.com' target='blank'>FameEX Exchange</a>

includes:
  # - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: FameEX API Documentation
  - name: keywords
    content: FameEX,API,Documentation
---

# Change Log

## 2023-09-12

- Coin trading interface update:
  - Delete the interface to get all outstanding orders `/v1/api/orders_pending` (use `/v1/api/spot/orderlist` instead)

## 2022-11-07

- New endpoint for Market Data:
  - GET `/v2/public/assets` to query detailed summary for each currency
  - GET `/v2/public/summary` to query an overview of market data for all tickers and all market pairs
  - GET `/v2/public/ticker` to query a 24-hour pricing and volume summary for each market pair
  - GET `/v2/public/orderbook/market_pair` to query full depth returned for a given market pair
  - GET `/v2/public/trades/market_pair` to query completed trades for a given market pair

## 2021-03-30

- New endpoint for Market Data:
  - GET `/api/v2/orderbook` to query order book.
  - GET `/api/v2/trades` to query recent trades.
  - GET `/api/v2/ticker/24hr` to query 24 hour rolling window price change statistics.
  - GET `/api/v2/ticker/price` to get latest price for a symbol.

## 2021-08-24

- Websocket market push update:

  - Update heartbeat connection `wss://www.fameex.com/push`
  - Update login information `wss://www.fameex.com/push`
  - Delete registration candle information `wss://www.fameex.com/push`
  - Delete registration homepage quotes `wss://www.fameex.com/push`
  - Delete registration in-depth quotation `wss://www.fameex.com/push`
  - Update and push the homepage quotation `wss://www.fameex.com/push`
  - Update the push currency pair depth list `wss://www.fameex.com/push`
  - Update push K-line/Candlestick data `wss://www.fameex.com/push`
  - Update and push the latest transaction order quotation `wss://www.fameex.com/push`
  - Delete push order transaction or cancellation `wss://www.fameex.com/push`
  - Delete push My order is partially cancelled `wss://www.fameex.com/push`
  - Update and logout home page quotes `wss://www.fameex.com/push`

- Updates to the currency trading API interface:

  - Modify the interface for obtaining K-line/Candlestick data `/v1/market/history/kline`
  - Modify the interface for obtaining market depth data `/v1/market/depth`
  - Modify the interface for obtaining transaction data `/v1/market/history/trade`
  - Modify the interface to obtain a ticker information `/v1/market/history/kline24h`
  - Modify the interface to get all ticker information `/v1/market/history/kline24h/all`
  - Modify the currency order interface `/v1/api/spot/orders`
  - Modify the currency withdrawal order interface `/v1/api/spot/cancel_orders`
  - Modify the batch cancellation interface `/spot/v1/cancel_batch_orders`
  - Modify the interface for obtaining order details `/v1/api/spot/orderdetail`
  - Modify the interface to get the list of orders `/v1/api/spot/orderlist`
  - Modify the interface for obtaining transaction details `/v1/api/spot/fills`
  - Modify the interface to get all outstanding orders `/v1/api/orders_pending`

- Margin trading API interface update:

  - Modify the leverage order interface `/v1/api/lever/orders/place`
  - Modify the interface of leveraged order cancellation `/v1/api/lever/cancel_orders`
  - Modify the leveraged batch cancellation interface `/v1/api/lever/orders/batch_cancel`
  - Modify the interface for obtaining the list of leveraged orders `/v1/api/lever/orders`
  - Modify the interface for obtaining the details of leveraged orders `/v1/api/lever/orders/detail`
  - Modify the interface for obtaining leveraged transaction details `/v1/api/lever/deals`

## 2020-12-22

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

## 2020-11-16

- Coin trading interface update:
  - Update obtain a list of orders `v1/api/spot/orderlist`to obtain a list of orders
  - Update get order details `v1/api/spot/orderdetail`to obtain orders details
  - Updated list of orders to obtain leverage `v1/api/lever/orders`to obtain a list of orders lever
  - Update get order details leverage `v1/api/lever/orders/detail`to acquire a lever Order details

## 2020-10-30

- Wallet interface update:
  - Modify the fund transfer function interface `v1/api/account/transfer`

## 2020-10-29

- Wallet interface update:
  - Added function interface for leveraged pending orders `v1/api/lever/orders/place`
  - Added a function interface for leveraged order cancellation `v1/api/lever/orders/cancel`
  - New interface for batch withdrawal of leveraged orders `v1/api/lever/orders/batch_cancel`
  - Added a function interface for obtaining the order list of margin accounts `v1/api/lever/orders`
  - Added a function interface for obtaining the details of a margin account order `v1/api/lever/orders/detail`
  - Added function interface for obtaining leverage configuration `v1/api/lever/pair/config`

## 2020-10-28

- Wallet interface update:
  - Added an interface for obtaining a margin account statement `v1/api/lever/ledger`
  - Added the prompt parameter interface for obtaining a specific currency pair of a margin account and repaying a currency under a specific currency `v1/api/lever/repayparam`
  - Added a new interface for obtaining specific currency pairs for margin accounts and repaying currencies under specific currencies `v1/api/lever/repay`
  - Added a new interface for obtaining specific currency pairs in a margin account, and a prompt parameter interface for borrowing currency in a specific currency `v1/api/lever/borrow`
  - Added interface for obtaining specific currency pairs in margin accounts and borrowing currency in specific currencies `v1/api/lever/borrowparam`

## 2020-10-27

- Wallet interface update:
  - Added an interface for obtaining margin account information `v1/api/lever/accounts`
  - Added an interface for obtaining the details of a specific currency pair under a margin account `v1/api/lever/accounts/{pairName}`

# Introduction

API overview

FameEX provides you with a simple and powerful API interface to help you obtain market information and trade quickly and efficiently.

Before using the API, please create your own API credentials through the FameEX UI, obtain your AccessKey and SecretKey, and set the IP access restriction of the API.

API trading permissions allow you to quickly obtain the latest market quotations and order book state information, query your available balance, query your current pending orders, buy or sell, and withdraw orders.

FameEX official website homepage: [www.fameex.com](http://www.fameex.com)

If you have any questions during use, please contact FameEX official customer service,

Our contact information is as follows:

Official customer service mailbox: [Service@mail.fameex.info](mailto:Service@mail.fameex.info)

Official Twitter: [https://twitter.com/FAMEEXGLOBAL](https://twitter.com/FAMEEXGLOBAL)

Official Telegram: [https://t.me/fameexgroup](https://t.me/fameexgroup)

Official Facebook: [https://www.facebook.com/FAMEEXGLOBAL](https://www.facebook.com/FAMEEXGLOBAL)

Our official support is the most authoritative source for information about this API.

# Access instructions

## Access URLs

| Access URLs               | Description             |
| ------------------------- | ----------------------- |
| `https://api.fameex.com`  | RESTFUL API             |
| `wss://www.fameex.com/ws` | WebSocket Feed (quotes) |

All requests are based on the Https protocol, and the contentType in the header information of the POST request needs to be uniformly set to:'application/json'

Accessing FameEX-API through a proxy is not recommended due to high latency and poor stability.

## Restriction rules

**Limit frequency:** The limit of each interface is different.

A single API Key dimension is restricted. It is recommended to add a signature to the market API access, otherwise the frequency limit will be stricter.

| Frequency limiting rules                        | Type                          | Description |
| ----------------------------------------------- | ----------------------------- | ----------- |
| Frequency limit for each AccessKey and each URL | 20 times/2s (most interfaces) | no          |

## Header setting

The parameters of the request header are as follows:

| Name             | Type   | Description                                  |
| ---------------- | ------ | -------------------------------------------- |
| AccessKey        | string | The Accesskey you applied for                |
| SignatureMethod  | string | HmacSHA256                                   |
| SignatureVersion | string | v1.0                                         |
| Timestamp        | int64  | Timestamp of the request time; unit: seconds |
| Signature        | string | signature                                    |
| Content-Type     | string | application/json                             |

Explanation of the parameters of the request header:

**API Access Key (AccessKey):** The AccessKey of the API you applied for.

**Signature Method (SignatureMethod):** A hash-based protocol for the user to calculate the signature. Here, HmacSHA256 is used.

**Signature Version (SignatureVersion):** the version of the signature protocol, here v1.0 is used.

**Timestamp:** The time when you made the request. For example: 2019-07-24 00:00:00 corresponds to the timestamp 1563897600. Including this value in the query request helps prevent third parties from intercepting your request.

**Signature:** The value calculated by the signature to ensure that the signature is valid and has not been tampered with.

## signature

1. Signature description

API requests are very likely to be tampered with during transmission via the internet. In order to ensure that the request has not been changed, all private interfaces except the push service interface must use your API’s AccessKey and SecretKey for signature authentication to distinguish parameters from parameters where the value has changed during transmission.

Method request address: access server address api.fameex.com, such as api.fameex.com/v1/order/orders

**API Key contains the following two parts:**

AccessKey: API access key

SecretKey: The key used for signature authentication and encryption (only visible at the time of application)

`Signature`It is a string spliced on a `timestamp（in seconds） + method（GET OR POST） + requestPath + body`string ("+" means string connection), using secretKey, encrypting it according to the HMAC SHA256 method, and outputting it through hex encoding.

Among them, the value of `timestamp`, is the same as the request header: `Timestamp`, and must be in the decimal seconds format of the UTC time zone Unix timestamp or the ISO8601 standard time format, accurate to the second

method is a request method, all uppercase letters: `GET/POST`.

requestPath is the request interface path. E.g:`/orders?state=1&type=2`

The body refers to the string of the request body (without blank characters, such as \n,\r,\t). If the request has no body (usually a GET request), the body can be omitted. E.g:`{"orderId":"377454671037440"}`

The secretKey is generated when the user applies for the API Key. For example: 533d6e70-21b2-eb5c-f801-c128021c70a1

# Websocket market push

## Heartbeat connection

**Function Description:**

Long connection heartbeat

**Request path:**

wss://www.fameex.com/spot

**Request method:**

websocket

> **Example request:**

```json
{
  "op": "ping"
}
```

**parameter:**

| Name | Mandatory | Type   | Description           |
| :--- | :-------- | :----- | :-------------------- |
| on   | Yes       | string | Message type ("ping") |

> **Return example:**

```json
{
  "code": 200,
  "op": "pong"
}
```

### Response

| Name | Type   | Description           |
| :--- | :----- | :-------------------- |
| code | int    | 200, normal           |
| on   | string | Message type ("pong") |

## Login information

**Function Description:**

Long connection login

**Request path:**

wss://www.fameex.com/spot

**Request method:**

websocket

> **Example request:**

```json
{
  "op": "req",
  "topic": "auth",
  "params": {
    "platform": "API",
    "accessKey": "e690af61-bc06-d936-50fc-4053bdc2cf85"
  }
}
```

**parameter:**

| Name      | Mandatory | Type   | Description                   |
| :-------- | :-------- | :----- | :---------------------------- |
| on        | Yes       | string | Message type ("req")          |
| topic     | Yes       | string | Request subject ("auth")      |
| params    | Yes       | object | Parameter                     |
| accessKey | Yes       | string | AccessKey applied for         |
| platform  | Yes       | string | Platform source (WEB/APP/API) |

> **Return example:**

```json
{
  "code": 200,
  "op": "req",
  "topic": "auth"
}
```

### Response

| Name  | Type   | Description              |
| :---- | :----- | :----------------------- |
| code  | int    | 200, normal              |
| on    | string | Message type ("req")     |
| topic | string | Request subject ("auth") |

## Push K line/Candlestick information

**Function Description:**

This interface is registered for K-line/Candlestick service

**Request path:**

wss://www.fameex.com/spot

**Request method:**

websocket

> **Example request:**

```json
{
  "op": "sub",
  "topic": "spot.market.kline",
  "params": {
    "symbol": "BTC-USDT",
    "period": "1"
  }
}
```

**parameter:**

| Name   | Mandatory | Type   | Description                                             |
| :----- | :-------- | :----- | :------------------------------------------------------ |
| on     | Yes       | string | Message type ("sub")                                    |
| topic  | Yes       | string | Subscribe to topic ("spot.market.kline")                |
| params | Yes       | object | Parameter                                               |
| symbol | Yes       | string | The name of the currency pair (for example, "BTC-USDT") |
| period | Yes       | string | Candlestick time granularity (1,5,15,30,60,120,240,1D)  |

> **Return example:**

```json
{
  "code": 200,
  "op": "req",
  "topic": "auth",
  "data": {
    "symbol": "BTC-USDT",
    "period": "1",
    "time": 1603785494,
    "open": "103.4",
    "low": "103.4",
    "high": "103.4",
    "close": "103.4",
    "amount": "1.66",
    "volume": "200.12"
  }
}
```

### Response

| Name   | Type   | Description                                             |
| :----- | :----- | :------------------------------------------------------ |
| code   | int    | 200, normal                                             |
| on     | string | Message type ("sub")                                    |
| topic  | string | Request subject ("spot.market.kline")                   |
| data   | object | Return data entity                                      |
| symbol | string | The name of the currency pair (for example, "BTC-USDT") |
| period | string | Candlestick time granularity (1,5,15,30,60,120,240,1D)  |
| time   | int64  | Start timestamp, seconds                                |
| open   | string | Opening price                                           |
| low    | string | Lowest price                                            |
| high   | string | Highest price                                           |
| close  | string | Latest price                                            |
| amount | string | Trading currency volume                                 |
| volume | string | Denominated currency trading volume                     |

## Push homepage quotation

**Function Description:**

This interface registers the homepage market quotation service

**Request path:**

wss://www.fameex.com/spot

**Request method:**

websocket

> **Example request:**

```json
{
  "op": "sub",
  "topic": "spot.market.ticker",
  "params": {
    "symbol": "BTC-USDT"
  }
}
```

**parameter:**

| Name   | Mandatory | Type   | Description                                             |
| :----- | :-------- | :----- | :------------------------------------------------------ |
| on     | Yes       | string | Message type ("sub")                                    |
| topic  | Yes       | string | Subscribe to topic ("spot.market.kline")                |
| params | Yes       | object | Parameter                                               |
| symbol | Yes       | string | The name of the currency pair (for example, "BTC-USDT") |

> **Return example:**

```json
{
  "code": 200,
  "op": "sub",
  "topic": "spot.market.ticker",
  "data": {
    "symbol": "BTC-USDT",
    "gain": "0.12",
    "open": "103.4",
    "low": "103.4",
    "high": "103.4",
    "close": "103.4",
    "amount": "1.66",
    "volume": "200.12",
    "quotePrice": "450.12"
  }
}
```

### Response

| Name       | Type   | Description                                             |
| :--------- | :----- | :------------------------------------------------------ |
| code       | int    | 200, normal                                             |
| on         | string | Message type ("sub")                                    |
| topic      | string | Request subject ("spot.market.ticker")                  |
| data       | object | Return data entity                                      |
| symbol     | string | The name of the currency pair (for example, "BTC-USDT") |
| open       | string | 24-hour opening price                                   |
| low        | string | Lowest price in 24 hours                                |
| high       | string | Highest price in 24 hours                               |
| close      | string | Latest transaction price                                |
| amount     | string | 24-hour trading currency volume                         |
| volume     | string | 24-hour denominated currency trading volume             |
| quotePrice | string | Denominated currency price                              |

## Push in-depth quotations

**Function Description:**

This interface registers for in-depth services

**Request path:**

wss://www.fameex.com/spot

**Request method:**

websocket

> **Example request:**

```json
{
  "op": "sub",
  "topic": "spot.market.ticker",
  "params": {
    "symbol": "BTC-USDT",
    "step": "step0"
  }
}
```

**parameter:**

| Name   | Mandatory | Type   | Description                                             |
| :----- | :-------- | :----- | :------------------------------------------------------ |
| on     | Yes       | string | Message type ("sub")                                    |
| topic  | Yes       | string | Subscribe to topic ("spot.market.ticker")               |
| params | Yes       | object | Parameter                                               |
| symbol | Yes       | string | The name of the currency pair (for example, "BTC-USDT") |
| step   | Yes       | string | In-depth price aggregation type (step0~step4)           |

> **Return example:**

```json
{
  "code": 200,
  "op": "sub",
  "topic": "spot.market.ticker",
  "data": {
    "symbol": "BTC-USDT",
    "step": "step0",
    "time": 1603785494,
    "bids": [["123.12", "1.2"]],
    "asks": [["123.12", "1.2"]]
  }
}
```

### Response

| Name   | Type   | Description                                             |
| :----- | :----- | :------------------------------------------------------ |
| code   | int    | 200, normal                                             |
| on     | string | Message type ("sub")                                    |
| topic  | string | Request subject ("spot.market.depth")                   |
| data   | object | Return data entity                                      |
| symbol | string | The name of the currency pair (for example, "BTC-USDT") |
| step   | string | In-depth price aggregation type (step0~step4)           |
| time   | string | Timestamp, seconds                                      |
| bids   | array  | All current buy orders [price, quantity]                |
| asks   | array  | All current sell orders [price, quantity]               |

## Push the latest transaction order quotation

**Function Description:**

This interface pushes the latest transaction order details

**Request path:**

wss://www.fameex.com/spot

**Request method:**

websocket

> **Example request:**

```json
{
  "op": "sub",
  "topic": "spot.market.last_trade",
  "params": {
    "symbol": "BTC-USDT"
  }
}
```

**parameter:**

| Name   | Mandatory | Type   | Description                                             |
| :----- | :-------- | :----- | :------------------------------------------------------ |
| on     | Yes       | string | Message type ("sub")                                    |
| topic  | Yes       | string | Subscribe to topic ("spot.market.last_trade")           |
| params | Yes       | object | Parameter                                               |
| symbol | Yes       | string | The name of the currency pair (for example, "BTC-USDT") |

> **Return example:**

```json
{
  "code": 200,
  "op": "sub",
  "topic": "spot.market.last_trade",
  "data": [
    {
      "symbol": "BTC-USDT",
      "tradeId": "10384834938169458677",
      "side": 1,
      "price": "7890.12",
      "amount": "1.12",
      "createTime": 156655468
    }
  ]
}
```

### Response

| Name       | Type   | Description                                             |
| :--------- | :----- | :------------------------------------------------------ |
| code       | int    | 200, normal                                             |
| on         | string | Message type ("sub")                                    |
| topic      | string | Request subject ("spot.market.last_trade")              |
| data       | object | Return data entity                                      |
| symbol     | string | The name of the currency pair (for example, "BTC-USDT") |
| tradeId    | string | Order ID                                                |
| side       | string | Order Direction 1-Buy 2-Sell                            |
| price      | array  | Transaction price                                       |
| amount     | array  | Number of transactions                                  |
| createTime | int64  | Creation timestamp, seconds                             |

## Push order transaction or cancellation

**Function Description:**

Push buyers and sellers or own orders to complete or cancel

**Request path:**

wss://www.fameex.com/spot

**Request method:**

websocket

> **Example request:**

```json
{
  "op": "sub",
  "topic": "spot.orders",
  "params": {
    "symbol": "BTC-USDT"
  }
}
```

**parameter:**

| Name   | Mandatory | Type   | Description                                             |
| :----- | :-------- | :----- | :------------------------------------------------------ |
| on     | Yes       | string | Message type ("sub")                                    |
| topic  | Yes       | string | Subscribe to topics ("spot.orders")                     |
| params | Yes       | object | Parameter                                               |
| symbol | Yes       | string | The name of the currency pair (for example, "BTC-USDT") |

> **Return example:**

```json
{
  "code": 200,
  "op": "sub",
  "topic": "spot.orders",
  "data": {
    "symbol": "BTC-USDT",
    "orderId": "10384834938169458688",
    "clientOid": "10567108063048237056",
    "side": 1,
    "orderType": 1,
    "price": "7890.12",
    "amount": "1.12",
    "money": "1.12",
    "filledAmount": "1.12",
    "filledMoney": "8562.12",
    "filledFee": "1.12",
    "feeCurrency": "usdt",
    "triggerPrice": "7600.12",
    "triggerType": "gte",
    "triggerState": 1,
    "liquidationType": 1,
    "strategyId": "123456789",
    "strategyType": 1,
    "strategyName": "abc",
    "state": 1,
    "accountType": "spot",
    "platform": "API",
    "cancelType": 1,
    "createTime": 15665546871,
    "updateTime": 15665546872
  }
}
```

### Response

| Name            | Type   | Description                                                                                                                           |
| :-------------- | :----- | :------------------------------------------------------------------------------------------------------------------------------------ |
| code            | int    | 200, normal                                                                                                                           |
| on              | string | Message type ("sub")                                                                                                                  |
| topic           | string | Request subject ("spot.orders")                                                                                                       |
| data            | object | Return data entity                                                                                                                    |
| symbol          | string | The name of the currency pair (for example, "BTC-USDT")                                                                               |
| orderId         | string | Order order ID                                                                                                                        |
| clientOid       | string | User-made order ID                                                                                                                    |
| side            | int    | Order direction 1-buy 2-sell                                                                                                          |
| orderType       | int    | Order Type 1-Limit Price 2-Market Price 3-Take Profit and Stop Loss 4-Tracking Order 5-Maker Only                                     |
| price           | string | Order price                                                                                                                           |
| amount          | string | Number of orders                                                                                                                      |
| money           | string | Entrusted amount (when buying at market price)                                                                                        |
| filledAmount    | sting  | Number of transactions                                                                                                                |
| filledMoney     | sting  | Transaction amount                                                                                                                    |
| filledFee       | string | Transaction fee                                                                                                                       |
| feeCurrency     | string | Transaction fee currency                                                                                                              |
| triggerPrice    | string | Order trigger price                                                                                                                   |
| triggerType     | string | Order trigger type gte-greater than or equal to lte-less than or equal to                                                             |
| triggerState    | int    | Trigger status 1-trigger successful                                                                                                   |
| liquidationType | int    | Forced liquidation type 1-liquidation                                                                                                 |
| strategyId      | string | Strategy Id                                                                                                                           |
| strategyType    | int    | Strategy type                                                                                                                         |
| strategyName    | string | Strategy name                                                                                                                         |
| state           | int    | Order Status 1- Created 2- Waiting for Transaction 3- Partially Completed 4- Completely Completed 5- Partially Cancelled 6- Cancelled |
| accountType     | string | Account type                                                                                                                          |
| platform        | int    | Platform source                                                                                                                       |
| cancelType      | int    | Order Cancellation Type 1-User Cancellation 2-System Cancellation 3-Operation Cancellation                                            |
| createTime      | int64  | Order time stamp, seconds                                                                                                             |
| updateTime      | int64  | Status update timestamp, seconds                                                                                                      |

## Cancel homepage quotes

**Function Description:**

This interface cancels the homepage quotation service

**Request path:**

wss://www.fameex.com/spot

**Request method:**

websocket

> **Example request:**

```json
{
  "op": "unsub",
  "topic": "spot.market.ticker",
  "params": {
    "symbol": "BTC-USDT",
    "period": "",
    "step": "",
    "activityId": ""
  }
}
```

**parameter:**

| Name       | Mandatory | Type   | Description                                                      |
| :--------- | :-------- | :----- | :--------------------------------------------------------------- |
| op         | YES       | string | Message type ("unsub")                                           |
| topic      | YES       | string | Subscribe to topics ("spot.market.ticker")                       |
| params     | YES       | object | Parameter                                                        |
| symbol     | NO        | string | The name of the currency pair (for example, "BTC-USDT")          |
| step       | NO        | string | In-depth price aggregation type (step0~step4)                    |
| period     | NO        | string | Time granularity（ "1","5","15","30","60","120","240","1D","1W") |
| activityId | NO        | string | Activity ID                                                      |

> **Return example:**

```json
{
  "code": 200,
  "op": "unsub",
  "topic": "spot.market.ticker"
}
```

### Response

| Name  | Type   | Description                                |
| ----- | ------ | ------------------------------------------ |
| code  | int    | 200, normal                                |
| op    | string | Message type ("unsub")                     |
| topic | string | Subscribe to topics ("spot.market.ticker") |

# General Info

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

### Response

| Name | Type  | Description                        |
| ---- | ----- | ---------------------------------- |
| code | int   | 200, normal                        |
| ts   | int64 | Request time, seconds              |
| data | int64 | Return value, current time, second |

## Get all trading currency pairs

Speed limit rule: 20 times/2s

**Function description:**

This interface returns all trading currency pairs supported by the FameEX platform.

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

### Response

| Name            | Type   | Description                                                                                    |
| --------------- | ------ | ---------------------------------------------------------------------------------------------- |
| code            | int    | 200, normal                                                                                    |
| ts              | int64  | Request time, seconds                                                                          |
| msg             | string | Description of the return value this time                                                      |
| total           | int    | Total number of trading currency pairs                                                         |
| data            | list   | Return data: currency pair information                                                         |
| base            | string | Transaction currency                                                                           |
| quote           | string | Denominated currency                                                                           |
| pair            | string | Trading currency pairs                                                                         |
| pricePercision  | string | The precision of the denominated currency in the trading pair (digits after the decimal point) |
| amountPercision | string | The precision of the trading currency in the trading pair (digits after the decimal point)     |
| permitAmount    | string | Minimum number of pending orders                                                               |

## Get all transaction currencies

Speed limit rule: 20 times/2s

**Function description:**

This interface returns all trading currencies supported by FameEX.

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

### Response

| Name                      | Type   | Description                                                                           |
| ------------------------- | ------ | ------------------------------------------------------------------------------------- |
| code                      | int    | 200, normal                                                                           |
| msg                       | string | Description of the return value this time                                             |
| data                      | list   | Return data: currency information                                                     |
| currency                  | string | Currency abbreviation                                                                 |
| nameEn                    | string | English name                                                                          |
| nameZh                    | string | Chinese name                                                                          |
| isBase                    | int    | 1- Can be used as transaction currency 2- Can not be used as transaction currency     |
| isQuote                   | int    | 1- Can be used as a denominated currency 2- Can not be used as a denominated currency |
| minChargeAmount           | string | Minimum deposit amount                                                                |
| blockConfirmNumber        | int    | Block confirmation number                                                             |
| onceminwithdraw           | string | Maximum number of withdrawals at a time                                               |
| daymaxwithdrawtimes       | int    | Maximum number of withdrawals in a single day                                         |
| feewithdraw               | string | Withdrawal fee                                                                        |
| state in currencyRecharge | int    | Deposit status 1-open 2-close                                                         |
| state in currencyWithdraw | int    | Withdrawal status 1-open 2-close                                                      |

# Market Data Endpoints

## Order Book

> Request

```shell
curl --request GET 'https://api.fameex.com/api/v2/orderbook?symbol=BTC-USDT&limit=5'
```

> Response

```json
{
  "timestamp": 1648456620000,
  "bids": [
    [
      "50006.1", // PRICE
      "0.024" // QTY
    ]
  ],
  "asks": [
    [
      "50006.34", // PRICE
      "0.01" // QTY
    ]
  ]
}
```

### HTTP Request

GET `/api/v2/orderbook`

### Parameters

| Name   | Mandatory | Type   | Description                                 |
| :----- | :-------- | :----- | :------------------------------------------ |
| symbol | YES       | string | Name of the trading pair, example: BTC-USDT |
| limit  | NO        | int    | Default value is 100                        |

### Response

| Name      | Type   | Description                                                            |
| :-------- | :----- | :--------------------------------------------------------------------- |
| timestamp | int    | Current time, unit in millisecond                                      |
| bids      | string | Bid price and quantity, with best bid prices ranked from top to bottom |
| asks      | string | Ask price and quantity, with best ask prices ranked from top to bottom |

## Recent Trades List

> Request

```shell
curl --request GET 'https://api.fameex.com/api/v2/trades?symbol=BTC-USDT'
```

> Response

```json
[
  {
    "trade_id": 728356542914519040,
    "price": "71000",
    "base_volume": "0.001",
    "quote_volume": "71",
    "timestamp": 1648456620000,
    "type": "sell"
  },
  {
    "trade_id": 728342639237160960,
    "price": "70727.2",
    "base_volume": "0.001",
    "quote_volume": "70.7272",
    "timestamp": 1648453305000,
    "type": "buy"
  }
]
```

### HTTP Request

GET `/api/v2/trades`

### Parameters

| Name   | Mandatory | Type   | Description                                 |
| ------ | --------- | ------ | ------------------------------------------- |
| symbol | YES       | string | Name of the trading pair, example: BTC-USDT |
| limit  | NO        | int    | Default value is 100, max 100               |

### Response

| Name         | Type   | Description                            |
| ------------ | ------ | -------------------------------------- |
| trade_id     | int    | Order ID                               |
| price        | string | Order price                            |
| base_volume  | string | Trading volume                         |
| quote_volume | string | Trading quote volume                   |
| timestamp    | int    | Current timestamp, unit in millisecond |
| type         | string | buy and sell direction                 |

## Kline/Candlestick Data

Speed limit rule: 20 times/2s

**Function Description:**

This interface obtains historical K-line/Candlestick data.

**Request path:**

/v1/market/history/kline

curl `https://api.fameex.com/v1/market/history/kline`

**Routing parameters:**

No

**Post parameters:**

| Name      | Mandatory | Type   | Description                                                      |
| :-------- | :-------- | :----- | :--------------------------------------------------------------- |
| symbol    | Yes       | string | The name of the currency pair, for example "ETH-BTC"             |
| period    | Yes       | string | Time granularity（ "1","5","15","30","60","120","240","1D","1W") |
| startTime | No        | int64  | Start time, timestamp (unit: seconds)                            |
| endTime   | No        | int64  | End time, timestamp (unit: seconds)                              |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": [
    {
      "time": 1570518900,
      "amount": "0.01",
      "open": "0.00481",
      "close": "0.00481",
      "low": "0.00481",
      "hight": "0.00481",
      "volume": "100"
    }
  ]
}
```

### Response

| Name   | Type   | Description                         |
| :----- | :----- | :---------------------------------- |
| code   | int    | Return value status                 |
| time   | int64  | Timestamp                           |
| amount | string | Trading currency volume             |
| open   | string | Opening price                       |
| close  | string | Closing price                       |
| low    | string | Lowest price                        |
| hight  | string | Highest price                       |
| volume | string | Denominated currency trading volume |

## 24hr Ticker Price Change Statistics

> Request

```shell
curl --request GET 'https://api.fameex.com/api/v2/ticker/24hr'
```

> Response

```json
[
  {
    "trading_pairs": "XLM-BTC",
    "last_price": "0.01",
    "lowest_ask": "0",
    "highest_bid": "0",
    "base_volume": "0",
    "quote_volume": "0",
    "price_change_percent_24h": "0",
    "highest_price_24h": "0.01",
    "lowest_price_24h": "0.01"
  },
  {
    "trading_pairs": "WINK-USDT",
    "last_price": "6.48",
    "lowest_ask": "6.48",
    "highest_bid": "6.47",
    "base_volume": "0.15432",
    "quote_volume": "0.9999936",
    "price_change_percent_24h": "0",
    "highest_price_24h": "6.48",
    "lowest_price_24h": "6.48"
  }
]
```

### HTTP Request

GET `/api/v2/ticker/24hr`

### Parameters

| Name   | Mandatory | Type   | Description                                 |
| ------ | --------- | ------ | ------------------------------------------- |
| symbol | NO        | string | Name of the trading pair, example: BTC-USDT |

### Response

| Name                     | Type   | Description              |
| :----------------------- | :----- | :----------------------- |
| trading_pairs            | string | Name of the trading pair |
| last_price               | string | Last traded price        |
| lowest_ask               | string | Best ask price           |
| highest_bid              | string | Best bid price           |
| base_volume              | string | Trading volume           |
| quote_volume             | string | Trading quote volume     |
| price_change_percent_24h | string | 24 hour increase         |
| highest_price_24h        | string | High price               |
| lowest_price_24h         | string | Low price                |

## Detailed summary for each currency

> Request

```shell
curl --request GET 'https://api.fameex.com/v2/public/assets'
```

> Response

```json
{
    "code": "0",
    "message": null,
    "data": {
        "BTC": {
            "name": "btc",
            "unified_cryptoasset_id": 95,
            "can_withdraw": "true",
            "can_deposit": "true",
            "min_withdraw": "10",
            "max_withdraw": "100",
        },
        "ETH": {
            "name": "eth",
            "unified_cryptoasset_id": 47,
            "can_withdraw": "true",
            "can_deposit": "true",
            "min_withdraw": "1",
            "max_withdraw": "2",
        }
    }

```

### HTTP Request

GET `/v2/public/assets`

### Parameters

无

### Response

| Name                   | Type   | Description                                                          |
| :--------------------- | :----- | :------------------------------------------------------------------- |
| name                   | string | currency name                                                        |
| unified_cryptoasset_id | string | currency id                                                          |
| can_withdraw           | bool   | Identifies whether withdrawals are enabled or disabled.              |
| can_deposit            | bool   | Identifies whether deposits are enabled or disabled.                 |
| min_withdraw           | string | Identifies the single minimum withdrawal amount of a cryptocurrency. |
| max_withdraw           | string | Identifies the single maximum withdrawal amount of a cryptocurrency. |

## Overview of market data for all tickers and all market pairs

> Request

```shell
curl --request GET 'https://api.fameex.com/v2/public/summary'
```

> Response

```json
{
  "code": "0",
  "message": null,
  "data": [
    {
      "trading_pairs": "btcusdt",
      "last_price": "60000",
      "lowest_ask": "60000",
      "highest_bid": "555",
      "base_volume": "0",
      "quote_volume": "0",
      "price_change_percent_24h": "0",
      "highest_price_24h": "60000",
      "lowest_price_24h": "60000",
      "base_currency": "BTC",
      "quote_currency": "USDT"
    },
    {
      "trading_pairs": "ethusdt",
      "last_price": "60000",
      "lowest_ask": "60000",
      "highest_bid": "555",
      "base_volume": "0",
      "quote_volume": "0",
      "price_change_percent_24h": "0",
      "highest_price_24h": "60000",
      "lowest_price_24h": "60000",
      "base_currency": "ETH",
      "quote_currency": "USDT"
    }
  ]
}
```

### HTTP Request

GET `/v2/public/summary`

### Parameters

无

### Response

| Name                     | Type   | Description                                                                     |
| :----------------------- | :----- | :------------------------------------------------------------------------------ |
| trading_pairs            | string | Identifier of a ticker with delimiter to separate base/quote,eg. BTC-USD        |
| last_price               | string | Last transacted price of base currency based on given quote currency            |
| lowest_ask               | string | Lowest Ask price of base currency based on given quote currency                 |
| highest_bid              | string | Highest bid price of base currency based on given quote currency                |
| base_volume              | string | 24-hr volume of market pair denoted in BASE currency                            |
| quote_volume             | string | 24-hr volume of market pair denoted in QUOTE currency                           |
| price_change_percent_24h | string | 24-hr % price change of market pair                                             |
| highest_price_24h        | string | Highest price of base currency based on given quote currency in the last 24-hrs |
| lowest_price_24h         | string | Lowest price of base currency based on given quote currency in the last 24-hrs  |
| base_currency            | string | Symbol/currency code of base currency, eg. BTC                                  |
| quote_currency           | string | Symbol/currency code of quote currency, eg. USD                                 |

## 24-hour pricing and volume summary

> Request

```shell
curl --request GET 'https://api.fameex.com/v2/public/ticker'
```

> Response

```json
{
  "code": "0",
  "message": null,
  "data": {
    "BTC_USDT": {
      "base_id": "BTC",
      "quote_id": "USDT",
      "last_price": "60000",
      "quote_volume": "0",
      "base_volume": "0",
      "isFrozen": 0
    },
    "ETH_USDT": {
      "base_id": "ETH",
      "quote_id": "USDT",
      "last_price": "60000",
      "quote_volume": "0",
      "base_volume": "0",
      "isFrozen": 0
    }
  }
}
```

### HTTP Request

GET `/v2/public/ticker`

### Parameters

无

### Response

| Name         | Type   | Description                                                          |
| :----------- | :----- | :------------------------------------------------------------------- |
| base_id      | string | The quote pair Unified Cryptoasset ID.                               |
| quote_id     | string | The base pair Unified Cryptoasset ID.                                |
| last_price   | string | Last transacted price of base currency based on given quote currency |
| quote_volume | string | 24 hour trading volume denoted in QUOTE currency                     |
| base_volume  | string | 24-hour trading volume denoted in BASE currency                      |
| isFrozen     | string | Indicates if the market is currently enabled (0) or disabled (1).    |

## Full depth returned for a given market pair

> Request

```shell
curl --request GET 'https://api.fameex.com/v2/public/orderbook/market_pair?market_pair=BTC_USDT&level=3&depth=100'
```

> Response

```json
{
  "code": "0",
  "message": null,
  "data": {
    "timestamp": "1622526449",
    "bids": [
      ["10", "0.1102"],
      ["20", "0.1"]
    ],
    "asks": [
      ["60000", "91.185787"],
      ["66000", "0.30322"]
    ]
  }
}
```

### HTTP Request

GET `/v2/public/orderbook/market_pair`

### Parameters

| Name        | Mandatory | Type   | Description                                                                                                                  |
| :---------- | :-------- | :----- | :--------------------------------------------------------------------------------------------------------------------------- |
| market_pair | YES       | string | A pair such as "BTC_USDT"                                                                                                    |
| level       | NO        | int    | eg: 3                                                                                                                        |
| depth       | NO        | int    | Orders depth quantity: [0,5,10,20,50,100,500] Not defined or 0 = full order book Depth = 100 means 50 for each bid/ask side. |

### Response

| Name      | Type   | Description |
| :-------- | :----- | :---------- |
| timestamp | int    | server time |
| bids      | string | 买          |
| asks      | string | 卖          |

## Completed trades for a given market pai

> Request

```shell
curl --request GET 'https://api.fameex.com/v2/public/trades/market_pair?market_pair=BTC_USDT'
```

> Response

```json
{
  "code": "0",
  "message": null,
  "data": [
    {
      "trade_id": 2101,
      "price": "60000",
      "base_volume": "0.003333",
      "quote_volume": "0",
      "timestamp": "1622526904",
      "type": "buy"
    },
    {
      "trade_id": 2100,
      "price": "60000",
      "base_volume": "0.008333",
      "quote_volume": "0",
      "timestamp": "1622526904",
      "type": "buy"
    }
  ]
}
```

### HTTP Request

GET `/v2/public/trades/market_pair`

### Parameters

| Name        | Mandatory | Type   | Description               |
| :---------- | :-------- | :----- | :------------------------ |
| market_pair | YES       | string | A pair such as "BTC_USDT" |

### Response

| Name         | Type   | Description                                                                                                                                                                                     |
| :----------- | :----- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| trade_id     | int    | A unique ID associated with the trade for the currency pair transaction Note: Unix timestamp does not qualify as trade_id.                                                                      |
| price        | string | Last transacted price of base currency based on given quote currency                                                                                                                            |
| base_volume  | string | Transaction amount in BASE currency.                                                                                                                                                            |
| quote_volume | string | Transaction amount in QUOTE currency.                                                                                                                                                           |
| timestamp    | string | Unix timestamp in milliseconds for when the transaction occurred.                                                                                                                               |
| type         | string | Used to determine whether or not the transaction originated as a buy or sell. Buy – Identifies an ask was removed from the order book. Sell – Identifies a bid was removed from the order book. |

## Symbol Price Ticker

> Request

```shell
curl --request GET 'https://api.fameex.com/api/v2/ticker/price'
```

> Response

```json
{
  "ETH-USDT": {
    "last_price": "1097.8",
    "base_volume": "0",
    "quote_volume": "0"
  },
  "WINK-USDT": {
    "last_price": "6.48",
    "base_volume": "0.15432",
    "quote_volume": "0.9999936"
  }
}
```

### HTTP Request

GET `/api/v2/ticker/price`

### Parameters

| Name   | Mandatory | Type   | Description                                 |
| :----- | :-------- | :----- | :------------------------------------------ |
| symbol | NO        | string | Name of the trading pair, example: BTC-USDT |

### Response

| Name         | Type   | Description          |
| :----------- | :----- | :------------------- |
| last_price   | string | Last traded price    |
| base_volume  | string | Trading volume       |
| quote_volume | string | Trading quote volume |

# Exchange API Endpoints

## New order

Speed limit rule: 100 times/2s

**Function Description:**

This interface provides the function of canceling all unexecuted orders of a specified currency pair or currency pairs.

**Request path:**

/v1/api/spot/orders

curl `https://api.fameex.com/v1/api/spot/orders`

**Routing parameters:**

No

**Post parameters:**

| Name         | Mandatory | Type   | Description                                                                                       |
| :----------- | :-------- | :----- | :------------------------------------------------------------------------------------------------ |
| symbol       | Yes       | string | For example, the name of the currency pair: "BTC-USDT"                                            |
| clientOid    | No        | string | User-made order ID                                                                                |
| side         | Yes       | int    | Order Direction 1-Buy 2-Sell                                                                      |
| orderType    | Yes       | int    | Order Type 1-Limit Price 2-Market Price 3-Take Profit and Stop Loss 4-Tracking Order 5-Maker Only |
| price        | No        | string | Commission price                                                                                  |
| amount       | Yes       | string | Entrusted quantity (trading amount when buying at market price)                                   |
| triggerPrice | No        | string | Trigger price                                                                                     |
| backRatio    | No        | string | Track the percentage of commissioned callbacks                                                    |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "orderId": "10383992916667793408",
    "clientOid": "10383992916667793408"
  }
}
```

### Response

| Name      | Type   | Description             |
| :-------- | :----- | :---------------------- |
| code      | int    | 200, normal             |
| msg       | string | Information Description |
| data      | object | Order information       |
| orderId   | string | Order ID                |
| clientOid | string | User-made order ID      |

## Cancel Order

Speed limit rule: 100 times/2s

**Function Description:**

This interface provides the function of canceling unfilled orders.

**Request path:**

/v1/api/spot/cancel_orders

curl `https://api.fameex.com/v1/api/spot/cancel_orders`

**Routing parameters:**

No

**Post parameters:**

| Name      | Mandatory | Type   | Description                                                           |
| :-------- | :-------- | :----- | :-------------------------------------------------------------------- |
| symbol    | Yes       | string | For example, the name of the currency pair: "BTC-USDT"                |
| orderid   | No        | string | Order ID (orderId and clientOid must and can only be filled in)       |
| clientOid | No        | string | User-made order ID (orderId and clientOid must be filled in only one) |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "orderId": "10383992916667793408"
  }
}
```

### Response

| Name      | Type   | Description              |
| :-------- | :----- | :----------------------- |
| code      | int    | 200, normal              |
| msg       | string | Description              |
| data      | object | Return order information |
| orderId   | string | Order ID                 |
| clientOid | string | User-made order ID       |

## Batch cancellation

Speed limit rule: 100 times/2s

**Function Description:**

This interface provides the function of canceling all unexecuted orders of a specified currency pair or currency pairs.

**Request path:**

/v1/api/spot/cancel_orders_all

curl `https://api.fameex.com/v1/api/spot/cancel_orders_all`

**Routing parameters:**

No

**Post parameters:**

| Name       | Mandatory | Type   | Description                                                                |
| :--------- | :-------- | :----- | :------------------------------------------------------------------------- |
| symbol     | Yes       | string | For example, the name of the currency pair: "BTC-USDT"                     |

```json
{
  "code": 200,
  "msg": "success",
  "data": [
    {
      "code": 200,
      "orderId": "111111"
    }
  ]
}
```

### Response

| Name      | Type         | Description                |
| :-------- | :----------- | :------------------------- |
| code      | int          | 200, normal                |
| msg       | string       | Description                |
| data      | object array | Batch cancellation details |
| code      | array        | Batch cancellation details |
| orderId   | string       | Order ID                   |
| clientOid | string       | User-made order ID         |

## Get order details

Speed limit rule: 20 times/2s

**Function Description:**

This interface obtains the specified order information through the order ID.

**Request path:**

/v1/api/spot/orderdetail

curl `https://api.fameex.com/v1/api/spot/orderdetail`

**Routing parameters:**

No

**Post parameters:**

| Name      | Mandatory | Type   | Description                                                           |
| :-------- | :-------- | :----- | :-------------------------------------------------------------------- |
| symbol    | Yes       | string | The name of the currency pair, such as "BTC-USDT"                     |
| orderId   | No        | string | Order ID (orderId and clientOid must and can only be filled in)       |
| clientOid | No        | string | User-made order ID (orderId and clientOid must be filled in only one) |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "symbol": "BTC-USDT",
    "orderId": "1111111",
    "side": 1,
    "orderType": 1,
    "price": "50000",
    "amount": "0.002",
    "filledAmount": "0.001"
  }
}
```

### Response

| Name            | Type   | Description                                                                                                                                     |
| :-------------- | :----- | :---------------------------------------------------------------------------------------------------------------------------------------------- |
| code            | int    | Return value status                                                                                                                             |
| msg             | string | Return value description                                                                                                                        |
| data            | object | Return value, order details                                                                                                                     |
| orderId         | string | Order ID                                                                                                                                        |
| clientOid       | string | User-made order ID                                                                                                                              |
| symbol          | string | The name of the currency pair (for example: BTC-USDT)                                                                                           |
| side            | int    | Order Direction 1-Buy 2-Sell                                                                                                                    |
| orderType       | int    | Order Type 1-Limit Price 2-Market Price 3-Take Profit and Stop Loss 4-Tracking Order 5-Maker Only                                               |
| price           | string | Commission price                                                                                                                                |
| amount          | string | Number of orders                                                                                                                                |
| money           | string | Entrusted amount (when buying at market price)                                                                                                  |
| filledAmount    | string | Number of transactions                                                                                                                          |
| filledMoney     | string | Transaction amount                                                                                                                              |
| filledFee       | string | Transaction fee                                                                                                                                 |
| feeCurrency     | string | Transaction fee currency                                                                                                                        |
| triggerPrice    | string | Order trigger price                                                                                                                             |
| triggerType     | string | Order trigger type gte-greater than or equal to lte-less than or equal to                                                                       |
| triggerState    | int    | Trigger status 1-trigger successful                                                                                                             |
| liquidationType | int    | Liquidation type 1- liquidation 2- lighten up 3- take profit lighten up                                                                         |
| strategyId      | string | Strategy Id                                                                                                                                     |
| strategyType    | int    | Strategy type                                                                                                                                   |
| strategyName    | string | Set the name of the strategy                                                                                                                    |
| state           | int    | Order Status 1- Created 2- Waiting for Transaction 3- Partially Completed 4- Completely Completed 5- Partially Cancelled 6- Cancelled           |
| accountType     | string | Account type                                                                                                                                    |
| platform        | string | Platform source                                                                                                                                 |
| cancelType      | int    | Order Cancellation Type 1-User Cancellation 2-System Cancellation 3-Operation Cancellation 4-Liquidation Cancellation 5-Lightening Cancellation |
| createTime      | int64  | Creation time                                                                                                                                   |
| updateTime      | int64  | Status update time                                                                                                                              |

## Get a list of orders

Speed limit rule: 20 times/2s

**Function Description:**

This interface obtains and lists your current order information (the order information of the last 3 months). This request supports paging, and is sorted and stored in reverse chronological order, with the latest one at the top.

**Request path:**

POST /v1/api/spot/orderlist

curl `https://api.fameex.com/v1/api/spot/orderlist`

**Routing parameters:**

No

**Post parameters:**

| Name         | Mandatory | Type      | Description                                                                                                 |
| :----------- | :-------- | :-------- | :---------------------------------------------------------------------------------------------------------- |
| base         | Yes       | string    | Transaction currency (uppercase, such as "BTC")                                                             |
| quote        | Yes       | string    | Denominated currency (uppercase, such as "USDT")                                                            |
| side         | No       | int    | Order Direction 1-Buy 2-Sell                                                                                |
| orderTypes   | No       | int array | List of order types 1- limit price 2- market price 3- stop profit stop loss 4- tracking order 5- Maker only |
| state        | Yes       | int    | Order status 7-uncompleted 8-completed 9-completed or partially cancelled                                   |
| pageNum      | Yes       | int       | Pagination, the first few pages (1<=pageNum)                 |
| pageSize     | Yes       | int       | Pagination, the number of pages (1<=pageSize<= 500)          |
| startTime    | No        | int       | Start timestamp, seconds                                     |
| endTime      | No        | int       | End timestamp, seconds                                       |
| strategyId   | No        | string    | Strategy Id                                                  |
| strategyType | No        | int       | Strategy type: 1-StrategyTypeGrid, 2-StrategyTypeInvest      |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "pageNum": 1,
    "pageSize": 10,
    "total": "10",
    "orders": [
      {
        "symbol": "BTC-USDT",
        "orderId": "1111111",
        "side": 1,
        "orderType": 1,
        "price": "50000",
        "amount": "0.002",
        "filledAmount": "0.001"
      }
    ]
  }
}
```

### Response

| Name            | Type         | Description                                                                                                                                     |
| :-------------- | :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------- |
| code            | int          | Return value status                                                                                                                             |
| msg             | string       | Return value description                                                                                                                        |
| data            | object       | Return value, order details                                                                                                                     |
| pageno          | int          | Pagination, the first few pages (1<=pageNum)                                                                                                    |
| pageSize        | int          | Pagination, the number of pages (1<=pageSize<= 500)                                                                                             |
| total           | int          | Total number                                                                                                                                    |
| orders          | object array | Order list                                                                                                                                      |
| orderId         | string       | Order ID                                                                                                                                        |
| clientOid       | string       | User-made order ID                                                                                                                              |
| symbol          | string       | The name of the currency pair (for example: BTC-USDT)                                                                                           |
| side            | int          | Order Direction 1-Buy 2-Sell                                                                                                                    |
| orderType       | int          | Order Type 1-Limit Price 2-Market Price 3-Take Profit and Stop Loss 4-Tracking Order 5-Maker Only                                               |
| price           | string       | Commission price                                                                                                                                |
| amount          | string       | Number of orders                                                                                                                                |
| money           | string       | Entrusted amount (when buying at market price)                                                                                                  |
| filledAmount    | string       | Number of transactions                                                                                                                          |
| filledMoney     | string       | Transaction amount                                                                                                                              |
| filledFee       | string       | Transaction fee                                                                                                                                 |
| feeCurrency     | string       | Transaction fee currency                                                                                                                        |
| triggerPrice    | string       | Order trigger price                                                                                                                             |
| triggerType     | string       | Order trigger type gte-greater than or equal to lte-less than or equal to                                                                       |
| triggerState    | int          | Trigger status 1-trigger successful                                                                                                             |
| liquidationType | int          | Liquidation type 1- liquidation 2- lighten up 3- take profit lighten up                                                                         |
| strategyId      | string       | Strategy Id                                                                                                                                     |
| strategyType    | int          | Strategy type                                                                                                                                   |
| strategyName    | string       | Set the name of the strategy                                                                                                                    |
| state           | int          | Order Status 1- Created 2- Waiting for Transaction 3- Partially Completed 4- Completely Completed 5- Partially Cancelled 6- Cancelled           |
| accountType     | string       | Account type                                                                                                                                    |
| platform        | string       | Platform source                                                                                                                                 |
| cancelType      | int          | Order Cancellation Type 1-User Cancellation 2-System Cancellation 3-Operation Cancellation 4-Liquidation Cancellation 5-Lightening Cancellation |
| createTime      | int64        | Creation time                                                                                                                                   |
| updateTime      | int64        | Status update time                                                                                                                              |

## Get transaction details

Speed limit rule: 20 times/2s

**Function Description:**

This interface gets all your current transaction order information. This request supports paging, and is sorted and stored in reverse chronological order, with the latest one at the top.

**Request path:**

/v1/api/spot/fills

curl `https://api.fameex.com/v1/api/spot/fills`

**Routing parameters:**

No

**Post parameters:**

| Name         | Mandatory | Type      | Description                                                                                                 |
| :----------- | :-------- | :-------- | :---------------------------------------------------------------------------------------------------------- |
| base         | No        | string    | Transaction currency (uppercase, such as "BTC")                                                             |
| quote        | No        | string    | Denominated currency (uppercase, such as "USDT")                                                            |
| orderId      | No        | string    | Order ID                                                                                                    |
| side         | No        | int       | Order Direction 1-Buy 2-Sell                                                                                |
| orderTypes   | No        | int array | List of order types 1- limit price 2- market price 3- stop profit stop loss 4- tracking order 5- Maker only |
| pageno       | Yes       | int       | Pagination, the first few pages (1<=pageNum)                                                                |
| pageSize     | Yes       | int       | Pagination, the number of pages (1<=pageSize<= 500)                                                         |
| startTime    | No        | int64     | Start timestamp, seconds                                                                                    |
| endTime      | No        | int64     | End timestamp, seconds                                                                                      |
| strategyId   | No        | string    | Strategy Id                                                                                                 |
| strategyType | No        | int       | Strategy type                                                                                               |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "pageNum": 1,
    "pageSize": 10,
    "total": "10",
    "trades": [
      {
        "symbol": "BTC-USDT",
        "tradeId": "1111111",
        "orderId": "1111111",
        "side": 1,
        "orderType": 1,
        "price": "50000",
        "amount": "0.002",
        "feeCurrency": "BTC",
        "feeRate": "0.0001",
        "fee": "0.000001",
        "accountType": "spot",
        "platform": "api",
        "role": "maker",
        "createTime": "1629854950"
      }
    ]
  }
}
```

### Response

| Name            | Type         | Description                                                                                       |
| :-------------- | :----------- | :------------------------------------------------------------------------------------------------ |
| code            | int          | Return value status                                                                               |
| msg             | string       | Return value description                                                                          |
| data            | object       | Return value, order details                                                                       |
| pageno          | int          | Pagination, the first few pages (1<=pageNum)                                                      |
| pageSize        | int          | Pagination, the number of pages (1<=pageSize<= 500)                                               |
| total           | int          | Total number                                                                                      |
| trades          | object array | List of commissioned orders                                                                       |
| orderId         | string       | Order ID                                                                                          |
| tradeId         | string       | Order ID                                                                                          |
| symbol          | string       | The name of the currency pair (for example: BTC-USDT)                                             |
| side            | int          | Order Direction 1-Buy 2-Sell                                                                      |
| orderType       | int          | Order Type 1-Limit Price 2-Market Price 3-Take Profit and Stop Loss 4-Tracking Order 5-Maker Only |
| price           | string       | Commission price                                                                                  |
| amount          | string       | Number of orders                                                                                  |
| feeRate         | string       | Actual handling fee rate                                                                          |
| feeCurrency     | string       | Transaction fee currency                                                                          |
| fee             | string       | Handling fee                                                                                      |
| liquidationType | int          | Liquidation type 1- liquidation 2- lighten up 3- take profit lighten up                           |
| strategyId      | string       | Strategy Id                                                                                       |
| strategyType    | int          | Strategy type                                                                                     |
| strategyName    | string       | Set the name of the strategy                                                                      |
| accountType     | string       | Account type                                                                                      |
| platform        | string       | Platform source                                                                                   |
| role            | string       | Character type 1-maker 2-taker                                                                    |
| selftrade       | int          | Whether self-deal 1-self-deal                                                                     |
| createTime      | int64        | Creation time                                                                                     |

# Wallet API Endpoints

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

### Response

| Name       | Type   | Description                                                         |
| ---------- | ------ | ------------------------------------------------------------------- |
| code       | int    | 200, normal                                                         |
| data       | list   | Return value, currency account data                                 |
| userid     | string | User id                                                             |
| walletType | string | Account type: spot-spot account otc-fiat account l2c-margin account |
| available  | string | Available Balance                                                   |
| total      | string | Total balance                                                       |
| currency   | string | Currency example: BTC                                               |
| hold       | string | Frozen amount                                                       |

## Get the details of single currency

Speed limit rule: 20 times/2s

**Function description:**

Get wallet account details (single currency)

**Request path:**

/v1/api/account/wallet/currency

curl `https://api.fameex.com/v1/api/account/wallet/currency`

**Routing parameters:**

| Name     | Mandatory | Type   | Description        |
| -------- | --------- | ------ | ------------------ |
| currency | Yes       | string | Currency, e.g. BTC |

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

### Response

| Name      | Type   | Description                                           |
| --------- | ------ | ----------------------------------------------------- |
| code      | int    | 200, normal                                           |
| msg       | string | Description of the return value this time             |
| userid    | string | User id                                               |
| data      | map    | Return value, currency account, details of a currency |
| available | string | Available Balance                                     |
| hold      | string | Frozen amount                                         |

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

| Name     | Mandatory | Type   | Description                                                                                                           |
| -------- | --------- | ------ | --------------------------------------------------------------------------------------------------------------------- |
| currency | Yes       | string | Currency type                                                                                                         |
| amount   | Yes       | string | Quantity                                                                                                              |
| from     | Yes       | string | Transfer account: spot spot account, otc fiat currency account, l2c margin account, swap USDT-futures account         |
| to       | Yes       | string | Transfer account: spot spot account, otc fiat currency account, l2c margin account, swap USDT-futures account         |
| fromPair | no        | string | The outgoing currency pair during the mutual transfer between margin account currency pairs, for example: BTC_USDT    |
| toPair   | no        | string | The transferred currency pair during the mutual transfer between margin account currency pairs, for example: ETH_USDT |

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

### Response

| Name    | Type   | Description                                       |
| ------- | ------ | ------------------------------------------------- |
| code    | int    | 200, normal                                       |
| msg     | string | success, normal                                   |
| data    | object | The response object returned by the fund transfer |
| orderid | string | Order id                                          |
| userid  | string | User id                                           |

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

| Name      | Mandatory | Type   | Description                                                         |
| --------- | --------- | ------ | ------------------------------------------------------------------- |
| tradeType | no        | int    | Transaction type: 0. All; 2. Buy; 3. Sell; 4. Actual fee            |
| currency  | no        | string | Example of currency name: ETH                                       |
| pageno    | Yes       | string | Page, 1 starts                                                      |
| pageSize  | Yes       | string | Number of pages (0 <pageSize ≤ 500)                                 |
| startTime | no        | string | Start time seconds to query records within the last 90 days at most |
| endTime   | no        | string | End time seconds                                                    |

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

### Response

| Name        | Type   | Description                                      |
| ----------- | ------ | ------------------------------------------------ |
| code        | int    | 200, normal                                      |
| msg         | string | success, normal                                  |
| data        | object | Empty string                                     |
| userId      | string | User id                                          |
| total       | int    | Number of bill records                           |
| list        | array  | Billing record list                              |
| tradeType   | int    | Transaction type: 2. Buy; 3. Sell; 4. Actual fee |
| operateTime | int64  | Operating time                                   |
| currency    | string | Example of currency name: ETH                    |
| amount      | string | Quantity                                         |

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

| Name      | Mandatory | Type   | Description                                         |
| --------- | --------- | ------ | --------------------------------------------------- |
| tradeType | no        | int    | Transaction type: 0. All; 1. Withdrawal; 2. Deposit |
| currency  | no        | string | Example of currency name: ETH                       |
| startTime | no        | int64  | Start time: second-level timestamp                  |
| endTime   | no        | int64  | End time time: second-level timestamp               |
| pageno    | Yes       | int    | Page number, starting from 1                        |
| pageSize  | Yes       | int    | Number of pages (0 <pageSize ≤ 500)                 |

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

### Response

| Name        | Type   | Description                                                                                                                                                                                                                                                                        |
| ----------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| code        | int    | 200, normal                                                                                                                                                                                                                                                                        |
| msg         | string | success, normal                                                                                                                                                                                                                                                                    |
| data        | object | Empty string                                                                                                                                                                                                                                                                       |
| total       | int    | Number of bill records                                                                                                                                                                                                                                                             |
| list        | array  | Billing record list                                                                                                                                                                                                                                                                |
| tradeType   | int    | Transaction type: 1. Withdraw coins; 2. Deposit coins                                                                                                                                                                                                                              |
| operateTime | int64  | Operating time                                                                                                                                                                                                                                                                     |
| currency    | string | Example of currency name: ETH                                                                                                                                                                                                                                                      |
| amount      | string | Quantity                                                                                                                                                                                                                                                                           |
| address     | string | When the tradeType is 1, it represents the withdrawal address; when the tradeType is 2, it represents the deposit address                                                                                                                                                          |
| fee         | string | Withdrawal fee                                                                                                                                                                                                                                                                     |
| label       | string | User's label                                                                                                                                                                                                                                                                       |
| chainType   | string | Chain type of currency                                                                                                                                                                                                                                                             |
| state       | int    | Bill status: When the tradeType is 1, state respectively represents: 1-Pending review; 2-Under review; 3-Completed; 4-Review failed; 5-Retracted; 6-Withdrawal failed; 7-Initial creation; 8- When the tradeType is 2 in confirmation , state respectively represents: 1-Completed |
| txId        | string | Transaction hash                                                                                                                                                                                                                                                                   |

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

| Name      | Mandatory | Type   | Description                                               |
| --------- | --------- | ------ | --------------------------------------------------------- |
| tradeType | no        | int    | Transaction type: 0. All; 1. Transfer in; 2. Transfer out |
| currency  | no        | string | Example of currency name: ETH                             |
| startTime | no        | int64  | Start time: second-level timestamp                        |
| endTime   | no        | int64  | End time time: second-level timestamp                     |
| pageno    | Yes       | int    | Page number, starting from 1                              |
| pageSize  | Yes       | int    | Number of pages (0 <pageSize ≤ 500)                       |

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

### Response

| Name         | Type   | Description                                                   |
| ------------ | ------ | ------------------------------------------------------------- |
| code         | int    | 200, normal                                                   |
| msg          | string | success, normal                                               |
| data         | object | Empty string                                                  |
| userId       | string | User id                                                       |
| total        | int    | Number of bill records                                        |
| list         | array  | Billing record list                                           |
| tradeType    | int    | Transaction type: 1. Transfer in; 2. Transfer out             |
| operateTime  | int64  | Operating time                                                |
| currency     | string | Example of currency name: ETH                                 |
| amount       | string | Quantity                                                      |
| fromCoinPair | string | Transferred currency pair                                     |
| toCoinPair   | string | Transfer out currency pair                                    |
| fromAccount  | string | Transfer out account: 0. Spot; 1. Leverage; 3. Legal currency |
| toAccount    | string | Transfer to account: 0. Spot; 1. Leverage; 3. Legal currency  |

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

| Name      | Mandatory | Type   | Description                                        |
| --------- | --------- | ------ | -------------------------------------------------- |
| tradeType | no        | int    | Transaction type: 0. All; 1. Rebate; 2. Activities |
| currency  | no        | string | Example of currency name: ETH                      |
| startTime | no        | int64  | Start time: second-level timestamp                 |
| endTime   | no        | int64  | End time time: second-level timestamp              |
| pageno    | Yes       | int    | Page number, starting from 1                       |
| pageSize  | Yes       | int    | Number of pages (0 <pageSize ≤ 500)                |

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

### Response

| Name        | Type   | Description                                |
| ----------- | ------ | ------------------------------------------ |
| code        | int    | 200, normal                                |
| msg         | string | success, normal                            |
| data        | object | Empty string                               |
| userId      | string | User id                                    |
| total       | int    | Number of bill records                     |
| list        | array  | Billing record list                        |
| tradeType   | int    | Transaction type: 1. Rebate; 2. Activities |
| operateTime | int64  | Operation time: second-level timestamp     |
| currency    | string | Example of currency name: ETH              |
| amount      | string | Quantity                                   |

## Get the deposit address

Speed limit rule: 20 times/2s

**Function description:**

This interface obtains the deposit address of each currency.

**Request path:**

/v1/api/account/deposit/address

curl `https://api.fameex.com/v1/api/account/deposit/address`

**Routing parameters:**

| Name      | Mandatory | Type   | Description        |
| --------- | --------- | ------ | ------------------ |
| coinType  | Yes       | string | Currency type USDT |
| chainType | Yes       | string | Chain type ERC20   |

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

### Response

| Name     | Type   | Description       |
| -------- | ------ | ----------------- |
| code     | int    | 200, normal       |
| request  | map    | Request parameter |
| userId   | string | User id           |
| coinType | string | Currency          |
| address  | string | address           |

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

### Response

| Name           | Type   | Description                                                                      |
| -------------- | ------ | -------------------------------------------------------------------------------- |
| code           | int    | 200, normal                                                                      |
| data           | list   | Return value, margin account data                                                |
| userid         | string | User id                                                                          |
| walletType     | string | Account type: spot-currency account otc-fiat currency account l2c-margin account |
| coinpair       | string | Example of currency pair name: BTC/USDT                                          |
| baseCurrency   | string | Example of transaction currency name: BTC                                        |
| quoteCurrency  | string | Example of denomination currency name: USDT                                      |
| baseAvailable  | string | Available amount of transaction currency                                         |
| quoteAvailable | string | Available amount in denominated currency                                         |
| baseHold       | string | Frozen amount of trading currency                                                |
| quoteHold      | string | Frozen amount in denominated currency                                            |
| baseTotal      | string | Total transaction currency                                                       |
| quoteTotal     | string | Total denominated currency                                                       |
| baseBorrowed   | string | Transaction currency loan amount                                                 |
| quote Borrowed | string | Denominated currency loan amount                                                 |
| baseInterest   | string | Transaction currency interest                                                    |
| quoteInterest  | string | Denominated currency interest                                                    |

# Margin trading API Endpoints

## Get the details of a currency pair under a margin account

Speed limit rule: 1 time/2s

**Function description:**

Get information about the balance, freeze, and availability of a currency pair account under a margin account

**Request path:**

/v1/api/lever/accounts

curl `https://api.fameex.com/v1/api/lever/accounts`

**Routing parameters:**

| Name     | Mandatory | Type   | Description                     |
| -------- | --------- | ------ | ------------------------------- |
| pairName | Yes       | string | Currency pair, example BTC_USDT |

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

### Response

| Name           | Type   | Description                                 |
| -------------- | ------ | ------------------------------------------- |
| code           | int    | 200, normal                                 |
| data           | list   | Return value, margin account data           |
| msg            | string | code response message                       |
| userid         | string | User id                                     |
| coinpair       | string | Example of currency pair name: BTC/USDT     |
| baseCurrency   | string | Example of transaction currency name: BTC   |
| quoteCurrency  | string | Example of denomination currency name: USDT |
| baseAvailable  | string | Available amount of transaction currency    |
| quoteAvailable | string | Available amount in denominated currency    |
| baseHold       | string | Frozen amount of trading currency           |
| quoteHold      | string | Frozen amount in denominated currency       |
| baseTotal      | string | Total transaction currency                  |
| quoteTotal     | string | Total denominated currency                  |
| baseBorrowed   | string | Transaction currency loan amount            |
| quote Borrowed | string | Denominated currency loan amount            |
| baseInterest   | string | Transaction currency interest               |
| quoteInterest  | string | Denominated currency interest               |
| burstPrice     | string | Liquidation price                           |
| riskRate       | string | Liquidation risk rate                       |

## Leverage order

Speed limit rule: 1 time/2s

**Function Description:**

This interface provides leverage to place orders.

**Request path:**

/v1/api/lever/orders/place

curl `https://api.fameex.com/v1/api/lever/orders/place`

**Routing parameters:**

No

**Post parameters:**

| Name         | Mandatory | Type   | Description                                                                                       |
| :----------- | :-------- | :----- | :------------------------------------------------------------------------------------------------ |
| symbol       | Yes       | string | For example, the name of the currency pair: "BTC-USDT"                                            |
| clientOid    | No        | string | User-made order ID                                                                                |
| side         | Yes       | int    | Order Direction 1-Buy 2-Sell                                                                      |
| orderType    | Yes       | int    | Order Type 1-Limit Price 2-Market Price 3-Take Profit and Stop Loss 4-Tracking Order 5-Maker Only |
| price        | No        | string | Commission price                                                                                  |
| amount       | Yes       | string | Entrusted quantity (trading amount when buying at market price)                                   |
| triggerPrice | No        | string | Trigger price                                                                                     |
| backRatio    | No        | string | Track the percentage of commissioned callbacks                                                    |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "orderId": "10383992916667793408",
    "clientOid": "10383992916667793408"
  }
}
```

### Response

| Name      | Type   | Description             |
| :-------- | :----- | :---------------------- |
| code      | int    | 200, normal             |
| msg       | string | Information Description |
| data      | object | Order information       |
| orderId   | string | Order ID                |
| clientOid | string | User-made order ID      |

## Leverage Cancellation

Speed limit rule: 1 time/2s

**Function Description:**

This interface provides the function of canceling unfilled leveraged orders.

**Request path:**

/v1/api/lever/orders/cancel

curl `https://api.fameex.com/v1/api/lever/orders/cancel`

**Routing parameters:**

No

**Post parameters:**

| Name      | Mandatory | Type   | Description                                                           |
| :-------- | :-------- | :----- | :-------------------------------------------------------------------- |
| symbol    | Yes       | string | For example, the name of the currency pair: "BTC-USDT"                |
| orderid   | No        | string | Order ID (orderId and clientOid must and can only be filled in)       |
| clientOid | No        | string | User-made order ID (orderId and clientOid must be filled in only one) |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "orderId": "10383992916667793408"
  }
}
```

### Response

| Name      | Type   | Description              |
| :-------- | :----- | :----------------------- |
| code      | int    | 200, normal              |
| msg       | string | Description              |
| data      | object | Return order information |
| orderId   | string | Order ID                 |
| clientOid | string | User-made order ID       |

## Leverage batch cancellation

Speed limit rule: 1 time/2s

**Function Description:**

This interface provides the function of canceling all unexecuted leveraged orders of a specified currency pair or currency pairs.

**Request path:**

/v1/api/lever/orders/batch_cancel

curl `https://api.fameex.com/v1/api/lever/orders/batch_cancel`

**Routing parameters:**

No

**Post parameters:**

| Name       | Mandatory | Type   | Description                                                                |
| :--------- | :-------- | :----- | :------------------------------------------------------------------------- |
| symbol     | Yes       | string | For example, the name of the currency pair: "BTC-USDT"                     |
| orderIds   | No        | array  | Order ID list (orderId and clientOid must be filled in only one)           |
| clientOids | No        | array  | User-made order ID list (orderId and clientOid must be filled in only one) |

```json
{
  "code": 200,
  "msg": "success",
  "data": [
    {
      "code": 200,
      "orderId": "111111"
    }
  ]
}
```

### Response

| Name      | Type         | Description                |
| :-------- | :----------- | :------------------------- |
| code      | int          | 200, normal                |
| msg       | string       | Description                |
| data      | object array | Batch cancellation details |
| code      | array        | Batch cancellation details |
| orderId   | string       | Order ID                   |
| clientOid | string       | User-made order ID         |

## Get a list of leveraged orders

Speed limit rule: 1 time/2s

**Function Description:**

List your current order information (the order information of the last 3 months). This request supports paging, and is sorted and stored in reverse chronological order, with the latest one at the top.

**Request path:**

/v1/api/lever/orders

curl `https://api.fameex.com/v1/api/lever/orders`

**Routing parameters:**

No

**Post parameters:**

| Name         | Mandatory | Type      | Description                                                                                                 |
| :----------- | :-------- | :-------- | :---------------------------------------------------------------------------------------------------------- |
| base         | Yes       | string    | Transaction currency (uppercase, such as "BTC")                                                             |
| quote        | Yes       | string    | Denominated currency (uppercase, such as "USDT")                                                            |
| side         | Yes       | string    | Order Direction 1-Buy 2-Sell                                                                                |
| orderTypes   | Yes       | int array | List of order types 1- limit price 2- market price 3- stop profit stop loss 4- tracking order 5- Maker only |
| state        | Yes       | string    | Order status 7-uncompleted 8-completed 9-completed or partially cancelled                                   |
| pageno       | No        | string    | Pagination, the first few pages (1<=pageNum)                                                                |
| pageSize     | No        | string    | Pagination, the number of pages (1<=pageSize<= 500)                                                         |
| startTime    | Yes       | string    | Start timestamp, seconds                                                                                    |
| endTime      | Yes       | string    | End timestamp, seconds                                                                                      |
| strategyId   | No        | string    | Strategy Id                                                                                                 |
| strategyType | No        | string    | Strategy type                                                                                               |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "pageNum": 1,
    "pageSize": 10,
    "total": "10",
    "orders": [
      {
        "symbol": "BTC-USDT",
        "orderId": "1111111",
        "side": 1,
        "orderType": 1,
        "price": "50000",
        "amount": "0.002",
        "filledAmount": "0.001"
      }
    ]
  }
}
```

### Response

| Name            | Type         | Description                                                                                                                                     |
| :-------------- | :----------- | :---------------------------------------------------------------------------------------------------------------------------------------------- |
| code            | int          | Return value status                                                                                                                             |
| msg             | string       | Return value description                                                                                                                        |
| data            | object       | Return value, order details                                                                                                                     |
| pageno          | int          | Pagination, the first few pages (1<=pageNum)                                                                                                    |
| pageSize        | int          | Pagination, the number of pages (1<=pageSize<= 500)                                                                                             |
| total           | int          | Total number                                                                                                                                    |
| orders          | object array | Order list                                                                                                                                      |
| orderId         | string       | Order ID                                                                                                                                        |
| clientOid       | string       | User-made order ID                                                                                                                              |
| symbol          | string       | The name of the currency pair (for example: BTC-USDT)                                                                                           |
| side            | int          | Order Direction 1-Buy 2-Sell                                                                                                                    |
| orderType       | int          | Order Type 1-Limit Price 2-Market Price 3-Take Profit and Stop Loss 4-Tracking Order 5-Maker Only                                               |
| price           | string       | Commission price                                                                                                                                |
| amount          | string       | Number of orders                                                                                                                                |
| money           | string       | Entrusted amount (when buying at market price)                                                                                                  |
| filledAmount    | string       | Number of transactions                                                                                                                          |
| filledMoney     | string       | Transaction amount                                                                                                                              |
| filledFee       | string       | Transaction fee                                                                                                                                 |
| feeCurrency     | string       | Transaction fee currency                                                                                                                        |
| triggerPrice    | string       | Order trigger price                                                                                                                             |
| triggerType     | string       | Order trigger type gte-greater than or equal to lte-less than or equal to                                                                       |
| triggerState    | int          | Trigger status 1-trigger successful                                                                                                             |
| liquidationType | int          | Liquidation type 1- liquidation 2- lighten up 3- take profit lighten up                                                                         |
| strategyId      | string       | Strategy Id                                                                                                                                     |
| strategyType    | int          | Strategy type                                                                                                                                   |
| strategyName    | string       | Set the name of the strategy                                                                                                                    |
| state           | int          | Order Status 1- Created 2- Waiting for Transaction 3- Partially Completed 4- Completely Completed 5- Partially Cancelled 6- Cancelled           |
| accountType     | string       | Account type                                                                                                                                    |
| platform        | string       | Platform source                                                                                                                                 |
| cancelType      | int          | Order Cancellation Type 1-User Cancellation 2-System Cancellation 3-Operation Cancellation 4-Liquidation Cancellation 5-Lightening Cancellation |
| createTime      | int64        | Creation time                                                                                                                                   |
| updateTime      | int64        | Status update time                                                                                                                              |

## Get details of leveraged orders

Speed limit rule: 1 time/2s

**Function Description:**

This interface obtains the specified order information through the order ID.

**Request path:**

/v1/api/lever/orders/detail

curl `https://api.fameex.com/v1/api/lever/orders/detail`

**Routing parameters:**

No

**Post parameters:**

| Name      | Mandatory | Type   | Description                                                           |
| :-------- | :-------- | :----- | :-------------------------------------------------------------------- |
| symbol    | Yes       | string | The name of the currency pair, such as "BTC-USDT"                     |
| orderId   | No        | string | Order ID (orderId and clientOid must and can only be filled in)       |
| clientOid | No        | string | User-made order ID (orderId and clientOid must be filled in only one) |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "symbol": "BTC-USDT",
    "orderId": "1111111",
    "side": 1,
    "orderType": 1,
    "price": "50000",
    "amount": "0.002",
    "filledAmount": "0.001"
  }
}
```

### Response

| Name            | Type   | Description                                                                                                                                     |
| :-------------- | :----- | :---------------------------------------------------------------------------------------------------------------------------------------------- |
| code            | int    | Return value status                                                                                                                             |
| msg             | string | Return value description                                                                                                                        |
| data            | object | Return value, order details                                                                                                                     |
| orderId         | string | Order ID                                                                                                                                        |
| clientOid       | string | User-made order ID                                                                                                                              |
| symbol          | string | The name of the currency pair (for example: BTC-USDT)                                                                                           |
| side            | int    | Order Direction 1-Buy 2-Sell                                                                                                                    |
| orderType       | int    | Order Type 1-Limit Price 2-Market Price 3-Take Profit and Stop Loss 4-Tracking Order 5-Maker Only                                               |
| price           | string | Commission price                                                                                                                                |
| amount          | string | Number of orders                                                                                                                                |
| money           | string | Entrusted amount (when buying at market price)                                                                                                  |
| filledAmount    | string | Number of transactions                                                                                                                          |
| filledMoney     | string | Transaction amount                                                                                                                              |
| filledFee       | string | Transaction fee                                                                                                                                 |
| feeCurrency     | string | Transaction fee currency                                                                                                                        |
| triggerPrice    | string | Order trigger price                                                                                                                             |
| triggerType     | string | Order trigger type gte-greater than or equal to lte-less than or equal to                                                                       |
| triggerState    | int    | Trigger status 1-trigger successful                                                                                                             |
| liquidationType | int    | Liquidation type 1- liquidation 2- lighten up 3- take profit lighten up                                                                         |
| strategyId      | string | Strategy Id                                                                                                                                     |
| strategyType    | int    | Strategy type                                                                                                                                   |
| strategyName    | string | Set the name of the strategy                                                                                                                    |
| state           | int    | Order Status 1- Created 2- Waiting for Transaction 3- Partially Completed 4- Completely Completed 5- Partially Cancelled 6- Cancelled           |
| accountType     | string | Account type                                                                                                                                    |
| platform        | string | Platform source                                                                                                                                 |
| cancelType      | int    | Order Cancellation Type 1-User Cancellation 2-System Cancellation 3-Operation Cancellation 4-Liquidation Cancellation 5-Lightening Cancellation |
| createTime      | int64  | Creation time                                                                                                                                   |
| updateTime      | int64  | Status update time                                                                                                                              |

## Get leveraged transaction details

Speed limit rule: 1 time/2s

**Function Description:**

This interface gets all your current transaction order information. This request supports paging, and is sorted and stored in reverse chronological order, with the latest one at the top.

**Request path:**

/v1/api/lever/deals

curl `https://api.fameex.com/v1/api/lever/deals`

**Routing parameters:**

No

**Post parameters:**

| Name         | Mandatory | Type      | Description                                                                                                 |
| :----------- | :-------- | :-------- | :---------------------------------------------------------------------------------------------------------- |
| base         | No        | string    | Transaction currency (uppercase, such as "BTC")                                                             |
| quote        | No        | string    | Denominated currency (uppercase, such as "USDT")                                                            |
| orderId      | No        | string    | Order ID                                                                                                    |
| side         | No        | int       | Order Direction 1-Buy 2-Sell                                                                                |
| orderTypes   | No        | int array | List of order types 1- limit price 2- market price 3- stop profit stop loss 4- tracking order 5- Maker only |
| pageno       | Yes       | int       | Pagination, the first few pages (1<=pageNum)                                                                |
| pageSize     | Yes       | int       | Pagination, the number of pages (1<=pageSize<= 500)                                                         |
| startTime    | No        | int64     | Start timestamp, seconds                                                                                    |
| endTime      | No        | int64     | End timestamp, seconds                                                                                      |
| strategyId   | No        | string    | Strategy Id                                                                                                 |
| strategyType | No        | int       | Strategy type                                                                                               |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "pageNum": 1,
    "pageSize": 10,
    "total": "10",
    "trades": [
      {
        "symbol": "BTC-USDT",
        "tradeId": "1111111",
        "orderId": "1111111",
        "side": 1,
        "orderType": 1,
        "price": "50000",
        "amount": "0.002",
        "feeCurrency": "BTC",
        "feeRate": "0.0001",
        "fee": "0.000001",
        "accountType": "spot",
        "platform": "api",
        "role": "maker",
        "createTime": "1629854950"
      }
    ]
  }
}
```

### Response

| Name            | Type         | Description                                                                                       |
| :-------------- | :----------- | :------------------------------------------------------------------------------------------------ |
| code            | int          | Return value status                                                                               |
| msg             | string       | Return value description                                                                          |
| data            | object       | Return value, order details                                                                       |
| pageno          | int          | Pagination, the first few pages (1<=pageNum)                                                      |
| pageSize        | int          | Pagination, the number of pages (1<=pageSize<= 500)                                               |
| total           | int          | Total number                                                                                      |
| trades          | object array | List of commissioned orders                                                                       |
| orderId         | string       | Order ID                                                                                          |
| tradeId         | string       | Order ID                                                                                          |
| symbol          | string       | The name of the currency pair (for example: BTC-USDT)                                             |
| side            | int          | Order Direction 1-Buy 2-Sell                                                                      |
| orderType       | int          | Order Type 1-Limit Price 2-Market Price 3-Take Profit and Stop Loss 4-Tracking Order 5-Maker Only |
| price           | string       | Commission price                                                                                  |
| amount          | string       | Number of orders                                                                                  |
| feeRate         | string       | Actual handling fee rate                                                                          |
| feeCurrency     | string       | Transaction fee currency                                                                          |
| fee             | string       | Handling fee                                                                                      |
| liquidationType | int          | Liquidation type 1- liquidation 2- lighten up 3- take profit lighten up                           |
| strategyId      | string       | Strategy Id                                                                                       |
| strategyType    | int          | Strategy type                                                                                     |
| strategyName    | string       | Set the name of the strategy                                                                      |
| accountType     | string       | Account type                                                                                      |
| platform        | string       | Platform source                                                                                   |
| role            | string       | Character type 1-maker 2-taker                                                                    |
| selftrade       | int          | Whether self-deal 1-self-deal                                                                     |
| createTime      | int64        | Creation time                                                                                     |

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

| Name     | Mandatory | Type   | Description                             |
| -------- | --------- | ------ | --------------------------------------- |
| pairName | no        | string | Example of currency pair name: ETH_USDT |

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

### Response

| Name                     | Type   | Description                                       |
| ------------------------ | ------ | ------------------------------------------------- |
| code                     | int    | 200, normal                                       |
| msg                      | string | success, normal                                   |
| data                     | array  | Return value, leverage configuration information  |
| coinPair                 | string | Currency pair name                                |
| leverMultiple            | string | Leverage                                          |
| quoteLeatestBorrowAmount | string | Minimum borrowing amount of denominated currency  |
| borrowFeeRate            | string | Loan rate                                         |
| quoteMostBorrowAmount    | string | The maximum loanable currency in a single day     |
| baseMostBorrowAmount     | string | Maximum loanable trading currency in a single day |

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

| Name     | Mandatory | Type   | Description                             |
| -------- | --------- | ------ | --------------------------------------- |
| pairName | Yes       | string | Example of currency pair name: ETH_USDT |
| currency | Yes       | string | Example of currency name: ETH           |

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

### Response

| Name              | Type   | Description                                      |
| ----------------- | ------ | ------------------------------------------------ |
| code              | int    | 200, normal                                      |
| msg               | string | success, normal                                  |
| data              | array  | Return value, leverage configuration information |
| canBorrowAmount   | string | Available amount                                 |
| borrowedAmount    | string | Amount borrowed                                  |
| borrowFeeRate     | string | Minimum borrowing amount of denominated currency |
| leastBorrowAmount | string | Minimum loan amount                              |

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

| Name     | Mandatory | Type   | Description                             |
| -------- | --------- | ------ | --------------------------------------- |
| pairName | Yes       | string | Example of currency pair name: ETH_USDT |
| currency | Yes       | string | Example of currency name: ETH           |
| amount   | Yes       | string | Loan amount                             |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": ""
}
```

### Response

| Name | Type   | Description     |
| ---- | ------ | --------------- |
| code | int    | 200, normal     |
| msg  | string | success, normal |
| data | array  | Empty string    |

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

| Name     | Mandatory | Type   | Description                             |
| -------- | --------- | ------ | --------------------------------------- |
| pairName | Yes       | string | Example of currency pair name: ETH_USDT |
| currency | Yes       | string | Example of currency name: ETH           |

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

### Response

| Name           | Type   | Description                                                  |
| -------------- | ------ | ------------------------------------------------------------ |
| code           | int    | 200, normal                                                  |
| msg            | string | success, normal                                              |
| data           | object | Return value, prompt message of user returning currency      |
| borrowedAmount | string | Unpaid principal                                             |
| interest       | string | Unpaid interest on borrowed currency                         |
| unReturnAmount | string | Outstanding amount                                           |
| availAmount    | string | The available amount of the currency under the currency pair |

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

| Name     | Mandatory | Type   | Description                             |
| -------- | --------- | ------ | --------------------------------------- |
| pairName | Yes       | string | Example of currency pair name: ETH_USDT |
| currency | Yes       | string | Currency name                           |
| amount   | Yes       | string | Refund amount                           |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": ""
}
```

### Response

| Name | Type   | Description     |
| ---- | ------ | --------------- |
| code | int    | 200, normal     |
| msg  | string | success, normal |
| data | array  | Empty string    |

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

| Name     | Mandatory | Type   | Description                             |
| -------- | --------- | ------ | --------------------------------------- |
| pairName | Yes       | string | Example of currency pair name: ETH_USDT |
| currency | Yes       | string | Example of currency name: ETH           |
| pageSize | Yes       | int    | Display quantity per page               |
| pageno   | Yes       | int    | page number                             |

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
    "pageSize": 5,
    "total": 2
  }
}
```

### Response

| Name           | Type   | Description                                       |
| -------------- | ------ | ------------------------------------------------- |
| code           | int    | 200, normal                                       |
| msg            | string | success, normal                                   |
| data           | list   | Return value, margin account data                 |
| borrowedTime   | int64  | Borrow time                                       |
| coinPair       | string | Example of borrowing currency pair name: BTC/USDT |
| coinType       | string | Example of borrowing currency name: BTC           |
| recordId       | string | Borrowing record id                               |
| borrowedAmount | string | Number of borrowed coins                          |
| amount         | string | Available amount of transaction currency          |
| borrowFeeRate  | string | Hourly rate                                       |
| interest       | string | Interest paid                                     |
| refund         | string | Frozen amount in denominated currency             |
| state          | int    | Loan status: 1. Not repaid; 2. Repaid             |

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

| Name       | Mandatory | Type   | Description                                                                                                                                                                   |
| ---------- | --------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| pageno     | Yes       | int    | page number                                                                                                                                                                   |
| pageSize   | Yes       | int    | Display quantity per page (0 <pageSize ≤ 500)                                                                                                                                 |
| currency   | no        | string | Currency type, all bills will be returned if not filled                                                                                                                       |
| ledgerType | no        | int    | Bill type 2 Buy in 3 Buy out 4 Handling fee 5 Loan currency 6 Return interest 7 Return principal 8 System buy 9 System sell 11 Liquidation fee 12 Transfer in 13 Transfer out |
| pairName   | no        | string | Currency pair type, if not filled in, the bill of all currency pairs will be returned                                                                                         |

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

### Response

| Name      | Type   | Description        |
| --------- | ------ | ------------------ |
| ledger_id | string | Bill ID            |
| coinPair  | string | Currency pair      |
| currency  | string | Currency           |
| balance   | string | Balance            |
| amount    | string | Number of changes  |
| typename  | string | Bill type          |
| timestamp | string | Bill creation time |

# Error message

| code   | Description                                                                              |
| ------ | ---------------------------------------------------------------------------------------- |
| 200    | normal                                                                                   |
| 112002 | API single key traffic exceeds limit                                                     |
| 112005 | API request frequency exceeded                                                           |
| 112007 | API-Key creation failed                                                                  |
| 112008 | API-Key remark name already exists                                                       |
| 112009 | The number of API-Key creation exceeds the limit (a single user can create up to 5 APIs) |
| 112010 | API-Key is invalid (the time limit for a single Key is 60 natural days)                  |
| 112011 | API request IP access is restricted (the bound IP is inconsistent with the request IP)   |
| 112015 | Signature error                                                                          |
| 112020 | Wrong signature                                                                          |
| 112021 | Wrong signature version                                                                  |
| 112022 | Signature timestamp error                                                                |
| 112047 | The spot API interface is temporarily inaccessible                                       |
| 112048 | The futures API interface is temporarily inaccessible                                    |
| 230030 | Please operate after KYC certification                                                   |
| 280007 | Query Coin Pair Not Exist                |
| 280014 | Query Side Err: 1-Buy 2-Sell             |
| 280048 | Query LiquidationType Error              |
| 280204 | Query StrategyType Error                 |
| 280044 | Query OrderTypes Error                   |
| 280045 | Query OrderState Error                   |
| 280042 | PageNum Error: should >0                 |
| 280043 | PageSize Error: should between 0 and 500 |

# Common problem

| common problem                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1. What is a trading currency? What is a denominated currency? Is the transaction volume counted in the transaction currency or the denominated currency? Answer: Each transaction currency pair is composed of transaction currency/denominated currency. The front of the currency pair is the transaction currency, and the back is the denominated currency. For example: In the BTC/USDT trading currency pair, BTC is the trading currency and USDT is the quotation currency. The transaction volume is calculated based on the transaction currency. The total transaction amount is calculated based on the denominated currency. |
| 2. Rest access restriction? Answer: 1. A single IP is restricted to 1200 visits per minute. If it exceeds 1200 times, it will be locked for 1 hour, and will be automatically unlocked after one hour. 2. A single user is restricted to 20 visits per second, and more than 20 requests within one second will be considered invalid.                                                                                                                                                                                                                                                                                                     |
| 3. WebSocket access restriction? Answer: A single user is restricted to 50 visits per second, and more than 50 requests in one second will be regarded as invalid.                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| 4. What is the use of the generated key? Answer: The key is the key used to operate the API, and the API key needs to be provided when calling the API interface. The private key is only displayed once when it is just generated, and it needs to be regenerated if it is forgotten.                                                                                                                                                                                                                                                                                                                                                     |
| 5. Can the candlestick chart obtain data from months or one year ago? Answer: The system candlestick chart only provides 1000 pieces of data at most. If you want to obtain longer data, you need to use the unit of hour or day to obtain it.                                                                                                                                                                                                                                                                                                                                                                                             |
| 6. Does the IP of the API need to be bound? Answer: 1. The IP binding of the API effectively prevents servers other than this IP from calling their own authority for transaction operations. 2. After the IP is bound, it can only be accessed by the bound IP. If it is not bound, the access to the IP is not restricted.                                                                                                                                                                                                                                                                                                               |
| 7. Does the API support withdrawals? Answer: No, withdrawals must be made on the FameEX official website.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| 8. Can the public key and private key be provided to others? Answer: It is not recommended, it will cause asset loss.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| 9. Frequent signature failures? • Check whether the API Key is valid, copied correctly, and whether there is a whitelist of bound IP; • Check whether the timestamp is UTC time; • Check whether the parameters are sorted alphabetically; • Check the code; • Check the signature code It should be hex; • Check whether it is submitted in a form ; • Check whether the url has a signature field, and whether the POST data format is json format; • Check whether the signature result is URI-encoded.                                                                                                                                 |
| 10. Return login-required? • Check whether the parameter account-id is returned by the /v1/account/accounts interface instead of the filled UID; • Check whether the request includes the business parameters into the signature; • Check whether the request includes parameters Sort in the order of the ASCII code table.                                                                                                                                                                                                                                                                                                               |
| 11. Return gateway-internal-error? Check whether the request declares Content-Type: application/json in the header.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
