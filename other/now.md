# 获取当前时间戳

> https://api.bilibili.com/x/report/click/now

请求方式：`GET`

是否需要登录：`否`

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名 | 类型  | 内容    | 备注   |
|-----|-----|-------|------|
| now | num | 当前时间戳 | 单位：秒 |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/report/click/now'
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
    "now": 1664981275
  }
}
```

</details>