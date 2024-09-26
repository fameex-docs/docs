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

## 2023-09-12

- Coin trading interface update:
  - 获取所有未完成的订单接口 `/v1/api/orders_pending` (使用 `/v1/api/spot/orderlist` 替代)

## 2022-11-07

- 新增现货行情接口:
  - GET `/v2/public/assets` 币种列表
  - GET `/v2/public/summary` 交易对信息
  - GET `/v2/public/ticker` 交易对摘要
  - GET `/v2/public/orderbook/market_pair` 深度信息
  - GET `/v2/public/trades/market_pair` 订单查询

## 2021-03-30

- 新增现货行情接口:
  - GET `/api/v2/orderbook` 获取深度信息
  - GET `/api/v2/trades` 获取近期成交
  - GET `/api/v2/ticker/24hr` 获取 24 小时滚动窗口价格变动数据
  - GET `/api/v2/ticker/price` 获取交易对最新价格

## 2021-08-24

- Websocket 行情推送更新：

  - 更新心跳连接 `wss://www.fameex.com/push`
  - 更新登录信息 `wss://www.fameex.com/push`
  - 删除注册 K 线信息 `wss://www.fameex.com/push`
  - 删除注册首页行情 `wss://www.fameex.com/push`
  - 删除注册深度行情 `wss://www.fameex.com/push`
  - 更新推送首页行情 `wss://www.fameex.com/push`
  - 更新推送币对深度列表 `wss://www.fameex.com/push`
  - 更新推送 K 线数据 `wss://www.fameex.com/push`
  - 更新推送最新成交订单行情 `wss://www.fameex.com/push`
  - 删除推送订单成交或者撤销 `wss://www.fameex.com/push`
  - 删除推送我的订单部分撤销 `wss://www.fameex.com/push`
  - 更新注销首页行情 `wss://www.fameex.com/push`

- 币币交易 API 接口更新：

  - 修改获取 K 线数据接口 `/v1/market/history/kline`
  - 修改获取市场深度数据接口 `/v1/market/depth`
  - 修改获取成交数据接口 `/v1/market/history/trade`
  - 修改获取某个 ticker 信息接口 `/v1/market/history/kline24h`
  - 修改获取全部 ticker 信息接口 `/v1/market/history/kline24h/all`
  - 修改币币下单接口 `/v1/api/spot/orders`
  - 修改币币撤单接口 `/v1/api/spot/cancel_orders`
  - 修改批量撤单接口 `/spot/v1/cancel_batch_orders`
  - 修改获取委托单详情接口 `/v1/api/spot/orderdetail`
  - 修改获取委托单列表接口 `/v1/api/spot/orderlist`
  - 修改获取成交明细接口 `/v1/api/spot/fills`
  - 修改获取所有未完成的订单接口 `/v1/api/orders_pending`

- 杠杆交易 API 接口更新：
  - 修改杠杆下单接口 `/v1/api/lever/orders/place`
  - 修改杠杆撤单接口 `/v1/api/lever/cancel_orders`
  - 修改杠杆批量撤单接口 `/v1/api/lever/orders/batch_cancel`
  - 修改获取杠杆委托单列表接口 `/v1/api/lever/orders`
  - 修改获取杠杆委托单详情接口 `/v1/api/lever/orders/detail`
  - 修改获取杠杆成交明细接口 `/v1/api/lever/deals`

## 2020-12-22

- 钱包接口更新：
  - 删除所有币种的提币记录接口 `v1/api/account/withdrawal/history`
  - 删除单个币种的提币记录接口 `v1/api/account/withdrawal/history/currency`
  - 删除获取所有币种的充币记录接口 `v1/api/account/deposit/histoty`
  - 删除查询账单流水记录接口 `v1/api/spot/bill_flow`
  - 新增查询现货账户交易账单接口 `v1/api/spot/record/trade`
  - 新增查询现货账户划转账单接口 `v1/api/spot/record/chargewithdraw`
  - 新增查询现货账户充提账单接口 `v1/api/spot/record/trans`
  - 新增查询现货账户其他账单接口 `v1/api/spot/record/others`
  - 修改资金划转接口参数接口 `v1/api/account/transfer`

## 2020-11-16

- 币币交易接口更新：
  - 更新获取订单列表 `v1/api/spot/orderlist`为获取委托单列表
  - 更新获取订单详情 `v1/api/spot/orderdetail` 为获取委托单详情
  - 更新获取杠杆订单列表 `v1/api/lever/orders`为获取杠杆订单列表
  - 更新获取杠杆订单详情 `v1/api/lever/orders/detail`为获取杠杆委托单详情

## 2020-10-30

- 钱包接口更新：
  - 修改资金划转功能接口 `v1/api/account/transfer`

## 2020-10-29

- 钱包接口更新：
  - 新增杠杆挂单功能接口 `v1/api/lever/orders/place`
  - 新增杠杆撤单功能接口 `v1/api/lever/orders/cancel`
  - 新增杠杆批量撤单接口 `v1/api/lever/orders/batch_cancel`
  - 新增获取杠杆账户委托单列表功能接口 `v1/api/lever/orders`
  - 新增获取杠杆账户委托单详情功能接口 `v1/api/lever/orders/detail`
  - 新增获取杠杆配置功能接口 `v1/api/lever/pair/config`

## 2020-10-28

- 钱包接口更新：
  - 新增获取杠杆账户账单接口 `v1/api/lever/ledger`
  - 新增获取杠杆账户特定币对，特定币种下还币的提示参数接口 `v1/api/lever/repayparam`
  - 新增获取杠杆账户特定币对，特定币种下还币接口 `v1/api/lever/repay`
  - 新增获取杠杆账户特定币对，特定币种下借币的提示参数接口 `v1/api/lever/borrow`
  - 新增获取杠杆账户特定币对，特定币种下借币接口 `v1/api/lever/borrowparam`

## 2020-10-27

- 钱包接口更新：
  - 新增获取杠杆账户信息接口 `v1/api/lever/accounts`
  - 新增获取杠杆账户下某一特定币对详情接口 `v1/api/lever/accounts/{pairName}`

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

| 接入 URLs                 | 说明                   |
| ------------------------- | ---------------------- |
| `https://api.fameex.com`  | RESTFUL API            |
| `wss://www.fameex.com/ws` | WebSocket Feed（行情） |

所有请求基于 Https 协议，POST 请求的请求头信息中 contentType 需要统一设置为:’application/json’

鉴于延迟高和稳定性差等原因，不建议通过代理的方式访问 FameEX- API。

## 限频规则

**限制频率：**每个接口的限制不同 。

单个 API Key 维度限制，建议行情 API 访问也要加上签名，否则限频会更严格。

| 限频规则                               | 数据类型               | 说明 |
| -------------------------------------- | ---------------------- | ---- |
| 对每个 AccessKey 及每个 url 的频率限制 | 20 次/2s（大部分接口） | 无   |

## 请求头设置

请求头(header)的参数如下：

| 参数             | 数据类型 | 说明                       |
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

# Websocket 行情推送

## 心跳连接

**功能说明：**

长连接心跳

**请求路径：**

wss://www.fameex.com/spot

**请求方式：**

websocket

> **请求示例：**

```json
{
  "op": "ping"
}
```

**参数：**

| 参数 | 是否必须 | 数据类型 | 说明             |
| ---- | -------- | -------- | ---------------- |
| op   | 是       | string   | 消息类型("ping") |

> **返回示例：**

```json
{
  "code": 200,
  "op": "pong"
}
```

### 响应参数

| 字段名称 | 数据类型 | 说明             |
| -------- | -------- | ---------------- |
| code     | int      | 200,正常         |
| op       | string   | 消息类型("pong") |

## 登录信息

**功能说明：**

长连接登录

**请求路径：**

wss://www.fameex.com/spot

**请求方式：**

websocket

> **请求示例：**

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

**参数：**

| 参数      | 是否必须 | 数据类型 | 说明                  |
| --------- | -------- | -------- | --------------------- |
| op        | 是       | string   | 消息类型("req")       |
| topic     | 是       | string   | 请求主题("auth")      |
| params    | 是       | object   | 参数                  |
| accessKey | 是       | string   | 申请的 AccessKey      |
| platform  | 是       | string   | 平台来源(WEB/APP/API) |

> **返回示例：**

```json
{
  "code": 200,
  "op": "req",
  "topic": "auth"
}
```

### 响应参数

| 字段名称 | 数据类型 | 说明             |
| -------- | -------- | ---------------- |
| code     | int      | 200, 正常        |
| op       | string   | 消息类型("req")  |
| topic    | string   | 请求主题("auth") |

## 推送 K 线信息

**功能说明：**

此接口注册 K 线服务

**请求路径：**

wss://www.fameex.com/spot

**请求方式：**

websocket

> **请求示例：**

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

**参数：**

| 参数   | 是否必须 | 数据类型 | 说明                                  |
| ------ | -------- | -------- | ------------------------------------- |
| op     | 是       | string   | 消息类型("sub")                       |
| topic  | 是       | string   | 订阅主题("spot.market.kline")         |
| params | 是       | object   | 参数                                  |
| symbol | 是       | string   | 币对名称（如，"BTC-USDT"）            |
| period | 是       | string   | K 线时间粒度(1,5,15,30,60,120,240,1D) |

> **返回示例：**

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

### 响应参数

| 字段名称 | 数据类型 | 说明                                  |
| -------- | -------- | ------------------------------------- |
| code     | int      | 200, 正常                             |
| op       | string   | 消息类型("sub")                       |
| topic    | string   | 请求主题("spot.market.kline")         |
| data     | object   | 返回数据实体                          |
| symbol   | string   | 币对名称（如，“BTC-USDT”）            |
| period   | string   | K 线时间粒度(1,5,15,30,60,120,240,1D) |
| time     | int64    | 开始时间戳,秒                         |
| open     | string   | 开盘价                                |
| low      | string   | 最低价                                |
| high     | string   | 最高价                                |
| close    | string   | 最新价                                |
| amount   | string   | 交易币成交量                          |
| volume   | string   | 计价币成交量                          |

## 推送首页行情

**功能说明：**

此接口注册首页行情服务

**请求路径：**

wss://www.fameex.com/spot

**请求方式：**

websocket

> **请求示例：**

```json
{
  "op": "sub",
  "topic": "spot.market.ticker",
  "params": {
    "symbol": "BTC-USDT"
  }
}
```

**参数：**

| 参数   | 是否必须 | 数据类型 | 说明                          |
| ------ | -------- | -------- | ----------------------------- |
| op     | 是       | string   | 消息类型("sub")               |
| topic  | 是       | string   | 订阅主题("spot.market.kline") |
| params | 是       | object   | 参数                          |
| symbol | 是       | string   | 币对名称（如，"BTC-USDT"）    |

> **返回示例：**

```json
{
  "code": 200,
  "op": "sub",
  "topic": "spot.market.ticker",
  "data": {
    "symbol": "BTC-USDT", //币对名称
    "gain": "0.12", //24小时涨幅
    "open": "103.4", //24小时开盘价
    "low": "103.4", //24小时最低价
    "high": "103.4", //24小时最高价
    "close": "103.4", //最新成交价
    "amount": "1.66", //24小时交易币成交量
    "volume": "200.12", //24小时计价币成交量
    "quotePrice": "450.12" //计价币价格
  }
}
```

### 响应参数

| 字段名称   | 数据类型 | 说明                           |
| ---------- | -------- | ------------------------------ |
| code       | int      | 200, 正常                      |
| op         | string   | 消息类型("sub")                |
| topic      | string   | 请求主题("spot.market.ticker") |
| data       | object   | 返回数据实体                   |
| symbol     | string   | 币对名称（如，“BTC-USDT”）     |
| open       | string   | 24 小时开盘价                  |
| low        | string   | 24 小时最低价                  |
| high       | string   | 24 小时最高价                  |
| close      | string   | 最新成交价                     |
| amount     | string   | 24 小时交易币成交量            |
| volume     | string   | 24 小时计价币成交量            |
| quotePrice | string   | 计价币价格                     |

## 推送深度行情

**功能说明：**

此接口注册深度服务

**请求路径：**

wss://www.fameex.com/spot

**请求方式：**

websocket

> **请求示例：**

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

**参数：**

| 参数   | 是否必须 | 数据类型 | 说明                              |
| ------ | -------- | -------- | --------------------------------- |
| op     | 是       | string   | 消息类型("sub")                   |
| topic  | 是       | string   | 订阅主题("spot.market.ticker")    |
| params | 是       | object   | 参数                              |
| symbol | 是       | string   | 币对名称（如，"BTC-USDT"）        |
| step   | 是       | string   | 深度的价格聚合度类型(step0~step4) |

> **返回示例：**

```json
{
  "code": 200,
  "op": "sub",
  "topic": "spot.market.ticker",
  "data": {
    "symbol": "BTC-USDT", //币对名称
    "step": "step0", //深度的价格聚合度类型
    "time": 1603785494, //时间戳
    "bids": [["123.12", "1.2"]], //当前的所有买单 [价格，数量]
    "asks": [["123.12", "1.2"]] //当前的所有卖单 [价格，数量]
  }
}
```

### 响应参数

| 字段名称 | 数据类型 | 说明                              |
| -------- | -------- | --------------------------------- |
| code     | int      | 200, 正常                         |
| op       | string   | 消息类型("sub")                   |
| topic    | string   | 请求主题("spot.market.depth")     |
| data     | object   | 返回数据实体                      |
| symbol   | string   | 币对名称（如，“BTC-USDT”）        |
| step     | string   | 深度的价格聚合度类型(step0~step4) |
| time     | string   | 时间戳,秒                         |
| bids     | array    | 当前的所有买单 [价格，数量]       |
| asks     | array    | 当前的所有卖单 [价格，数量]       |

## 推送最新成交订单行情

**功能说明：**

此接口推送最新成交订单详情

**请求路径：**

wss://www.fameex.com/spot

**请求方式：**

websocket

> **请求示例：**

```json
{
  "op": "sub",
  "topic": "spot.market.last_trade",
  "params": {
    "symbol": "BTC-USDT"
  }
}
```

**参数：**

| 参数   | 是否必须 | 数据类型 | 说明                               |
| ------ | -------- | -------- | ---------------------------------- |
| op     | 是       | string   | 消息类型("sub")                    |
| topic  | 是       | string   | 订阅主题("spot.market.last_trade") |
| params | 是       | object   | 参数                               |
| symbol | 是       | string   | 币对名称（如，"BTC-USDT"）         |

> **返回示例：**

```json
{
  "code": 200,
  "op": "sub",
  "topic": "spot.market.last_trade",
  "data": [
    {
      "symbol": "BTC-USDT", //币对名称
      "tradeId": "10384834938169458677", //成交单ID
      "side": 1, //委托方向 1-买 2-卖
      "price": "7890.12", //成交价格
      "amount": "1.12", //成交数量
      "createTime": 156655468 //创建时间
    }
  ]
}
```

### 响应参数

| 字段名称   | 数据类型 | 说明                               |
| ---------- | -------- | ---------------------------------- |
| code       | int      | 200, 正常                          |
| op         | string   | 消息类型("sub")                    |
| topic      | string   | 请求主题("spot.market.last_trade") |
| data       | object   | 返回数据实体                       |
| symbol     | string   | 币对名称（如，“BTC-USDT”）         |
| tradeId    | string   | 成交单 ID                          |
| side       | string   | 委托方向 1-买 2-卖                 |
| price      | array    | 成交价格                           |
| amount     | array    | 成交数量                           |
| createTime | int64    | 创建时间戳，秒                     |

## 推送订单成交或者撤销

**功能说明：**

推送买卖方或自己订单成交或取消

**请求路径：**

wss://www.fameex.com/spot

**请求方式：**

websocket

> **请求示例：**

```json
{
  "op": "sub",
  "topic": "spot.orders",
  "params": {
    "symbol": "BTC-USDT"
  }
}
```

**参数：**

| 参数   | 是否必须 | 数据类型 | 说明                       |
| ------ | -------- | -------- | -------------------------- |
| op     | 是       | string   | 消息类型("sub")            |
| topic  | 是       | string   | 订阅主题("spot.orders")    |
| params | 是       | object   | 参数                       |
| symbol | 是       | string   | 币对名称（如，"BTC-USDT"） |

> **返回示例：**

```json
{
  "code": 200,
  "op": "sub",
  "topic": "spot.orders",
  "data": {
    "symbol": "BTC-USDT", //币对名称
    "orderId": "10384834938169458688", //委托单ID
    "clientOid": "10567108063048237056", //用户自编委托单ID
    "side": 1, //委托方向 1-买 2-卖
    "orderType": 1, //委托类型 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做Maker
    "price": "7890.12", //委托价格
    "amount": "1.12", //委托数量
    "money": "1.12", //委托金额(市价买时)
    "filledAmount": "1.12", //已成交数量
    "filledMoney": "8562.12", //已成交金额
    "filledFee": "1.12", //已成交手续费
    "feeCurrency": "usdt", //手续费币种
    "triggerPrice": "7600.12", //委托单触发价
    "triggerType": "gte", //委托单触发类型 gte-大于等于 lte-小于等于
    "triggerState": 1, //触发状态 1-触发成功
    "liquidationType": 1, //强平类型 1-爆仓
    "strategyId": "123456789", //策略Id
    "strategyType": 1, //策略类型
    "strategyName": "abc", //策略名称
    "state": 1, //委托单状态 1-已创建 2-等待成交 3-部分成交 4-完全成交 5-部分成交撤销 6-已撤销
    "accountType": "spot", //账户类型
    "platform": "API", //平台来源
    "cancelType": 1, //撤单类型 1-用户撤单 2-系统撤单 3-运营撤单
    "createTime": 15665546871, //创建时间
    "updateTime": 15665546872 //状态更新时间
  }
}
```

### 响应参数

| 字段名称        | 数据类型 | 说明                                                                         |
| --------------- | -------- | ---------------------------------------------------------------------------- |
| code            | int      | 200, 正常                                                                    |
| op              | string   | 消息类型("sub")                                                              |
| topic           | string   | 请求主题("spot.orders")                                                      |
| data            | object   | 返回数据实体                                                                 |
| symbol          | string   | 币对名称（如，“BTC-USDT”）                                                   |
| orderId         | string   | 订委托单 ID                                                                  |
| clientOid       | string   | 用户自编委托单 ID                                                            |
| side            | int      | 订委托方向 1-买 2-卖                                                         |
| orderType       | int      | 委托类型 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker                    |
| price           | string   | 委托单价格                                                                   |
| amount          | string   | 委托数量                                                                     |
| money           | string   | 委托金额(市价买时)                                                           |
| filledAmount    | sting    | 已成交数量                                                                   |
| filledMoney     | sting    | 已成交金额                                                                   |
| filledFee       | string   | 已成交手续费                                                                 |
| feeCurrency     | string   | 手续费币种                                                                   |
| triggerPrice    | string   | 委托单触发价                                                                 |
| triggerType     | string   | 委托单触发类型 gte-大于等于 lte-小于等于                                     |
| triggerState    | int      | 触发状态 1-触发成功                                                          |
| liquidationType | int      | 委强平类型 1-爆仓                                                            |
| strategyId      | string   | 策略 Id                                                                      |
| strategyType    | int      | 策略类型                                                                     |
| strategyName    | string   | 策略名称                                                                     |
| state           | int      | 委托单状态 1-已创建 2-等待成交 3-部分成交 4-完全成交 5-部分成交撤销 6-已撤销 |
| accountType     | string   | 账户类型                                                                     |
| platform        | int      | 平台来源                                                                     |
| cancelType      | int      | 撤单类型 1-用户撤单 2-系统撤单 3-运营撤单                                    |
| createTime      | int64    | 下单时间戳，秒                                                               |
| updateTime      | int64    | 状态更新时间戳，秒                                                           |

## 注销首页行情

**功能说明：**

此接口注销首页行情服务

**请求路径：**

wss://www.fameex.com/spot

**请求方式：**

websocket

> **请求示例：**

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

**参数：**

| 参数       | 是否必须 | 数据类型 | 说明                                                        |
| ---------- | -------- | -------- | ----------------------------------------------------------- |
| op         | 是       | string   | 消息类型("unsub")                                           |
| topic      | 是       | string   | 订阅主题("spot.orders")                                     |
| params     | 是       | object   | 参数                                                        |
| symbol     | 否       | string   | 币对名称（如，"BTC-USDT"）                                  |
| step       | 否       | string   | 深度的价格聚合度类型(step0~step4)                           |
| period     | 否       | string   | 时间粒度 例（ "1","5","15","30","60","120","240","1D","1W") |
| activityId | 否       | string   | 活动 ID                                                     |

> **返回示例：**

```json
{
  "code": 200,
  "op": "unsub",
  "topic": "spot.market.ticker"
}
```

### 响应参数

| 参数  | 数据类型 | 说明                           |
| ----- | -------- | ------------------------------ |
| code  | int      | 200, 正常 =                    |
| op    | string   | 消息类型("unsub")              |
| topic | string   | 请求主题("spot.market.ticker") |

# 基础 API 接口

## 获取当前系统时间

限速规则：20 次/2s

**功能说明：**

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

### 响应参数

| 字段名称 | 数据类型 | 说明                |
| -------- | -------- | ------------------- |
| code     | int      | 200, 正常           |
| ts       | int64    | 请求时间, 秒        |
| data     | int64    | 返回值,当前时间, 秒 |

## 获取所有交易币对

限速规则：20 次/2s

**功能说明：**

此接口返回 FameEX 平台支持的所有交易币对。

**请求路径：**

/v1/common/symbols

curl `https://api.fameex.com/v1/common/symbols`

**路由参数：**

无

**Post 参数：**

无

> **返回示例：**

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

### 响应参数

| 字段名称        | 数据类型 | 说明                                   |
| --------------- | -------- | -------------------------------------- |
| code            | int      | 返回值状态                             |
| ts              | int64    | 请求时间, 秒                           |
| msg             | string   | 此次返回值说明                         |
| total           | int      | 交易币对总数量                         |
| data            | list     | 返回数据：币对信息                     |
| base            | string   | 交易币                                 |
| quote           | string   | 计价币                                 |
| pair            | string   | 交易币对                               |
| pricePercision  | string   | 交易对中计价币种的精度（小数点后位数） |
| amountPercision | string   | 交易对中交易币种的精度（小数点后位数） |
| permitAmount    | string   | 最小挂单数量                           |

## 获取所有交易币种

限速规则：20 次/2s

**功能说明：**

此接口返回 FameEX 支持的所有交易币种。

**请求路径：**

/v1/common/currencys

curl `https://api.fameex.com/v1/common/currencys`

**路由参数：**

无

**Post 参数：**

无

> **返回示例：**

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

### 响应参数

| 字段名称                    | 数据类型 | 说明                                |
| --------------------------- | -------- | ----------------------------------- |
| code                        | int      | 200, 正常                           |
| msg                         | string   | 此次返回值说明                      |
| data                        | list     | 返回数据：币种信息                  |
| currency                    | string   | 币种简称                            |
| nameEn                      | string   | 英文名                              |
| nameZh                      | string   | 中文名                              |
| isBase                      | int      | 1-可以作为交易币 2-不可以作为交易币 |
| isQuote                     | int      | 1-可以作为计价币 2-不可以作为计价币 |
| minChargeAmount             | string   | 最小充币数量                        |
| blockConfirmNumber          | int      | 区块确认数                          |
| onceminwithdraw             | string   | 单次最大提币数量                    |
| daymaxwithdrawtimes         | int      | 单日最大提币次数                    |
| feewithdraw                 | string   | 提币手续费                          |
| currencyRecharge 里的 state | int      | 充币的状态 1-开启 2-关闭            |
| currencyWithdraw 里的 state | int      | 提币的状态 1-开启 2-关闭            |

# 行情接口

## 深度信息

> 请求示例

```shell
curl --request GET 'https://api.fameex.com/api/v2/orderbook?symbol=BTC-USDT&limit=5'
```

> 响应

```json
{
  "timestamp": 1648456620000,
  "bids": [
    [
      "50006.1", // 价格
      "0.024" // 挂单量
    ]
  ],
  "asks": [
    [
      "50006.34", // 价格
      "0.01" // 挂单量
    ]
  ]
}
```

### HTTP 请求

GET `/api/v2/orderbook`

### 请求参数

| 参数   | 是否必须 | 数据类型 | 说明                        |
| ------ | -------- | -------- | --------------------------- |
| symbol | YES      | string   | 示例例: "BTC-USDT"          |
| limit  | NO       | int      | 可选值:[5, 10, 20, 50, 100] |

### 响应参数

| 参数      | 数据类型 | 说明                                            |
| --------- | -------- | ----------------------------------------------- |
| timestamp | int      | 当前时间                                        |
| bids      | string   | bid 的价格和數量信息，最优 bid 价格由上到下排列 |
| asks      | string   | ask 的价格和數量信息，最优 ask 价格由上到下排列 |

## 近期成交列表

> 请求示例

```shell
curl --request GET 'https://api.fameex.com/api/v2/trades?symbol=BTC-USDT'
```

> 响应

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

### HTTP 请求

GET `/api/v2/trades`

### 请求参数

| 参数   | 是否必须 | 数据类型 | 说明                  |
| ------ | -------- | -------- | --------------------- |
| symbol | YES      | string   | 示例例: "BTC-USDT"    |
| limit  | NO       | int      | 默认 100; 最大值 100. |

### 响应参数

| 参数         | 数据类型 | 说明               |
| ------------ | -------- | ------------------ |
| trade_id     | int      | 成交单 ID          |
| price        | string   | 成交价             |
| base_volume  | string   | 成交量             |
| quote_volume | string   | 成交额             |
| timestamp    | int      | 成交时间, 毫秒(ms) |
| type         | string   | 买卖方向           |

## K 线数据

限速规则：20 次/2s

**功能说明：**

此接口获取历史 K 线数据。

**请求路径：**

/v1/market/history/kline

curl `https://api.fameex.com/v1/market/history/kline`

**路由参数：**

无

**Post 参数：**

| 参数      | 是否必须 | 数据类型 | 说明                                                        |
| --------- | -------- | -------- | ----------------------------------------------------------- |
| symbol    | 是       | string   | 币对名称, 例"ETH-BTC"                                       |
| period    | 是       | string   | 时间粒度 例（ "1","5","15","30","60","120","240","1D","1W") |
| startTime | 否       | int64    | 开始时间，时间戳（单位:秒）                                 |
| endTime   | 否       | int64    | 结束时间，时间戳（单位:秒）                                 |

> **返回示例：**

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

### 响应参数

| 字段名称 | 数据类型 | 说明         |
| -------- | -------- | ------------ |
| code     | int      | 返回值状态   |
| time     | int64    | 时间戳       |
| amount   | string   | 交易币成交量 |
| open     | string   | 开盘价       |
| close    | string   | 收盘价       |
| low      | string   | 最低价       |
| hight    | string   | 最高价       |
| volume   | string   | 计价币成交量 |

## 24hr 价格变动情况

> 请求示例

```shell
curl --request GET 'https://api.fameex.com/api/v2/ticker/24hr'
```

> 响应

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

### HTTP 请求

GET `/api/v2/ticker/24hr`

### 请求参数

| 参数   | 是否必须 | 数据类型 | 说明               |
| :----- | :------- | :------- | :----------------- |
| symbol | NO       | string   | 示例例: "BTC-USDT" |

### 响应参数

| 参数                     | 数据类型 | 说明          |
| :----------------------- | :------- | :------------ |
| trading_pairs            | string   | 币对名称      |
| last_price               | string   | 最新成交价    |
| lowest_ask               | string   | 最佳卖价      |
| highest_bid              | string   | 最佳买价      |
| base_volume              | string   | 成交量        |
| quote_volume             | string   | 成交额        |
| price_change_percent_24h | string   | 24 小时涨幅   |
| highest_price_24h        | string   | 24 小时最高价 |
| lowest_price_24h         | string   | 24 小时最低价 |

## 币种信息

> 请求示例

```shell
curl --request GET 'https://api.fameex.com/v2/public/assets'
```

> 响应

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

### HTTP 请求

GET `/v2/public/assets`

### 请求参数

无

### 响应参数

| 参数                   | 数据类型 | 说明         |
| :--------------------- | :------- | :----------- |
| name                   | string   | 币种名称     |
| unified_cryptoasset_id | string   | 币种 id      |
| can_withdraw           | bool     | 是否可以提现 |
| can_deposit            | bool     | 是否可以充值 |
| min_withdraw           | string   | 最小提现数量 |
| max_withdraw           | string   | 最大提现数量 |

## 交易对信息

> 请求示例

```shell
curl --request GET 'https://api.fameex.com/v2/public/summary'
```

> 响应

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

### HTTP 请求

GET `/v2/public/summary`

### 请求参数

无

### 响应参数

| 参数                     | 数据类型 | 说明          |
| :----------------------- | :------- | :------------ |
| trading_pairs            | string   | 币对名称      |
| last_price               | string   | 最新成交价    |
| lowest_ask               | string   | 最佳卖价      |
| highest_bid              | string   | 最佳买价      |
| base_volume              | string   | 成交量        |
| quote_volume             | string   | 成交额        |
| price_change_percent_24h | string   | 24 小时涨幅   |
| highest_price_24h        | string   | 24 小时最高价 |
| lowest_price_24h         | string   | 24 小时最低价 |
| base_currency            | string   | 交易币种      |
| quote_currency           | string   | 支付币种      |

## 交易对摘要

> 请求示例

```shell
curl --request GET 'https://api.fameex.com/v2/public/ticker'
```

> 响应

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

### HTTP 请求

GET `/v2/public/ticker`

### 请求参数

无

### 响应参数

| 参数         | 数据类型 | 说明       |
| :----------- | :------- | :--------- |
| base_id      | string   | 币对名称   |
| quote_id     | string   | 最新成交价 |
| last_price   | string   | 最佳卖价   |
| quote_volume | string   | 最佳买价   |
| base_volume  | string   | 成交量     |
| isFrozen     | string   | 是否启用   |

## 深度信息

> 请求示例

```shell
curl --request GET 'https://api.fameex.com/v2/public/orderbook/market_pair?market_pair=BTC_USDT&level=3&depth=100'
```

> 响应

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

### HTTP 请求

GET `/v2/public/orderbook/market_pair`

### 请求参数

| 参数        | 是否必须 | 数据类型 | 说明               |
| :---------- | :------- | :------- | :----------------- |
| market_pair | YES      | string   | 示例例: "BTC_USDT" |
| level       | NO       | int      | 示例例: 3          |
| depth       | NO       | int      | 示例例: 100        |

### 响应参数

| 参数      | 数据类型 | 说明       |
| :-------- | :------- | :--------- |
| timestamp | int      | 服务器时间 |
| bids      | string   | 买         |
| asks      | string   | 卖         |

## 订单查询

> 请求示例

```shell
curl --request GET 'https://api.fameex.com/v2/public/trades/market_pair?market_pair=BTC_USDT'
```

> 响应

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

### HTTP 请求

GET `/v2/public/trades/market_pair`

### 请求参数

| 参数        | 是否必须 | 数据类型 | 说明               |
| :---------- | :------- | :------- | :----------------- |
| market_pair | YES      | string   | 示例例: "BTC_USDT" |

### 响应参数

| 参数         | 数据类型 | 说明            |
| :----------- | :------- | :-------------- |
| trade_id     | int      | 订单 id         |
| price        | string   | 最新成交价      |
| base_volume  | string   | volume          |
| quote_volume | string   | price \* volume |
| timestamp    | string   | 服务器时间      |
| type         | string   | 买/卖           |

## 最新价格

### HTTP 请求

GET `/api/v2/ticker/price`

> 请求示例

```shell
curl --request GET 'https://api.fameex.com/api/v2/ticker/price'
```

> 响应

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

### 请求参数

| 参数   | 是否必须 | 数据类型 | 说明               |
| ------ | -------- | -------- | ------------------ |
| symbol | NO       | string   | 示例例: "BTC-USDT" |

### 响应参数

| 参数         | 数据类型 | 说明       |
| :----------- | :------- | :--------- |
| last_price   | string   | 最新成交价 |
| base_volume  | string   | 成交量     |
| quote_volume | string   | 成交额     |

# 币币交易 API 接口

## 币币下单

限速规则：100 次/2s

**功能说明：**

此接口提供撤销指定的某一种或多种币对的所有未成交订单的功能。

**请求路径：**

/v1/api/spot/orders

curl `https://api.fameex.com/v1/api/spot/orders`

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型 | 说明                                                      |
| ------------ | -------- | -------- | --------------------------------------------------------- |
| symbol       | 是       | string   | 币对名称 例如:"BTC-USDT"                                  |
| clientOid    | 否       | string   | 用户自编委托单 ID                                         |
| side         | 是       | int      | 委托方向 1-买 2-卖                                        |
| orderType    | 是       | int      | 委托类型 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker |
| price        | 否       | string   | 委托价格                                                  |
| amount       | 是       | string   | 委托数量(市价买时为交易额)                                |
| triggerPrice | 否       | string   | 触发价格                                                  |
| backRatio    | 否       | string   | 跟踪委托的回调比例                                        |

> **返回示例：**

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

### 响应参数

| 字段名称  | 数据类型 | 说明              |
| --------- | -------- | ----------------- |
| code      | int      | 200, 正常         |
| msg       | string   | 信息说明          |
| data      | object   | 委托单信息        |
| orderId   | string   | 委托单 ID         |
| clientOid | string   | 用户自编委托单 ID |

## 币币撤单

限速规则：100 次/2s

**功能说明：**

此接口提供将未成交的订单撤销的功能。

**请求路径：**

/v1/api/spot/cancel_orders

curl `https://api.fameex.com/v1/api/spot/cancel_orders`

**路由参数：**

无

**Post 参数：**

| 参数      | 是否必须 | 数据类型 | 说明                                                         |
| --------- | -------- | -------- | ------------------------------------------------------------ |
| symbol    | 是       | string   | 币对名称 例如:"BTC-USDT"                                     |
| orderid   | 否       | string   | 委托单 ID(orderId 和 clientOid 必须且只能选一个填写)         |
| clientOid | 否       | string   | 用户自编委托单 ID(orderId 和 clientOid 必须且只能选一个填写) |

> **返回示例：**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "orderId": "10383992916667793408"
  }
}
```

### 响应参数

| 字段名称  | 数据类型 | 说明              |
| --------- | -------- | ----------------- |
| code      | int      | 200, 正常         |
| msg       | string   | 说明              |
| data      | object   | 返回委托单信息    |
| orderId   | string   | 委托单 ID         |
| clientOid | string   | 用户自编委托单 ID |

## 币币批量撤单

限速规则：100 次/2s

**功能说明：**

此接口提供撤销指定的某一种或多种币对的所有未成交订单的功能。

**请求路径：**

/v1/api/spot/cancel_orders_all

curl `https://api.fameex.com/v1/api/spot/cancel_orders_all`

**路由参数：**

无

**Post 参数：**

| 参数       | 是否必须 | 数据类型 | 说明                                                              |
| ---------- | -------- | -------- | ----------------------------------------------------------------- |
| symbol     | 是       | string   | 币对名称 例如:"BTC-USDT"                                          |

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

### 响应参数

| 字段名称  | 数据类型     | 说明              |
| --------- | ------------ | ----------------- |
| code      | int          | 200,正常          |
| msg       | string       | 说明              |
| data      | object array | 批量撤单详情      |
| code      | array        | 批量撤单详情      |
| orderId   | string       | 委托单 ID         |
| clientOid | string       | 用户自编委托单 ID |

## 获取委托单详情

限速规则：20 次/2s

**功能说明：**

此接口通过订单 ID 获取指定委托单信息。

**请求路径：**

/v1/api/spot/orderdetail

curl `https://api.fameex.com/v1/api/spot/orderdetail`

**路由参数：**

无

**Post 参数：**

| 参数      | 是否必须 | 数据类型 | 说明                                                         |
| --------- | -------- | -------- | ------------------------------------------------------------ |
| symbol    | 是       | string   | 币对名称,例如“BTC-USDT”                                      |
| orderId   | 否       | string   | 委托单 ID(orderId 和 clientOid 必须且只能选一个填写)         |
| clientOid | 否       | string   | 用户自编委托单 ID(orderId 和 clientOid 必须且只能选一个填写) |

> **返回示例：**

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

### 响应参数

| 字段名称        | 数据类型 | 说明                                                                         |
| --------------- | -------- | ---------------------------------------------------------------------------- |
| code            | int      | 返回值状态                                                                   |
| msg             | string   | 返回值描述                                                                   |
| data            | object   | 返回值,订单详情                                                              |
| orderId         | string   | 委托单 ID                                                                    |
| clientOid       | string   | 用户自编委托单 ID                                                            |
| symbol          | string   | 币对名称（例:BTC-USDT）                                                      |
| side            | int      | 委托方向 1-买 2-卖                                                           |
| orderType       | int      | 委托类型 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker                    |
| price           | string   | 委托价格                                                                     |
| amount          | string   | 委托数量                                                                     |
| money           | string   | 委托金额(市价买时)                                                           |
| filledAmount    | string   | 已成交数量                                                                   |
| filledMoney     | string   | 已成交金额                                                                   |
| filledFee       | string   | 已成交手续费                                                                 |
| feeCurrency     | string   | 手续费币种                                                                   |
| triggerPrice    | string   | 委托单触发价                                                                 |
| triggerType     | string   | 委托单触发类型 gte-大于等于 lte-小于等于                                     |
| triggerState    | int      | 触发状态 1-触发成功                                                          |
| liquidationType | int      | 强平类型 1-爆仓 2-减仓 3-止盈减仓                                            |
| strategyId      | string   | 策略 Id                                                                      |
| strategyType    | int      | 策略类型                                                                     |
| strategyName    | string   | 订策略名称                                                                   |
| state           | int      | 委托单状态 1-已创建 2-等待成交 3-部分成交 4-完全成交 5-部分成交撤销 6-已撤销 |
| accountType     | string   | 账户类型                                                                     |
| platform        | string   | 平台来源                                                                     |
| cancelType      | int      | 撤单类型 1-用户撤单 2-系统撤单 3-运营撤单 4-爆仓撤单 5-减仓撤单              |
| createTime      | int64    | 创建时间                                                                     |
| updateTime      | int64    | 状态更新时间                                                                 |

## 获取委托单列表

限速规则：20 次/2s

**功能说明：**

此接口获取列出您当前的委托单信息（最近 3 个月的委托单信息）。这个请求支持分页，并且按时间倒序排序和存储，最新的排在最前面。

**请求路径：**

POST /v1/api/spot/orderlist

curl `https://api.fameex.com/v1/api/spot/orderlist`

`headers参数`

无

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型  | 说明                                                          |
| ------------ | -------- | --------- | ------------------------------------------------------------- |
| base         | 否       | string    | 交易币(大写，例如“BTC”)                                       |
| quote        | 否       | string    | 计价币(大写，例如“USDT”)                                      |
| side         | 否       | int    | 委托方向 1-买 2-卖                                            |
| orderTypes   | 否       | int array | 委托类型列表 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker |
| state        | 是       | int       | 委托单状态 7-未完成 8-已完成 9-完全成交或部分成交撤销         |
| pageNum      | 是       | int       | 分页, 第几页(1<=pageNum)                                      |
| pageSize     | 是       | int       | 分页, 每页数量(1<=pageSize<= 500)                             |
| startTime    | 否       | int64     | 开始时间戳，秒                                                |
| endTime      | 否       | int64     | 结束时间戳，秒                                                |
| strategyId   | 否       | string    | 策略 Id                                                       |
| strategyType | 否       | int       | 策略类型                                                      |

> **返回示例：**

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

### 响应参数

| 字段名称        | 数据类型     | 说明                                                                         |
| --------------- | ------------ | ---------------------------------------------------------------------------- |
| code            | int          | 返回值状态                                                                   |
| msg             | string       | 返回值描述                                                                   |
| data            | object       | 返回值,订单详情                                                              |
| pageNum         | int          | 分页, 第几页(1<=pageNum)                                                     |
| pageSize        | int          | 分页, 每页数量(1<=pageSize<= 500)                                            |
| total           | int          | 总条数                                                                       |
| orders          | object array | 委托单列表                                                                   |
| orderId         | string       | 委托单 ID                                                                    |
| clientOid       | string       | 用户自编委托单 ID                                                            |
| symbol          | string       | 币对名称（例:BTC-USDT）                                                      |
| side            | int          | 委托方向 1-买 2-卖                                                           |
| orderType       | int          | 委托类型 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker                    |
| price           | string       | 委托价格                                                                     |
| amount          | string       | 委托数量                                                                     |
| money           | string       | 委托金额(市价买时)                                                           |
| filledAmount    | string       | 已成交数量                                                                   |
| filledMoney     | string       | 已成交金额                                                                   |
| filledFee       | string       | 已成交手续费                                                                 |
| feeCurrency     | string       | 手续费币种                                                                   |
| triggerPrice    | string       | 委托单触发价                                                                 |
| triggerType     | string       | 委托单触发类型 gte-大于等于 lte-小于等于                                     |
| triggerState    | int          | 触发状态 1-触发成功                                                          |
| liquidationType | int          | 强平类型 1-爆仓 2-减仓 3-止盈减仓                                            |
| strategyId      | string       | 策略 Id                                                                      |
| strategyType    | int          | 策略类型                                                                     |
| strategyName    | string       | 订策略名称                                                                   |
| state           | int          | 委托单状态 1-已创建 2-等待成交 3-部分成交 4-完全成交 5-部分成交撤销 6-已撤销 |
| accountType     | string       | 账户类型                                                                     |
| platform        | string       | 平台来源                                                                     |
| cancelType      | int          | 撤单类型 1-用户撤单 2-系统撤单 3-运营撤单 4-爆仓撤单 5-减仓撤单              |
| createTime      | int64        | 创建时间                                                                     |
| updateTime      | int64        | 状态更新时间                                                                 |

## 获取成交明细

限速规则：20 次/2s

**功能说明：**

此接口获取您当前所有的成交订单信息。这个请求支持分页，并且按时间倒序排序和存储，最新的排在最前面。

**请求路径：**

/v1/api/spot/fills

curl `https://api.fameex.com/v1/api/spot/fills`

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型  | 说明                                                          |
| ------------ | -------- | --------- | ------------------------------------------------------------- |
| base         | 否       | string    | 交易币(大写，例如“BTC”)                                       |
| quote        | 否       | string    | 计价币(大写，例如“USDT”)                                      |
| orderId      | 否       | string    | 委托单 ID                                                     |
| side         | 否       | int       | 委托方向 1-买 2-卖                                            |
| orderTypes   | 否       | int array | 委托类型列表 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker |
| pageNum      | 是       | int       | 分页, 第几页(1<=pageNum)                                      |
| pageSize     | 是       | int       | 分页, 每页数量(1<=pageSize<= 500)                             |
| startTime    | 否       | int64     | 开始时间戳，秒                                                |
| endTime      | 否       | int64     | 结束时间戳，秒                                                |
| strategyId   | 否       | string    | 策略 Id                                                       |
| strategyType | 否       | int       | 策略类型                                                      |

> **返回示例：**

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

### 响应参数

| 字段名称        | 数据类型     | 说明                                                      |
| --------------- | ------------ | --------------------------------------------------------- |
| code            | int          | 返回值状态                                                |
| msg             | string       | 返回值描述                                                |
| data            | object       | 返回值,订单详情                                           |
| pageNum         | int          | 分页, 第几页(1<=pageNum)                                  |
| pageSize        | int          | 分页, 每页数量(1<=pageSize<= 500)                         |
| total           | int          | 总条数                                                    |
| trades          | object array | 委成交单列表                                              |
| orderId         | string       | 委托单 ID                                                 |
| tradeId         | string       | 成交单 ID                                                 |
| symbol          | string       | 币对名称（例:BTC-USDT）                                   |
| side            | int          | 委托方向 1-买 2-卖                                        |
| orderType       | int          | 委托类型 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker |
| price           | string       | 委托价格                                                  |
| amount          | string       | 委托数量                                                  |
| feeRate         | string       | 实际手续费率                                              |
| feeCurrency     | string       | 手续费币种                                                |
| fee             | string       | 手续费                                                    |
| liquidationType | int          | 强平类型 1-爆仓 2-减仓 3-止盈减仓                         |
| strategyId      | string       | 策略 Id                                                   |
| strategyType    | int          | 策略类型                                                  |
| strategyName    | string       | 订策略名称                                                |
| accountType     | string       | 账户类型                                                  |
| platform        | string       | 平台来源                                                  |
| role            | string       | 角色类型 1-maker 2-taker                                  |
| selfTrade       | int          | 是否自成交 1-自成交                                       |
| createTime      | int64        | 创建时间                                                  |

## 获取所有未完成的订单

限速规则：20 次/2s

**功能说明：**

此接口获取您当前所有的成交订单信息。这个请求支持分页，并且按时间倒序排序和存储，最新的排在最前面。

**请求路径：**

/v1/api/orders_pending

curl `https://api.fameex.com /v1/api/orders_pending`

**路由参数：**

| 参数     | 是否必须 | 数据类型 | 说明                                   |
| -------- | -------- | -------- | -------------------------------------- |
| pairName | 是       | string   | 币对名称（例:BTC_USDT）                |
| pageNum  | 是       | string   | 分页使用, 第几页,从第一页开始          |
| pageSize | 是       | string   | 分页使用, 每页数量 (0< pageSize ≤ 500) |

**Post 参数：**

无

> **返回示例：**

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

### 响应参数

| 字段名称    | 数据类型 | 说明                         |
| ----------- | -------- | ---------------------------- |
| code        | int      | 返回值状态                   |
| msg         | string   | 返回值描述                   |
| data        | string   | 返回值,成交明细              |
| pairName    | string   | 币对名称（例:BTC_USDT）      |
| orderId     | string   | 订单编号                     |
| buyClass    | int      | 交易类型: 0 限价交易         |
| buyType     | int      | 买卖方向: 0 买, 1 卖         |
| price       | string   | 委托价格                     |
| count       | string   | 委托数量                     |
| dealedCount | string   | 已成交数量                   |
| dealedMoney | string   | 已成交金额                   |
| state       | int      | 1 未生效 2 未成交 3 部分成交 |
| time        | int64    | 时间（单位:纳秒）            |

# 钱包 API 接口

## 获取钱包账户信息

限速规则：20 次/2s

**功能说明：**

此接口获取钱包币币账户所有资产信息列表，查询各币种的余额、冻结和可用等信息。

**请求路径：**

/v1/api/account/wallet

curl `https://api.fameex.com/v1/api/account/wallet`

**路由参数：**

无

**Post 参数：**

无

> **返回示例：**

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

### 响应参数

| 字段名称   | 数据类型 | 说明                                             |
| ---------- | -------- | ------------------------------------------------ |
| code       | int      | 200, 正常                                        |
| data       | list     | 返回值,币币账户数据                              |
| userid     | string   | 用户 id                                          |
| walletType | string   | 账户类型:spot-现货账户 otc-法币账户 l2c-杠杆账户 |
| available  | string   | 可用余额                                         |
| total      | string   | 总余额                                           |
| currency   | string   | 币种 例:BTC                                      |
| hold       | string   | 冻结金额                                         |

## 获取钱包账户某币种详情

限速规则：20 次/2s

**功能说明：**

获取钱包账户详情（单一币种）

**请求路径：**

/v1/api/account/wallet/currency

curl `https://api.fameex.com/v1/api/account/wallet/currency`

**路由参数：**

| 参数     | 是否必须 | 数据类型 | 说明         |
| -------- | -------- | -------- | ------------ |
| currency | 是       | string   | 币种, 例 BTC |

**Post 参数：**

无

> **返回示例：**

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

### 响应参数

| 字段名称  | 数据类型 | 说明                            |
| --------- | -------- | ------------------------------- |
| code      | int      | 200, 正常                       |
| msg       | string   | 此次返回值说明                  |
| userid    | string   | 用户 id                         |
| data      | map      | 返回值,币币账户，某一币种的详情 |
| available | string   | 可用余额                        |
| hold      | string   | 冻结金额                        |

## 资金划转

限速规则：1 次/2s

**功能说明：**

此接口提供平台内现货钱包、法币钱包、杠杆钱包之间进行资金划转。【注：杠杆账户币对之间互相划转仅支持计价币之间的划转，例如从杠杆账户下的 BTC_USDT 将 USDT 划转至 ETH_USDT 币对下】

**请求路径：**

POST /v1/api/account/transfer

curl `https://api.fameex.com/v1/api/account/transfer`

**路由参数：**

无

**Post 参数：**

| 参数     | 是否必须 | 数据类型 | 说明                                                                 |
| -------- | -------- | -------- | -------------------------------------------------------------------- |
| currency | 是       | string   | 币种类型                                                             |
| amount   | 是       | string   | 数量                                                                 |
| from     | 是       | string   | 转出账户: spot 现货账户, otc 法币账户，l2c 杠杆账户，swap U 合约账户 |
| to       | 是       | string   | 转入账户: spot 现货账户, otc 法币账户，l2c 杠杆账户，swap U 合约账户 |
| fromPair | 否       | string   | 杠杆账户币对间互转时的转出币对，例:BTC_USDT                          |
| toPair   | 否       | string   | 杠杆账户币对间互转时的转入币对,例:ETH_USDT                           |

> **返回示例：**

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

### 响应参数

| 字段名称 | 数据类型 | 说明                   |
| -------- | -------- | ---------------------- |
| code     | int      | 200, 正常              |
| msg      | string   | success,正常           |
| data     | object   | 资金划转返回的响应对象 |
| orderid  | string   | 订单 id                |
| userid   | string   | 用户 id                |

## 获取现货账户交易账单

限速规则：20 次/2s

**功能说明：**

此接口查询现货账户交易账单。

**请求路径：**

POST /v1/api/spot/record/trade

curl `https://api.fameex.com/v1/api/spot/record/trade`

**路由参数：**

无

**Post 参数：**

| 参数      | 是否必须 | 数据类型 | 说明                                           |
| --------- | -------- | -------- | ---------------------------------------------- |
| tradeType | 否       | int      | 交易类型：0.全部；2.买入；3.卖出；4.实收手续费 |
| currency  | 否       | string   | 币种名称 例:ETH                                |
| pageNum   | 是       | int      | 第几页，1 开始                                 |
| pageSize  | 是       | int      | 每页数量 (0 < pageSize ≤ 500)                  |
| startTime | 否       | int64    | 开始时间 秒 最多查询最近 90 天内的记录         |
| endTime   | 否       | int64    | 结束时间 秒                                    |

> **返回示例：**

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

### 响应参数

| 字段名称    | 数据类型 | 说明                                   |
| ----------- | -------- | -------------------------------------- |
| code        | int      | 200, 正常                              |
| msg         | string   | success,正常                           |
| data        | object   | 空字符串                               |
| userId      | string   | 用户 id                                |
| total       | int      | 账单记录数量                           |
| list        | array    | 账单记录列表                           |
| tradeType   | int      | 交易类型：2.买入；3.卖出；4.实收手续费 |
| operateTime | int64    | 操作时间                               |
| currency    | string   | 币种名称 例:ETH                        |
| amount      | string   | 数量                                   |

## 获取现货账户充提账单

限速规则：20 次/2s

**功能说明：**

此接口查询现货账户充提账单。

**请求路径：**

POST /v1/api/spot/record/chargewithdraw

curl `https://api.fameex.com/v1/api/spot/record/chargewithdraw`

**路由参数：**

无

**Post 参数：**

| 参数      | 是否必须 | 数据类型 | 说明                             |
| --------- | -------- | -------- | -------------------------------- |
| tradeType | 否       | int      | 交易类型：0.全部；1.提币；2.充币 |
| currency  | 否       | string   | 币种名称 例:ETH                  |
| startTime | 否       | int64    | 开始时间：秒级时间戳             |
| endTime   | 否       | int64    | 结束时间时间：秒级时间戳         |
| pageNum   | 是       | int      | 页码，从 1 开始                  |
| pageSize  | 是       | int      | 每页数量 (0 < pageSize ≤ 500)    |

> **返回示例：**

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

### 响应参数

| 字段名称    | 数据类型 | 说明                                                                                                                                                                                         |
| ----------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| code        | int      | 200, 正常                                                                                                                                                                                    |
| msg         | string   | success,正常                                                                                                                                                                                 |
| data        | object   | 空字符串                                                                                                                                                                                     |
| total       | int      | 账单记录数量                                                                                                                                                                                 |
| list        | array    | 账单记录列表                                                                                                                                                                                 |
| tradeType   | int      | 交易类型：1.提币；2.充币                                                                                                                                                                     |
| operateTime | int64    | 操作时间                                                                                                                                                                                     |
| currency    | string   | 币种名称 例:ETH                                                                                                                                                                              |
| amount      | string   | 数量                                                                                                                                                                                         |
| address     | string   | 当 tradeType 为 1 时，代表提币地址；tradeType 为 2 时，代表充币地址                                                                                                                          |
| fee         | string   | 提币手续费                                                                                                                                                                                   |
| label       | string   | 用户的标签                                                                                                                                                                                   |
| chainType   | string   | 币种的链类型                                                                                                                                                                                 |
| state       | int      | 账单状态:<br> 当 tradeType 为 1 时, state 分别代表: 1-待审核; 2-审核中; 3-已完成; 4-审核失败; 5-已撤单; 6-提币失败; 7-初始化创建; 8-确认中<br>当 tradeType 为 2 时, state 分别代表: 1-已完成 |
| txId        | string   | 交易哈希                                                                                                                                                                                     |

## 获取现货账户划转账单

限速规则：20 次/2s

**功能说明：**

此接口查询现货账户划转账单。

**请求路径：**

POST /v1/api/spot/record/trans

curl `https://api.fameex.com/v1/api/spot/record/trans`

`**路由参数：**

无

**Post 参数：**

| 参数      | 是否必须 | 数据类型 | 说明                             |
| --------- | -------- | -------- | -------------------------------- |
| tradeType | 否       | int      | 交易类型：0.全部；1.转入；2.转出 |
| currency  | 否       | string   | 币种名称 例:ETH                  |
| startTime | 否       | int64    | 开始时间：秒级时间戳             |
| endTime   | 否       | int64    | 结束时间时间：秒级时间戳         |
| pageNum   | 是       | int      | 页码，从 1 开始                  |
| pageSize  | 是       | int      | 每页数量 (0 < pageSize ≤ 500)    |

> **返回示例：**

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

### 响应参数

| 字段名称     | 数据类型 | 说明                             |
| ------------ | -------- | -------------------------------- |
| code         | int      | 200, 正常                        |
| msg          | string   | success,正常                     |
| data         | object   | 空字符串                         |
| userId       | string   | 用户 id                          |
| total        | int      | 账单记录数量                     |
| list         | array    | 账单记录列表                     |
| tradeType    | int      | 交易类型：1.转入；2.转出         |
| operateTime  | int64    | 操作时间                         |
| currency     | string   | 币种名称 例:ETH                  |
| amount       | string   | 数量                             |
| fromCoinPair | string   | 转入币对                         |
| toCoinPair   | string   | 转出币对                         |
| fromAccount  | string   | 转出账户：0.现货；1.杠杆；3.法币 |
| toAccount    | string   | 转入账户：0.现货；1.杠杆；3.法币 |

## 获取现货账户其他账单

限速规则：20 次/2s

**功能说明：**

此接口查询现货账户其他账单，包括返佣及活动。

**请求路径：**

POST /v1/api/spot/record/others

curl `https://api.fameex.com/v1/api/spot/record/others`

**路由参数：**

无

**Post 参数：**

| 参数      | 是否必须 | 数据类型 | 说明                             |
| --------- | -------- | -------- | -------------------------------- |
| tradeType | 否       | int      | 交易类型：0.全部；1.返佣；2.活动 |
| currency  | 否       | string   | 币种名称 例:ETH                  |
| startTime | 否       | int64    | 开始时间：秒级时间戳             |
| endTime   | 否       | int64    | 结束时间时间：秒级时间戳         |
| pageNum   | 是       | int      | 页码，从 1 开始                  |
| pageSize  | 是       | int      | 每页数量 (0 < pageSize ≤ 500)    |

> **返回示例：**

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

### 响应参数

| 字段名称    | 数据类型 | 说明                     |
| ----------- | -------- | ------------------------ |
| code        | int      | 200, 正常                |
| msg         | string   | success,正常             |
| data        | object   | 空字符串                 |
| userId      | string   | 用户 id                  |
| total       | int      | 账单记录数量             |
| list        | array    | 账单记录列表             |
| tradeType   | int      | 交易类型：1.返佣；2.活动 |
| operateTime | int64    | 操作时间：秒级时间戳     |
| currency    | string   | 币种名称 例:ETH          |
| amount      | string   | 数量                     |

## 获取充币地址

限速规则：20 次/2s

**功能说明：**

此接口获取各个币种的充币地址。

**请求路径：**

/v1/api/account/deposit/address

curl `https://api.fameex.com/v1/api/account/deposit/address`

**路由参数：**

| 参数      | 是否必须 | 数据类型 | 说明          |
| --------- | -------- | -------- | ------------- |
| coinType  | 是       | string   | 币种类型 USDT |
| chainType | 是       | string   | 链类型 ERC20  |

**Post 参数：**

无

> **返回示例：**

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

### 响应参数

| 字段名称 | 数据类型 | 说明      |
| -------- | -------- | --------- |
| code     | int      | 200, 正常 |
| request  | map      | 请求参数  |
| userId   | string   | 用户 id   |
| coinType | string   | 币种      |
| address  | string   | 地址      |

## 获取杠杆账户信息

限速规则：1 次/2s

**功能说明：**

此接口获取杠杆账户所有资产信息列表，查询各币种的余额、冻结和可用等信息。

**请求路径：**

/v1/api/lever/accounts

curl `https://api.fameex.com/v1/api/lever/accounts`

**路由参数：**

无

**Post 参数：**

无

> **返回示例：**

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

### 响应参数

| 字段名称       | 数据类型 | 说明                                             |
| -------------- | -------- | ------------------------------------------------ |
| code           | int      | 200, 正常                                        |
| data           | list     | 返回值,杠杆账户数据                              |
| userid         | string   | 用户 id                                          |
| walletType     | string   | 账户类型:spot-币币账户 otc-法币账户 l2c-杠杆账户 |
| coinpair       | string   | 币对名称 例:BTC/USDT                             |
| baseCurrency   | string   | 交易币名称 例:BTC                                |
| quoteCurrency  | string   | 计价币名称 例:USDT                               |
| baseAvailable  | string   | 交易币可用金额                                   |
| quoteAvailable | string   | 计价币可用金额                                   |
| baseHold       | string   | 交易币冻结金额                                   |
| quoteHold      | string   | 计价币冻结金额                                   |
| baseTotal      | string   | 交易币总额                                       |
| quoteTotal     | string   | 计价币总额                                       |
| baseBorrowed   | string   | 交易币借币金额                                   |
| quoteBorrowed  | string   | 计价币借币金额                                   |
| baseInterest   | string   | 交易币利息                                       |
| quoteInterest  | string   | 计价币利息                                       |

# 杠杆交易 API 接口

## 获取杠杆账户下某币对详情

限速规则：1 次/2s

**功能说明：**

获取杠杆账户下某币对账户余额、冻结和可用等信息

**请求路径：**

/v1/api/lever/accounts

curl `https://api.fameex.com/v1/api/lever/accounts`

**路由参数：**

| 参数     | 是否必须 | 数据类型 | 说明              |
| -------- | -------- | -------- | ----------------- |
| pairName | 是       | string   | 币对, 例 BTC_USDT |

**Post 参数：**

无

> **返回示例：**

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

### 响应参数

| 字段名称       | 数据类型 | 说明                 |
| -------------- | -------- | -------------------- |
| code           | int      | 200, 正常            |
| data           | list     | 返回值,杠杆账户数据  |
| msg            | string   | code 响应信息        |
| userid         | string   | 用户 id              |
| coinpair       | string   | 币对名称 例:BTC/USDT |
| baseCurrency   | string   | 交易币名称 例:BTC    |
| quoteCurrency  | string   | 计价币名称 例:USDT   |
| baseAvailable  | string   | 交易币可用金额       |
| quoteAvailable | string   | 计价币可用金额       |
| baseHold       | string   | 交易币冻结金额       |
| quoteHold      | string   | 计价币冻结金额       |
| baseTotal      | string   | 交易币总额           |
| quoteTotal     | string   | 计价币总额           |
| baseBorrowed   | string   | 交易币借币金额       |
| quoteBorrowed  | string   | 计价币借币金额       |
| baseInterest   | string   | 交易币利息           |
| quoteInterest  | string   | 计价币利息           |
| burstPrice     | string   | 爆仓价               |
| riskRate       | string   | 爆仓风险率           |

## 杠杆下单

限速规则：1 次/2s

**功能说明：**

此接口提供杠杆下单功能。

**请求路径：**

/v1/api/lever/orders/place

curl `https://api.fameex.com/v1/api/lever/orders/place`

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型 | 说明                                                      |
| ------------ | -------- | -------- | --------------------------------------------------------- |
| symbol       | 是       | string   | 币对名称 例如:"BTC-USDT"                                  |
| clientOid    | 否       | string   | 用户自编委托单 ID                                         |
| side         | 是       | int      | 委托方向 1-买 2-卖                                        |
| orderType    | 是       | int      | 委托类型 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker |
| price        | 否       | string   | 委托价格                                                  |
| amount       | 是       | string   | 委托数量(市价买时为交易额)                                |
| triggerPrice | 否       | string   | 触发价格                                                  |
| backRatio    | 否       | string   | 跟踪委托的回调比例                                        |

> **返回示例：**

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

### 响应参数

| 字段名称  | 数据类型 | 说明              |
| --------- | -------- | ----------------- |
| code      | int      | 200, 正常         |
| msg       | string   | 信息说明          |
| data      | object   | 委托单信息        |
| orderId   | string   | 委托单 ID         |
| clientOid | string   | 用户自编委托单 ID |

## 杠杆撤单

限速规则：1 次/2s

**功能说明：**

此接口提供将未成交的杠杆订单撤销的功能。

**请求路径：**

/v1/api/lever/orders/cancel

curl `https://api.fameex.com/v1/api/lever/orders/cancel`

**路由参数：**

无

**Post 参数：**

| 参数      | 是否必须 | 数据类型 | 说明                                                         |
| --------- | -------- | -------- | ------------------------------------------------------------ |
| symbol    | 是       | string   | 币对名称 例如:"BTC-USDT"                                     |
| orderid   | 否       | string   | 委托单 ID(orderId 和 clientOid 必须且只能选一个填写)         |
| clientOid | 否       | string   | 用户自编委托单 ID(orderId 和 clientOid 必须且只能选一个填写) |

> **返回示例：**

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "orderId": "10383992916667793408"
  }
}
```

### 响应参数

| 字段名称  | 数据类型 | 说明              |
| --------- | -------- | ----------------- |
| code      | int      | 200, 正常         |
| msg       | string   | 说明              |
| data      | object   | 返回委托单信息    |
| orderId   | string   | 委托单 ID         |
| clientOid | string   | 用户自编委托单 ID |

## 杠杆批量撤单

限速规则：1 次/2s

**功能说明：**

此接口提供撤销指定的某一种或多种币对的所有未成交的杠杆订单的功能。

**请求路径：**

/v1/api/lever/orders/batch_cancel

curl `https://api.fameex.com/v1/api/lever/orders/batch_cancel`

**路由参数：**

无

**Post 参数：**

| 参数       | 是否必须 | 数据类型 | 说明                                                              |
| ---------- | -------- | -------- | ----------------------------------------------------------------- |
| symbol     | 是       | string   | 币对名称 例如:"BTC-USDT"                                          |
| orderIds   | 否       | array    | 委托单 ID 列表(orderId 和 clientOid 必须且只能选一个填写)         |
| clientOids | 否       | array    | 用户自编委托单 ID 列表(orderId 和 clientOid 必须且只能选一个填写) |

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

### 响应参数

| 字段名称  | 数据类型     | 说明              |
| --------- | ------------ | ----------------- |
| code      | int          | 200,正常          |
| msg       | string       | 说明              |
| data      | object array | 批量撤单详情      |
| code      | array        | 批量撤单详情      |
| orderId   | string       | 委托单 ID         |
| clientOid | string       | 用户自编委托单 ID |

## 获取杠杆委托单列表

限速规则：1 次/2s

**功能说明：**

列出您当前的委托单信息（最近 3 个月的委托单信息）。这个请求支持分页，并且按时间倒序排序和存储，最新的排在最前面。

**请求路径：**

/v1/api/lever/orders

curl `https://api.fameex.com/v1/api/lever/orders`

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型  | 说明                                                          |
| ------------ | -------- | --------- | ------------------------------------------------------------- |
| base         | 是       | string    | 交易币(大写，例如“BTC”)                                       |
| quote        | 是       | string    | 计价币(大写，例如“USDT”)                                      |
| side         | 是       | string    | 委托方向 1-买 2-卖                                            |
| orderTypes   | 是       | int array | 委托类型列表 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker |
| state        | 是       | string    | 委托单状态 7-未完成 8-已完成 9-完全成交或部分成交撤销         |
| pageNum      | 否       | string    | 分页, 第几页(1<=pageNum)                                      |
| pageSize     | 否       | string    | 分页, 每页数量(1<=pageSize<= 500)                             |
| startTime    | 是       | string    | 开始时间戳，秒                                                |
| endTime      | 是       | string    | 结束时间戳，秒                                                |
| strategyId   | 否       | string    | 策略 Id                                                       |
| strategyType | 否       | string    | 策略类型                                                      |

> **返回示例：**

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

### 响应参数

| 字段名称        | 数据类型     | 说明                                                                         |
| --------------- | ------------ | ---------------------------------------------------------------------------- |
| code            | int          | 返回值状态                                                                   |
| msg             | string       | 返回值描述                                                                   |
| data            | object       | 返回值,订单详情                                                              |
| pageNum         | int          | 分页, 第几页(1<=pageNum)                                                     |
| pageSize        | int          | 分页, 每页数量(1<=pageSize<= 500)                                            |
| total           | int          | 总条数                                                                       |
| orders          | object array | 委托单列表                                                                   |
| orderId         | string       | 委托单 ID                                                                    |
| clientOid       | string       | 用户自编委托单 ID                                                            |
| symbol          | string       | 币对名称（例:BTC-USDT）                                                      |
| side            | int          | 委托方向 1-买 2-卖                                                           |
| orderType       | int          | 委托类型 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker                    |
| price           | string       | 委托价格                                                                     |
| amount          | string       | 委托数量                                                                     |
| money           | string       | 委托金额(市价买时)                                                           |
| filledAmount    | string       | 已成交数量                                                                   |
| filledMoney     | string       | 已成交金额                                                                   |
| filledFee       | string       | 已成交手续费                                                                 |
| feeCurrency     | string       | 手续费币种                                                                   |
| triggerPrice    | string       | 委托单触发价                                                                 |
| triggerType     | string       | 委托单触发类型 gte-大于等于 lte-小于等于                                     |
| triggerState    | int          | 触发状态 1-触发成功                                                          |
| liquidationType | int          | 强平类型 1-爆仓 2-减仓 3-止盈减仓                                            |
| strategyId      | string       | 策略 Id                                                                      |
| strategyType    | int          | 策略类型                                                                     |
| strategyName    | string       | 订策略名称                                                                   |
| state           | int          | 委托单状态 1-已创建 2-等待成交 3-部分成交 4-完全成交 5-部分成交撤销 6-已撤销 |
| accountType     | string       | 账户类型                                                                     |
| platform        | string       | 平台来源                                                                     |
| cancelType      | int          | 撤单类型 1-用户撤单 2-系统撤单 3-运营撤单 4-爆仓撤单 5-减仓撤单              |
| createTime      | int64        | 创建时间                                                                     |
| updateTime      | int64        | 状态更新时间                                                                 |

### 响应参数

| 字段名称       | 数据类型 | 说明                                                                                                          |
| -------------- | -------- | ------------------------------------------------------------------------------------------------------------- |
| code           | int      | 返回值状态                                                                                                    |
| msg            | string   | 返回值描述                                                                                                    |
| data           | string   | 返回值,订单列表                                                                                               |
| id             | int64    | 数据编号                                                                                                      |
| orderId        | string   | 委托单 id                                                                                                     |
| userId         | string   | 用户 id                                                                                                       |
| userType       | int      | 用户类型 1 普通用户 2 api 用户                                                                                |
| userLevel      | int      | 用户等级                                                                                                      |
| base           | string   | 交易对中的交易币种                                                                                            |
| quote          | string   | 交易对中的计价币种                                                                                            |
| buyType        | int      | 0 买 1 卖                                                                                                     |
| buyClass       | int      | 0 限价单                                                                                                      |
| state          | int      | 订单状态 1-待撮合 4-taker 完全成交 7-在深度队列 8-taker 部分成交 9-maker 部分成交 10-maker 完全成交 11-已撤销 |
| price          | string   | 委托单价                                                                                                      |
| totalPrice     | string   | 初始委托价格                                                                                                  |
| count          | string   | 未成交数量                                                                                                    |
| lossPrice      | string   | 止盈止损触发价                                                                                                |
| totalCount     | string   | 总数量                                                                                                        |
| dealedCount    | string   | 已成交数量                                                                                                    |
| dealedMoney    | string   | 累计成交额                                                                                                    |
| priceAvg       | string   | 成交均价                                                                                                      |
| triggerGreater | bool     | 是否大于等于止盈止损触发价                                                                                    |
| matchCount     | int      | 匹配次数                                                                                                      |
| createTime     | int64    | 订单创建时间 单位：纳秒                                                                                       |
| endTime        | int64    | 订单最后的更新时间 单位：纳秒                                                                                 |
| isErr          | int      | 0 正常委托单 其他为解锁资产失败的委托单                                                                       |
| triggered      | int      | 止盈止损是否触发 0 未触发 1 已触发                                                                            |
| accountFlag    | int      | 订单类型：1.普通杠杆订单；2.杠杆爆仓                                                                          |
| detail         | object   | 详情                                                                                                          |

## 获取杠杆委托单详情

限速规则：1 次/2s

**功能说明：**

此接口通过订单 ID 获取指定委托单信息。

**请求路径：**

/v1/api/lever/orders/detail

curl `https://api.fameex.com/v1/api/lever/orders/detail`

**路由参数：**

无

**Post 参数：**

| 参数      | 是否必须 | 数据类型 | 说明                                                         |
| --------- | -------- | -------- | ------------------------------------------------------------ |
| symbol    | 是       | string   | 币对名称,例如“BTC-USDT”                                      |
| orderId   | 否       | string   | 委托单 ID(orderId 和 clientOid 必须且只能选一个填写)         |
| clientOid | 否       | string   | 用户自编委托单 ID(orderId 和 clientOid 必须且只能选一个填写) |

> **返回示例：**

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

### 响应参数

| 字段名称        | 数据类型 | 说明                                                                         |
| --------------- | -------- | ---------------------------------------------------------------------------- |
| code            | int      | 返回值状态                                                                   |
| msg             | string   | 返回值描述                                                                   |
| data            | object   | 返回值,订单详情                                                              |
| orderId         | string   | 委托单 ID                                                                    |
| clientOid       | string   | 用户自编委托单 ID                                                            |
| symbol          | string   | 币对名称（例:BTC-USDT）                                                      |
| side            | int      | 委托方向 1-买 2-卖                                                           |
| orderType       | int      | 委托类型 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker                    |
| price           | string   | 委托价格                                                                     |
| amount          | string   | 委托数量                                                                     |
| money           | string   | 委托金额(市价买时)                                                           |
| filledAmount    | string   | 已成交数量                                                                   |
| filledMoney     | string   | 已成交金额                                                                   |
| filledFee       | string   | 已成交手续费                                                                 |
| feeCurrency     | string   | 手续费币种                                                                   |
| triggerPrice    | string   | 委托单触发价                                                                 |
| triggerType     | string   | 委托单触发类型 gte-大于等于 lte-小于等于                                     |
| triggerState    | int      | 触发状态 1-触发成功                                                          |
| liquidationType | int      | 强平类型 1-爆仓 2-减仓 3-止盈减仓                                            |
| strategyId      | string   | 策略 Id                                                                      |
| strategyType    | int      | 策略类型                                                                     |
| strategyName    | string   | 订策略名称                                                                   |
| state           | int      | 委托单状态 1-已创建 2-等待成交 3-部分成交 4-完全成交 5-部分成交撤销 6-已撤销 |
| accountType     | string   | 账户类型                                                                     |
| platform        | string   | 平台来源                                                                     |
| cancelType      | int      | 撤单类型 1-用户撤单 2-系统撤单 3-运营撤单 4-爆仓撤单 5-减仓撤单              |
| createTime      | int64    | 创建时间                                                                     |
| updateTime      | int64    | 状态更新时间                                                                 |

### 响应参数

| 字段名称    | 数据类型 | 说明                                                                                         |
| ----------- | -------- | -------------------------------------------------------------------------------------------- |
| code        | int      | 返回值状态                                                                                   |
| msg         | string   | 返回值描述                                                                                   |
| data        | string   | 返回值,订单详情                                                                              |
| orderId     | string   | 撮合任务 id                                                                                  |
| pairName    | string   | 币对名称（例:BTC_USDT）                                                                      |
| buyType     | int      | 买卖方向 0-买 1-卖                                                                           |
| buyClass    | int      | 委托类型 0-限价 1-市价 2-止盈止损                                                            |
| state       | int      | 订单状态 1-待撮合 4-taker 完全成交 7-在深度队列 9-maker 部分成交 10-maker 完全成交 11-已撤销 |
| price       | string   | 挂单单价                                                                                     |
| count       | string   | 未成交数量                                                                                   |
| lossPrice   | string   | 止盈止损触发价                                                                               |
| totalCount  | string   | 总挂单数量                                                                                   |
| dealedCount | string   | 已成交数量                                                                                   |
| dealedMoney | string   | 已成交金额                                                                                   |
| priceAvg    | string   | 成交均价                                                                                     |
| createTime  | int64    | 订单创建时间 纳秒                                                                            |
| endTime     | int64    | 订单状态最后更新时间 纳秒                                                                    |

## 获取杠杆成交明细

限速规则：1 次/2s

**功能说明：**

此接口获取您当前所有的成交订单信息。这个请求支持分页，并且按时间倒序排序和存储，最新的排在最前面。

**请求路径：**

/v1/api/lever/deals

curl `https://api.fameex.com/v1/api/lever/deals`

**路由参数：**

无

**Post 参数：**

| 参数         | 是否必须 | 数据类型  | 说明                                                          |
| ------------ | -------- | --------- | ------------------------------------------------------------- |
| base         | 否       | string    | 交易币(大写，例如“BTC”)                                       |
| quote        | 否       | string    | 计价币(大写，例如“USDT”)                                      |
| orderId      | 否       | string    | 委托单 ID                                                     |
| side         | 否       | int       | 委托方向 1-买 2-卖                                            |
| orderTypes   | 否       | int array | 委托类型列表 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker |
| pageNum      | 是       | int       | 分页, 第几页(1<=pageNum)                                      |
| pageSize     | 是       | int       | 分页, 每页数量(1<=pageSize<= 500)                             |
| startTime    | 否       | int64     | 开始时间戳，秒                                                |
| endTime      | 否       | int64     | 结束时间戳，秒                                                |
| strategyId   | 否       | string    | 策略 Id                                                       |
| strategyType | 否       | int       | 策略类型                                                      |

> **返回示例：**

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

### 响应参数

| 字段名称        | 数据类型     | 说明                                                      |
| --------------- | ------------ | --------------------------------------------------------- |
| code            | int          | 返回值状态                                                |
| msg             | string       | 返回值描述                                                |
| data            | object       | 返回值,订单详情                                           |
| pageNum         | int          | 分页, 第几页(1<=pageNum)                                  |
| pageSize        | int          | 分页, 每页数量(1<=pageSize<= 500)                         |
| total           | int          | 总条数                                                    |
| trades          | object array | 委成交单列表                                              |
| orderId         | string       | 委托单 ID                                                 |
| tradeId         | string       | 成交单 ID                                                 |
| symbol          | string       | 币对名称（例:BTC-USDT）                                   |
| side            | int          | 委托方向 1-买 2-卖                                        |
| orderType       | int          | 委托类型 1-限价 2-市价 3-止盈止损 4-跟踪委托 5-只做 Maker |
| price           | string       | 委托价格                                                  |
| amount          | string       | 委托数量                                                  |
| feeRate         | string       | 实际手续费率                                              |
| feeCurrency     | string       | 手续费币种                                                |
| fee             | string       | 手续费                                                    |
| liquidationType | int          | 强平类型 1-爆仓 2-减仓 3-止盈减仓                         |
| strategyId      | string       | 策略 Id                                                   |
| strategyType    | int          | 策略类型                                                  |
| strategyName    | string       | 订策略名称                                                |
| accountType     | string       | 账户类型                                                  |
| platform        | string       | 平台来源                                                  |
| role            | string       | 角色类型 1-maker 2-taker                                  |
| selfTrade       | int          | 是否自成交 1-自成交                                       |
| createTime      | int64        | 创建时间                                                  |

### 响应参数

| 字段名称      | 数据类型 | 说明                             |
| ------------- | -------- | -------------------------------- |
| code          | int      | 返回值状态                       |
| msg           | string   | 返回值描述                       |
| data          | string   | 返回值,成交明细                  |
| pairName      | string   | 币对名称（例：BTC_USDT）         |
| base          | string   | 交易币                           |
| quote         | string   | 计价币                           |
| orderId       | string   | 委托单 id                        |
| time          | int64    | 成交时间 纳秒                    |
| buyClass      | int      | 交易类型: 0 限价交易             |
| buyType       | int      | 买卖方向: 0 买, 1 卖             |
| price         | string   | 成交价格                         |
| count         | string   | 成交数量                         |
| fee           | string   | 手续费                           |
| feeRate       | string   | 实际手续费费率                   |
| originFeeRate | string   | 原始手续费费率                   |
| accountFlag   | int      | 类型：1.普通杠杆订单；2.杠杆爆仓 |

## 获取杠杆配置

限速规则：1 次/2s

**功能说明：**

此接口获取钱包杠杆账户下币对配置信息。

**请求路径：**

/v1/api/lever/pair/config

curl `https://api.fameex.com/v1/api/lever/pair/config`

**路由参数：**

无

**Post 参数：**

| 参数     | 是否必须 | 数据类型 | 说明                 |
| -------- | -------- | -------- | -------------------- |
| pairName | 否       | string   | 币对名称 例:ETH_USDT |

> **返回示例：**

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

### 响应参数

| 字段名称                 | 数据类型 | 说明                |
| ------------------------ | -------- | ------------------- |
| code                     | int      | 200, 正常           |
| msg                      | string   | success,正常        |
| data                     | array    | 返回值,杠杆配置信息 |
| coinPair                 | string   | 币对名称            |
| leverMultiple            | string   | 杠杆倍数            |
| quoteLeatestBorrowAmount | string   | 计价币最少借币金额  |
| borrowFeeRate            | string   | 借币费率            |
| quoteMostBorrowAmount    | string   | 计价币单日最大可借  |
| baseMostBorrowAmount     | string   | 交易币单日最大可借  |

## 获取杠杆借币参数

限速规则：1 次/2s

**功能说明：**

此接口获取用户借币时的提示参数。

**请求路径：**

/v1/api/lever/borrowparam

curl `https://api.fameex.com/v1/api/lever/borrowparam`

**路由参数：**

无

**Post 参数：**

| 参数     | 是否必须 | 数据类型 | 说明                 |
| -------- | -------- | -------- | -------------------- |
| pairName | 是       | string   | 币对名称 例:ETH_USDT |
| currency | 是       | string   | 币种名称 例:ETH      |

> **返回示例：**

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

### 响应参数

| 字段名称          | 数据类型 | 说明                |
| ----------------- | -------- | ------------------- |
| code              | int      | 200, 正常           |
| msg               | string   | success,正常        |
| data              | array    | 返回值,杠杆配置信息 |
| canBorrowAmount   | string   | 可借金额            |
| borrowedAmount    | string   | 已借金额            |
| borrowFeeRate     | string   | 计价币最少借币金额  |
| leastBorrowAmount | string   | 最小借币金额        |

## 杠杆借币

限速规则：1 次/2s

**功能说明：**

此接口用于杠杆借币。

**请求路径：**

/v1/api/lever/borrow

curl `https://api.fameex.com/v1/api/lever/borrow`

**路由参数：**

无

**Post 参数：**

| 参数     | 是否必须 | 数据类型 | 说明                 |
| -------- | -------- | -------- | -------------------- |
| pairName | 是       | string   | 币对名称 例:ETH_USDT |
| currency | 是       | string   | 币种名称 例:ETH      |
| amount   | 是       | string   | 借币金额             |

> **返回示例：**

```json
{
  "code": 200,
  "msg": "success",
  "data": ""
}
```

### 响应参数

| 字段名称 | 数据类型 | 说明         |
| -------- | -------- | ------------ |
| code     | int      | 200, 正常    |
| msg      | string   | success,正常 |
| data     | array    | 空字符串     |

## 获取杠杆还币参数

限速规则：1 次/2s

**功能说明：**

此接口获取特定币对下特定币种的还币提示参数。

**请求路径：**

/v1/api/lever/repayparam

curl `https://api.fameex.com/v1/api/lever/repayparam`

**路由参数：**

无

**Post 参数：**

| 参数     | 是否必须 | 数据类型 | 说明                 |
| -------- | -------- | -------- | -------------------- |
| pairName | 是       | string   | 币对名称 例:ETH_USDT |
| currency | 是       | string   | 币种名称 例:ETH      |

> **返回示例：**

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

### 响应参数

| 字段名称       | 数据类型 | 说明                     |
| -------------- | -------- | ------------------------ |
| code           | int      | 200, 正常                |
| msg            | string   | success,正常             |
| data           | object   | 返回值,用户还币提示信息  |
| borrowedAmount | string   | 借币未还本金             |
| interest       | string   | 借币未还利息             |
| unReturnAmount | string   | 未还金额                 |
| availAmount    | string   | 该币对下该币种的可用金额 |

## 杠杆还币

限速规则：1 次/2s

**功能说明：**

此接口用于杠杆还币。

**请求路径：**

/v1/api/lever/repay

curl `https://api.fameex.com/v1/api/lever/repay`

**路由参数：**

无

**Post 参数：**

| 参数     | 是否必须 | 数据类型 | 说明                 |
| -------- | -------- | -------- | -------------------- |
| pairName | 是       | string   | 币对名称 例:ETH_USDT |
| currency | 是       | string   | 币种名称             |
| amount   | 是       | string   | 还币金额             |

> **返回示例：**

```json
{
  "code": 200,
  "msg": "success",
  "data": ""
}
```

### 响应参数

| 字段名称 | 数据类型 | 说明         |
| -------- | -------- | ------------ |
| code     | int      | 200, 正常    |
| msg      | string   | success,正常 |
| data     | array    | 空字符串     |

## 获取杠杆账户借还记录

限速规则：1 次/2s

**功能说明：**

此接口获取杠杆借还记录信息。

**请求路径：**

/v1/api/lever/record/borrow_repay

curl `https://api.fameex.com/v1/api/lever/record/borrow_repay`

**路由参数：**

无

**Post 参数：**

| 参数     | 是否必须 | 数据类型 | 说明                 |
| -------- | -------- | -------- | -------------------- |
| pairName | 是       | string   | 币对名称 例:ETH_USDT |
| currency | 是       | string   | 币种名称 例:ETH      |
| pageSize | 是       | int      | 每页显示数量         |
| pageNum  | 是       | int      | 页码                 |

> **返回示例：**

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

### 响应参数

| 字段名称       | 数据类型 | 说明                         |
| -------------- | -------- | ---------------------------- |
| code           | int      | 200, 正常                    |
| msg            | string   | success,正常                 |
| data           | list     | 返回值,杠杆账户数据          |
| borrowedTime   | int64    | 借币时间                     |
| coinPair       | string   | 借币币对名称 例:BTC/USDT     |
| coinType       | string   | 借币币种名称 例:BTC          |
| recordId       | string   | 借币记录 id                  |
| borrowedAmount | string   | 借币数量                     |
| amount         | string   | 交易币可用金额               |
| borrowFeeRate  | string   | 每小时利率                   |
| interest       | string   | 已还利息                     |
| refund         | string   | 计价币冻结金额               |
| state          | int      | 借币状态：1.未还清；2.已还清 |

## 获取杠杆账户账单

限速规则：1 次/2s

**功能说明：**

此接口获取杠杆账单。

**请求路径：**

/v1/api/lever/ledger

curl `https://api.fameex.com/v1/api/lever/ledger`

**路由参数：**

无

**Post 参数：**

| 参数       | 是否必须 | 数据类型 | 说明                                                                                                         |
| ---------- | -------- | -------- | ------------------------------------------------------------------------------------------------------------ |
| pageNum    | 是       | int      | 页码                                                                                                         |
| pageSize   | 是       | int      | 每页显示数量 (0 < pageSize ≤ 500)                                                                            |
| currency   | 否       | string   | 币种类型,不填时返回所有的账单                                                                                |
| ledgerType | 否       | int      | 账单类型 2 买入 3 买出 4 手续费 5 借币 6 归还利息 7 归还本金 8 系统买入 9 系统卖出 11 强平费 12 转入 13 转出 |
| pairName   | 否       | string   | 币对类型，不填时返回所有币对的账单                                                                           |

> **返回示例：**

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

### 响应参数

| 字段名称  | 数据类型 | 说明         |
| --------- | -------- | ------------ |
| ledger_id | string   | 账单 ID      |
| coinPair  | string   | 币对         |
| currency  | string   | 币种         |
| balance   | string   | 余额         |
| amount    | string   | 变动数量     |
| typename  | string   | 账单类型     |
| timestamp | string   | 账单创建时间 |

# 错误信息

| code 码 | 说明                                              |
| ------- | ------------------------------------------------- |
| 200     | 正常                                              |
| 112002  | API 单个 Key 流量超限                             |
| 112005  | API 请求频率超限                                  |
| 112007  | API-Key 创建失败                                  |
| 112008  | API-Key 说明名称已存在                            |
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
| 280007 | 币对不存在或未开启交易                |
| 280014 | 买卖方向参数错误             |
| 280048 | 强平类型参数错误              |
| 280204 | 策略类型参数错误                 |
| 280044 | 订单类型参数错误                   |
| 280045 | 订单状态参数错误                   |
| 280042 | 页码要大于0                 |
| 280043 | 页数要在 0 - 500 之间 |

# 常见问题

| 常见问题                                                                                                                                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.什么是交易币种?什么是计价币种？交易量是以交易币种还是计价币种进行数量统计？<br>答：<br>每一个交易币对都是由 交易币种/计价币种 组成的，币对中前方为交易货币，后方为计价货币。<br>举例说明：BTC/USDT 这个交易币对中，BTC 为交易货币，USDT 为计价货币。<br>交易量是以交易币种为准进行统计。<br>成交总额是以计价币种为准进行统计。          |
| 2.Rest 访问限制?<br>答: <br>1.单个 IP 限制每分钟 1200 次访问，超过 1200 次将被锁定 1 小时，一小时后自动解锁。<br>2.单个用户限制每秒钟 20 次访问，一秒钟内 20 次以上的请求，将会视作无效。                                                                                                                                                 |
| 3.WebSocket 访问限制?<br>答:<br> 单个用户限制每秒钟 50 次访问，一秒钟内 50 次以上的请求，将会视作无效。                                                                                                                                                                                                                                   |
| 4.生成的密钥有什么用处?<br>答:<br> 密钥是用来操作 API 的钥匙，在调用 API 接口时需要提供 API 密钥。私有密钥只在刚生成时显示一次，遗忘需重新生成。                                                                                                                                                                                          |
| 5.k 线图是否可以获取几个月或者一年前的数据?<br>答:<br> 系统 k 线图最多只提供 1000 条数据,如果要获取比较久的数据需要使用小时或者天的单位获取。                                                                                                                                                                                             |
| 6.API 的 IP 是否需要绑定?<br>答:<br> 1.API 的 IP 绑定有效的防止除了这个 IP 之外的服务器进行调用自己的权限进行交易操作。<br> 2.绑定 IP 后，只能由绑定的 IP 进行访问，如不绑定，则不限制访问 IP。                                                                                                                                           |
| 7.API 是否支持提币?<br>答:<br> 不支持,提币必须现在 FameEX 官网进行提币。                                                                                                                                                                                                                                                                  |
| 8.公钥私钥可以提供给别人吗?<br>答:<br> 不建议,会导致资产损失。                                                                                                                                                                                                                                                                            |
| 9.签名失败频繁?<br> • 检查 API Key 是否有效，是否复制正确，是否有绑定 IP 白名单；<br>• 检查时间戳是否是 UTC 时间；<br>• 检查参数是否按字母排序；<br>• 检查编码；<br>• 检查签名编码应该是 hex；<br>• 检查 是否以表单方式提交；<br>• 检查 的 url 是否带着签名字段，POST 的数据格式是否是 json 格式；<br>• 检查签名结果是否有进行 URI 编码。 |
| 10.返回 login-required?<br>• 检查参数 account-id 是否是由 /v1/account/accounts 接口返回的，而不是填的 UID；<br>• 检查请求是否把业务参数也计算进签名；<br>• 检查请求是否将参数按照 ASCII 码表顺序排序。                                                                                                                                    |
| 11.返回 gateway-internal-error?<br>检查请求是否在 header 中声明 Content-Type:application/json。                                                                                                                                                                                                                                           |
