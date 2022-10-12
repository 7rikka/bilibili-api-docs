# 创建关注分组

> https://api.bilibili.com/x/relation/tag/create

请求方式：`POST`

是否需要登录：`是`

Content-Type：`application/x-www-form-urlencoded`

## FORM参数

| 参数名  | 类型  | 必填  | 内容     | 备注  |
|------|-----|-----|--------|-----|
| tag  | str | √   | 分组名称   |     |
| csrf | str | √   | 用户csrf |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                                                                                                        |
|---------|-----|------|---------------------------------------------------------------------------------------------------------------------------|
| code    | num | 响应码  | 0：成功<br/>-101：账号未登录<br/>-400：请求错误<br/>-111：csrf 校验失败<br/>22101：分组名称命名不允许包含特殊字符<br/>22103：分组名称长度不超过16个字符<br/>22106：该分组已经存在 |
| message | str | 0    |                                                                                                                           |
| ttl     | num | 1    |                                                                                                                           |
| data    | obj | 信息本体 |                                                                                                                           |

### `data`对象

| 字段名   | 类型  | 内容   | 备注  |
|-------|-----|------|-----|
| tagid | num | 分组id |     |

## 请求示例

```shell
curl -L -X POST 'https://api.bilibili.com/x/relation/tag/create' \
-H 'cookie: SESSDATA=xxx' \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'tag=1' \
--data-urlencode 'csrf=xxx'
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
        "tagid": 10086
    }
}
```

</details>