# 获取登录二维码

> https://passport.snm0516.aisee.tv/x/passport-tv-login/qrcode/auth_code

请求方式：`POST`

是否需要登录：`否`

Content-Type：`application/x-www-form-urlencoded`

## URL参数

| 参数名               | 类型   | 必填  | 内容  | 备注  |
|-------------------|------|-----|-----|-----|
| appkey            | str  | √   |     |     |
| bili_local_id     | str  |     |     |     |
| brand             | str  |     |     |     |
| build             | num  |     |     |     |
| buvid             | str  |     |     |     |
| channel           | str  |     |     |     |
| cpu               | str  |     |     |     |
| device            | str  |     |     |     |
| device_id         | str  |     |     |     |
| device_name       | str  |     |     |     |
| device_platform   | str  |     |     |     |
| device_tourist_id | num  |     |     |     |
| explor_attr       | num  |     |     |     |
| extend            | str  |     |     |     |
| fingerprint       | str  |     |     |     |
| fourk             | num  |     |     |     |
| gourl             | str  |     |     |     |
| guest_access_key  | str  |     |     |     |
| guest_id          | num  |     |     |     |
| guid              | str  |     |     |     |
| local_fingerprint | str  |     |     |     |
| local_id          | str  | √   |     |     |
| login_session_id  | str  |     |     |     |
| memory            | num  |     |     |     |
| mobi_app          | str  |     |     |     |
| mode_switch       | bool |     |     |     |
| model             | str  |     |     |     |
| mpi_id            | str  |     |     |     |
| mpi_model         | str  |     |     |     |
| mpi_type          | str  |     |     |     |
| networkstate      | str  |     |     |     |
| platform          | str  |     |     |     |
| resource_id       | str  |     |     |     |
| spm_id            | str  |     |     |     |
| statistics        | str  |     |     |     |
| sys_ver           | num  |     |     |     |
| teenager_mode     | num  |     |     |     |
| ts                | num  | √   |     |     |
| tv_brand          | str  |     |     |     |
| uid               | num  |     |     |     |
| sign              | str  | √   |     |     |

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
curl -L -X POST 'https://passport.snm0516.aisee.tv/x/passport-tv-login/qrcode/auth_code?local_id=0&build=105301&sign=aa746667caf6b2835479dec92491bf07&appkey=4409e2ce8ffd12b8&ts=1664521821'
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
    "url": "https://b23.snm0516.aisee.tv/oLXy75m",
    "auth_code": "c5a119f119f51fce8e1bf7d772013701"
  }
}
```

</details>

# 获取二维码扫描状态

> https://passport.snm0516.aisee.tv/x/passport-tv-login/qrcode/poll

请求方式：`POST`

是否需要登录：`否`

Content-Type：`application/x-www-form-urlencoded`

## URL参数

| 参数名               | 类型   | 必填  | 内容      | 备注  |
|-------------------|------|-----|---------|-----|
| appkey            | str  | √   |         |     |
| auth_code         | str  | √   | 验证码code |     |
| bili_local_id     | str  |     |         |     |
| brand             | str  |     |         |     |
| build             | num  |     |         |     |
| buvid             | str  |     |         |     |
| channel           | str  |     |         |     |
| cpu               | str  |     |         |     |
| device            | str  |     |         |     |
| device_id         | str  |     |         |     |
| device_name       | str  |     |         |     |
| device_platform   | str  |     |         |     |
| device_tourist_id | num  |     |         |     |
| explor_attr       | num  |     |         |     |
| extend            | str  |     |         |     |
| fingerprint       | str  |     |         |     |
| fourk             | num  |     |         |     |
| guest_access_key  | str  |     |         |     |
| guest_id          | num  |     |         |     |
| guid              | str  |     |         |     |
| local_fingerprint | str  |     |         |     |
| local_id          | str  | √   |         |     |
| login_session_id  | str  |     |         |     |
| memory            | num  |     |         |     |
| mobi_app          | str  |     |         |     |
| mode_switch       | bool |     |         |     |
| model             | str  |     |         |     |
| mpi_id            | str  |     |         |     |
| mpi_model         | str  |     |         |     |
| mpi_type          | str  |     |         |     |
| networkstate      | str  |     |         |     |
| platform          | str  |     |         |     |
| resource_id       | str  |     |         |     |
| spm_id            | str  |     |         |     |
| statistics        | str  |     |         |     |
| sys_ver           | num  |     |         |     |
| teenager_mode     | num  |     |         |     |
| ts                | num  | √   |         |     |
| tv_brand          | str  |     |         |     |
| uid               | num  |     |         |     |
| sign              | str  | √   |         |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                                                     |
|---------|-----|------|------------------------------------------------------------------------|
| code    | num | 响应码  | 0：成功<br/>-3：API校验密匙错误<br/>-400：请求错误<br/>86038：二维码已失效<br/>86039：二维码尚未确认 |
| message | str |      |                                                                        |
| ttl     | num | 1    |                                                                        |
| data    | obj | 信息本体 |                                                                        |

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
curl -L -X POST 'https://passport.snm0516.aisee.tv/x/passport-tv-login/qrcode/poll?local_id=0&sign=ba48a78346503646a818f80ba955b4c2&appkey=4409e2ce8ffd12b8&auth_code=d810ac26f33a5e730efd31e535b35b01&ts=1664521841'
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