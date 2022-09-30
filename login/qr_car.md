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

# 获取二维码扫描状态

> https://passport.bilibili.com/x/passport-tv-login/qrcode/poll

请求方式：`POST`

是否需要登录：`否`

Content-Type：`application/x-www-form-urlencoded`

## URL参数

| 参数名       | 类型  | 必填  | 内容      | 备注  |
|-----------|-----|-----|---------|-----|
| appkey    | str | √   |         |     |
| auth_code | str | √   | 验证码code |     |
| build     | str |     |         |     |
| c_locale  | str |     |         |     |
| channel   | str |     |         |     |
| local_id  | str | √   |         |     |
| mobi_app  | str |     |         |     |
| platform  | str |     |         |     |
| s_locale  | str |     |         |     |
| ts        | str | √   |         |     |
| sign      | str | √   |         |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                                                          |
|---------|-----|------|-----------------------------------------------------------------------------|
| code    | num | 响应码  | 0：成功<br/>-3：API校验密匙错误<br/>-400：请求错误<br/>86038：二维码已失效<br/>86039：二维码尚未确认<br/> |
| message | str |      |                                                                             |
| ttl     | num | 1    |                                                                             |
| data    | obj | 信息本体 |                                                                             |

### `data`对象

| 字段名           | 类型    | 内容        | 备注                  |
|---------------|-------|-----------|---------------------|
| is_new        | bool  |           |                     |
| mid           | num   | 当前用户id    |                     |
| access_token  | str   | 登录状态token |                     |
| refresh_token | str   | 刷新token   |                     |
| expires_in    | num   | 有效时长      | 默认：15552000秒，等于180天 |
| token_info    | obj   | token信息   |                     |
| cookie_info   | obj   | cookie信息  |                     |
| sso           | array |           |                     |

#### `data`对象 -> `token_info`对象

| 字段名           | 类型  | 内容        | 备注                  |
|---------------|-----|-----------|---------------------|
| mid           | num | 当前用户id    |                     |
| access_token  | str | 登录状态token |                     |
| refresh_token | str | 刷新token   |                     |
| expires_in    | num | 有效时长      | 默认：15552000秒，等于180天 |

#### `data`对象 -> `cookie_info`对象

| 字段名     | 类型    | 内容       | 备注  |
|---------|-------|----------|-----|
| cookies | array | cookie信息 |     |
| domains | array |          |     |

##### `data`对象 -> `cookie_info`对象 -> `cookies`数组中的对象

| 字段名       | 类型  | 内容       | 备注     |
|-----------|-----|----------|--------|
| name      | str | cookie名称 |        |
| value     | str | cookie值  |        |
| http_only | num | 是否http专用 | 取值：0,1 |
| expires   | num | 过期时间     | 秒级时间戳  |
| secure    | num | `0`      |        |

## 请求示例

```shell
curl -L -X GET 'https://passport.bilibili.com/x/passport-tv-login/qrcode/poll?appkey=8d23902c1688a798&auth_code=74df372c894ffbe55b32cf8d5de27341&mobi_app=android_bilithings&platform=android&local_id=0&sign=b52b76a42718e01154a23330da7f1372&ts=1664513181'
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
    "is_new": false,
    "mid": 10086,
    "access_token": "********************************",
    "refresh_token": "********************************",
    "expires_in": 15552000,
    "token_info": {
      "mid": 10086,
      "access_token": "********************************",
      "refresh_token": "********************************",
      "expires_in": 15552000
    },
    "cookie_info": {
      "cookies": [
        {
          "name": "SESSDATA",
          "value": "********************************",
          "http_only": 1,
          "expires": 1679988973,
          "secure": 0
        },
        {
          "name": "bili_jct",
          "value": "********************************",
          "http_only": 0,
          "expires": 1679988973,
          "secure": 0
        },
        {
          "name": "DedeUserID",
          "value": "*******",
          "http_only": 0,
          "expires": 1679988973,
          "secure": 0
        },
        {
          "name": "DedeUserID__ckMd5",
          "value": "****************",
          "http_only": 0,
          "expires": 1679988973,
          "secure": 0
        },
        {
          "name": "sid",
          "value": "********",
          "http_only": 0,
          "expires": 1679988973,
          "secure": 0
        }
      ],
      "domains": [
        ".bilibili.com",
        ".biligame.com",
        ".bigfun.cn",
        ".bigfunapp.cn",
        ".dreamcast.hk"
      ]
    },
    "sso": [
      "https://passport.bilibili.com/api/v2/sso",
      "https://passport.biligame.com/api/v2/sso",
      "https://passport.bigfunapp.cn/api/v2/sso"
    ]
  }
}
```

</details>