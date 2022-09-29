# \[APP]\[TV端]获取登录二维码

> https://passport.bilibili.com/x/passport-tv-login/qrcode/auth_code

请求方式：`POST`

是否需要登录：`否`

Content-Type：`application/x-www-form-urlencoded`

## URL参数

| 参数名      | 类型  | 必填  | 内容  | 备注  |
|----------|-----|-----|-----|-----|
| appkey   | str | √   |     |     |
| build    | str |     |     |     |
| c_locale | str |     |     |     |
| channel  | str |     |     |     |
| local_id | str | √   |     |     |
| mobi_app | str |     |     |     |
| platform | str |     |     |     |
| s_locale | str |     |     |     |
| ts       | str | √   |     |     |
| sign     | str | √   |     |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                  |
|---------|-----|------|-------------------------------------|
| code    | num | 响应码  | 0：成功<br/>-3：API校验密匙错误<br/>-400：请求错误 |
| message | str | 0    |                                     |
| ttl     | num | 1    |                                     |
| data    | obj | 信息本体 |                                     |

### `data`对象

| 字段名       | 类型  | 内容                        | 备注  |
|-----------|-----|---------------------------|-----|
| url       | str | 登录地址，需要用APP扫描该地址的二维码，实现登录 |     |
| auth_code | str | 验证码code                   |     |

## 请求示例

```shell
curl -L -X POST 'https://passport.bilibili.com/x/passport-tv-login/qrcode/auth_code?local_id=0&mobi_app=android_bilithings&sign=573c48ef19383297aab5891d86c19ddb&appkey=8d23902c1688a798&ts=1664435004' \
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
    "url": "https://passport.bilibili.com/x/passport-tv-login/h5/qrcode/auth?auth_code=efbb1d7ea96d89f11d84fd59134a5c41&mobi_app=android_bilithings",
    "auth_code": "efbb1d7ea96d89f11d84fd59134a5c41"
  }
}
```
</details>