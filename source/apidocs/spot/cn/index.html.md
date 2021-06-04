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

# 更新日志

**2020-12-22**

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

**2020-11-16**

- 币币交易接口更新：
  - 更新获取订单列表 `v1/api/spot/orderlist`为获取委托单列表
  - 更新获取订单详情 `v1/api/spot/orderdetail` 为获取委托单详情
  - 更新获取杠杆订单列表 `v1/api/lever/orders`为获取杠杆订单列表
  - 更新获取杠杆订单详情 `v1/api/lever/orders/detail`为获取杠杆委托单详情

**2020-10-30**

- 钱包接口更新：
  - 修改资金划转功能接口 `v1/api/account/transfer`

**2020-10-29**

- 钱包接口更新：
  - 新增杠杆挂单功能接口 `v1/api/lever/orders/place`
  - 新增杠杆撤单功能接口 `v1/api/lever/orders/cancel`
  - 新增杠杆批量撤单接口 `v1/api/lever/orders/batch_cancel`
  - 新增获取杠杆账户委托单列表功能接口 `v1/api/lever/orders`
  - 新增获取杠杆账户委托单详情功能接口 `v1/api/lever/orders/detail`
  - 新增获取杠杆配置功能接口 `v1/api/lever/pair/config`

**2020-10-28**

- 钱包接口更新：
  - 新增获取杠杆账户账单接口 `v1/api/lever/ledger`
  - 新增获取杠杆账户特定币对，特定币种下还币的提示参数接口 `v1/api/lever/repayparam`
  - 新增获取杠杆账户特定币对，特定币种下还币接口 `v1/api/lever/repay`
  - 新增获取杠杆账户特定币对，特定币种下借币的提示参数接口 `v1/api/lever/borrow`
  - 新增获取杠杆账户特定币对，特定币种下借币接口 `v1/api/lever/borrowparam`

**2020-10-27**

- 钱包接口更新：
  - 新增获取杠杆账户信息接口 `v1/api/lever/accounts`
  - 新增获取杠杆账户下某一特定币对详情接口 `v1/api/lever/accounts/{pairName}`

# 简介

API 概述

FAMEEX 为您提供了一套简单又强大的 API 接口，帮助您快速、高效的获取行情和进行交易。

使用 API 前，请先创建您个人的 API，获取您的 AccessKey 和 SecretKey，并设置 API 的 IP 访问限制。

API 的交易权限让您可以快速的获取当前市场最新行情及时的下单交易、查询自己可用和冻结金额、查询自己当前尚未成交的挂单、买进或卖出、撤单。

FAMEEX 官网首页： www.fameex.com <br><br>

如果在使用过程中有任何问题，请联系 FAMEEX 官方客服，

我们的联系方式如下：

官方客服邮箱：Service@mail.fameex.info

官方微博：https://m.weibo.cn/u/7130914300

官方 Twitter：https://twitter.com/FameexGroup

我们将为您做出最权威的解答。

# 接入说明

## 接入URLs

| 接入 URLs                 | 备注                   |
| ------------------------- | ---------------------- |
| `https://api.fameex.com`  | RESTFUL API            |
| `wss://www.fameex.com/ws` | WebSocket Feed（行情） |

所有请求基于 Https 协议，POST 请求的请求头信息中 contentType 需要统一设置为:’application/json’

鉴于延迟高和稳定性差等原因，不建议通过代理的方式访问 FAMEEX- API。

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

# Websocket 行情推送

## 心跳连接

`说明`

长连接心跳

`请求路径`

wss://www.fameex.com/push

`请求方式`

websocket

`请求示例`

``` json
{
  "op": "heartBeat"
}
```

`参数`

| 参数 | 是否必须 | 数据类型 | 备注                  |
| ---- | -------- | -------- | --------------------- |
| op   | 是       | string   | 消息类型("heartBeat") |

`返回值`

| 字段名称 | 数据类型 | 备注                  |
| -------- | -------- | --------------------- |
| type     | string   | 消息类型("heartBeat") |

``` json
  {
    "code": 200,
    "msg": "***",
    "type":"heartBeat"
  }
```

## 登录信息

`说明`

长连接登录

`请求路径`

wss://www.fameex.com/push

`请求方式`

websocket

`请求示例`

```json
{
  "op": "login",
  "AccessKey": "***",
  "sign": "***"
}
```

`参数`

| 参数      | 是否必须 | 数据类型 | 备注               |
| --------- | -------- | -------- | ------------------ |
| op        | 是       | string   | 消息类型("Login")  |
| AccessKey | 是       | string   | 申请的 AccessKey   |
| sign      | 是       | string   | 页面唯一标识(uuid) |

`返回值`

| 字段名称 | 数据类型 | 备注              |
| -------- | -------- | ----------------- |
| code     | int      | 200, 正常         |
| msg      | string   | 备注              |
| type     | string   | 消息类型("login") |

```json
{
  "code": 200,
  "msg": "***",
  "type": "login"
}
```

## 注册K线信息

`说明`

此接口注册 K 线服务

`请求路径`

wss://www.fameex.com/push

`请求方式`

websocket

`请求示例`

```json
{
  "op": "register",
  "type": "kLineData",
  "base": "***",
  "quote": "***",
  "KTime": "***"
}
```

`参数`

| 参数  | 是否必须 | 数据类型 | 备注                                                   |
| ----- | -------- | -------- | ------------------------------------------------------ |
| op    | 是       | string   | 消息类型("register")                                   |
| type  | 是       | string   | 注册类型("kLineData")                                  |
| base  | 是       | string   | 交易对中的交易币种                                     |
| quote | 是       | string   | 交易对中的计价币种                                     |
| KTime | 是       | string   | K 线时间("1","5","15","30","60","120","240","1D","1W") |

`返回值`

无

## 注册首页行情

`说明`

此接口注册首页行情服务

`请求路径`

wss://www.fameex.com/push

`请求方式`

websocket

`请求示例`

```json
{
  "op": "register",
  "type": "homemarket"
}
```

`参数`

| 参数 | 是否必须 | 数据类型 | 备注     |
| ---- | -------- | -------- | -------- |
| op   | 是       | string   | 消息类型 |
| type | 是       | string   | 注册类型 |

`返回值`

无

## 注册深度行情

`说明`

此接口注册深度服务

`请求路径`

wss://www.fameex.com/push

`请求方式`

websocket

`请求示例`

```json
{
  "op": "register",
  "type": "transDepth",
  "base": "***",
  "quote": "***",
  "percision": 0
}
```

`参数`

| 参数      | 是否必须 | 数据类型 | 备注               |
| --------- | -------- | -------- | ------------------ |
| op        | 是       | string   | 消息类型           |
| type      | 是       | string   | 注册类型           |
| base      | 是       | string   | 交易对中的交易币种 |
| quote     | 是       | string   | 交易对中的计价币种 |
| percision | 是       | int      | 深度精度位数       |

`返回值`

无

## 推送首页行情

`说明`

此接口推送首页行情数据

`请求路径`

wss://www.fameex.com/push

`请求方式`

websocket

`参数`

无

`返回值`

| 字段名称            | 数据类型 | 备注                   |
| ------------------- | -------- | ---------------------- |
| type                | string   | 消息类型               |
| base_quote          | string   | 币对 key               |
| base                | string   | 交易对中的交易币种     |
| quote               | string   | 交易对中的计价币种     |
| transactionPrice    | float    | 成交价                 |
| gain                | float    | 24 小时涨幅            |
| coinHour24OpenPrice | float    | 24 小时开盘            |
| coinHour24LowPrice  | float    | 24 小时最低            |
| coinHour24HighPrice | float    | 24 小时最高            |
| hour24Volume        | float    | 24 小时成交量          |
| tranHour24Volume    | float    | 24 小时成交总额        |
| tranByCnyPrice      | float    | 计价币价格(单位人民币) |
| baseByCnyPrice      | float    | 交易币价格(单位人民币) |

``` json
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

## 推送币对深度列表

`说明`

此接口推送币对深度列表数据

`请求路径`

wss://www.fameex.com/push

`请求方式`

websocket

`参数`

无

`返回值`

| 字段名称   | 数据类型 | 备注                   |
| ---------- | -------- | ---------------------- |
| type       | string   | 消息类型("transDepth") |
| base       | string   | 交易对中的交易币种     |
| quote      | string   | 交易对中的计价币种     |
| buyList    | array    | 买入列表               |
| price      | string   | 单价                   |
| count      | string   | 单价对应深度数量       |
| orderCount | int      | 订单数量               |
| sellList   | array    | 卖出列表               |
| timestamp  | int64    | 时间戳                 |

``` json
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

## 推送K线数据

`说明`

此接口推送 K 线数据

`请求路径`

wss://www.fameex.com/push

`请求方式`

websocket

`参数`

无

`返回值`

| 字段名称 | 数据类型 | 备注                                |
| -------- | -------- | ----------------------------------- |
| type     | string   | 消息类型("kLineData")               |
| time     | int64    | K 线时间戳（根据注册 K 线服务推送） |
| open     | float    | 开盘价                              |
| high     | float    | 最高价                              |
| low      | float    | 最低价                              |
| close    | float    | 收盘价                              |
| volume   | float    | 成交量                              |

``` json
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

## 推送最新成交订单行情

`说明`

此接口推送最新成交订单详情

`请求路径`

wss://www.fameex.com/push

`请求方式`

websocket

`参数`

无

`返回值`

| 字段名称 | 数据类型 | 备注                 |
| -------- | -------- | -------------------- |
| type     | string   | 消息类型             |
| base     | string   | 交易对中的交易币种   |
| quote    | string   | 交易对中的计价币种   |
| price    | float    | 成交单价             |
| count    | float    | 成交数量             |
| time     | int64    | 成交时间 单位: 毫秒  |
| buyType  | int      | 买卖方向 0, 买, 1 卖 |

``` json
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

## 推送订单成交或者撤销

`说明`

推送买卖方或自己订单成交或取消

`请求路径`

wss://www.fameex.com/push

`请求方式`

websocket

`参数`

无

`返回值`

| 字段名称    | 数据类型 | 备注                                                                                        |
| ----------- | -------- | ------------------------------------------------------------------------------------------- |
| type        | string   | 消息类型("myTransDepth")                                                                    |
| orderId     | string   | 订单 id                                                                                     |
| base        | string   | 交易币                                                                                      |
| quote       | string   | 计价币                                                                                      |
| state       | int      | 订单的状态码 4-taker 完全成交 8-taker 部分成交 9-maker 部分成交 10-maker 完全成交 11-已撤销 |
| price       | float    | 委托单价格                                                                                  |
| count       | float    | 未成交数量                                                                                  |
| totalCount  | float    | 委托单数量                                                                                  |
| dealedCount | float    | 已成交数量                                                                                  |
| dealedMoney | float    | 已成交额                                                                                    |
| buyType     | int      | 买卖方向 0-买 1-卖                                                                          |
| buyClass    | int      | 交易类型 0-限价 1 市价 2 止盈止损                                                           |
| lossPrice   | float    | 止盈止损触发价格                                                                            |
| createTime  | int64    | 下单时间                                                                                    |

``` json
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

## 推送我的订单部分撤销

`说明`

此接口推送我的订单部分成交或部分取消数据

`请求路径`

wss://www.fameex.com/push

`请求方式`

websocket

`参数`

无

`返回值`

| 字段名称 | 数据类型 | 备注                          |
| -------- | -------- | ----------------------------- |
| type     | string   | 消息类型("myOrderPartCancel") |
| orderId  | string   | 订单 id                       |

``` json
 {
    "code": 200,
    "msg": "***",
    "type":"myOrderPartCancel",
    "data": {"orderId":""}
  }
```

## 注销首页行情

`说明`

此接口注销首页行情服务

`请求路径`

wss://www.fameex.com/push

`请求方式`

websocket

`请求示例`

```json
{
  "op": "unregister",
  "type": "homemarket"
}
```

`参数`

| 参数 | 是否必须 | 数据类型 | 备注     |
| ---- | -------- | -------- | -------- |
| op   | 是       | string   | 消息类型 |
| type | 是       | string   | 注册类型 |

`返回值`

无

# 基础 API 接口

## 获取当前系统时间

限速规则：20 次/2s

`说明`

获取当前系统时间，单位秒

`请求路径`

/v1/common/timestamp

curl `https://api.fameex.com/v1/common/timestamp`

`路由参数`

无

`Post参数`

无

`返回值`

| 字段名称 | 数据类型 | 备注                |
| -------- | -------- | ------------------- |
| code     | int      | 200, 正常           |
| ts       | int64    | 请求时间, 秒        |
| data     | int64    | 返回值,当前时间, 秒 |

`返回示例`

```json
{
  "code": 200,
  "ts": 1553254857,
  "data": 1553254857
}
```

## 获取所有交易币对

限速规则：20 次/2s

`功能说明`

此接口返回 FAMEEX 平台支持的所有交易币对。

`请求路径`

/v1/common/symbols

curl `https://api.fameex.com/v1/common/symbols`

`路由参数`

无

`Post参数`

无

`返回值`

| 字段名称        | 数据类型 | 备注                                   |
| --------------- | -------- | -------------------------------------- |
| code            | int      | 200, 正常                              |
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

`返回示例`

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

## 获取所有交易币种

限速规则：20 次/2s

`功能说明`

此接口返回 FAMEEX 支持的所有交易币种。

`请求路径`

/v1/common/currencys

curl `https://api.fameex.com/v1/common/currencys`

`路由参数`

无

`Post参数`

无

`返回值`

| 字段名称                    | 数据类型 | 备注                                |
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

`返回示例`

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
            //链类型的名称
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

# 行情 API 接口

## 获取k线数据

限速规则：20 次/2s

`功能说明`

此接口获取历史 K 线数据。

`请求路径`

GET/v1/market/history/kline

curl `https://api.fameex.com/v1/market/history/kline`

`路由参数`

| 参数        | 是否必须 | 数据类型 | 备注                                                        |
| ----------- | -------- | -------- | ----------------------------------------------------------- |
| pairName    | 是       | string   | 币对, 例"ETH_BTC"                                           |
| granularity | 是       | string   | 时间粒度 例（ "1","5","15","30","60","120","240","1D","1W") |
| startTime   | 否       | string   | 开始时间，时间戳（单位:秒）                                 |
| endTime     | 否       | string   | 结束时间，时间戳（单位:秒）                                 |

`Post参数`

无

`返回值`

| 字段名称 | 数据类型 | 备注                   |
| -------- | -------- | ---------------------- |
| code     | int      | 返回值状态             |
| time     | int64    | 时间戳                 |
| amount   | float    | 以计价币种统计的交易额 |
| open     | float    | 开盘价                 |
| close    | float    | 收盘价                 |
| low      | float    | 最低价                 |
| hight    | float    | 最高价                 |
| vol      | float    | 以交易币种统计的交易量 |

`返回示例`

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

## 市场深度数据

限速规则：20 次/2s

`功能说明`

此接口返回指定交易对的当前市场深度数据。

`请求路径`

/v1/market/depth

curl `https://api.fameex.com/v1/market/depth`

`路由参数`

| 参数     | 是否必须 | 数据类型 | 备注                              |
| -------- | -------- | -------- | --------------------------------- |
| pairName | 是       | string   | 币对 例如: BTC_USDT               |
| size     | 否       | string   | 返回深度档位数量，最多返回 200    |
| depth    | 否       | string   | 深度价格小数位数，例如：-2,-1,0,1 |

`返回值`

`Post参数`

无

`返回值`

| 字段名称   | 数据类型 | 备注                   |
| ---------- | -------- | ---------------------- |
| code       | int      | 200,正常               |
| msg        | string   | 备注                   |
| data       | map      | 返回数据：市场深度数据 |
| base       | string   | 交易币                 |
| quote      | string   | 计价币                 |
| price      | string   | 单价                   |
| count      | string   | 数量                   |
| orderCount | int      | 订单数量               |
| timestamp  | int64    | 时间戳                 |

`返回示例`

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

## 获取成交数据

限速规则：20 次/2s

`功能说明`

此接口返回指定交易对的成交明细记录。

`请求路径`

GET/v1/market/history/trade

curl `https://api.fameex.com/v1/market/history/trade`

`路由参数`

| 参数     | 是否必须 | 数据类型 | 备注                            |
| -------- | -------- | -------- | ------------------------------- |
| pairName | 是       | string   | 币对名称 例如: BTC_USDT         |
| size     | 否       | string   | 最大为 100，不填默认返回 100 条 |

`Post参数`

无

`返回值`

| 字段名称 | 数据类型 | 备注                       |
| -------- | -------- | -------------------------- |
| code     | int      | 200,正常                   |
| msg      | string   | 备注                       |
| data     | list     | 返回值,最新成交记录        |
| orderId  | string   | 成交订单 id                |
| price    | string   | 成交单价                   |
| count    | string   | 成交数量                   |
| time     | string   | 成交时间 时间戳 单位：纳秒 |
| buyType  | string   | 买卖方向 0, 买, 1 卖       |

`返回示例`

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

## 获取某个ticker信息

限速规则：20 次/2s

`功能说明`

此接口返回最近 24 小时的行情数据汇总，数据取值时间区间为 24 小时滚动。

`请求路径`

/v1/market/history/kline24h

curl `https://api.fameex.com/v1/market/history/kline24h`

`路由参数`

| 参数     | 是否必须 | 数据类型 | 备注                  |
| -------- | -------- | -------- | --------------------- |
| pairName | 是       | string   | 交易币对, 例"ETH_BTC" |

`Post参数`

无

`返回值`

| 字段名称            | 数据类型 | 备注                         |
| ------------------- | -------- | ---------------------------- |
| code                | int      | 200,正常                     |
| pairName            | string   | 币对名称 例如:"OMG_ETH"      |
| last                | string   | 最新成交价                   |
| buyFirst            | string   | 买一价                       |
| sellFirst           | string   | 卖一价                       |
| coinHour24OpenPrice | string   | 24 小时开盘价                |
| coinHour24LowPrice  | string   | 24 小时最低价                |
| coinHour24HighPrice | string   | 24 小时最高价                |
| base24Volume        | string   | 按交易货币统计 24 小时成交量 |
| quoteHour24Volume   | string   | 按计价货币统计 24 小时成交量 |
| timestamp           | int64    | 系统时间戳 (单位：纳秒)      |

`返回示例`

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

## 获取全部ticker信息

限速规则：20 次/2s

`功能说明`

此接口返回最近 24 小时的行情数据汇总，数据取值时间区间为 24 小时滚动。

`请求路径`

/v1/market/history/kline24h/all

curl `https://api.fameex.com/v1/market/history/kline24h/all`

`路由参数`

无

`Post参数`

无

`返回值`

| 字段名称            | 数据类型 | 备注                         |
| ------------------- | -------- | ---------------------------- |
| code                | int      | 200,正常                     |
| pairName            | string   | 币对名称 例如:"OMG_ETH"      |
| last                | string   | 最新成交价                   |
| buyFirst            | string   | 买一价                       |
| sellFirst           | string   | 卖一价                       |
| coinHour24OpenPrice | string   | 24 小时开盘价                |
| coinHour24LowPrice  | string   | 24 小时最低价                |
| coinHour24HighPrice | string   | 24 小时最高价                |
| base24Volume        | string   | 按交易货币统计 24 小时成交量 |
| quoteHour24Volume   | string   | 按计价货币统计 24 小时成交量 |
| timestamp           | int64    | 系统时间戳 (单位：纳秒)      |

`返回示例`

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

# 币币交易 API 接口

## 币币下单

限速规则：100 次/2s

`功能说明`

此接口提供撤销指定的某一种或多种币对的所有未成交订单的功能。

`请求路径`

/v1/api/spot/orders

curl `https://api.fameex.com/v1/api/spot/orders`

`路由参数`

无

`Post参数`

| 参数    | 是否必须 | 数据类型 | 备注               |
| ------- | -------- | -------- | ------------------ |
| base    | 是       | string   | 交易对中的交易币种 |
| quote   | 是       | string   | 交易对中的计价币种 |
| buyType | 是       | int      | 0 买, 1 卖         |
| price   | 是       | string   | 下单单价           |
| count   | 是       | string   | 下单数量           |

`返回值`

| 字段名称 | 数据类型 | 备注      |
| -------- | -------- | --------- |
| code     | int      | 200, 正常 |
| msg      | string   | 信息说明  |
| orderId  | string   | 挂单 id   |

`返回示例`

```json
{
  "code": 200,
  "msg": "SUCCESS",
  "orderId": "10383992916667793408"
}
```

## 币币撤单

限速规则：100 次/2s

`功能说明`

此接口提供将未成交的订单撤销的功能。

`请求路径`

/v1/api/spot/cancel_orders

curl `https://api.fameex.com/v1/api/spot/cancel_orders`

`路由参数`

无

`Post参数`

| 参数    | 是否必须 | 数据类型 | 备注               |
| ------- | -------- | -------- | ------------------ |
| orderid | 是       | string   | 订单 id            |
| base    | 是       | string   | 交易对中的交易币种 |
| quote   | 是       | string   | 交易对中的计价币种 |

`返回值`

| 字段名称 | 数据类型 | 备注        |
| -------- | -------- | ----------- |
| code     | int      | 200, 正常   |
| msg      | string   | 备注        |
| orderId  | string   | 要撤单的 id |

`返回示例`

```json
{
    "code": 200,
    "msg": "SUCCESS",
    "orderId": "10383992916667793408"
}
```

## 币币批量撤单

限速规则：100 次/2s

`功能说明`

此接口提供撤销指定的某一种或多种币对的所有未成交订单的功能。

`请求路径`

/v1/api/spot/cancel_orders_all

curl `https://api.fameex.com/v1/api/spot/cancel_orders_all`

`路由参数`

无

`Post参数`

| 参数      | 是否必须 | 数据类型 | 备注                         |
| --------- | -------- | -------- | ---------------------------- |
| buyType   | 是       | int      | 买卖方向 0 买, 1 卖, -1 全部 |
| base      | 是       | string   | 交易对中的交易币种           |
| quote     | 是       | string   | 交易对中的计价币种           |
| startTime | 是       | int64    | "0" 全部                     |
| endTime   | 是       | int64    | "0" 全部                     |

`返回值`

| 字段名称 | 数据类型 | 备注     |
| -------- | -------- | -------- |
| code     | int      | 200,正常 |
| msg      | string   | SUCCESS  |

```json
{
  "code": 200,
  "msg": "SUCCESS"
}
```

## 获取委托单详情

限速规则：20 次/2s

`功能说明`

此接口通过订单 ID 获取指定委托单信息。

`请求路径`

/v1/api/spot/orderdetail

curl `https://api.fameex.com/v1/api/spot/orderdetail`

`headers参数`

无

`路由参数`

| 参数     | 是否必须 | 数据类型 | 备注                    |
| -------- | -------- | -------- | ----------------------- |
| orderId  | 是       | string   | 订单 id                 |
| pairName | 是       | string   | 币对名称（例:BTC_USDT） |

`Post参数`

无

`返回值`

| 字段名称    | 数据类型 | 备注                                                                                         |
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

`返回示例`

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

## 获取委托单列表

限速规则：20 次/2s

`功能说明`

此接口获取列出您当前的委托单信息（最近 3 个月的委托单信息）。这个请求支持分页，并且按时间倒序排序和存储，最新的排在最前面。

`请求路径`

/v1/api/spot/orderlist

curl `https://api.fameex.com/v1/api/spot/orderlist`

`headers参数`

无

`路由参数`

| 参数      | 是否必须 | 数据类型 | 备注                                              |
| --------- | -------- | -------- | ------------------------------------------------- |
| type      | 是       | string   | 0 所有, 1 完成,2 未完成, 3 已撤销, 4 已撤单和完成 |
| buyType   | 是       | string   | 买卖方向: 0 买, 1 卖, -1 全部                     |
| pairName  | 是       | string   | 币对名称（例:BTC_USDT）                           |
| pageNum   | 是       | string   | 分页使用, 第几页                                  |
| pageSize  | 是       | string   | 分页使用, 每页数量 (0 < pageSize ≤ 500)             |
| startTime | 否       | string   | 时间戳,查询订单的开始时间 秒                      |
| endTime   | 否       | string   | 时间戳,查询订单的结束时间 秒                      |

`Post参数`

无

`返回值`

| 字段名称       | 数据类型 | 备注                                                                                                          |
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

`返回示例`

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

## 获取成交明细

限速规则：20 次/2s

`功能说明`

此接口获取您当前所有的成交订单信息。这个请求支持分页，并且按时间倒序排序和存储，最新的排在最前面。

`请求路径`

/v1/api/spot/fills

curl `https://api.fameex.com/v1/api/spot/fills`

`路由参数`

| 参数      | 是否必须 | 数据类型 | 备注                                  |
| --------- | -------- | -------- | ------------------------------------- |
| pairName  | 是       | string   | 币对名称 (例:BTC_UDST)                |
| orderId   | 否       | string   | 委托单订单 id                         |
| buyType   | 是       | string   | 买卖方向: 0 买, 1 卖, -1 全部         |
| pageNum   | 是       | string   | 分页使用, 第几页,从第一页开始         |
| pageSize  | 是       | string   | 分页使用, 每页数量 (0 < pageSize ≤ 500) |
| startTime | 否       | string   | 时间戳, 秒                            |
| endTime   | 否       | string   | 时间戳, 秒                            |

`Post参数`

无

`返回值`

| 字段名称      | 数据类型 | 备注                     |
| ------------- | -------- | ------------------------ |
| code          | int      | 返回值状态               |
| msg           | string   | 返回值描述               |
| data          | string   | 返回值,成交明细          |
| pairName      | string   | 币对名称（例：BTC_USDT） |
| base          | string   | 交易币                   |
| quote         | string   | 计价币                   |
| orderId       | string   | 委托单 id                |
| time          | int64    | 成交时间 纳秒            |
| buyClass      | int      | 交易类型: 0 限价交易     |
| buyType       | int      | 买卖方向: 0 买, 1 卖     |
| price         | string   | 成交价格                 |
| count         | string   | 成交数量                 |
| fee           | string   | 手续费                   |
| feeRate       | string   | 实际手续费费率           |
| originFeeRate | string   | 原始手续费费率           |

`返回示例`

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

## 获取所有未完成的订单

限速规则：20 次/2s

`功能说明`

此接口获取您当前所有的成交订单信息。这个请求支持分页，并且按时间倒序排序和存储，最新的排在最前面。

`请求路径`

/v1/api/orders_pending

curl `https://api.fameex.com /v1/api/orders_pending`

`路由参数

| 参数     | 是否必须 | 数据类型 | 备注                                  |
| -------- | -------- | -------- | ------------------------------------- |
| pairName | 是       | string   | 币对名称（例:BTC_USDT）               |
| pageNum  | 是       | string   | 分页使用, 第几页,从第一页开始         |
| pageSize | 是       | string   | 分页使用, 每页数量 (0< pageSize ≤ 500) |

`Post参数`

无

`返回值`

| 字段名称    | 数据类型 | 备注                         |
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

`返回示例`

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

# 钱包 API 接口

## 获取钱包账户信息

限速规则：20 次/2s

`功能说明`

此接口获取钱包币币账户所有资产信息列表，查询各币种的余额、冻结和可用等信息。

`请求路径`

/v1/api/account/wallet

curl `https://api.fameex.com/v1/api/account/wallet`

`路由参数`

无

`Post参数`

无

`返回值`

| 字段名称   | 数据类型 | 备注                                                                      |
| ---------- | -------- | ------------------------------------------------------------------------- |
| code       | int      | 200, 正常                                                                 |
| data       | list     | 返回值,币币账户数据                                                       |
| userid     | string   | 用户 id                                                                   |
| walletType | string   | 账户类型:spot-现货账户 otc-法币账户 l2c-杠杆账户 |
| available  | string   | 可用余额                                                                  |
| total      | string   | 总余额                                                                    |
| currency   | string   | 币种 例:BTC                                                               |
| hold       | string   | 冻结金额                                                                  |

`返回示例`

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

## 获取钱包账户某币种详情

限速规则：20 次/2s

`功能说明`

获取钱包账户详情（单一币种）

`请求路径`

/v1/api/account/wallet/currency

curl `https://api.fameex.com/v1/api/account/wallet/currency`

`路由参数`

| 参数     | 是否必须 | 数据类型 | 备注         |
| -------- | -------- | -------- | ------------ |
| currency | 是       | string   | 币种, 例 BTC |

`Post参数`

无

`返回值`

| 字段名称  | 数据类型 | 备注                            |
| --------- | -------- | ------------------------------- |
| code      | int      | 200, 正常                       |
| msg       | string   | 此次返回值说明                  |
| userid    | string   | 用户 id                         |
| data      | map      | 返回值,币币账户，某一币种的详情 |
| available | string   | 可用余额                        |
| hold      | string   | 冻结金额                        |

`返回示例`

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

## 资金划转

限速规则：1 次/2s

`功能说明`

此接口提供平台内现货钱包、法币钱包、杠杆钱包之间进行资金划转。【注：杠杆账户币对之间互相划转仅支持计价币之间的划转，例如从杠杆账户下的 BTC_USDT 将 USDT 划转至 ETH_USDT 币对下】

`请求路径`

POST /v1/api/account/transfer

curl `https://api.fameex.com/v1/api/account/transfer`

`路由参数`

无

`Post参数`

| 参数     | 是否必须 | 数据类型 | 备注                                            |
| -------- | -------- | -------- | ----------------------------------------------- |
| currency | 是       | string   | 币种类型                                        |
| amount   | 是       | string   | 数量                                            |
| from     | 是       | string   | 转出账户: spot 现货账户, otc 法币账户，l2c 杠杆账户 |
| to       | 是       | string   | 转入账户: spot 现货账户, otc 法币账户，l2c 杠杆账户 |
| fromPair | 否       | string   | 杠杆账户币对间互转时的转出币对，例:BTC_USDT     |
| toPair   | 否       | string   | 杠杆账户币对间互转时的转入币对,例:ETH_USDT      |

`返回值`

| 字段名称 | 数据类型 | 备注                   |
| -------- | -------- | ---------------------- |
| code     | int      | 200, 正常              |
| msg      | string   | success,正常           |
| data     | object   | 资金划转返回的响应对象 |
| orderid  | string   | 订单 id                |
| userid   | string   | 用户 id                |

`返回示例`

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

## 获取现货账户交易账单

限速规则：20 次/2s

`功能说明`

此接口查询现货账户交易账单。

`请求路径`

POST /v1/api/spot/record/trade

curl `https://api.fameex.com/v1/api/spot/record/trade`

`路由参数`

无

`Post参数`

| 参数      | 是否必须 | 数据类型 | 备注                                   |
| --------- | -------- | -------- | -------------------------------------- |
| tradeType | 否       | int      | 交易类型：0.全部；2.买入；3.卖出；4.实收手续费 |
| currency  | 否       | string   | 币种名称 例:ETH                        |
| pageNum   | 是       | string   | 第几页，1 开始                         |
| pageSize  | 是       | string   | 每页数量 (0 < pageSize ≤ 500)            |
| startTime | 否       | string   | 开始时间 秒 最多查询最近 90 天内的记录 |
| endTime   | 否       | string   | 结束时间 秒                            |

`返回值`

| 字段名称    | 数据类型 | 备注                                   |
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

`返回示例`

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

## 获取现货账户充提账单

限速规则：20 次/2s

`功能说明`

此接口查询现货账户充提账单。

`请求路径`

POST /v1/api/spot/record/chargewithdraw

curl `https://api.fameex.com/v1/api/spot/record/chargewithdraw`

`路由参数`

无

`Post参数`

| 参数      | 是否必须 | 数据类型 | 备注                               |
| --------- | -------- | -------- | ---------------------------------- |
| tradeType | 否       | int      | 交易类型：0.全部；1.提币；2.充币 |
| currency  | 否       | string   | 币种名称 例:ETH                    |
| startTime | 否       | int64    | 开始时间：秒级时间戳               |
| endTime   | 否       | int64    | 结束时间时间：秒级时间戳           |
| pageNum   | 是       | int      | 页码，从 1 开始                    |
| pageSize  | 是       | int      | 每页数量 (0 < pageSize ≤ 500)     |

`返回值`

| 字段名称    | 数据类型 | 备注                                                                                                                                                                                     |
| ----------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| code        | int      | 200, 正常                                                                                                                                                                                |
| msg         | string   | success,正常                                                                                                                                                                             |
| data        | object   | 空字符串                                                                                                                                                                                 |
| total       | int      | 账单记录数量                                                                                                                                                                             |
| list        | array    | 账单记录列表                                                                                                                                                                             |
| tradeType   | int      | 交易类型：1.提币；2.充币                                                                                                                                                                 |
| operateTime | int64    | 操作时间                                                                                                                                                                                 |
| currency    | string   | 币种名称 例:ETH                                                                                                                                                                          |
| amount      | string   | 数量                                                                                                                                                                                     |
| address     | string   | 当 tradeType 为 1 时，代表提币地址；tradeType 为 2 时，代表充币地址                                                                                                                      |
| fee         | string   | 提币手续费                                                                                                                                                                               |
| label       | string   | 用户的标签                                                                                                                                                                               |
| chainType   | string   | 币种的链类型                                                                                                                                                                             |
| state       | int      | 账单状态:<br> 当 tradeType 为 1 时, state 分别代表: 1-待审核; 2-审核中; 3-已完成; 4-审核失败; 5-已撤单; 6-提币失败; 7-初始化创建; 8-确认中<br>当 tradeType 为 2 时, state 分别代表: 1-已完成 |
| txId        | string   | 交易哈希                                                                                                                                                                                 |

`返回示例`

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

​

## 获取现货账户划转账单

限速规则：20 次/2s

`功能说明`

此接口查询现货账户划转账单。

`请求路径`

POST /v1/api/spot/record/trans

curl `https://api.fameex.com/v1/api/spot/record/trans`

``路由参数`

无

`Post参数`

| 参数      | 是否必须 | 数据类型 | 备注                               |
| --------- | -------- | -------- | ---------------------------------- |
| tradeType | 否       | int      | 交易类型：0.全部；1.转入；2.转出 |
| currency  | 否       | string   | 币种名称 例:ETH                    |
| startTime | 否       | int64    | 开始时间：秒级时间戳               |
| endTime   | 否       | int64    | 结束时间时间：秒级时间戳           |
| pageNum   | 是       | int      | 页码，从 1 开始                    |
| pageSize  | 是       | int      | 每页数量 (0 < pageSize ≤ 500)        |

`返回值`

| 字段名称     | 数据类型 | 备注                                     |
| ------------ | -------- | ---------------------------------------- |
| code         | int      | 200, 正常                                |
| msg          | string   | success,正常                             |
| data         | object   | 空字符串                                 |
| userId       | string   | 用户 id                                  |
| total        | int      | 账单记录数量                             |
| list         | array    | 账单记录列表                             |
| tradeType    | int      | 交易类型：1.转入；2.转出         |
| operateTime  | int64    | 操作时间                                 |
| currency     | string   | 币种名称 例:ETH                          |
| amount       | string   | 数量                                     |
| fromCoinPair | string   | 转入币对                                 |
| toCoinPair   | string   | 转出币对                                 |
| fromAccount  | string   | 转出账户：0.现货；1.杠杆；3.法币 |
| toAccount    | string   | 转入账户：0.现货；1.杠杆；3.法币 |

`返回示例`

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

## 获取现货账户其他账单

限速规则：20 次/2s

`功能说明`

此接口查询现货账户其他账单，包括返佣及活动。

`请求路径`

POST /v1/api/spot/record/others

curl `https://api.fameex.com/v1/api/spot/record/others`

``路由参数`

无

`Post参数`

| 参数      | 是否必须 | 数据类型 | 备注                             |
| --------- | -------- | -------- | -------------------------------- |
| tradeType | 否       | int      | 交易类型：0.全部；1.返佣；2.活动 |
| currency  | 否       | string   | 币种名称 例:ETH                  |
| startTime | 否       | int64    | 开始时间：秒级时间戳             |
| endTime   | 否       | int64    | 结束时间时间：秒级时间戳         |
| pageNum   | 是       | int      | 页码，从 1 开始                  |
| pageSize  | 是       | int      | 每页数量 (0 < pageSize ≤ 500)      |

`返回值`

| 字段名称    | 数据类型 | 备注                             |
| ----------- | -------- | -------------------------------- |
| code        | int      | 200, 正常                        |
| msg         | string   | success,正常                     |
| data        | object   | 空字符串                         |
| userId      | string   | 用户 id                          |
| total       | int      | 账单记录数量                     |
| list        | array    | 账单记录列表                     |
| tradeType   | int      | 交易类型：1.返佣；2.活动 |
| operateTime | int64    | 操作时间：秒级时间戳             |
| currency    | string   | 币种名称 例:ETH                  |
| amount      | string   | 数量                             |

`返回示例`

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

## 获取充币地址

限速规则：20 次/2s

`功能说明`

此接口获取各个币种的充币地址。

`请求路径`

/v1/api/account/deposit/address

curl `https://api.fameex.com/v1/api/account/deposit/address`

`路由参数`

| 参数      | 是否必须 | 数据类型 | 备注          |
| --------- | -------- | -------- | ------------- |
| coinType  | 是       | string   | 币种类型 USDT |
| chainType | 是       | string   | 链类型 ERC20  |

`Post参数`

无

`返回值`

| 字段名称 | 数据类型 | 备注      |
| -------- | -------- | --------- |
| code     | int      | 200, 正常 |
| request  | map      | 请求参数  |
| userId   | string   | 用户 id   |
| coinType | string   | 币种      |
| address  | string   | 地址      |

`返回示例`

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

## 获取杠杆账户信息

限速规则：1 次/2s

`功能说明`

此接口获取杠杆账户所有资产信息列表，查询各币种的余额、冻结和可用等信息。

`请求路径`

/v1/api/lever/accounts

curl `https://api.fameex.com/v1/api/lever/accounts`

`路由参数`

无

`Post参数`

无

`返回值`

| 字段名称       | 数据类型 | 备注                                                                      |
| -------------- | -------- | ------------------------------------------------------------------------- |
| code           | int      | 200, 正常                                                                 |
| data           | list     | 返回值,杠杆账户数据                                                       |
| userid         | string   | 用户 id                                                                   |
| walletType     | string   | 账户类型:spot-币币账户 otc-法币账户 l2c-杠杆账户 |
| coinpair       | string   | 币对名称 例:BTC/USDT                                                      |
| baseCurrency   | string   | 交易币名称 例:BTC                                                         |
| quoteCurrency  | string   | 计价币名称 例:USDT                                                        |
| baseAvailable  | string   | 交易币可用金额                                                            |
| quoteAvailable | string   | 计价币可用金额                                                            |
| baseHold       | string   | 交易币冻结金额                                                            |
| quoteHold      | string   | 计价币冻结金额                                                            |
| baseTotal      | string   | 交易币总额                                                                |
| quoteTotal     | string   | 计价币总额                                                                |
| baseBorrowed   | string   | 交易币借币金额                                                            |
| quoteBorrowed  | string   | 计价币借币金额                                                            |
| baseInterest   | string   | 交易币利息                                                                |
| quoteInterest  | string   | 计价币利息                                                                |

`返回示例`

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

# 杠杆交易 API 接口

## 获取杠杆账户下某币对详情

限速规则：1 次/2s

`功能说明`

获取杠杆账户下某币对账户余额、冻结和可用等信息

`请求路径`

/v1/api/lever/accounts

curl `https://api.fameex.com/v1/api/lever/accounts`

`路由参数`

| 参数     | 是否必须 | 数据类型 | 备注              |
| -------- | -------- | -------- | ----------------- |
| pairName | 是       | string   | 币对, 例 BTC_USDT |

`Post参数`

无

`返回值`

| 字段名称       | 数据类型 | 备注                 |
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

## 杠杆下单

限速规则：1 次/2s

`功能说明`

此接口提供杠杆下单功能。

`请求路径`

/v1/api/lever/orders/place

curl `https://api.fameex.com/v1/api/lever/orders/place`

`路由参数`

无

`Post参数`

| 参数    | 是否必须 | 数据类型 | 备注               |
| ------- | -------- | -------- | ------------------ |
| base    | 是       | string   | 交易对中的交易币种 |
| quote   | 是       | string   | 交易对中的计价币种 |
| buyType | 是       | int      | 0 买, 1 卖         |
| price   | 是       | string   | 下单单价           |
| count   | 是       | string   | 下单数量           |

`返回值`

| 字段名称 | 数据类型 | 备注      |
| -------- | -------- | --------- |
| code     | int      | 200, 正常 |
| msg      | string   | 信息说明  |
| orderId  | string   | 挂单 id   |

`返回示例`

```json
{
  "code": 200,
  "msg": "success",
  "orderId": "10541638782567317504"
}
```

## 杠杆撤单

限速规则：1 次/2s

`功能说明`

此接口提供将未成交的杠杆订单撤销的功能。

`请求路径`

/v1/api/lever/orders/cancel

curl `https://api.fameex.com/v1/api/lever/orders/cancel`

`路由参数`

无

`Post参数`

| 参数    | 是否必须 | 数据类型 | 备注    |
| ------- | -------- | -------- | ------- |
| orderId | 是       | string   | 订单 id |

`返回值`

| 字段名称 | 数据类型 | 备注        |
| -------- | -------- | ----------- |
| code     | int      | 200, 正常   |
| msg      | string   | 备注        |
| orderId  | string   | 要撤单的 id |

`返回示例`

```json
{
  "code": 200, //成功
  "msg": "success",
  "orderId": "10541638782567317504"
}
```

## 杠杆批量撤单

限速规则：1 次/2s

`功能说明`

此接口提供撤销指定的某一种或多种币对的所有未成交的杠杆订单的功能。

`请求路径`

/v1/api/lever/orders/batch_cancel

curl `https://api.fameex.com/v1/api/lever/orders/batch_cancel`

`路由参数`

无

`Post参数`

| 参数      | 是否必须 | 数据类型 | 备注                         |
| --------- | -------- | -------- | ---------------------------- |
| buyType   | 是       | int      | 买卖方向 0 买, 1 卖, -1 全部 |
| base      | 是       | string   | 交易对中的交易币种           |
| quote     | 是       | string   | 交易对中的计价币种           |
| startTime | 是       | int64    | "0" 全部                     |
| endTime   | 是       | int64    | "0" 全部                     |

`返回值`

| 字段名称 | 数据类型 | 备注     |
| -------- | -------- | -------- |
| code     | int      | 200,正常 |
| msg      | string   | SUCCESS  |

```json
{
  "code": 200,
  "msg": "SUCCESS"
}
```

## 获取杠杆委托单列表

限速规则：1 次/2s

`功能说明`

列出您当前的委托单信息（最近 3 个月的委托单信息）。这个请求支持分页，并且按时间倒序排序和存储，最新的排在最前面。

`请求路径`

/v1/api/lever/orders

curl `https://api.fameex.com/v1/api/lever/orders`

`路由参数`

无

`Post参数`

| 参数      | 是否必须 | 数据类型 | 备注                                                                                                                         |
| --------- | -------- | -------- | ---------------------------------------------------------------------------------------------------------------------------- |
| pageNum   | 是       | int      | 分页使用, 第几页                                                                                                             |
| pageSize  | 是       | int      | 分页使用, 每页数量 (0 < pageSize ≤ 500)                                                                                        |
| type      | 是       | int      | 0 所有, 1 完成(完全成交),2 未完成, 3 已撤销, 4 已撤销和完成 5 部分成交已撤销 6 完成(完全成交)和部分成交已撤销 7 未成交已撤销 |
| buyType   | 否       | int      | 买卖方向: 0 买, 1 卖, -1 全部                                                                                                |
| base      | 否       | string   | 交易币名称 例:BTC                                                                                                            |
| quote     | 否       | string   | 计价币名称 例:USDT                                                                                                           |
| startTime | 否       | int64    | 时间戳,查询订单的开始时间 秒                                                                                                 |
| endTime   | 否       | int64    | 时间戳,查询订单的结束时间 秒                                                                                                 |

`返回值`

| 字段名称       | 数据类型 | 备注                                                                                                          |
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

`返回示例`

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

## 获取杠杆委托单详情

限速规则：1 次/2s

`功能说明`

此接口通过订单 ID 获取指定委托单信息。

`请求路径`

/v1/api/lever/orders/detail

curl `https://api.fameex.com/v1/api/lever/orders/detail`

`路由参数`

无

`Post参数`

| 参数     | 是否必须 | 数据类型 | 备注                    |
| -------- | -------- | -------- | ----------------------- |
| orderId  | 是       | string   | 订单 id                 |
| pairName | 是       | string   | 币对名称（例:BTC_USDT） |

`返回值`

| 字段名称    | 数据类型 | 备注                                                                                         |
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

`返回示例`

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

## 获取杠杆成交明细

限速规则：1 次/2s

`功能说明`

此接口获取您当前所有的成交订单信息。这个请求支持分页，并且按时间倒序排序和存储，最新的排在最前面。

`请求路径`

/v1/api/lever/deals

curl `https://api.fameex.com/v1/api/lever/deals`

`路由参数`

无

`Post参数`

| 参数        | 是否必须 | 数据类型 | 备注                                  |
| ----------- | -------- | -------- | ------------------------------------- |
| pairName    | 是       | string   | 币对名称 (例:BTC_UDST)                |
| buyType     | 是       | int      | 买卖方向: 0 买, 1 卖, -1 全部         |
| pageNum     | 是       | int      | 分页使用, 第几页,从第一页开始         |
| pageSize    | 是       | int      | 分页使用, 每页数量 (0 < pageSize ≤ 500) |
| accountFlag | 是       | int      | 账户来源( 0-币币 1-杠杆 2-杠杆爆仓)   |
| orderId     | 否       | string   | 委托单订单 id                         |
| startTime   | 否       | int64    | 时间戳, 秒                            |
| endTime     | 否       | int64    | 时间戳, 秒                            |

`返回值`

| 字段名称      | 数据类型 | 备注                             |
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

`返回示例`

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

## 获取杠杆配置

限速规则：1 次/2s

`功能说明`

此接口获取钱包杠杆账户下币对配置信息。

`请求路径`

/v1/api/lever/pair/config

curl `https://api.fameex.com/v1/api/lever/pair/config`

`路由参数`

无

`Post参数`

| 参数     | 是否必须 | 数据类型 | 备注                 |
| -------- | -------- | -------- | -------------------- |
| pairName | 否       | string   | 币对名称 例:ETH_USDT |

`返回值`

| 字段名称                 | 数据类型 | 备注                |
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

`返回示例`

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

## 获取杠杆借币参数

限速规则：1 次/2s

`功能说明`

此接口获取用户借币时的提示参数。

`请求路径`

/v1/api/lever/borrowparam

curl `https://api.fameex.com/v1/api/lever/borrowparam`

`路由参数`

无

`Post参数`

| 参数     | 是否必须 | 数据类型 | 备注                 |
| -------- | -------- | -------- | -------------------- |
| pairName | 是       | string   | 币对名称 例:ETH_USDT |
| currency | 是       | string   | 币种名称 例:ETH      |

`返回值`

| 字段名称          | 数据类型 | 备注                |
| ----------------- | -------- | ------------------- |
| code              | int      | 200, 正常           |
| msg               | string   | success,正常        |
| data              | array    | 返回值,杠杆配置信息 |
| canBorrowAmount   | string   | 可借金额            |
| borrowedAmount    | string   | 已借金额            |
| borrowFeeRate     | string   | 计价币最少借币金额  |
| leastBorrowAmount | string   | 最小借币金额        |

`返回示例`

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

## 杠杆借币

限速规则：1 次/2s

`功能说明`

此接口用于杠杆借币。

`请求路径`

/v1/api/lever/borrow

curl `https://api.fameex.com/v1/api/lever/borrow`

`路由参数`

无

`Post参数`

| 参数     | 是否必须 | 数据类型 | 备注                 |
| -------- | -------- | -------- | -------------------- |
| pairName | 是       | string   | 币对名称 例:ETH_USDT |
| currency | 是       | string   | 币种名称 例:ETH      |
| amount   | 是       | string   | 借币金额             |

`返回值`

| 字段名称 | 数据类型 | 备注         |
| -------- | -------- | ------------ |
| code     | int      | 200, 正常    |
| msg      | string   | success,正常 |
| data     | array    | 空字符串     |

`返回示例`

```json
{
  "code": 200,
  "msg": "success",
  "data": ""
}
```

## 获取杠杆还币参数

限速规则：1 次/2s

`功能说明`

此接口获取特定币对下特定币种的还币提示参数。

`请求路径`

/v1/api/lever/repayparam

curl `https://api.fameex.com/v1/api/lever/repayparam`

`路由参数`

无

`Post参数`

| 参数     | 是否必须 | 数据类型 | 备注                 |
| -------- | -------- | -------- | -------------------- |
| pairName | 是       | string   | 币对名称 例:ETH_USDT |
| currency | 是       | string   | 币种名称 例:ETH      |

`返回值`

| 字段名称       | 数据类型 | 备注                     |
| -------------- | -------- | ------------------------ |
| code           | int      | 200, 正常                |
| msg            | string   | success,正常             |
| data           | object   | 返回值,用户还币提示信息  |
| borrowedAmount | string   | 借币未还本金             |
| interest       | string   | 借币未还利息             |
| unReturnAmount | string   | 未还金额                 |
| availAmount    | string   | 该币对下该币种的可用金额 |

`返回示例`

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

## 杠杆还币

限速规则：1 次/2s

`功能说明`

此接口用于杠杆还币。

`请求路径`

/v1/api/lever/repay

curl `https://api.fameex.com/v1/api/lever/repay`

`路由参数`

无

`Post参数`

| 参数     | 是否必须 | 数据类型 | 备注                 |
| -------- | -------- | -------- | -------------------- |
| pairName | 是       | string   | 币对名称 例:ETH_USDT |
| currency | 是       | string   | 币种名称             |
| amount   | 是       | string   | 还币金额             |

`返回值`

| 字段名称 | 数据类型 | 备注         |
| -------- | -------- | ------------ |
| code     | int      | 200, 正常    |
| msg      | string   | success,正常 |
| data     | array    | 空字符串     |

`返回示例`

```json
{
    "code": 200,
    "msg": "success",
    "data": ""
}
```

## 获取杠杆账户借还记录

限速规则：1 次/2s

`功能说明`

此接口获取杠杆借还记录信息。

`请求路径`

/v1/api/lever/record/borrow_repay

curl `https://api.fameex.com/v1/api/lever/record/borrow_repay`

`路由参数`

无

`Post参数`

| 参数     | 是否必须 | 数据类型 | 备注                 |
| -------- | -------- | -------- | -------------------- |
| pairName | 是       | string   | 币对名称 例:ETH_USDT |
| currency | 是       | string   | 币种名称 例:ETH      |
| pageSize | 是       | int      | 每页显示数量         |
| pageNum  | 是       | int      | 页码                 |

`返回值`

| 字段名称       | 数据类型 | 备注                         |
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

`返回示例`

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

## 获取杠杆账户账单

限速规则：1 次/2s

`功能说明`

此接口获取杠杆账单。

`请求路径`

/v1/api/lever/ledger

curl `https://api.fameex.com/v1/api/lever/ledger`

`路由参数`

无

`Post参数`

| 参数       | 是否必须 | 数据类型 | 备注                                                                                         |
| ---------- | -------- | -------- | -------------------------------------------------------------------------------------------- |
| pageNum    | 是       | int      | 页码                                                                                         |
| pageSize   | 是       | int      | 每页显示数量 (0 < pageSize ≤ 500)                                                              |
| currency   | 否       | string   | 币种类型,不填时返回所有的账单                                                            |
| ledgerType | 否       | int      | 账单类型 2 买入 3 买出 4 手续费 5 借币 6 归还利息 7 归还本金 8 系统买入 9 系统卖出 11 强平费 12 转入 13 转出 |
| pairName   | 否       | string   | 币对类型，不填时返回所有币对的账单                                                       |

`返回值`

| 字段名称  | 数据类型 | 备注         |
| --------- | -------- | ------------ |
| ledger_id | string   | 账单 ID      |
| coinPair  | string   | 币对         |
| currency  | string   | 币种         |
| balance   | string   | 余额         |
| amount    | string   | 变动数量     |
| typename  | string   | 账单类型     |
| timestamp | string   | 账单创建时间 |

`返回示例`

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
      "ledger_id": "10541354256305774592",
      "coinPair": "BTC/USDT",
      "currency": "USDT",
      "balance": "3902.49015080",
      "amount": "3249.23200000",
      "typename": "lever_trade",
      "timestamp": "2020-10-28T15:56:40Z"
    },
    {
      "ledger_id": "10541354255949258752",
      "coinPair": "BTC/USDT",
      "currency": "USDT",
      "balance": "653.25815080",
      "amount": "0.00008736",
      "typename": "lever_trade",
      "timestamp": "2020-10-28T15:56:40Z"
    },
    {
      "ledger_id": "10541354255949258752",
      "coinPair": "BTC/USDT",
      "currency": "BTC",
      "balance": "1.06446832",
      "amount": "0.00100100",
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

# 常见问题

| 常见问题                                                                                                                                                                                                                                                                                                                         |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.什么是交易币种?什么是计价币种？交易量是以交易币种还是计价币种进行数量统计？<br>答：<br>每一个交易币对都是由 交易币种/计价币种 组成的，币对中前方为交易货币，后方为计价货币。<br>举例说明：BTC/USDT 这个交易币对中，BTC 为交易货币，USDT 为计价货币。<br>交易量是以交易币种为准进行统计。<br>成交总额是以计价币种为准进行统计。 |
| 2.Rest 访问限制?<br>答: <br>1.单个 IP 限制每分钟 1200 次访问，超过 1200 次将被锁定 1 小时，一小时后自动解锁。<br>2.单个用户限制每秒钟 20 次访问，一秒钟内 20 次以上的请求，将会视作无效。                                                                                                                                        |
| 3.WebSocket 访问限制?<br>答:<br> 单个用户限制每秒钟 50 次访问，一秒钟内 50 次以上的请求，将会视作无效。                                                                                                                                                                                                                          |
| 4.生成的密钥有什么用处?<br>答:<br> 密钥是用来操作 API 的钥匙，在调用 API 接口时需要提供 API 密钥。私有密钥只在刚生成时显示一次，遗忘需重新生成。                                                                                                                                                                                 |
| 5.k 线图是否可以获取几个月或者一年前的数据?<br>答:<br> 系统 k 线图最多只提供 1000 条数据,如果要获取比较久的数据需要使用小时或者天的单位获取。                                                                                                                                                                                      |
| 6.API 的 IP 是否需要绑定?<br>答:<br> 1.API 的 IP 绑定有效的防止除了这个 IP 之外的服务器进行调用自己的权限进行交易操作。<br> 2.绑定 IP 后，只能由绑定的 IP 进行访问，如不绑定，则不限制访问 IP。                                     |
| 7.API 是否支持提币?<br>答:<br> 不支持,提币必须现在 FAMEEX 官网进行提币。                                                                                                                                                                                                                            |
| 8.公钥私钥可以提供给别人吗?<br>答:<br> 不建议,会导致资产损失。                                                                                                                                                                                                                                                                     |
| 9.签名失败频繁?<br> • 检查 API Key 是否有效，是否复制正确，是否有绑定 IP 白名单；<br>• 检查时间戳是否是 UTC 时间；<br>• 检查参数是否按字母排序；<br>• 检查编码；<br>• 检查签名编码应该是 hex；<br>• 检查 是否以表单方式提交；<br>• 检查 的 url 是否带着签名字段，POST 的数据格式是否是 json 格式；<br>• 检查签名结果是否有进行 URI 编码。        |
| 10.返回 login-required?<br>• 检查参数 account-id 是否是由 /v1/account/accounts 接口返回的，而不是填的 UID；<br>• 检查请求是否把业务参数也计算进签名；<br>• 检查请求是否将参数按照 ASCII 码表顺序排序。                                                                                                                           |
| 11.返回 gateway-internal-error?<br>检查请求是否在 header 中声明 Content-Type:application/json。                                                                                                                                                                                                                                   |
