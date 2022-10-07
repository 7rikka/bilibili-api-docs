# 接口名

> 接口URL

请求方式：`POST`
请求方式：`GET`

是否需要登录：`是`
是否需要登录：`否`

鉴权方式：`SESSDATA`/`access_key`

Content-Type：`application/x-www-form-urlencoded`
Content-Type：`application/json`

## URL参数

| 参数名      | 类型  | 必填  | 内容   | 备注                                |
|----------|-----|-----|------|-----------------------------------|
| xxx      | str |     |      |                                   |

## FORM参数

| 参数名 | 类型  | 必填  | 内容  | 备注  |
|-----|-----|-----|-----|-----|
| xxx | str |     |     |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名 | 类型  | 内容  | 备注  |
|-----|-----|-----|-----|
| xxx | str |     |     |

## 请求示例

```shell

```

## 响应示例

<details>
<summary>点击查看</summary>

```json

```
</details>