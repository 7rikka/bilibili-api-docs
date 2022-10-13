# 获取关注列表

> https://api.bilibili.com/x/relation/followings

请求方式：`GET`

是否需要登录：`是`

## URL参数

| 参数名        | 类型  | 必填   | 内容                            | 备注  |
|------------|-----|------|-------------------------------|-----|
| vmid       | str | √    | 查看其他用户关注列表，只能查看前5页            |     |
| pn         | num | 当前页数 |                               |     |
| ps         | num | 分页大小 | 范围：[1,50]                     |     |
| order      | str | 排序方式 | `desc`：降序排列<br/>`asc`升序排列     |     |
| order_type | str | 排序依据 | `空`：最近关注<br/>`attention`：最常访问 |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                                           |
|---------|-----|------|--------------------------------------------------------------|
| code    | num | 响应码  | 0：成功<br/>-400：请求错误<br/>22007：限制只访问前5页<br/>22115：用户已设置隐私，无法查看 |
| message | str | 0    |                                                              |
| ttl     | num | 1    |                                                              |
| data    | obj | 信息本体 |                                                              |

### `data`对象

| 字段名        | 类型    | 内容    | 备注  |
|------------|-------|-------|-----|
| list       | array | 数据列表  |     |
| re_version | num   | `0`   |     |
| total      | num   | 关注总人数 |     |

### `data`对象 -> `list`数组中的对象

| 字段名             | 类型    | 内容       | 备注               |
|-----------------|-------|----------|------------------|
| mid             | num   | 用户uid    |                  |
| attribute       | num   | 关系编号     | 2：已关注<br/>6：互相关注 |
| mtime           | num   |          |                  |
| tag             | array | 个人tag    |                  |
| special         | num   | 是否特别关注   | 0：否<br/>1：是      |
| contract_info   | obj   |          |                  |
| uname           | str   | 用户名      |                  |
| face            | str   | 头像       |                  |
| sign            | str   | 个人签名     |                  |
| face_nft        | num   | 是否NFT头像  | 0：否<br/>1：是      |
| official_verify | obj   | 认证信息     |                  |
| vip             | obj   | 大会员信息    |                  |
| nft_icon        | str   | NFT图标URL |                  |

### `data`对象 -> `list`数组中的对象 -> `contract_info`对象

| 字段名           | 类型   | 内容  | 备注  |
|---------------|------|-----|-----|
| is_contractor | bool |     |     |
| ts            | num  |     |     |
| is_contract   | bool |     |     |
| user_attr     | num  |     |     |

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
curl -L -X GET 'https://api.bilibili.com/x/relation/followings?vmid=10086&pn=1&ps=1&order=desc&order_type=attention' \
-H 'cookie: SESSDATA=xxx'
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
    "list": [
      {
        "mid": 11783021,
        "attribute": 2,
        "mtime": 1642346614,
        "tag": [
          -10
        ],
        "special": 1,
        "contract_info": {
          "is_contractor": false,
          "ts": 0,
          "is_contract": false,
          "user_attr": 0
        },
        "uname": "哔哩哔哩番剧出差",
        "face": "http://i2.hdslb.com/bfs/face/9f10323503739e676857f06f5e4f5eb323e9f3f2.jpg",
        "sign": "",
        "face_nft": 0,
        "official_verify": {
          "type": 1,
          "desc": "哔哩哔哩番剧出差 官方账号"
        },
        "vip": {
          "vipType": 0,
          "vipDueDate": 0,
          "dueRemark": "",
          "accessStatus": 0,
          "vipStatus": 0,
          "vipStatusWarn": "",
          "themeType": 0,
          "label": {
            "path": "",
            "text": "",
            "label_theme": "",
            "text_color": "",
            "bg_style": 0,
            "bg_color": "",
            "border_color": ""
          },
          "avatar_subscript": 0,
          "nickname_color": "",
          "avatar_subscript_url": ""
        },
        "nft_icon": ""
      }
    ],
    "re_version": 0,
    "total": 1309
  }
}
```

</details>