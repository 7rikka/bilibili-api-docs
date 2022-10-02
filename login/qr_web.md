# 获取登录二维码

> https://passport.bilibili.com/x/passport-login/web/qrcode/generate

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名    | 类型  | 必填  | 内容         | 备注  |
|--------|-----|-----|------------|-----|
| source | str |     | `main-web` |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名        | 类型  | 内容                        | 备注  |
|------------|-----|---------------------------|-----|
| url        | str | 登录地址，需要用APP扫描该地址的二维码，实现登录 |     |
| qrcode_key | str | 二维码key                    |     |

## 请求示例

```shell
curl -L -X GET 'https://passport.bilibili.com/x/passport-login/web/qrcode/generate'
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
        "url": "https://passport.bilibili.com/h5-app/passport/login/scan?navhide=1&qrcode_key=4cef8584ff9ba515d912e2e8d4982e58&from=",
        "qrcode_key": "4cef8584ff9ba515d912e2e8d4982e58"
    }
}
```
</details>

# 获取二维码扫描状态

> https://passport.bilibili.com/x/passport-login/web/qrcode/poll

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名        | 类型  | 必填  | 内容     | 备注  |
|------------|-----|-----|--------|-----|
| qrcode_key | str | √   | 二维码key |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名           | 类型  | 内容                                                      | 备注    |
|---------------|-----|---------------------------------------------------------|-------|
| url           | str | 跨域登录url                                                 |       |
| refresh_token | str | 刷新用token                                                |       |
| timestamp     | str | 登录成功时的时间戳                                               | 单位：毫秒 |
| code          | str | 0：成功<br/>86101：未扫码<br/>86038：二维码已失效<br/>86090：二维码已扫码未确认 |       |
| message       | str |                                                         |       |

## 请求示例

```shell
curl -L -X GET 'https://passport.bilibili.com/x/passport-login/web/qrcode/poll?qrcode_key=********************************'
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
        "url": "https://passport.biligame.com/crossDomain?DedeUserID=*******&DedeUserID__ckMd5=****************&Expires=1680273441&SESSDATA=****************************&bili_jct=********************************&gourl=https%3A%2F%2Fpassport.bilibili.com%2Faccount%2Fsecurity%23%2Fhome",
        "refresh_token": "********************************",
        "timestamp": 1664721441443,
        "code": 0,
        "message": ""
    }
}
```
</details>

## 解析Cookie

**从响应返回的Header中获取`SESSDATA`、`bili_jct`、`DedeUserID`、`DedeUserID__ckMd5`和`sid`**