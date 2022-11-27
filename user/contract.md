# 加入老粉计划

> https://api.bilibili.com/x/v1/contract/add_contract

请求方式：`POST`

是否需要登录：`是`

鉴权方式：`SESSDATA`

Content-Type：`application/x-www-form-urlencoded`

## FORM参数

| 参数名      | 类型  | 必填  | 内容     | 备注  |
|----------|-----|-----|--------|-----|
| aid      | str |     | `空串`   |     |
| up_mid   | str | √   | UP主UID |     |
| source   | str |     | `4`    |     |
| scene    | str |     | `105`  |     |
| platform | str |     | `web`  |     |
| mobi_app | str |     | `pc`   |     |
| csrf     | str | √   | 用户csrf |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                      |
|---------|-----|------|-------------------------|
| code    | num | 响应码  | 0：成功<br/>158001：`不满足条件` |
| message | str | 0    |                         |
| ttl     | num | 1    |                         |
| data    | obj | 信息本体 |                         |

### `data`对象

| 字段名           | 类型   | 内容                                | 备注  |
|---------------|------|-----------------------------------|-----|
| allow_message | bool | `true`                            |     |
| input_text    | str  | `UP主加油！看好你噢`                      |     |
| input_title   | str  | `感谢你对UP主的特别支持，“老粉”可期！私信留言鼓励下TA吧 ` |     |

## 请求示例

### `SESSDATA`方式

```shell
curl --location --request POST 'https://api.bilibili.com/x/v1/contract/add_contract' \
--header 'Cookie: SESSDATA=xxx' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'up_mid=2' \
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
    "allow_message": true,
    "input_text": "UP主加油！看好你噢",
    "input_title": "感谢你对UP主的特别支持，“老粉”可期！私信留言鼓励下TA吧 "
  }
}
```

</details>