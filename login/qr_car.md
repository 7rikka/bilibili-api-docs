# 获取登录二维码

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

| 字段名     | 类型  | 内容     | 备注   |
|---------|-----|--------|------|
| code    | num | 响应码    | 0：成功 |
| message | str | 0      |      |
| msg     |     | `null` |      |
| data    | obj | 信息本体   |      |

### `data`对象

| 字段名       | 类型  | 内容                        | 备注  |
|-----------|-----|---------------------------|-----|
| url       | str | 登录地址，需要用APP扫描该地址的二维码，实现登录 |     |
| auth_code | str | 验证码code                   |     |

## 请求示例

```shell
curl -L -X POST 'https://passport.bilibili.com/x/passport-tv-login/qrcode/auth_code?local_id=0&mobi_app=android_bilithings&sign=b85e76c77ba1324458332c6f753152a0&appkey=8d23902c1688a798&platform=android&ts=1664512278'
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
    "url": "https://passport.bilibili.com/x/passport-tv-login/h5/qrcode/auth?auth_code=ab4f5d1d14b96ab6ab7746ff03848741&mobi_app=android_bilithings",
    "auth_code": "ab4f5d1d14b96ab6ab7746ff03848741"
  }
}
```
</details>