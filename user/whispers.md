# 获取我的悄悄关注列表

> https://api.bilibili.com/x/relation/whispers

请求方式：`GET`

是否需要登录：`是`

## URL参数

| 参数名 | 类型  | 必填  | 内容  | 备注  |
|-----|-----|-----|-----|-----|
| pn  | num |     |     |     |
| ps  | num |     |     |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名        | 类型    | 内容  | 备注  |
|------------|-------|-----|-----|
| list       | array |     |     |
| re_version | num   |     |     |

### `data`对象 -> `list`数组中的对象

| 字段名             | 类型   | 内容  | 备注  |
|-----------------|------|-----|-----|
| mid             | num  |     |     |
| attribute       | num  |     |     |
| mtime           | num  |     |     |
| tag             | null |     |     |
| special         | num  |     |     |
| uname           | str  |     |     |
| face            | str  |     |     |
| sign            | str  |     |     |
| face_nft        | num  |     |     |
| official_verify | obj  |     |     |
| vip             | obj  |     |     |
| nft_icon        | str  |     |     |

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
curl -L -X GET 'https://api.bilibili.com/x/relation/whispers?pn=1&ps=1' \
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
        "mid": 928123,
        "attribute": 1,
        "mtime": 1665669032,
        "tag": null,
        "special": 0,
        "uname": "哔哩哔哩番剧",
        "face": "https://i1.hdslb.com/bfs/face/d094f4dd5086321351c72068e86623e46d8eb12b.jpg",
        "sign": "关注最帅的官号，你就成为最帅的粉丝了！↗",
        "face_nft": 0,
        "official_verify": {
          "type": 1,
          "desc": "哔哩哔哩番剧区官方账号"
        },
        "vip": {
          "vipType": 2,
          "vipDueDate": 1967126400000,
          "dueRemark": "",
          "accessStatus": 0,
          "vipStatus": 1,
          "vipStatusWarn": "",
          "themeType": 0,
          "label": {
            "path": "",
            "text": "十年大会员",
            "label_theme": "ten_annual_vip",
            "text_color": "#FFFFFF",
            "bg_style": 1,
            "bg_color": "#FB7299",
            "border_color": ""
          },
          "avatar_subscript": 1,
          "nickname_color": "#FB7299",
          "avatar_subscript_url": ""
        },
        "nft_icon": ""
      }
    ],
    "re_version": 0
  }
}
```

</details>