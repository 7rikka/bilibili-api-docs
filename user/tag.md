# 获取关注分组列表

> https://api.bilibili.com/x/relation/tags

请求方式：`GET`

是否需要登录：`是`

## Json回复

### 根对象

| 字段名     | 类型    | 内容   | 备注                  |
|---------|-------|------|---------------------|
| code    | num   | 响应码  | 0：成功<br/>-101：账号未登录 |
| message | str   |      |                     |
| ttl     | num   | 1    |                     |
| data    | array | 信息本体 |                     |

### `data`数组中的对象

| 字段名   | 类型  | 内容    | 备注  |
|-------|-----|-------|-----|
| tagid | num | 分组id  |     |
| name  | str | 分组名称  |     |
| count | num | 已添加人数 |     |
| tip   | str | 提示    |     |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/relation/tags' \
-H 'Cookie: SESSDATA=xxx'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "code": 0,
  "message": "0",
  "ttl": 1,
  "data": [
    {
      "tagid": -10,
      "name": "特别关注",
      "count": 29,
      "tip": "第一时间收到该分组下用户更新稿件的通知"
    },
    {
      "tagid": 0,
      "name": "默认分组",
      "count": 1276,
      "tip": ""
    }
  ]
}
```

</details>

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
| code    | num | 响应码  | 0：成功<br/>-101：账号未登录<br/>-111：csrf 校验失败<br/>-400：请求错误<br/>22101：分组名称命名不允许包含特殊字符<br/>22103：分组名称长度不超过16个字符<br/>22106：该分组已经存在 |
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
-H 'Cookie: SESSDATA=xxx' \
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

# 修改关注分组名称

> https://api.bilibili.com/x/relation/tag/update

请求方式：`POST`

是否需要登录：`是`

Content-Type：`application/x-www-form-urlencoded`

## FORM参数

| 参数名   | 类型  | 必填  | 内容     | 备注  |
|-------|-----|-----|--------|-----|
| tagid | num | √   | 分组id   |     |
| name  | str | √   | 分组名称   |     |
| csrf  | str | √   | 用户csrf |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                                                                                                                         |
|---------|-----|------|--------------------------------------------------------------------------------------------------------------------------------------------|
| code    | num | 响应码  | 0：成功<br/>-101：账号未登录<br/>-111：csrf 校验失败<br/>-400：请求错误<br/>22101：分组名称命名不允许包含特殊字符<br/>22103：分组名称长度不超过16个字符<br/>22104：该分组不存在<br/>22106：该分组已经存在 |
| message | str | 0    |                                                                                                                                            |
| ttl     | num | 1    |                                                                                                                                            |

## 请求示例

```shell
curl -L -X POST 'https://api.bilibili.com/x/relation/tag/update' \
-H 'Cookie: SESSDATA=xxx' \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'tagid=xxx' \
--data-urlencode 'name=xxx' \
--data-urlencode 'csrf=xxx'
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

# 删除关注分组

> https://api.bilibili.com/x/relation/tag/del

请求方式：`POST`

是否需要登录：`是`

Content-Type：`application/x-www-form-urlencoded`

## FORM参数

| 参数名   | 类型  | 必填  | 内容     | 备注  |
|-------|-----|-----|--------|-----|
| tagid | str | √   | 分组id   |     |
| csrf  | str | √   | 用户csrf |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                                   |
|---------|-----|------|------------------------------------------------------|
| code    | num | 响应码  | 0：成功<br/>-101：账号未登录<br/>-111：csrf 校验失败<br/>-400：请求错误 |
| message | str | 0    |                                                      |
| ttl     | num | 1    |                                                      |

## 请求示例

```shell
curl -L -X POST 'https://api.bilibili.com/x/relation/tag/del' \
-H 'Cookie: SESSDATA=xxx' \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'tagid=xxx' \
--data-urlencode 'csrf=xxx'
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

# 查看指定关注分组列表

> https://api.bilibili.com/x/relation/tag

请求方式：`GET`

是否需要登录：`是`

## URL参数

| 参数名   | 类型  | 必填  | 内容      | 备注                              |
|-------|-----|-----|---------|---------------------------------|
| mid   | num |     | 当前用户uid |                                 |
| tagid | num | √   | 关注分组id  | `-10`为`特别关注`分组<br/>最多有30个特别关注用户 |
| pn    | num |     | 当前页数    |                                 |
| ps    | num |     | 分页大小    | 取值范围：[1,50]                     |

## Json回复

### 根对象

| 字段名     | 类型    | 内容   | 备注                                |
|---------|-------|------|-----------------------------------|
| code    | num   | 响应码  | 0：成功<br/>-101：账号未登录<br/>-400：请求错误 |
| message | str   |      |                                   |
| ttl     | num   | 1    |                                   |
| data    | array | 信息本体 |                                   |

### `data`数组中的对象

| 字段名             | 类型   | 内容       | 备注  |
|-----------------|------|----------|-----|
| mid             | num  | 用户uid    |     |
| attribute       | num  | `0`      |     |
| tag             | null | `null`   |     |
| special         | num  | `0`      |     |
| contract_info   | obj  |          |     |
| uname           | str  | 用户名      |     |
| face            | str  | 头像       |     |
| sign            | str  | 签名       |     |
| face_nft        | num  | 是否为nft头像 |     |
| official_verify | obj  | 个人认证     |     |
| vip             | obj  | 大会员状态    |     |
| live            | obj  | 直播状态     |     |
| nft_icon        | str  |          |     |

### `data`数组中的对象 -> `contract_info`对象

| 字段名           | 类型   | 内容  | 备注  |
|---------------|------|-----|-----|
| is_contractor | bool |     |     |
| ts            | num  |     |     |
| is_contract   | bool |     |     |
| user_attr     | num  |     |     |

### `data`数组中的对象 -> `official_verify`对象

| 字段名  | 类型  | 内容  | 备注  |
|------|-----|-----|-----|
| type | num |     |     |
| desc | str |     |     |

### `data`数组中的对象 -> `vip`对象

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

### `data`数组中的对象 -> `vip`对象 -> `label`对象

| 字段名          | 类型  | 内容  | 备注  |
|--------------|-----|-----|-----|
| path         | str |     |     |
| text         | str |     |     |
| label_theme  | str |     |     |
| text_color   | str |     |     |
| bg_style     | num |     |     |
| bg_color     | str |     |     |
| border_color | str |     |     |

### `data`数组中的对象 -> `live`对象

| 字段名         | 类型  | 内容    | 备注               |
|-------------|-----|-------|------------------|
| live_status | num | 直播状态  | 0：未直播<br/>1：正在直播 |
| jump_url    | str | 直播间地址 |                  |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/relation/tag?tagid=-10&pn=1&ps=1' \
-H 'Cookie: SESSDATA=xxx'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "code": 0,
  "message": "0",
  "ttl": 1,
  "data": [
    {
      "mid": 624841994,
      "attribute": 0,
      "tag": null,
      "special": 0,
      "contract_info": {
        "is_contractor": false,
        "ts": 0,
        "is_contract": false,
        "user_attr": 0
      },
      "uname": "靠谱读书",
      "face": "https://i2.hdslb.com/bfs/face/4063c4a5040cacffd5c9a936ab18b61a6a239913.jpg",
      "sign": "陪你一起，读书成长～",
      "face_nft": 0,
      "official_verify": {
        "type": -1,
        "desc": ""
      },
      "vip": {
        "vipType": 1,
        "vipDueDate": 1594051200000,
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
      "live": {
        "live_status": 0,
        "jump_url": ""
      },
      "nft_icon": ""
    }
  ]
}
```

</details>