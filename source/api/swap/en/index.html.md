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

## 2022-03-30

- New endpoint for USDT Futures:
  - GET `/swap-api/v2/orderbook` to query order book.
  - GET `/swap-api/v2/tickers` to query 24 hour rolling window price change statistics.
  - POST `/swap-api/v1/margin-mode` to change margin mode

## 2021-05-27

- Futures interface update:
  - Added U futures order interface `/swap-api/v1/order`
  - Added U futures cancellation interface `/swap-api/v1/cancel_order`
  - Added U futures condition cancellation interface `/swap-api/v1/cancel_cond_orders`
  - Added U futures to obtain single currency pair market data interface `/swap-api/v1/ticker`
  - Added U futures to get all currency pair market data interface `/swap-api/v1/tickers`
  - Added U futures to obtain order list interface `/swap-api/v1/orders`
  - Added U futures to obtain order information interface `/swap-api/v1/order_info`
  - Added U futures to obtain transaction details list interface `/swap-api/v1/trades`
  - Added U futures to get the latest transaction details list interface `/swap-api/v1/last_trades`
  - Added U futures to obtain in-depth data interface `/swap-api/v1/depth`
  - Added U futures to obtain K-line/Candlestick data interface `/swap-api/v1/kline`
  - Added U futures to obtain all currency pairs and configuration interface `/swap-api/v1/symbols`
  - Added U futures to obtain futures account asset interface `/swap-api/v1/wallet/asset`
  - Added U futures to obtain futures position interface `/swap-api/v1/wallet/pos`
  - Added U futures adjustment leverage multiple interface `/swap-api/v1/wallet/leverage/adjust`

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

# General Info

## Get current system time

Speed limit rule: 20 times/2s

**Description**

Get the current system time, in seconds

**Request path:**

/v1/common/timestamp

curl `https://api.fameex.com/v1/common/timestamp`

**Routing parameters:**

no

**Post parameters:**

no

> **Return example:**

```json
{
  "code": 200,
  "ts": 1553254857,
  "data": 1553254857
}
```

**Return value:**

| Field Name | Type  | Description                        |
| ---------- | ----- | ---------------------------------- |
| code       | int   | 200, normal                        |
| ts         | int64 | Request time, seconds              |
| data       | int64 | Return value, current time, second |

## Get all currency pairs and configurations

Speed limit rule: 20 times/2s

**Description**

Obtain all currency pairs and configurations of the U futures.

**Request path:**

/swap-api/v1/symbols

curl `https://api.fameex.com/swap-api/v1/symbols`

**Routing parameters:**

no

**Post parameters:**

no

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": [
    {
      "base": "BTC",
      "quote": "USDT",
      "leverMultiple": 20,
      "defaultLeverage": 10,
      "initPrice": "50000",
      "quotePrecision": 2,
      "limitMarketAmount": "0.001",
      "basePrecision": 6,
      "riskRate": "0.1",
      "status": 1,
      "forceLiquidationTime": 0,
      "orderLimitRate": "1",
      "buyMinPricePercent": "0.3",
      "buyMaxPricePercent": "0.05",
      "sellMinPricePercent": "0.05",
      "sellMaxPricePercent": "0.3",
      "interest": "0",
      "limitsA": "-0.00125",
      "limitsB": "0.00125",
      "isEffect": 2,
      "effectTime": 0,
      "marginRateGear": [
        {
          "gear": 1,
          "start": "0",
          "end": "2000",
          "leverMultiple": 20,
          "initRate": "0.05",
          "warnRate": "0.01",
          "maintenanceRate": "0.008"
        },
        {
          "gear": 2,
          "start": "2000",
          "end": "-1",
          "leverMultiple": 19,
          "initRate": "0.0526",
          "warnRate": "0.02",
          "maintenanceRate": "0.015"
        }
      ]
    },
    {
      "base": "BIRD",
      "quote": "USDT",
      "leverMultiple": 20,
      "defaultLeverage": 10,
      "initPrice": "1",
      "quotePrecision": 2,
      "limitMarketAmount": "1",
      "basePrecision": 5,
      "riskRate": "0.1",
      "status": 1,
      "forceLiquidationTime": 0,
      "orderLimitRate": "0.3",
      "buyMinPricePercent": "0.3",
      "buyMaxPricePercent": "0.05",
      "sellMinPricePercent": "0.05",
      "sellMaxPricePercent": "0.3",
      "interest": "1",
      "limitsA": "-0.01",
      "limitsB": "0.02",
      "isEffect": 2,
      "effectTime": 0,
      "marginRateGear": [
        {
          "gear": 1,
          "start": "0",
          "end": "-1",
          "leverMultiple": 20,
          "initRate": "0.05",
          "warnRate": "0.01",
          "maintenanceRate": "0.005"
        }
      ]
    }
  ]
}
```

**Return value:**

| Field Name        | Type         | Description                                        |
| ----------------- | ------------ | -------------------------------------------------- |
| code              | int          | 200, normal                                        |
| msg               | string       | success, normal                                    |
| data              | object array | Return value, contract currency pair configuration |
| base              | string       | Transaction currency                               |
| quote             | string       | Denominated currency                               |
| leverMultiple     | int          | Maximum leverage                                   |
| quotePrecision    | int          | Price display digits                               |
| limitMarketAmount | int          | Minimum number of transactions                     |
| basePrecision     | int          | Number of display digits                           |
| defaultLeverage   | int          | Default leverage                                   |
| riskRate          | string       | Contract risk reserve                              |
| marginRateGear    | object array | Gear information                                   |
| gear              | string       | Gradient gear                                      |
| start             | string       | Starting position of the position                  |
| end               | string       | End of position                                    |
| leverMultiple     | int          | Maximum leverage                                   |
| initRate          | string       | Initial margin rate                                |
| warnRate          | string       | Early warning margin rate                          |
| maintenanceRate   | string       | Maintenance margin rate                            |

# Market Data Endpoints

## Get k-line/Candlestick data

Speed limit rule: 20 times/2s

`Function Description`

This interface obtains historical K-line/Candlestick data.

**Request path:**

/swap-api/v1/kline

curl `https://api.fameex.com/swap-api/v1/kline`

**Routing parameters:**

no

**Post parameters:**

| Name         | Mandatory | Type   | Description                                            |
| ------------ | --------- | ------ | ------------------------------------------------------ |
| contractCode | Yes       | string | Contract code, for example "BTC-USDT"                  |
| period       | Yes       | string | 时间粒度 例（ "1","5","15","30","60","120","240","1D") |
| startTime    | no        | int64  | Start time, timestamp (unit: seconds)                  |
| endTime      | no        | int64  | End time, timestamp (unit: seconds)                    |

> **Return example:**

```json
{
  "code": 200,
  "msg": "ok",
  "data": [
    {
      "time": 1622019900,
      "open": "2851.66",
      "close": "2861.23",
      "high": "2863.5",
      "low": "2850",
      "amount": "671.194",
      "volume": "959418.48168"
    },
    {
      "time": 1622020200,
      "open": "2862.38",
      "close": "2861.39",
      "high": "2866.76",
      "low": "2856.65",
      "amount": "933.28",
      "volume": "1335716.34709"
    },
    {
      "time": 1622020500,
      "open": "2860.22",
      "close": "2869.23",
      "high": "2869.23",
      "low": "2852.38",
      "amount": "661.23",
      "volume": "946152.16526"
    },
    {
      "time": 1622106000,
      "open": "2760.33",
      "close": "2763.04",
      "high": "2769.59",
      "low": "2760.33",
      "amount": "1150.02",
      "volume": "1590741.62857"
    }
  ]
}
```

**Return value:**

| Field Name | Type   | Description                         |
| ---------- | ------ | ----------------------------------- |
| code       | int    | 200, normal                         |
| msg        | string | success, normal                     |
| data       | object | Return value, bar data              |
| time       | int64  | Start timestamp                     |
| open       | string | Opening price                       |
| low        | string | Lowest price                        |
| hight      | string | Highest price                       |
| close      | string | Closing price                       |
| amount     | string | Trading currency volume             |
| volume     | string | Denominated currency trading volume |

## Order Book

**HTTP Request**

GET `/swap-api/v2/orderbook`

> Request

```curl
curl --request GET 'https://api.fameex.com/swap-api/v2/orderbook?symbol=ETH-USDT'
```

> Response

```json
{
  "ticker_id": "ETC-USDT",
  "timestamp": 1648539997000,
  "bids": [
    ["35", "0.7"],
    ["34", "0.1"]
  ],
  "asks": [
    ["36", "0.2"],
    ["37", "0.1"]
  ]
}
```

### Parameters

| Name   | Mandatory | Type   | Description                                 |
| :----- | :-------- | :----- | :------------------------------------------ |
| symbol | YES       | string | Name of the trading pair, example: ETH-USDT |
| limit  | NO        | int    | Default value is 100                        |

### Response

| Name      | Type   | Description                                                            |
| :-------- | :----- | :--------------------------------------------------------------------- |
| ticker_id | string | Name of the trading pair                                               |
| timestamp | int    | Current time, unit in millisecond                                      |
| bids      | string | Bid price and quantity, with best bid prices ranked from top to bottom |
| asks      | string | Ask price and quantity, with best ask prices ranked from top to bottom |

## 24hr Ticker Price Change Statistics

**HTTP Request**

GET `/swap-api/v2/tickers`

> Request

```curl
curl --request GET 'https://api.fameex.com/swap-api/v2/tickers?symbol=ETH-USDT'
```

> Response

```json
[
  {
    "ticker_id": "ETH-USDT",
    "base_currency": "ETH",
    "quote_currency": "USDT",
    "last_price": "3500.7",
    "base_volume": "0.06",
    "quote_volume": "209.042",
    "bid": "3500.7",
    "ask": "3600.7",
    "high": "3500.7",
    "low": "3400.7",
    "product_type": "Perpetual",
    "open_interest": "0.06",
    "index_price": "3407.072",
    "funding_rate": "0.00125",
    "next_funding_rate_timestam": 1648598400000
  }
]
```

### Parameters

| Name   | Mandatory | Type   | Description                                 |
| ------ | --------- | ------ | ------------------------------------------- |
| symbol | NO        | string | Name of the trading pair, example: ETH-USDT |

### Response

| Name                       | Type   | Description                               |
| :------------------------- | :----- | :---------------------------------------- |
| ticker_id                  | string | Name of the trading pair                  |
| base_currency              | string | base                                      |
| quote_currency             | string | quote                                     |
| last_price                 | string | Latest transaction price                  |
| base_volume                | string | Trading volume in the last 24 hours       |
| quote_volume               | string | Trading quote volume in the last 24 hours |
| bid                        | string | Purchase price of the first order         |
| ask                        | string | Selling price of the first order          |
| high                       | string | The highest price in the last 24 hours    |
| low                        | string | Lowest price in the last 24 hours         |
| product_type               | string | futures type                              |
| open_interest              | string | Open interest                             |
| index_price                | string | Index price                               |
| funding_rate               | string | Funding rate                              |
| next_funding_rate_timestam | int    | Next settlement time of capital cost      |

# U futures Exchange Endpoints

## Futures orders

Speed limit rule: 100 times/2s

`Function Description`

This interface provides the U futures order function.

**Request path:**

/swap-api/v1/order

curl `https://api.fameex.com/swap-api/v1/order`

**Routing parameters:**

no

**Post parameters:**

| Name         | Mandatory | Type   | Description                                                                                                                                                |
| ------------ | --------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| leverage     | Yes       | int    | Leverage                                                                                                                                                   |
| marginMode   | Yes       | int    | Margin mode 1-full position 2-position by position                                                                                                         |
| clientOid    | no        | string | User-made order ID                                                                                                                                         |
| side         | Yes       | int    | Order Direction 1-Buy 2-Sell                                                                                                                               |
| offset       | Yes       | int    | Kaiping direction 1-open 2-level                                                                                                                           |
| orderType    | Yes       | int    | Order Type 1-Limit Price 2-Market Price 3-Limit Price Take Profit 4-Market Price Take Profit 5-Limit Price Stop Loss 6-Market Price Stop Loss 7-Maker Only |
| price        | Yes       | string | Commission price                                                                                                                                           |
| amount       | Yes       | string | Number of orders                                                                                                                                           |
| triggerPrice | no        | string | Order unit price                                                                                                                                           |
| workingType  | no        | int    | Conditional price trigger type 1-latest price 2-mark price                                                                                                 |
| closeType    | no        | int    | Types of closing positions 1-ordinary closing 2-quick closing 3-one-click closing 4-system closing                                                         |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "orderId": "10383992916667793408"
}
```

**Return value:**

| Name      | Type   | Description                           |
| --------- | ------ | ------------------------------------- |
| code      | int    | 200, normal                           |
| msg       | string | success, normal                       |
| data      | object | Return information: order information |
| orderId   | string | Order ID                              |
| clientOid | string | User-made order ID                    |

## Futures cancellation

Speed limit rule: 100 times/2s

`Function Description`

This interface provides the function of canceling unfilled orders.

**Request path:**

/swap-api/v1/cancel_order

curl `https://api.fameex.com/swap-api/v1/cancel_order`

**Routing parameters:**

no

**Post parameters:**

| Name         | Mandatory | Type   | Description                                                                        |
| ------------ | --------- | ------ | ---------------------------------------------------------------------------------- |
| orderid      | Yes       | string | Order ID (orderId and clientOid must and can only choose one to fill in)           |
| clientOid    | Yes       | string | User-made order ID (orderId and clientOid must and can only choose one to fill in) |
| contractCode | Yes       | string | Contract code (e.g. BTC-USDT)                                                      |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "orderId": "10383992916667793408"
}
```

**Return value:**

| Field Name | Type   | Description                  |
| ---------- | ------ | ---------------------------- |
| code       | int    | 200, normal                  |
| msg        | string | success, normal              |
| data       | object | Return information: order id |
| orderId    | string | Order ID                     |
| clientOid  | string | User-made order ID           |

## Futures limit cancellation

Speed limit rule: 100 times/2s

`Function Description`

This interface provides the function of canceling uncompleted orders of a specified type.

**Request path:**

/swap-api/v1/cancel_cond_orders

curl `https://api.fameex.com/swap-api/v1/cancel_cond_orders`

**Routing parameters:**

no

**Post parameters:**

| Name         | Mandatory | Type      | Description                                                                                                                                                                            |
| ------------ | --------- | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| contractCode | Yes       | string    | Contract code (e.g. BTC-USDT)                                                                                                                                                          |
| side         | no        | string    | Order Direction 1-Buy 2-Sell                                                                                                                                                           |
| offset       | no        | int       | Kaiping direction 1-open 2-level                                                                                                                                                       |
| orderTypes   | no        | int array | List of Order Types 1-Limit Price 2- Market Price 3- Limit Price Take Profit 4- Market Price Stop Profit 5- Limit Price Stop Loss 6 Market Price Stop Loss 7- Maker Only (eg, [1,2,3]) |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success"
}
```

**Return value:**

| Field Name | Type   | Description     |
| ---------- | ------ | --------------- |
| code       | int    | 200, normal     |
| msg        | string | success, normal |

## Get order information

Speed limit rule: 20 times/2s

`Function Description`

This interface obtains the specified order information through the order ID.

**Request path:**

/swap-api/v1/order_info

curl `https://api.fameex.com/swap-api/v1/order_info`

`Headers parameter`

no

**Routing parameters:**

no

**Post parameters:**

| Name         | Mandatory | Type   | Description                                                                        |
| ------------ | --------- | ------ | ---------------------------------------------------------------------------------- |
| contractCode | Yes       | string | Contract code (e.g. BTC-USDT)                                                      |
| orderId      | no        | string | Order ID (orderId and clientOid must and can only choose one to fill in)           |
| clientOid    | no        | string | User-made order ID (orderId and clientOid must and can only choose one to fill in) |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "contractCode": "BTC-USDT",
    "marginMode": 1,
    "orderId": "10617388945218469888",
    "clientOid": "",
    "side": 2,
    "orderType": 2,
    "offset": 2,
    "price": "0",
    "amount": "0.004",
    "filledAmount": "0.004",
    "filledMoney": "157.5786",
    "filledFee": "0.06303144",
    "feeCurrency": "usdt",
    "triggerPrice": "0",
    "triggerType": "",
    "triggerState": 0,
    "workingType": 0,
    "leverage": 20,
    "liquidationType": 0,
    "state": 4,
    "accountType": "swap",
    "platform": "WEB",
    "cancelType": 0,
    "createTime": 1621999883,
    "updateTime": 1621999883
  }
}
```

**Return value:**

| Field Name      | Type   | Description                                                                                                                                                |
| --------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| code            | int    | 200, normal                                                                                                                                                |
| msg             | string | success, normal                                                                                                                                            |
| data            | object | Return information: Order details                                                                                                                          |
| contractCode    | string | Contract code                                                                                                                                              |
| marginMode      | int    | Margin mode 1-full position 2-position by position                                                                                                         |
| orderId         | string | Order ID                                                                                                                                                   |
| clientOid       | string | User-made order ID                                                                                                                                         |
| side            | int    | Order Direction 1-Buy 2-Sell                                                                                                                               |
| orderType       | int    | Order Type 1-Limit Price 2-Market Price 3-Limit Price Take Profit 4-Market Price Take Profit 5-Limit Price Stop Loss 6-Market Price Stop Loss 7-Maker Only |
| offset          | int    | Kaiping direction 1-open 2-level                                                                                                                           |
| price           | string | Commission price                                                                                                                                           |
| amount          | string | Number of orders                                                                                                                                           |
| filledAmount    | string | Number of transactions                                                                                                                                     |
| filledMoney     | string | Transaction amount                                                                                                                                         |
| filledFee       | string | Transaction fee                                                                                                                                            |
| feeCurrency     | string | Transaction fee currency                                                                                                                                   |
| triggerPrice    | string | Order trigger price                                                                                                                                        |
| triggerType     | string | Order trigger type gte-greater than or equal to lte-less than or equal to                                                                                  |
| triggerState    | int    | Trigger status 1-trigger successful                                                                                                                        |
| workingType     | int    | Conditional price trigger type 1-latest price 2-mark price                                                                                                 |
| leverage        | int    | Leverage                                                                                                                                                   |
| liquidationType | int    | Liquidation type 1- liquidation 2- lighten up 3- take profit lighten up                                                                                    |
| state           | int    | Order Status 1- Created 2- Waiting for Transaction 3- Partially Completed 4- Completely Completed 5- Partially Cancelled 6- Cancelled                      |
| accountType     | string | account type                                                                                                                                               |
| platform        | string | Platform source                                                                                                                                            |
| cancelType      | int    | Order Cancellation Type 1-User Cancellation 2-System Cancellation 3-Operation Cancellation 4-Liquidation Cancellation 5-Lightening Cancellation            |
| closeType       | int64  | Types of closing positions 1-ordinary closing 2-quick closing 3-one-click closing 4-system closing                                                         |
| createTime      | int64  | Creation time                                                                                                                                              |
| updateTime      | int64  | Status update time                                                                                                                                         |

## Get a list of orders

Speed limit rule: 20 times/2s

`Function Description`

This interface obtains and lists your current order information (the order information of the last 3 months). This request supports paging, and is sorted and stored in reverse chronological order, with the latest one at the top.

**Request path:**

/swap-api/v1/orders

curl `https://api.fameex.com/swap-api/v1/orders`

`Headers parameter`

no

**Routing parameters:**

| Name            | Mandatory | Type      | Description                                                                                                                                                                                |
| --------------- | --------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| contractCode    | Yes       | string    | Contract code (e.g. BTC-USDT)                                                                                                                                                              |
| side            | no        | int       | Trading direction: 0 buy, 1 sell, -1 all                                                                                                                                                   |
| offset          | no        | int       | The name of the currency pair (for example: BTC_USDT)                                                                                                                                      |
| closeType       | no        | int       | Types of closing positions 1-ordinary closing 2-quick closing 3-one-click closing 4-system closing                                                                                         |
| liquidationType | no        | int       | Liquidation type 1- liquidation 2- lighten up 3- take profit lighten up                                                                                                                    |
| orderTypes      | no        | int array | List of Order Types 1-Limit Price 2- Market Price 3- Limit Price Take Profit 4- Market Price Stop Profit 5- Limit Price Stop Loss 6 Market Price Stop Loss 7- Maker Only (such as [1,2,3]) |
| state           | Yes       | int       | Order status 7-uncompleted 8-completed 9-completed or partially cancelled                                                                                                                  |
| pageNum         | Yes       | int       | Paging usage, which page                                                                                                                                                                   |
| pageSize        | Yes       | int       | Paging usage, number per page (0 <pageSize ≤ 500)                                                                                                                                          |
| startTime       | no        | int64     | Timestamp, query the start time of the order in seconds                                                                                                                                    |
| endTime         | no        | int64     | Timestamp, query the end time of the order in seconds                                                                                                                                      |

**Post parameters:**

> **Return example:**

```json
{
  "code": 200,
  "msg": "ok",
  "data": {
    "orders": [
      {
        "contractCode": "BTC-USDT",
        "marginMode": 1,
        "orderId": "10617388945218469888",
        "clientOid": "",
        "side": 2,
        "orderType": 2,
        "offset": 2,
        "price": "0",
        "amount": "0.004",
        "filledAmount": "0.004",
        "filledMoney": "157.5786",
        "filledFee": "0.06303144",
        "feeCurrency": "usdt",
        "triggerPrice": "0",
        "triggerType": "",
        "triggerState": 0,
        "workingType": 0,
        "leverage": 20,
        "liquidationType": 0,
        "state": 4,
        "accountType": "swap",
        "platform": "WEB",
        "cancelType": 0,
        "createTime": 1621999883,
        "updateTime": 1621999883
      },
      {
        "contractCode": "BTC-USDT",
        "marginMode": 1,
        "orderId": "10613096118414213120",
        "clientOid": "",
        "side": 1,
        "orderType": 1,
        "offset": 1,
        "price": "49630",
        "amount": "0.003",
        "filledAmount": "0",
        "filledMoney": "0",
        "filledFee": "0",
        "feeCurrency": "usdt",
        "triggerPrice": "0",
        "triggerType": "",
        "triggerState": 0,
        "workingType": 0,
        "leverage": 25,
        "liquidationType": 0,
        "state": 6,
        "accountType": "swap",
        "platform": "WEB",
        "cancelType": 1,
        "createTime": 1620976393,
        "updateTime": 1620979562
      }
    ],
    "pageNum": 1,
    "pageSize": 50,
    "total": 44
  }
}
```

no

**Return value:**

| Field Name      | Type         | Description                                                                                                                                                |
| --------------- | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| code            | int          | 200, normal                                                                                                                                                |
| msg             | string       | success, normal                                                                                                                                            |
| data            | object       | Return information: Order                                                                                                                                  |
| pageno          | int          | Pagination, the first few pages (1<=pageNum)                                                                                                               |
| pageSize        | int          | Pagination, the number of pages (1<=pageSize<= 500)                                                                                                        |
| total           | int64        | Total number                                                                                                                                               |
| orders          | object array | Order list                                                                                                                                                 |
| contractCode    | string       | Contract code                                                                                                                                              |
| marginMode      | int          | Margin mode 1-full position 2-position by position                                                                                                         |
| orderId         | string       | Order ID                                                                                                                                                   |
| clientOid       | string       | User-made order ID                                                                                                                                         |
| side            | int          | Order Direction 1-Buy 2-Sell                                                                                                                               |
| orderType       | int          | Order Type 1-Limit Price 2-Market Price 3-Limit Price Take Profit 4-Market Price Take Profit 5-Limit Price Stop Loss 6-Market Price Stop Loss 7-Maker Only |
| offset          | int          | Kaiping direction 1-open 2-level                                                                                                                           |
| price           | string       | Commission price                                                                                                                                           |
| amount          | string       | Number of orders                                                                                                                                           |
| filledAmount    | string       | Number of transactions                                                                                                                                     |
| filledMoney     | string       | Transaction amount                                                                                                                                         |
| filledFee       | string       | Transaction fee                                                                                                                                            |
| feeCurrency     | string       | Transaction fee currency                                                                                                                                   |
| triggerPrice    | string       | Order trigger price                                                                                                                                        |
| triggerType     | string       | Order trigger type gte-greater than or equal to lte-less than or equal to                                                                                  |
| triggerState    | int          | Trigger status 1-trigger successful                                                                                                                        |
| workingType     | int          | Conditional price trigger type 1-latest price 2-mark price                                                                                                 |
| leverage        | int          | Leverage                                                                                                                                                   |
| liquidationType | int          | Liquidation type 1- liquidation 2- lighten up 3- take profit lighten up                                                                                    |
| state           | int          | Order Status 1- Created 2- Waiting for Transaction 3- Partially Completed 4- Completely Completed 5- Partially Cancelled 6- Cancelled                      |
| accountType     | string       | account type                                                                                                                                               |
| platform        | string       | Platform source                                                                                                                                            |
| cancelType      | int          | Order Cancellation Type 1-User Cancellation 2-System Cancellation 3-Operation Cancellation 4-Liquidation Cancellation 5-Lightening Cancellation            |
| closeType       | int64        | Types of closing positions 1-ordinary closing 2-quick closing 3-one-click closing 4-system closing                                                         |
| createTime      | int64        | Creation time                                                                                                                                              |
| updateTime      | int64        | Status update time                                                                                                                                         |

## Get transaction details

Speed limit rule: 20 times/2s

`Function Description`

This interface gets all your current transaction order information. This request supports paging, and is sorted and stored in reverse chronological order, with the latest one at the top.

**Request path:**

/swap-api/v1/trades

curl `https://api.fameex.com/swap-api/v1/trades`

**Routing parameters:**

no

**Post parameters:**

| Name            | Mandatory | Type      | Description                                                                                                                                                                                |
| --------------- | --------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| contractCode    | no        | string    | Contract code (e.g. BTC-USDT)                                                                                                                                                              |
| orderId         | no        | string    | Order ID                                                                                                                                                                                   |
| side            | no        | int       | Order Direction 1-Buy 2-Sell                                                                                                                                                               |
| offset          | no        | int       | Kaiping direction 1-open 2-level                                                                                                                                                           |
| closeType       | no        | int       | Types of closing positions 1-ordinary closing 2-quick closing 3-one-click closing 4-system closing                                                                                         |
| liquidationType | no        | int       | Liquidation type 1- liquidation 2- lighten up 3- take profit lighten up                                                                                                                    |
| orderTypes      | no        | int array | List of Order Types 1-Limit Price 2- Market Price 3- Limit Price Take Profit 4- Market Price Stop Profit 5- Limit Price Stop Loss 6 Market Price Stop Loss 7- Maker Only (such as [1,2,3]) |
| pageno          | Yes       | int       | Pagination use, the first few pages, starting from the first page                                                                                                                          |
| pageSize        | Yes       | int       | Paging usage, number per page (0 <pageSize ≤ 500)                                                                                                                                          |
| startTime       | no        | int64     | Start timestamp, seconds                                                                                                                                                                   |
| endTime         | no        | int64     | End timestamp, seconds                                                                                                                                                                     |

> **Return example:**

```json
{
  "code": 200,
  "msg": "ok",
  "data": {
    "pageNum": 1,
    "pageSize": 50,
    "total": 24,
    "trades": [
      {
        "contractCode": "BTC-USDT",
        "tradeId": "10617388945239465984",
        "orderId": "10617388945218469888",
        "side": 2,
        "orderType": 2,
        "offset": 2,
        "price": "39394.65",
        "amount": "0.004",
        "feeCurrency": "usdt",
        "feeRate": "0.0004",
        "fee": "0.06303144",
        "profitReal": "0.16321",
        "liquidationType": 0,
        "accountType": "swap",
        "platform": "WEB",
        "role": 2,
        "selfTrade": 0,
        "createTime": 1621999883
      },
      {
        "contractCode": "BTC-USDT",
        "tradeId": "10613109942471122944",
        "orderId": "10613109942445932544",
        "side": 1,
        "orderType": 1,
        "offset": 1,
        "price": "50162.33",
        "amount": "0.002",
        "feeCurrency": "usdt",
        "feeRate": "0.0004",
        "fee": "0.04012987",
        "profitReal": "0",
        "liquidationType": 0,
        "accountType": "swap",
        "platform": "WEB",
        "role": 2,
        "selfTrade": 0,
        "createTime": 1620979689
      }
    ]
  }
}
```

**Return value:**

| Field Name      | Type   | Description                                                                                                                                                |
| --------------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| code            | int    | 200, normal                                                                                                                                                |
| msg             | string | success, normal                                                                                                                                            |
| data            | string | Return value, transaction details                                                                                                                          |
| pageno          | int    | Pagination, the first few pages (1<=pageNum)                                                                                                               |
| pageSize        | int    | Pagination, the number of pages (1<=pageSize<= 500)                                                                                                        |
| total           | int64  | Total number                                                                                                                                               |
| contractCode    | string | Contract code                                                                                                                                              |
| tradeId         | string | Order ID                                                                                                                                                   |
| orderId         | string | Order ID                                                                                                                                                   |
| userId          | string | User ID                                                                                                                                                    |
| side            | int    | Order Direction 1-Buy 2-Sell                                                                                                                               |
| orderType       | int    | Order Type 1-Limit Price 2-Market Price 3-Limit Price Take Profit 4-Market Price Take Profit 5-Limit Price Stop Loss 6-Market Price Stop Loss 7-Maker Only |
| offset          | int    | Kaiping direction 1-open 2-level                                                                                                                           |
| price           | string | the deal price                                                                                                                                             |
| amount          | string | The number of transactions                                                                                                                                 |
| feeCurrency     | string | Transaction fee currency                                                                                                                                   |
| feeRate         | string | Actual handling fee rate                                                                                                                                   |
| fee             | string | Handling fee                                                                                                                                               |
| profitReal      | string | Realized profit and loss                                                                                                                                   |
| liquidationType | int    | Liquidation type 1- liquidation 2- lighten up 3- take profit lighten up                                                                                    |
| accountType     | string | account type                                                                                                                                               |
| platform        | string | Platform source                                                                                                                                            |
| role            | int    | Character type 1-maker 2-taker                                                                                                                             |
| selftrade       | int    | Whether self-deal 1-self-deal                                                                                                                              |
| closeType       | int    | Types of closing positions 1-ordinary closing 2-quick closing 3-one-click closing 4-system closing                                                         |
| createTime      | int64  | Creation time                                                                                                                                              |

## Get the latest transaction details

Speed limit rule: 20 times/2s

`Function Description`

This interface gets you to get the information of the most recently traded order.

**Request path:**

/swap-api/v1/last_trades

curl `https://api.fameex.com/swap-api/v1/last_trades`

**Routing parameters:**

no

**Post parameters:**

| Name         | Mandatory | Type   | Description                                                |
| ------------ | --------- | ------ | ---------------------------------------------------------- |
| contractCode | Yes       | string | Contract code, for example "BTC-USDT"                      |
| accountType  | Yes       | string | Account type, "swap"                                       |
| size         | Yes       | int    | The number of returned transaction details (1<=size<= 100) |

> **Return example:**

```json
{
  "code": 200,
  "msg": "success",
  "data": [
    {
      "tradeId": "10385145101749346304",
      "side": "1",
      "price": "0.5",
      "amount": "1",
      "createTime": 1566628635
    }
  ]
}
```

**Return value:**

| Field Name | Type   | Description                              |
| ---------- | ------ | ---------------------------------------- |
| code       | int    | 200, normal                              |
| msg        | string | success, normal                          |
| data       | object | Return value, recent transaction details |
| tradeId    | string | Order ID                                 |
| side       | int    | Order Direction 1-Buy 2-Sell             |
| price      | string | the deal price                           |
| amount     | string | The number of transactions               |
| createTime | int64  | Creation time                            |

## Adjust leverage

Speed limit rule: 20 times/2s

`Function Description`

This interface adjusts the futures leverage.

**Request path:**

/swap-api/v1/wallet/leverage/adjust

curl `https://api.fameex.com/swap-api/v1/wallet/leverage/adjust`

**Routing parameters:**

no

**Post parameters:**

| Name         | Mandatory | Type   | Description                                   |
| ------------ | --------- | ------ | --------------------------------------------- |
| contractCode | Yes       | string | Contract code, for example "BTC-USDT"         |
| leverage     | Yes       | int    | Leverage                                      |
| marginMode   | Yes       | string | Position type 1: Full position 2: By position |

> **Return example:**

```json
{
  "code": 200,
  "data": {
    "userId": "32102739",
    "contractCode": "BTC-USDT",
    "leverage": 5
  },
  "msg": "success"
}
```

**Return value:**

| Field Name   | Type   | Description     |
| ------------ | ------ | --------------- |
| code         | int    | 200, normal     |
| msg          | string | success, normal |
| data         | object | return value    |
| userid       | string | User id         |
| contractCode | string | Contract code   |
| leverage     | int    | Leverage        |

## Change Margin Mode (TRADE)

### HTTP Request

POST `/swap-api/v1/margin-mode`

### Parameters

| Name       | Mandatory | Type   | Description                        |
| ---------- | --------- | ------ | ---------------------------------- |
| symbol     | Yes       | string | For example "BTC-USDT"             |
| marginMode | Yes       | int    | margin mode 1: CROSSED 2: ISOLATED |

> Response

```json
{
  "code": 200,
  "data": {
    "userId": "32102739",
    "contractCode": "BTC-USDT",
    "marginMode": 2
  },
  "msg": "success"
}
```

### Response

| Field Name | Type   | Description   |
| ---------- | ------ | ------------- |
| userid     | string | User id       |
| symbol     | string | Contract code |
| marginMode | int    | Margin mode   |

# U futures wallet API Endpoints

## Get futures wallet

Speed limit rule: 20 times/2s

`Function Description`

This interface obtains wallet futures account data.

**Request path:**

/swap-api/v1/wallet/asset

curl `https://api.fameex.com/swap-api/v1/wallet/asset`

**Routing parameters:**

no

**Post parameters:**

no

> **Return example:**

```json
{
  "code": 200,
  "data": {
    "userId": "31090571",
    "balance": "26.97550799",
    "valuation": "0",
    "btcValuation": "0",
    "marginBalance": "0",
    "available": "0",
    "totalFrozen": "0",
    "frozenList": [
      {
        "contractCode": "BTC-USDT",
        "posSide": 1,
        "frozen": "0"
      },
      {
        "contractCode": "BTC-USDT",
        "posSide": 2,
        "frozen": "0"
      },
      {
        "contractCode": "ETH-USDT",
        "posSide": 1,
        "frozen": "0"
      },
      {
        "contractCode": "ETH-USDT",
        "posSide": 2,
        "frozen": "0"
      }
    ]
  },
  "msg": "success"
}
```

**Return value:**

| Field Name    | Type         | Description                                           |
| ------------- | ------------ | ----------------------------------------------------- |
| code          | int          | 200, normal                                           |
| msg           | string       | success, normal                                       |
| data          | object       | Return value, contract account data                   |
| available     | string       | Available                                             |
| balance       | string       | Account Balance                                       |
| userid        | string       | User id                                               |
| valuation     | string       | The margin balance is converted into other            |
| btcValuation  | string       | Margin balance is equivalent to BTC                   |
| totalFrozen   | string       | Freeze all                                            |
| marginBalance | string       | Margin balance                                        |
| frozenList    | object array | Return position information                           |
| contractCode  | string       | Contract code                                         |
| frozen        | string       | freeze                                                |
| get           | int          | Position direction 1: Long position 2: Short position |

## Get futures positions

Speed limit rule: 20 times/2s

`Function Description`

This interface obtains the user's futures account position.

**Request path:**

/swap-api/v1/wallet/pos

curl `https://api.fameex.com/swap-api/v1/wallet/pos`

**Routing parameters:**

no

**Post parameters:**

| Name         | Mandatory | Type   | Description                           |
| ------------ | --------- | ------ | ------------------------------------- |
| contractCode | Yes       | string | Contract code, for example "BTC-USDT" |

> **Return example:**

```json
{
  "code": 200,
  "data": [
    {
      "currency": "USDT",
      "isolatedMargin": "0",
      "leverage": 10,
      "liquidation": "0",
      "marginMode": 1,
      "openPriceAvg": "2",
      "openTime": 1616663132,
      "pos": "25",
      "posAvailable": "25",
      "posSide": 1,
      "posValue": "0",
      "profitReal": "0",
      "profitUnreal": "-50",
      "rivalScore": "0",
      "contractCode": "OMG-USDT",
      "userId": "99213512"
    }
  ],
  "msg": "success"
}
```

**Return value:**

| Field Name     | Type         | Description                                                                                                                                       |
| -------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| code           | int          | 200, normal                                                                                                                                       |
| msg            | string       | success, normal                                                                                                                                   |
| data           | object       | Return value, contract account data                                                                                                               |
| currency       | string       | Asset currency                                                                                                                                    |
| isolatedMargin | string       | Margin for each position (full position margin needs to be calculated by the front end (real-time change): (MarkPrice\*Pos)/Leverage = [rounded]) |
| leverage       | int          | Leverage                                                                                                                                          |
| liquidation    | string       | Estimated Strong Parity                                                                                                                           |
| marginMode     | int          | Position type 1: Full position 2: By position                                                                                                     |
| openPriceAvg   | string       | Average opening price                                                                                                                             |
| openTime       | int64        | Position opening time, second-level timestamp                                                                                                     |
| post           | object array | Return position information                                                                                                                       |
| posAvailable   | string       | Closeable position                                                                                                                                |
| get            | int          | Position direction (1: long position 2: short position)                                                                                           |
| posValue       | string       | Position value                                                                                                                                    |
| profitReal     | string       | Total realized profit and loss                                                                                                                    |
| profitUnreal   | string       | Unrealized profit and loss                                                                                                                        |
| rivalScore     | string       | Counterparty Lighten Up Index                                                                                                                     |
| contractCode   | string       | Contract code                                                                                                                                     |
| userId         | string       | User ID                                                                                                                                           |

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

# common problem

| common problem                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1. What is a trading currency? What is a denominated currency? Is the transaction volume counted in the transaction currency or the denominated currency? Answer: Each transaction currency pair is composed of transaction currency/denominated currency. The front of the currency pair is the transaction currency, and the back is the denominated currency. For example: In the BTC/USDT trading currency pair, BTC is the trading currency and USDT is the quotation currency. The transaction volume is calculated based on the transaction currency. The total transaction amount is calculated based on the denominated currency. |
| 2. Rest access restriction? Answer: 1. A single IP is restricted to 1200 visits per minute. If it exceeds 1200 times, it will be locked for 1 hour, and will be automatically unlocked after one hour. 2. A single user is restricted to 20 visits per second, and more than 20 requests within one second will be considered invalid.                                                                                                                                                                                                                                                                                                     |
| 3. WebSocket access restriction? Answer: A single user is restricted to 50 visits per second, and more than 50 requests in one second will be regarded as invalid.                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| 4. What is the use of the generated key? Answer: The key is the key used to operate the API, and the API key needs to be provided when calling the API interface. The private key is only displayed once when it is just generated, and it needs to be regenerated if it is forgotten.                                                                                                                                                                                                                                                                                                                                                     |
| 5. Can the candlestick chart obtain data from months or one year ago? Answer: The system candlestick chart only provides 1000 pieces of data at most. If you want to obtain longer data, you need to use the unit of hour or day to obtain it.                                                                                                                                                                                                                                                                                                                                                                                             |
| 6. Does the IP of the API need to be bound? Answer: 1. The IP binding of the API effectively prevents servers other than this IP from calling their own authority for transaction operations. 2. After the IP is bound, it can only be accessed by the bound IP. If it is not bound, the access to the IP is not restricted.                                                                                                                                                                                                                                                                                                               |
| 7. Can the public key and private key be provided to others? Answer: It is not recommended, it will cause asset loss.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| 8. Signature fail frequently? • Check API Key is valid, whether the copy is correct, if there are binding IP whitelist; • Check the time stamp is UTC time; • Check whether the parameters are sorted alphabetically; • Check encoder; • checks the signature coding It should be hex; • Check whether it is submitted in a form ; • Check whether the url has a signature field, and whether the POST data format is json format; • Check whether the signature result is URI-encoded.                                                                                                                                                    |
| 9. Return login-required? • Check whether the parameter account-id is returned by the /v1/account/accounts interface instead of the filled UID; • Check whether the request includes business parameters into the signature; • Check whether the request includes parameters Sort in the order of the ASCII code table.                                                                                                                                                                                                                                                                                                                    |
| 10. Return gateway-internal-error? Check whether the request declares Content-Type: application/json in the header.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
