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

# 更新日志

## 2022-03-30

- 新增合约接口：
  - GET `/swap-api/v2/orderbook` 获取深度信息
  - GET `/swap-api/v2/tickers` 获取 24 小时滚动窗口价格变动数据

## 2021-05-27

- 新增合约接口：
  - 新增 U 合约下单接口 `/swap-api/v1/order`
  - 新增 U 合约撤单接口 `/swap-api/v1/cancel_order`
  - 新增 U 合约条件撤单接口 `/swap-api/v1/cancel_cond_orders`
  - 新增 U 合约获取单币对行情数据接口 `/swap-api/v1/ticker`
  - 新增 U 合约获取所有币对行情数据接口 `/swap-api/v1/tickers`
  - 新增 U 合约获取委托单列表接口 `/swap-api/v1/orders`
  - 新增 U 合约获取委托单信息接口 `/swap-api/v1/order_info`
  - 新增 U 合约获取成交明细列表接口 `/swap-api/v1/trades`
  - 新增 U 合约获取最近成交明细列表接口 `/swap-api/v1/last_trades`
  - 新增 U 合约获取深度数据接口 `/swap-api/v1/depth`
  - 新增 U 合约获取 K 线数据接口 `/swap-api/v1/kline`
  - 新增 U 合约获取所有币对及配置接口 `/swap-api/v1/symbols`
  - 新增 U 合约获取合约账户资产接口 `/swap-api/v1/wallet/asset`
  - 新增 U 合约获取合约持仓接口 `/swap-api/v1/wallet/pos`
  - 新增 U 合约调整杠杆倍数接口 `/swap-api/v1/wallet/leverage/adjust`

# 简介

API 概述

FameEX 为您提供了一套简单又强大的 API 接口，帮助您快速、高效的获取行情和进行交易。

使用 API 前，请先创建您个人的 API，获取您的 AccessKey 和 SecretKey，并设置 API 的 IP 访问限制。

API 的交易权限让您可以快速的获取当前市场最新行情及时的下单交易、查询自己可用和冻结金额、查询自己当前尚未成交的挂单、买进或卖出、撤单。

FameEX 官网首页： www.fameex.com <br><br>

如果在使用过程中有任何问题，请联系 FameEX 官方客服，

我们的联系方式如下：

官方客服邮箱：Service@mail.fameex.info

官方微博：[https://weibo.com/fameexgroup](https://weibo.com/fameexgroup)

官方 Twitter：[https://twitter.com/FAMEEXGLOBAL](https://twitter.com/FAMEEXGLOBAL)

官方 Telegram：[https://t.me/fameexgroup](https://t.me/fameexgroup)

官方 Facebook：[https://www.facebook.com/FAMEEXGLOBAL](https://www.facebook.com/FAMEEXGLOBAL)

我们将为您做出最权威的解答。

# 接入说明

## 接入 URLs

| 接入 URLs                 | 备注                   |
| ------------------------- | ---------------------- |
| `https://api.fameex.com`  | RESTFUL API            |
| `wss://www.fameex.com/ws` | WebSocket Feed（行情） |

所有请求基于 Https 协议，POST 请求的请求头信息中 contentType 需要统一设置为:’application/json’

鉴于延迟高和稳定性差等原因，不建议通过代理的方式访问 FameEX- API。

## 限频规则

**限制频率：**每个接口的限制不同 。

单个 API Key 维度限制，建议行情 API 访问也要加上签名，否则限频会更严格。

| 限频规则                               | 数据类型               | 备注 |
| -------------------------------------- | ---------------------- | ---- |
| 对每个 AccessKey 及每个 url 的频率限制 | 20 次/2s（大部分接口） | 无   |

## 请求头设置

请求头(header)的参数如下：

| 参数             | 数据类型 | 备注                       |
| ---------------- | -------- | -------------------------- |
| AccessKey        | string   | 您申请的 Accesskey         |
| SignatureMethod  | string   | HmacSHA256                 |
| SignatureVersion | string   | v1.0                       |
| Timestamp        | int64    | 请求时间的时间戳; 单位: 秒 |
| Signature        | string   | 签名                       |
| Content-Type     | string   | application/json           |

请求头(header)的参数解释：

**API 访问密钥（AccessKey）：**您申请的 API 的 AccessKey。

**签名方法（SignatureMethod）：**用户计算签名的基于哈希的协议，此处使用 HmacSHA256。

**签名版本（SignatureVersion）：**签名协议的版本，此处使用 v1.0。

**时间戳（Timestamp）：**您发出请求的时间。 如：2019-07-24 00:00:00 对应时间戳 1563897600。在查询请求中包含此值有助于防止第三方截取您的请求。

**签名（Signature）：**签名计算得出的值，用于确保签名有效和未被篡改。

## 签名

1、签名说明

API 请求在通过 internet 传输的过程中极有可能被篡改，为了确保请求未被更改，除推送服务接口外的私有接口均必须使用您的 API 的 AccessKey 和 SecretKey 做签名认证，以校验参数或参数值在传输途中是否发生了更改。

方法请求地址：即访问服务器地址 api.fameex.com，比如 api.fameex.com/v1/order/orders

**API Key 包含以下两部分：**

AccessKey：API 访问密钥

SecretKey： 签名认证加密所使用的密钥（仅申请时可见）

`Signature`是对`timestamp（单位 秒） + method（GET或POST） + requestPath + body`字符串(+表示字符串连接)拼接的字符串，使用 secretKey，按照 HMAC SHA256 方法加密，通过 hex 编码输出而得到的。

其中，`timestamp`的值与请求头的`Timestamp`相同，必须是 UTC 时区 Unix 时间戳的十进制秒数格式或 ISO8601 标准的时间格式，精确到秒

method 是请求方法，字母全部大写：`GET/POST`。

requestPath 是请求接口路径。例如：`/orders?state=1&type=2`

body 是指请求主体的字符串(去掉空白字符，如\n,\r,\t)，如果请求没有主体(通常为 GET 请求)则 body 可省略。例如：`{"orderId":"377454671037440"}`

secretKey 为用户申请 API Key 时所生成。例如：533d6e70-21b2-eb5c-f801-c128021c70a1

# 基础 API 接口

## 获取当前系统时间

限速规则：20 次/2s

`说明`

获取当前系统时间，单位秒

**请求路径：**

/v1/common/timestamp

curl `https://api.fameex.com/v1/common/timestamp`

**路由参数：**

无

**Post 参数：**

无

> **返回示例：**

```json
{
  "code": 200,
  "ts": 1553254857,
  "data": 1553254857
}
```

**返回值：**

| 字段名称 | 数据类型 | 备注                |
| -------- | -------- | ------------------- |
| code     | int      | 200, 正常           |
| ts       | int64    | 请求时间, 秒        |
| data     | int64    | 返回值,当前时间, 秒 |

## 获取所有的币对及配置

限速规则：20 次/2s

`说明`

获取 U 合约所有的币对及配置。

**请求路径：**

/swap-api/v1/symbols

curl `https://api.fameex.com/swap-api/v1/symbols`

**路由参数：**

无

**Post 参数：**

无

> **返回示例：**

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

**返回值：**

| 字段名称          | 数据类型     | 备注                |
| ----------------- | ------------ | ------------------- |
| code              | int          | 200, 正常           |
| msg               | string       | success,正常        |
| data              | object array | 返回值,合约币对配置 |
| base              | string       | 交易币              |
| quote             | string       | 计价币              |
| leverMultiple     | int          | 最大杠杆倍数        |
| quotePrecision    | int          | 价格显示位数        |
| limitMarketAmount | int          | 最小交易数量        |
| basePrecision     | int          | 数量显示位数        |
| defaultLeverage   | int          | 默认杠杆倍数        |
| riskRate          | string       | 合约风险准备金      |
| marginRateGear    | object array | 档位信息            |
| gear              | string       | 梯度档位            |
| start             | string       | 持仓仓位起点        |
| end               | string       | 持仓仓位终点        |
| leverMultiple     | int          | 最大杠杆倍数        |
| initRate          | string       | 初始保证金率        |
| warnRate          | string       | 预警保证金率        |
| maintenanceRate   | string       | 维持保证金率        |

# 行情接口

## 获取 k 线数据

限速规则：20 次/2s

**功能说明：**

此接口获取历史 K 线数据。

**请求路径：**

/swap-api/v1/kline

curl `https://api.fameex.com/swap-api/v1/kline`

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型 | 备注                                                   |
| ------------ | -------- | -------- | ------------------------------------------------------ |
| contractCode | 是       | string   | 合约代码, 例"BTC-USDT"                                 |
| period       | 是       | string   | 时间粒度 例（ "1","5","15","30","60","120","240","1D") |
| startTime    | 否       | int64    | 开始时间，时间戳（单位:秒）                            |
| endTime      | 否       | int64    | 结束时间，时间戳（单位:秒）                            |

> **返回示例：**

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

**返回值：**

| 字段名称 | 数据类型 | 备注            |
| -------- | -------- | --------------- |
| code     | int      | 200，正常       |
| msg      | string   | success,正常    |
| data     | object   | 返回值,k 线数据 |
| time     | int64    | 开始时间戳      |
| open     | string   | 开盘价          |
| low      | string   | 最低价          |
| hight    | string   | 最高价          |
| close    | string   | 收盘价          |
| amount   | string   | 交易币成交量    |
| volume   | string   | 计价币成交量    |

## 深度信息

> 请求示例

```curl
curl --request GET 'https://api.fameex.com/swap-api/v2/orderbook?symbol=BTC-USDT'
```

> 响应

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

### HTTP 请求

GET `/swap-api/v2/orderbook`

### 请求参数

| 参数   | 是否必须 | 数据类型 | 说明                        |
| ------ | -------- | -------- | --------------------------- |
| symbol | YES      | string   | 示例例: "BTC-USDT"          |
| limit  | NO       | int      | 可选值:[5, 10, 20, 50, 100] |

### 响应参数

| 参数      | 数据类型 | 说明                                            |
| :-------- | :------- | :---------------------------------------------- |
| ticker_id | string   | 币对名称                                        |
| timestamp | int      | 当前时间                                        |
| bids      | string   | bid 的价格和數量信息，最优 bid 价格由上到下排列 |
| asks      | string   | ask 的价格和數量信息，最优 ask 价格由上到下排列 |

## 24hr 价格变动情况

> 请求示例

```curl
curl --request GET 'https://api.fameex.com/swap-api/v2/tickers?symbol=ETH-USDT'
```

> 响应

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

### HTTP 请求

GET `/swap-api/v2/tickers`

### 请求参数

| 参数   | 是否必须 | 数据类型 | 说明             |
| ------ | -------- | -------- | ---------------- |
| symbol | NO       | string   | 示例: "ETH-USDT" |

### 响应参数

| 参数                       | 数据类型 | 说明                 |
| :------------------------- | :------- | :------------------- |
| ticker_id                  | string   | 币对名称             |
| base_currency              | string   | 交易币               |
| quote_currency             | string   | 计价币               |
| last_price                 | string   | 最新成交价           |
| base_volume                | string   | 成交量               |
| quote_volume               | string   | 成交额               |
| bid                        | string   | 最优买价             |
| ask                        | string   | 最优卖价             |
| high                       | string   | 24 小时最高价        |
| low                        | string   | 24 小时最低价        |
| product_type               | string   | 合约类型             |
| open_interest              | string   | 未平仓合约数量       |
| index_price                | string   | 指数价格             |
| funding_rate               | string   | 资金费率             |
| next_funding_rate_timestam | int      | 下次结算资金费用时间 |

# U 合约交易 API 接口

## 合约下单

限速规则：100 次/2s

**功能说明：**

此接口提供 U 合约下单功能。

**请求路径：**

/swap-api/v1/order

curl `https://api.fameex.com/swap-api/v1/order`

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型 | 备注                                                                            |
| ------------ | -------- | -------- | ------------------------------------------------------------------------------- |
| leverage     | 是       | int      | 杠杆倍数                                                                        |
| contractCode | 是       | string   | 合约代码(如 BTC-USDT)                                                           |
| marginMode   | 是       | int      | 保证金模式 1-全仓 2-逐仓                                                        |
| clientOid    | 否       | string   | 用户自编委托单 ID                                                               |
| side         | 是       | int      | 委托方向 1-买 2-卖                                                              |
| offset       | 是       | int      | 开平方向 1-开 2-平                                                              |
| orderType    | 是       | int      | 委托类型 1-限价 2-市价 3-限价止盈 4-市价止盈 5-限价止损 6-市价止损 7-只做 Maker |
| price        | 是       | string   | 委托价格                                                                        |
| amount       | 是       | string   | 委托数量                                                                        |
| triggerPrice | 否       | string   | 下单单价                                                                        |
| workingType  | 否       | int      | 条件价格触发类型 1-最新价格 2-标记价格                                          |
| closeType    | 否       | int      | 平仓类型 1-普通平仓 2-快速平仓 3-一键平仓 4-系统平仓                            |

> **返回示例：**

```json
{
  "code": 200,
  "msg": "success",
  "orderId": "10383992916667793408"
}
```

**返回值：**

| 字段名称  | 数据类型 | 备注                 |
| --------- | -------- | -------------------- |
| code      | int      | 200, 正常            |
| msg       | string   | success,正常         |
| data      | object   | 返回信息：委托单信息 |
| orderId   | string   | 委托单 ID            |
| clientOid | string   | 用户自编委托单 ID    |

## 合约撤单

限速规则：100 次/2s

**功能说明：**

此接口提供将未成交的订单撤销的功能。

**请求路径：**

/swap-api/v1/cancel_order

curl `https://api.fameex.com/swap-api/v1/cancel_order`

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型 | 备注                                                         |
| ------------ | -------- | -------- | ------------------------------------------------------------ |
| orderid      | 是       | string   | 委托单 ID(orderId 和 clientOid 必须且只能选一个填写)         |
| clientOid    | 是       | string   | 用户自编委托单 ID(orderId 和 clientOid 必须且只能选一个填写) |
| contractCode | 是       | string   | 合约代码(如 BTC-USDT)                                        |

> **返回示例：**

```json
{
  "code": 200,
  "msg": "success",
  "orderId": "10383992916667793408"
}
```

**返回值：**

| 字段名称  | 数据类型 | 备注                |
| --------- | -------- | ------------------- |
| code      | int      | 200, 正常           |
| msg       | string   | success，正常       |
| data      | object   | 返回信息：委托单 id |
| orderId   | string   | 委托单 ID           |
| clientOid | string   | 用户自编委托单 ID   |

## 合约条件撤单

限速规则：100 次/2s

**功能说明：**

此接口提供将未成交的指定类型的订单撤销的功能。

**请求路径：**

/swap-api/v1/cancel_cond_orders

curl `https://api.fameex.com/swap-api/v1/cancel_cond_orders`

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型  | 备注                                                                                                |
| ------------ | -------- | --------- | --------------------------------------------------------------------------------------------------- |
| contractCode | 是       | string    | 合约代码(如 BTC-USDT)                                                                               |
| side         | 否       | string    | 委托方向 1-买 2-卖                                                                                  |
| offset       | 否       | int       | 开平方向 1-开 2-平                                                                                  |
| orderTypes   | 否       | int array | 委托类型列表 1-限价 2-市价 3-限价止盈 4-市价止盈 5-限价止损 6-市价止损 7-只做 Maker （如，[1,2,3]） |

> **返回示例：**

```json
{
  "code": 200,
  "msg": "success"
}
```

**返回值：**

| 字段名称 | 数据类型 | 备注          |
| -------- | -------- | ------------- |
| code     | int      | 200, 正常     |
| msg      | string   | success，正常 |

## 获取委托单信息

限速规则：20 次/2s

**功能说明：**

此接口通过订单 ID 获取指定委托单信息。

**请求路径：**

/swap-api/v1/order_info

curl `https://api.fameex.com/swap-api/v1/order_info`

`headers参数`

无

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型 | 备注                                                         |
| ------------ | -------- | -------- | ------------------------------------------------------------ |
| contractCode | 是       | string   | 合约代码(如 BTC-USDT)                                        |
| orderId      | 否       | string   | 委托单 ID(orderId 和 clientOid 必须且只能选一个填写)         |
| clientOid    | 否       | string   | 用户自编委托单 ID(orderId 和 clientOid 必须且只能选一个填写) |

> **返回示例：**

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

**返回值：**

| 字段名称        | 数据类型 | 备注                                                                            |
| --------------- | -------- | ------------------------------------------------------------------------------- |
| code            | int      | 200,正常                                                                        |
| msg             | string   | success,正常                                                                    |
| data            | object   | 返回信息：委托单详情                                                            |
| contractCode    | string   | 合约代码                                                                        |
| marginMode      | int      | 保证金模式 1-全仓 2-逐仓                                                        |
| orderId         | string   | 委托单 ID                                                                       |
| clientOid       | string   | 用户自编委托单 ID                                                               |
| side            | int      | 委托方向 1-买 2-卖                                                              |
| orderType       | int      | 委托类型 1-限价 2-市价 3-限价止盈 4-市价止盈 5-限价止损 6-市价止损 7-只做 Maker |
| offset          | int      | 开平方向 1-开 2-平                                                              |
| price           | string   | 委托价格                                                                        |
| amount          | string   | 委托数量                                                                        |
| filledAmount    | string   | 已成交数量                                                                      |
| filledMoney     | string   | 已成交金额                                                                      |
| filledFee       | string   | 已成交手续费                                                                    |
| feeCurrency     | string   | 手续费币种                                                                      |
| triggerPrice    | string   | 委托单触发价                                                                    |
| triggerType     | string   | 委托单触发类型 gte-大于等于 lte-小于等于                                        |
| triggerState    | int      | 触发状态 1-触发成功                                                             |
| workingType     | int      | 条件价格触发类型 1-最新价格 2-标记价格                                          |
| leverage        | int      | 杠杆倍数                                                                        |
| liquidationType | int      | 强平类型 1-爆仓 2-减仓 3-止盈减仓                                               |
| state           | int      | 委托单状态 1-已创建 2-等待成交 3-部分成交 4-完全成交 5-部分成交撤销 6-已撤销    |
| accountType     | string   | 账户类型                                                                        |
| platform        | string   | 平台来源                                                                        |
| cancelType      | int      | 撤单类型 1-用户撤单 2-系统撤单 3-运营撤单 4-爆仓撤单 5-减仓撤单                 |
| closeType       | int64    | 平仓类型 1-普通平仓 2-快速平仓 3-一键平仓 4-系统平仓                            |
| createTime      | int64    | 创建时间                                                                        |
| updateTime      | int64    | 状态更新时间                                                                    |

## 获取委托单列表

限速规则：20 次/2s

**功能说明：**

此接口获取列出您当前的委托单信息（最近 3 个月的委托单信息）。这个请求支持分页，并且按时间倒序排序和存储，最新的排在最前面。

**请求路径：**

/swap-api/v1/orders

curl `https://api.fameex.com/swap-api/v1/orders`

`headers参数`

无

**路由参数：**

无

**Post 参数：**

| 参数            | 是否必须 | 数据类型  | 备注                                                                                              |
| --------------- | -------- | --------- | ------------------------------------------------------------------------------------------------- |
| contractCode    | 是       | string    | 合约代码(如 BTC-USDT)                                                                             |
| side            | 否       | int       | 委托方向 1-买 2-卖                                                                                |
| offset          | 否       | int       | 开平方向 1-开 2-平                                                                                |
| closeType       | 否       | int       | 平仓类型 1-普通平仓 2-快速平仓 3-一键平仓 4-系统平仓                                              |
| liquidationType | 否       | int       | 强平类型 1-爆仓 2-减仓 3-止盈减仓                                                                 |
| orderTypes      | 否       | int array | 委托类型列表 1-限价 2-市价 3-限价止盈 4-市价止盈 5-限价止损 6-市价止损 7-只做 Maker （如[1,2,3]） |
| state           | 是       | int       | 委托单状态 7-未完成 8-已完成 9-完全成交或部分成交撤销                                             |
| pageNum         | 是       | int       | 分页使用, 第几页                                                                                  |
| pageSize        | 是       | int       | 分页使用, 每页数量 (0 < pageSize ≤ 500)                                                           |
| startTime       | 否       | int64     | 时间戳,查询订单的开始时间 秒                                                                      |
| endTime         | 否       | int64     | 时间戳,查询订单的结束时间 秒                                                                      |

> **返回示例：**

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

**返回值：**

| 字段名称        | 数据类型     | 备注                                                                            |
| --------------- | ------------ | ------------------------------------------------------------------------------- |
| code            | int          | 200,正常                                                                        |
| msg             | string       | success,正常                                                                    |
| data            | object       | 返回信息：委托单                                                                |
| pageNum         | int          | 分页, 第几页(1<=pageNum)                                                        |
| pageSize        | int          | 分页, 每页数量(1<=pageSize<= 500)                                               |
| total           | int64        | 总条数                                                                          |
| orders          | object array | 委托单列表                                                                      |
| contractCode    | string       | 合约代码                                                                        |
| marginMode      | int          | 保证金模式 1-全仓 2-逐仓                                                        |
| orderId         | string       | 委托单 ID                                                                       |
| clientOid       | string       | 用户自编委托单 ID                                                               |
| side            | int          | 委托方向 1-买 2-卖                                                              |
| orderType       | int          | 委托类型 1-限价 2-市价 3-限价止盈 4-市价止盈 5-限价止损 6-市价止损 7-只做 Maker |
| offset          | int          | 开平方向 1-开 2-平                                                              |
| price           | string       | 委托价格                                                                        |
| amount          | string       | 委托数量                                                                        |
| filledAmount    | string       | 已成交数量                                                                      |
| filledMoney     | string       | 已成交金额                                                                      |
| filledFee       | string       | 已成交手续费                                                                    |
| feeCurrency     | string       | 手续费币种                                                                      |
| triggerPrice    | string       | 委托单触发价                                                                    |
| triggerType     | string       | 委托单触发类型 gte-大于等于 lte-小于等于                                        |
| triggerState    | int          | 触发状态 1-触发成功                                                             |
| workingType     | int          | 条件价格触发类型 1-最新价格 2-标记价格                                          |
| leverage        | int          | 杠杆倍数                                                                        |
| liquidationType | int          | 强平类型 1-爆仓 2-减仓 3-止盈减仓                                               |
| state           | int          | 委托单状态 1-已创建 2-等待成交 3-部分成交 4-完全成交 5-部分成交撤销 6-已撤销    |
| accountType     | string       | 账户类型                                                                        |
| platform        | string       | 平台来源                                                                        |
| cancelType      | int          | 撤单类型 1-用户撤单 2-系统撤单 3-运营撤单 4-爆仓撤单 5-减仓撤单                 |
| closeType       | int64        | 平仓类型 1-普通平仓 2-快速平仓 3-一键平仓 4-系统平仓                            |
| createTime      | int64        | 创建时间                                                                        |
| updateTime      | int64        | 状态更新时间                                                                    |

## 获取成交明细

限速规则：20 次/2s

**功能说明：**

此接口获取您当前所有的成交订单信息。这个请求支持分页，并且按时间倒序排序和存储，最新的排在最前面。

**请求路径：**

/swap-api/v1/trades

curl `https://api.fameex.com/swap-api/v1/trades`

**路由参数：**

无

**Post 参数：**

| 参数            | 是否必须 | 数据类型  | 备注                                                                                             |
| --------------- | -------- | --------- | ------------------------------------------------------------------------------------------------ |
| contractCode    | 否       | string    | 合约代码(如 BTC-USDT)                                                                            |
| orderId         | 否       | string    | 委托单 ID                                                                                        |
| side            | 否       | int       | 委托方向 1-买 2-卖                                                                               |
| offset          | 否       | int       | 开平方向 1-开 2-平                                                                               |
| closeType       | 否       | int       | 平仓类型 1-普通平仓 2-快速平仓 3-一键平仓 4-系统平仓                                             |
| liquidationType | 否       | int       | 强平类型 1-爆仓 2-减仓 3-止盈减仓                                                                |
| orderTypes      | 否       | int array | 委托类型列表 1-限价 2-市价 3-限价止盈 4-市价止盈 5-限价止损 6-市价止损 7-只做 Maker（如[1,2,3]） |
| pageNum         | 是       | int       | 分页使用, 第几页,从第一页开始                                                                    |
| pageSize        | 是       | int       | 分页使用, 每页数量 (0 < pageSize ≤ 500)                                                          |
| startTime       | 否       | int64     | 开始时间戳，秒                                                                                   |
| endTime         | 否       | int64     | 结束时间戳，秒                                                                                   |

> **返回示例：**

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

**返回值：**

| 字段名称        | 数据类型 | 备注                                                                            |
| --------------- | -------- | ------------------------------------------------------------------------------- |
| code            | int      | 200，正常                                                                       |
| msg             | string   | success，正常                                                                   |
| data            | string   | 返回值,成交明细                                                                 |
| pageNum         | int      | 分页, 第几页(1<=pageNum)                                                        |
| pageSize        | int      | 分页, 每页数量(1<=pageSize<= 500)                                               |
| total           | int64    | 总条数                                                                          |
| contractCode    | string   | 合约代码                                                                        |
| tradeId         | string   | 成交单 ID                                                                       |
| orderId         | string   | 委托单 ID                                                                       |
| userId          | string   | 用户 ID                                                                         |
| side            | int      | 委托方向 1-买 2-卖                                                              |
| orderType       | int      | 委托类型 1-限价 2-市价 3-限价止盈 4-市价止盈 5-限价止损 6-市价止损 7-只做 Maker |
| offset          | int      | 开平方向 1-开 2-平                                                              |
| price           | string   | 成交价格                                                                        |
| amount          | string   | 成交数量                                                                        |
| feeCurrency     | string   | 手续费币种                                                                      |
| feeRate         | string   | 实际手续费率                                                                    |
| fee             | string   | 手续费                                                                          |
| profitReal      | string   | 已实现盈亏                                                                      |
| liquidationType | int      | 强平类型 1-爆仓 2-减仓 3-止盈减仓                                               |
| accountType     | string   | 账户类型                                                                        |
| platform        | string   | 平台来源                                                                        |
| role            | int      | 角色类型 1-maker 2-taker                                                        |
| selfTrade       | int      | 是否自成交 1-自成交                                                             |
| closeType       | int      | 平仓类型 1-普通平仓 2-快速平仓 3-一键平仓 4-系统平仓                            |
| createTime      | int64    | 创建时间                                                                        |

## 获取最近成交明细

限速规则：20 次/2s

**功能说明：**

此接口获取您获取最近成交订单信息。

**请求路径：**

/swap-api/v1/last_trades

curl `https://api.fameex.com/swap-api/v1/last_trades`

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型 | 备注                              |
| ------------ | -------- | -------- | --------------------------------- |
| contractCode | 是       | string   | 合约代码, 例"BTC-USDT"            |
| accountType  | 是       | string   | 账户类型，"swap"                  |
| size         | 是       | int      | 返回的成交明细数量(1<=size<= 100) |

> **返回示例：**

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

**返回值：**

| 字段名称   | 数据类型 | 备注                |
| ---------- | -------- | ------------------- |
| code       | int      | 200，正常           |
| msg        | string   | success，正常       |
| data       | object   | 返回值,最近成交明细 |
| tradeId    | string   | 成交单 ID           |
| side       | int      | 委托方向 1-买 2-卖  |
| price      | string   | 成交价格            |
| amount     | string   | 成交数量            |
| createTime | int64    | 创建时间            |

## 调整合约杠杆倍数

限速规则：20 次/2s

**功能说明：**

此接口调整合约杠杆倍数。

**请求路径：**

/swap-api/v1/wallet/leverage/adjust

curl `https://api.fameex.com/swap-api/v1/wallet/leverage/adjust`

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型 | 备注                   |
| ------------ | -------- | -------- | ---------------------- |
| contractCode | 是       | string   | 合约代码, 例"BTC-USDT" |
| leverage     | 是       | int      | 杠杆倍数               |
| marginMode   | 是       | string   | 仓位类型 1:全仓 2:逐仓 |

> **返回示例：**

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

**返回值：**

| 字段名称     | 数据类型 | 备注         |
| ------------ | -------- | ------------ |
| code         | int      | 200, 正常    |
| msg          | string   | success,正常 |
| data         | object   | 返回值       |
| userid       | string   | 用户 id      |
| contractCode | string   | 合约代码     |
| leverage     | int      | 杠杆倍数     |

# U 合约钱包 API 接口

## 获取合约账户资产

限速规则：20 次/2s

**功能说明：**

此接口获取钱包合约账户数据。

**请求路径：**

/swap-api/v1/wallet/asset

curl `https://api.fameex.com/swap-api/v1/wallet/asset`

**路由参数：**

无

**Post 参数：**

无

> **返回示例：**

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

**返回值：**

| 字段名称      | 数据类型     | 备注                   |
| ------------- | ------------ | ---------------------- |
| code          | int          | 200, 正常              |
| msg           | string       | success,正常           |
| data          | object       | 返回值,合约账户数据    |
| available     | string       | 可用                   |
| balance       | string       | 账户余额               |
| userid        | string       | 用户 id                |
| valuation     | string       | 保证金余额折合其他     |
| btcValuation  | string       | 保证金余额折合 BTC     |
| totalFrozen   | string       | 全部冻结               |
| marginBalance | string       | 保证金余额             |
| frozenList    | object array | 返回仓位信息           |
| contractCode  | string       | 合约代码               |
| frozen        | string       | 冻结                   |
| posSide       | int          | 仓位方向 1:多仓 2:空仓 |

## 获取合约账户持仓

限速规则：20 次/2s

**功能说明：**

此接口获取用户合约账户持仓。

**请求路径：**

/swap-api/v1/wallet/pos

curl `https://api.fameex.com/swap-api/v1/wallet/pos`

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型 | 备注                   |
| ------------ | -------- | -------- | ---------------------- |
| contractCode | 是       | string   | 合约代码, 例"BTC-USDT" |

> **返回示例：**

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

**返回值：**

| 字段名称       | 数据类型     | 备注                                                                                          |
| -------------- | ------------ | --------------------------------------------------------------------------------------------- |
| code           | int          | 200, 正常                                                                                     |
| msg            | string       | success,正常                                                                                  |
| data           | object       | 返回值,合约账户数据                                                                           |
| currency       | string       | 资产币种                                                                                      |
| isolatedMargin | string       | 逐仓仓位保证金 (全仓保证金需要前端自己计算(实时变化): (MarkPrice\*Pos)/Leverage = [四舍五入]) |
| leverage       | int          | 杠杆倍数                                                                                      |
| liquidation    | string       | 预估强平价                                                                                    |
| marginMode     | int          | 仓位类型 1:全仓 2:逐仓                                                                        |
| openPriceAvg   | string       | 开仓均价                                                                                      |
| openTime       | int64        | 开仓时间，秒级时间戳                                                                          |
| pos            | object array | 返回仓位信息                                                                                  |
| posAvailable   | string       | 可平仓位                                                                                      |
| posSide        | int          | 仓位方向 (1:多仓 2:空仓)                                                                      |
| posValue       | string       | 仓位价值                                                                                      |
| profitReal     | string       | 总已实现盈亏                                                                                  |
| profitUnreal   | string       | 未实现盈亏                                                                                    |
| rivalScore     | string       | 对手方减仓指数                                                                                |
| contractCode   | string       | 合约代码                                                                                      |
| userId         | string       | 用户 ID                                                                                       |

# 错误信息

| code 码 | 备注                                              |
| ------- | ------------------------------------------------- |
| 200     | 正常                                              |
| 112002  | API 单个 Key 流量超限                             |
| 112005  | API 请求频率超限                                  |
| 112007  | API-Key 创建失败                                  |
| 112008  | API-Key 备注名称已存在                            |
| 112009  | API-Key 创建数量超限（单个用户最多创建 5 个 API） |
| 112010  | API-Key 失效（单个 Key 的时限为 60 天自然日）     |
| 112011  | API 请求 IP 访问受限（绑定 IP 与请求 IP 不一致）  |
| 112015  | 签名错误                                          |
| 112020  | 签名方式错误                                      |
| 112021  | 签名版本错误                                      |
| 112022  | 签名时间戳错误                                    |
| 112047  | 现货 API 接口暂时不可访问                         |
| 112048  | 期货 API 接口暂时不可访问                         |
| 230030  | 请通过 KYC 认证后进行操作                         |

# 常见问题

| 常见问题                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.什么是交易币种?什么是计价币种？交易量是以交易币种还是计价币种进行数量统计？<br>答：<br>每一个交易币对都是由 交易币种/计价币种 组成的，币对中前方为交易货币，后方为计价货币。<br>举例说明：BTC/USDT 这个交易币对中，BTC 为交易货币，USDT 为计价货币。<br>交易量是以交易币种为准进行统计。<br>成交总额是以计价币种为准进行统计。      |
| 2.Rest 访问限制?<br>答: <br>1.单个 IP 限制每分钟 1200 次访问，超过 1200 次将被锁定 1 小时，一小时后自动解锁。<br>2.单个用户限制每秒钟 20 次访问，一秒钟内 20 次以上的请求，将会视作无效。                                                                                                                                             |
| 3.WebSocket 访问限制?<br>答:<br> 单个用户限制每秒钟 50 次访问，一秒钟内 50 次以上的请求，将会视作无效。                                                                                                                                                                                                                               |
| 4.生成的密钥有什么用处?<br>答:<br> 密钥是用来操作 API 的钥匙，在调用 API 接口时需要提供 API 密钥。私有密钥只在刚生成时显示一次，遗忘需重新生成。                                                                                                                                                                                      |
| 5.k 线图是否可以获取几个月或者一年前的数据?<br>答:<br> 系统 k 线图最多只提供 1000 条数据,如果要获取比较久的数据需要使用小时或者天的单位获取。                                                                                                                                                                                         |
| 6.API 的 IP 是否需要绑定?<br>答:<br> 1.API 的 IP 绑定有效的防止除了这个 IP 之外的服务器进行调用自己的权限进行交易操作。<br> 2.绑定 IP 后，只能由绑定的 IP 进行访问，如不绑定，则不限制访问 IP。                                                                                                                                       |
| 7.公钥私钥可以提供给别人吗?<br>答:<br> 不建议,会导致资产损失。                                                                                                                                                                                                                                                                        |
| 8.签名失败频繁?<br> • 检查 API Key 是否有效，是否复制正确，是否有绑定 IP 白名单；<br>• 检查时间戳是否是 UTC 时间；<br>• 检查参数是否按字母排序；<br>• 检查编码；<br>• 检查签名编码应该是 hex；<br>• 检查是否以表单方式提交；<br>• 检查 url 是否带着签名字段，POST 的数据格式是否是 json 格式；<br>• 检查签名结果是否有进行 URI 编码。 |
| 9.返回 login-required?<br>• 检查参数 account-id 是否是由 /v1/account/accounts 接口返回的，而不是填的 UID；<br>• 检查请求是否把业务参数也计算进签名；<br>• 检查 请求是否将参数按照 ASCII 码表顺序排序。                                                                                                                                |
| 10.返回 gateway-internal-error?<br>检查请求是否在 header 中声明 Content-Type:application/json。                                                                                                                                                                                                                                       |
