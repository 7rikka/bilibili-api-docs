# 卡券类型

| id  | 描述      |
|-----|---------|
| 1   | B币券     |
| 2   | 会员购优惠券  |
| 3   | 漫画福利券   |
| 4   | 会员购包邮券  |
| 5   | 漫画商城优惠券 |

# 查询卡券状态

> https://api.bilibili.com/x/vip/privilege/my

请求方式：`GET`

是否需要登录：`是`

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                  |
|---------|-----|------|---------------------|
| code    | num | 响应码  | 0：成功<br/>-101：账号未登录 |
| message | str |      |                     |
| ttl     | num | 1    |                     |
| data    | obj | 信息本体 |                     |

### `data`对象

| 字段名             | 类型    | 内容      | 备注  |
|-----------------|-------|---------|-----|
| list            | array | 卡券信息列表  |     |
| is_short_vip    | bool  | `false` |     |
| is_freight_open | bool  | `true`  |     |

### `data`对象 -> `list`数组中的对象

| 字段名               | 类型  | 内容         | 备注               |
|-------------------|-----|------------|------------------|
| type              | num | 卡券类型       | [卡券类型](#卡券类型)    |
| state             | num | 兑换状态       | 0：未兑换<br />1：已兑换 |
| expire_time       | num | 本轮卡券过期时间戳  | 单位：秒             |
| vip_type          | num | 固定值：`2`    | 年度大会员可兑换         |
| next_receive_days | num | 距下一轮兑换剩余天数 |                  |
| period_end_unix   | num | 下一轮兑换开始时间戳 | 单位：秒             |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/vip/privilege/my' \
-H 'cookie: SESSDATA=xxx'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "code": 0,
  "message": "0",
  "ttl": 1,
  "data": {
    "list": [
      {
        "type": 1,
        "state": 0,
        "expire_time": 1667231999,
        "vip_type": 2,
        "next_receive_days": 29,
        "period_end_unix": 1667491200
      },
      {
        "type": 2,
        "state": 0,
        "expire_time": 1667231999,
        "vip_type": 2,
        "next_receive_days": 29,
        "period_end_unix": 1667491200
      },
      {
        "type": 3,
        "state": 0,
        "expire_time": 1667231999,
        "vip_type": 2,
        "next_receive_days": 29,
        "period_end_unix": 1667491200
      },
      {
        "type": 4,
        "state": 0,
        "expire_time": 1667231999,
        "vip_type": 2,
        "next_receive_days": 29,
        "period_end_unix": 1667491200
      },
      {
        "type": 5,
        "state": 0,
        "expire_time": 1667231999,
        "vip_type": 2,
        "next_receive_days": 29,
        "period_end_unix": 1667491200
      }
    ],
    "is_short_vip": false,
    "is_freight_open": true
  }
}
```

</details>

# 兑换卡券

> https://api.bilibili.com/x/vip/privilege/receive

请求方式：`POST`

是否需要登录：`是`

Content-Type：`application/x-www-form-urlencoded`

## FORM参数

| 参数名      | 类型  | 必填  | 内容     | 备注            |
|----------|-----|-----|--------|---------------|
| type     | num | √   | 卡券类型   | [卡券类型](#卡券类型) |
| platform | str |     | `web`  |               |
| csrf     | str | √   | 用户csrf |               |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                                                                              |
|---------|-----|------|-------------------------------------------------------------------------------------------------|
| code    | num | 响应码  | 0：成功<br/>-101：账号未登录<br/>-111：csrf 校验失败<br/>69155：当前非大会员<br/>69800：网络繁忙 请稍后再试<br/>69801：你已领取过该权益 |
| message | str |      |                                                                                                 |
| ttl     | num | 1    |                                                                                                 |
| data    | obj | 信息本体 |                                                                                                 |

## 请求示例

```shell
curl -L -X POST 'https://api.bilibili.com/x/vip/privilege/receive' \
-H 'Cookie: SESSDATA=xxx' \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'type=1' \
--data-urlencode 'csrf=********************************'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "code": 0,
  "message": "0",
  "ttl": 1
}
```

</details>