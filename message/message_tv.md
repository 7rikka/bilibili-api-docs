# 获取通知中心信息

> https://api.snm0516.aisee.tv/x/tv/message/list

请求方式：`GET`

是否需要登录：`否`

Content-Type：`application/x-www-form-urlencoded`

## URL参数

| 参数名              | 类型   | 必填   | 内容                | 备注  |
|------------------|------|------|-------------------|-----|
| access_key       | str  |      |                   |     |
| appkey           | str  |      |                   |     |
| brand            | str  |      |                   |     |
| build            | num  |      |                   |     |
| channel          | str  |      |                   |     |
| cpu              | str  |      |                   |     |
| cursor_id        | num  |      |                   |     |
| explor_attr      | num  |      |                   |     |
| fourk            | num  |      |                   |     |
| guest_access_key | str  |      |                   |     |
| guest_id         | num  |      |                   |     |
| memory           | num  |      |                   |     |
| mobi_app         | str  |      |                   |     |
| mode_switch      | bool |      |                   |     |
| model            | str  |      |                   |     |
| mpi_id           | str  |      |                   |     |
| mpi_model        | str  |      |                   |     |
| mpi_type         | str  |      |                   |     |
| platform         | str  |      |                   |     |
| resource_id      | str  |      |                   |     |
| statistics       | str  |      |                   |     |
| sys_ver          | num  |      |                   |     |
| teenager_mode    | num  |      |                   |     |
| ts               | num  |      |                   |     |
| tv_brand         | str  |      |                   |     |
| type             | num  | 通知类别 | 1：系统通知<br/>2：预约提醒 |     |
| uid              | num  |      |                   |     |
| sign             | str  |      |                   |     |
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

TODO

## 请求示例

```shell

```

## 响应示例

<details>
<summary>点击查看</summary>

```json

```
</details>