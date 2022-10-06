# 退出登录

> https://passport.bilibili.com/x/passport-login/revoke

请求方式：`POST`

是否需要登录：`是`

Content-Type：`application/x-www-form-urlencoded`

## URL参数

| 参数名             | 类型  | 必填  | 内容    | 备注   |
|-----------------|-----|-----|-------|------|
| access_key      | str | √   |       |      |
| appkey          | str | √   |       |      |
| bili_local_id   | str |     |       |      |
| build           | str |     |       |      |
| buvid           | str |     |       |      |
| c_locale        | str |     |       |      |
| channel         | str |     |       |      |
| device          | str |     |       |      |
| device_id       | str |     |       |      |
| device_name     | str |     |       |      |
| device_platform | str |     |       |      |
| local_id        | str |     |       |      |
| mobi_app        | str |     |       |      |
| platform        | str |     |       |      |
| s_locale        | str |     |       |      |
| ts              | str | √   | 当前时间戳 | 单位：秒 |
| sign            | str | √   |       |      |

## Json回复

### 根对象

| 字段名     | 类型  | 内容  | 备注                                    |
|---------|-----|-----|---------------------------------------|
| code    | num | 响应码 | 0：成功<br/>-3：API校验密匙错误<br/> -101：账号未登录 |
| message | str |     |                                       |
| ttl     | num | 1   |                                       |

## 请求示例

```shell
curl -L -X POST 'https://passport.bilibili.com/x/passport-login/revoke?appkey=8d23902c1688a798&access_key=xxx&sign=xxx&ts=1664520774'
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