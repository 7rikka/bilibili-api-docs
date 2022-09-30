# 查询token有效时间

> https://passport.snm0516.aisee.tv/x/passport-login/oauth2/info

请求方式：`GET`

是否需要登录：`是`

## URL参数

| 参数名               | 类型   | 必填  | 内容       | 备注  |
|-------------------|------|-----|----------|-----|
| access_key        | str  | √   | 登录的token |     |
| appkey            | str  | √   |          |     |
| bili_local_id     | str  |     |          |     |
| brand             | str  |     |          |     |
| build             | num  |     |          |     |
| buvid             | str  |     |          |     |
| channel           | str  |     |          |     |
| cpu               | str  |     |          |     |
| device            | str  |     |          |     |
| device_id         | str  |     |          |     |
| device_name       | str  |     |          |     |
| device_platform   | str  |     |          |     |
| explor_attr       | num  |     |          |     |
| fingerprint       | str  |     |          |     |
| fourk             | num  |     |          |     |
| guest_access_key  | str  |     |          |     |
| guest_id          | num  |     |          |     |
| guid              | str  |     |          |     |
| local_fingerprint | str  |     |          |     |
| local_id          | str  |     |          |     |
| memory            | num  |     |          |     |
| mobi_app          | str  |     |          |     |
| mode_switch       | bool |     |          |     |
| model             | str  |     |          |     |
| mpi_id            | str  |     |          |     |
| mpi_model         | str  |     |          |     |
| mpi_type          | str  |     |          |     |
| networkstate      | str  |     |          |     |
| platform          | str  |     |          |     |
| resource_id       | str  |     |          |     |
| statistics        | str  |     |          |     |
| sys_ver           | num  |     |          |     |
| teenager_mode     | num  |     |          |     |
| ts                | num  | √   |          |     |
| tv_brand          | str  |     |          |     |
| uid               | num  |     |          |     |
| sign              | str  | √   |          |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名          | 类型   | 内容          | 备注   |
|--------------|------|-------------|------|
| mid          | num  | 当前用户id      |      |
| access_token | str  | 登录token     |      |
| expires_in   | num  | token剩余有效时间 | 单位：秒 |
| refresh      | bool | 是否需要刷新      |      |

## 请求示例

```shell
curl -L -X GET 'https://passport.snm0516.aisee.tv/x/passport-login/oauth2/info?access_key=********************************&sign=********************************&appkey=4409e2ce8ffd12b8&ts=**********'
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
        "mid": 10086,
        "access_token": "********************************",
        "expires_in": 15551079,
        "refresh": false
    }
}
```
</details>