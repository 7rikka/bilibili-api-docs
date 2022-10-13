# relation

| attribute           | 说明      |
|---------------------|---------|
| 1                   | 悄悄关注了对方 |
| 2                   | 关注了对方   |
| 2,special=1,tag=-10 | 特别关注了对方 |
| 6                   | 双方互相关注  |
| 128                 | 拉黑了对方   |

# 获取粉丝列表

> https://api.bilibili.com/x/relation/followers

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名        | 类型  | 必填  | 内容    | 备注                                         |
|------------|-----|-----|-------|--------------------------------------------|
| vmid       | num | √   | 用户uid |                                            |
| pn         | num |     | 页数    | 查看他人的粉丝列表只能获得前5页数据<br/>查看自己的粉丝列表只能获得前20页数据 |
| ps         | num |     | 分页大小  |                                            |
| order      | str |     | 排序方式  | `desc`                                     |
| order_type | str |     | 排序类型  | `attention`                                |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                    |
|---------|-----|------|---------------------------------------|
| code    | num | 响应码  | 0：成功<br/>-400：请求错误<br/>22007：限制只访问前5页 |
| message | str | 0    |                                       |
| ttl     | num | 1    |                                       |
| data    | obj | 信息本体 |                                       |

### `data`对象

| 字段名        | 类型    | 内容     | 备注  |
|------------|-------|--------|-----|
| list       | array | 用户信息列表 |     |
| re_version | num   | `0`    |     |
| total      | num   | 粉丝总数   |     |

### `data`对象 -> `list`数组中的对象

| 字段名             | 类型  | 内容     | 备注                            |
|-----------------|-----|--------|-------------------------------|
| mid             | num |        |                               |
| attribute       | num |        | 0：未关注<br />2：已关注对方<br />6：已互粉 |
| mtime           | num |        |                               |
| tag             |     | `null` |                               |
| special         | num |        |                               |
| contract_info   | obj |        |                               |
| uname           | str |        |                               |
| face            | str |        |                               |
| face_nft        | num |        |                               |
| sign            | str |        |                               |
| official_verify | obj |        |                               |
| vip             | obj |        |                               |
| nft_icon        | str |        |                               |

### `data`对象 -> `list`数组中的对象 -> `contract_info`对象

| 字段名           | 类型   | 内容      | 备注  |
|---------------|------|---------|-----|
| is_contractor | bool | `false` |     |
| ts            | num  | `0`     |     |
| is_contract   | bool | `false` |     |
| user_attr     | num  | `0`     |     |

### `data`对象 -> `list`数组中的对象 -> `official_verify`对象

| 字段名  | 类型  | 内容  | 备注  |
|------|-----|-----|-----|
| type | num |     |     |
| desc | str |     |     |

### `data`对象 -> `list`数组中的对象 -> `vip`对象

| 字段名                  | 类型  | 内容  | 备注  |
|----------------------|-----|-----|-----|
| vipType              | num |     |     |
| vipDueDate           | num |     |     |
| dueRemark            | str |     |     |
| accessStatus         | num |     |     |
| vipStatus            | num |     |     |
| vipStatusWarn        | str |     |     |
| themeType            | num |     |     |
| label                | obj |     |     |
| avatar_subscript     | num |     |     |
| nickname_color       | str |     |     |
| avatar_subscript_url | str |     |     |

### `data`对象 -> `list`数组中的对象 -> `vip`对象 -> `label`对象

| 字段名          | 类型  | 内容  | 备注  |
|--------------|-----|-----|-----|
| path         | str |     |     |
| text         | str |     |     |
| label_theme  | str |     |     |
| text_color   | str |     |     |
| bg_style     | num |     |     |
| bg_color     | str |     |     |
| border_color | str |     |     |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/relation/followers?vmid=10086&pn=1&ps=20&order=desc&order_type=attention' \
-H 'cookie: SESSDATA=xxx'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json

```

</details>