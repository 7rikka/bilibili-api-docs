# 关注/取消关注用户

> https://api.bilibili.com/x/relation/modify

请求方式：`POST`

是否需要登录：`是`

鉴权方式：`SESSDATA`/`access_key`

Content-Type：`application/x-www-form-urlencoded`

## FORM参数

| 参数名            | 类型  | 必填  | 内容       | 备注                                      |
|----------------|-----|-----|----------|-----------------------------------------|
| fid            | num | √   | 被关注用户uid |                                         |
| act            | num | √   | 操作类型     | 1：关注<br/>2：取消关注<br/>3：悄悄关注<br/>4：取消悄悄关注 |
| re_src         | num |     |          |                                         |
| spmid          | str |     |          |                                         |
| extend_content | str |     |          |                                         |
| jsonp          | str |     |          |                                         |
| csrf           | str | √   | 用户csrf   | `SESSDATA`方式需要                          |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                          |
|---------|-----|------|---------------------------------------------|
| code    | num | 响应码  | 0：成功<br/>22013：账号已注销，无法完成操作<br/>40061：用户不存在 |
| message | str |      |                                             |
| ttl     | num | 1    |                                             |
| data    | obj | 信息本体 |                                             |

## 请求示例

### `SESSDATA`方式

```shell
curl -L -X POST 'https://api.bilibili.com/x/relation/modify' \
-H 'cookie: SESSDATA=xxx' \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'fid=xxx' \
--data-urlencode 'act=1' \
--data-urlencode 'csrf=xxx'
```

### `access_key`方式

```shell
curl -L -X POST 'https://api.bilibili.com/x/relation/modify' \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'access_key=xxx' \
--data-urlencode 'act=1' \
--data-urlencode 'fid=xxx'
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