# 申请发送短信

> https://passport.snm0516.aisee.tv/x/passport-tv-login/sms/send

请求方式：`POST`

是否需要登录：`否`

Content-Type：`application/x-www-form-urlencoded`

## URL参数

| 参数名               | 类型   | 必填  | 内容            | 备注   |
|-------------------|------|-----|---------------|------|
| appkey            | str  | √   |               |      |
| bili_local_id     | str  |     |               |      |
| brand             | str  |     |               |      |
| build             | num  |     |               |      |
| buvid             | str  |     |               |      |
| channel           | str  |     |               |      |
| cid               | num  | √   | 中国大陆电话区号：`86` |      |
| code              | str  |     |               |      |
| cpu               | str  |     |               |      |
| device            | str  |     |               |      |
| device_id         | str  |     |               |      |
| device_name       | str  |     |               |      |
| device_platform   | str  |     |               |      |
| device_tourist_id | num  |     |               |      |
| explor_attr       | num  |     |               |      |
| extend            | str  |     |               |      |
| fingerprint       | str  |     |               |      |
| fourk             | num  |     |               |      |
| guest_access_key  | str  |     |               |      |
| guest_id          | num  |     |               |      |
| guid              | str  |     |               |      |
| local_fingerprint | str  |     |               |      |
| local_id          | str  | √   |               |      |
| login_session_id  | str  |     |               |      |
| memory            | num  |     |               |      |
| mobi_app          | str  |     |               |      |
| mode_switch       | bool |     |               |      |
| model             | str  |     |               |      |
| mpi_id            | str  |     |               |      |
| mpi_model         | str  |     |               |      |
| mpi_type          | str  |     |               |      |
| networkstate      | str  |     |               |      |
| platform          | str  |     |               |      |
| resource_id       | str  |     |               |      |
| spm_id            | str  |     |               |      |
| statistics        | str  |     |               |      |
| sys_ver           | num  |     |               |      |
| teenager_mode     | num  |     |               |      |
| tel               | num  | √   | 手机号           |      |
| token             | str  |     |               |      |
| ts                | num  | √   | 当前时间戳         | 单位：秒 |
| tv_brand          | str  |     |               |      |
| uid               | num  |     |               |      |
| sign              | str  | √   |               |      |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                            |
|---------|-----|------|-----------------------------------------------|
| code    | num | 响应码  | 0：成功<br/>66031：手机号码格式不正确<br/>86046：请使用中国大陆手机号 |
| message | str |      |                                               |
| ttl     | num | 1    |                                               |
| data    | obj | 信息本体 |                                               |

### `data`对象

| 字段名         | 类型  | 内容                  | 备注  |
|-------------|-----|---------------------|-----|
| captcha_key | str | 本次短信验证码的captcha_key |     |

## 请求示例

```shell
curl -L -X POST 'https://passport.snm0516.aisee.tv/x/passport-tv-login/sms/send?appkey=4409e2ce8ffd12b8&cid=86&local_id=0&tel=xxx&ts=xxx&sign=xxx'
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
    "captcha_key": "********************************"
  }
}
```

</details>

# 使用短信验证码登录

> https://passport.snm0516.aisee.tv/x/passport-tv-login/login/sms

请求方式：`POST`

是否需要登录：`否`

Content-Type：`application/x-www-form-urlencoded`

## URL参数

| 参数名               | 类型   | 必填  | 内容                  | 备注   |
|-------------------|------|-----|---------------------|------|
| appkey            | str  | √   |                     |      |
| bili_local_id     | str  |     |                     |      |
| brand             | str  |     |                     |      |
| build             | num  |     |                     |      |
| buvid             | str  |     |                     |      |
| captcha_key       | str  | √   | 本次短信验证码的captcha_key |      |
| channel           | str  |     |                     |      |
| cid               | num  | √   | 中国大陆电话区号：`86`       |      |
| code              | num  | √   | 短信验证码，6位数字          |      |
| cpu               | str  |     |                     |      |
| device            | str  |     |                     |      |
| device_id         | str  |     |                     |      |
| device_name       | str  |     |                     |      |
| device_platform   | str  |     |                     |      |
| device_tourist_id | num  |     |                     |      |
| explor_attr       | num  |     |                     |      |
| extend            | str  |     |                     |      |
| fingerprint       | str  |     |                     |      |
| fourk             | num  |     |                     |      |
| guest_access_key  | str  |     |                     |      |
| guest_id          | num  |     |                     |      |
| guid              | str  |     |                     |      |
| local_fingerprint | str  |     |                     |      |
| local_id          | str  | √   |                     |      |
| login_session_id  | str  |     |                     |      |
| memory            | num  |     |                     |      |
| mobi_app          | str  |     |                     |      |
| mode_switch       | bool |     |                     |      |
| model             | str  |     |                     |      |
| mpi_id            | str  |     |                     |      |
| mpi_model         | str  |     |                     |      |
| mpi_type          | str  |     |                     |      |
| networkstate      | str  |     |                     |      |
| platform          | str  |     |                     |      |
| resource_id       | str  |     |                     |      |
| spm_id            | str  |     |                     |      |
| statistics        | str  |     |                     |      |
| sys_ver           | num  |     |                     |      |
| teenager_mode     | num  |     |                     |      |
| tel               | num  | √   |                     |      |
| ts                | num  | √   | 当前时间戳               | 单位：秒 |
| tv_brand          | str  |     |                     |      |
| uid               | num  |     |                     |      |
| sign              | str  | √   |                     |      |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                                                                      |
|---------|-----|------|-----------------------------------------------------------------------------------------|
| code    | num | 响应码  | 0：成功<br/>86202：验证码错误<br/>86205：验证码失效，请重新获取<br/>86206：区号不一致，请重新确认<br/>86207：手机号不一致，请重新确认 |
| message | str |      |                                                                                         |
| ttl     | num | 1    |                                                                                         |
| data    | obj | 信息本体 |                                                                                         |

### `data`对象

| 字段名           | 类型   | 内容        | 备注                  |
|---------------|------|-----------|---------------------|
| is_new        | bool |           |                     |
| mid           | num  | 当前用户id    |                     |
| access_token  | str  | 登录状态token |                     |
| refresh_token | str  | 刷新token   |                     |
| expires_in    | num  | 有效时长      | 固定为15552000秒，等于180天 |
| token_info    |      | `null`    |                     |
| cookie_info   |      | `null`    |                     |
| sso           |      | `null`    |                     |

## 请求示例

```shell
curl -L -X POST 'https://passport.snm0516.aisee.tv/x/passport-tv-login/login/sms?code=xxx&local_id=0&captcha_key=xxx&sign=xxx&appkey=4409e2ce8ffd12b8&tel=xxx&cid=86&ts=xxx'
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
    "token_info": null,
    "cookie_info": null,
    "sso": null
  }
}
```

</details>