> https://www.bilibili.com/medialist/detail/ml1172134631

# 获取收藏夹信息

> https://api.bilibili.com/x/v3/fav/folder/info

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名      | 类型  | 必填  | 内容    | 备注  |
|----------|-----|-----|-------|-----|
| media_id | num | √   | 收藏夹id |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名         | 类型  | 内容            | 备注  |
|-------------|-----|---------------|-----|
| id          | num | 收藏夹id         |     |
| fid         | num | 收藏夹短id        |     |
| mid         | num | UP主UID        |     |
| attr        | num | `0` `22` `55` |     |
| title       | str | 收藏夹标题         |     |
| cover       | str | 收藏夹封面         |     |
| upper       | obj | UP主信息         |     |
| cover_type  | num | `0` `2`       |     |
| cnt_info    | obj | 数据统计信息        |     |
| type        | num | `11`          |     |
| intro       | str | 收藏夹简介         |     |
| ctime       | num | 创建时间戳         |     |
| mtime       | num | 修改时间戳         |     |
| state       | num | `0`           |     |
| fav_state   | num | 当前用户是否收藏      |     |
| like_state  | num | 当前用户是否点赞      |     |
| media_count | num | 包含视频数         |     |

### `data`对象 -> `upper`对象

| 字段名        | 类型   | 内容     | 备注                              |
|------------|------|--------|---------------------------------|
| mid        | num  | UP主UID |                                 |
| name       | str  | UP主名称  |                                 |
| face       | str  | 头像     |                                 |
| followed   | bool | 是否关注   |                                 |
| vip_type   | num  | 大会员类型  | 0：无<br />1：月大会员<br />2：年度及以上大会员 |
| vip_statue | num  | 是否是大会员 | 0：无<br />1：有                    |

### `data`对象 -> `cnt_info`对象

| 字段名      | 类型  | 内容  | 备注  |
|----------|-----|-----|-----|
| collect  | num | 收藏数 |     |
| play     | num | 播放数 |     |
| thumb_up | num | 点赞数 |     |
| share    | num | 转发数 |     |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/v3/fav/folder/info?media_id=1172134631'
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
        "id": 1172134631,
        "fid": 11721346,
        "mid": 63231,
        "attr": 22,
        "title": "泛式生贺合集",
        "cover": "http://i2.hdslb.com/bfs/archive/9de62df037b585af287655ecc03f540b66e97b1a.jpg",
        "upper": {
            "mid": 63231,
            "name": "泛式",
            "face": "https://i0.hdslb.com/bfs/face/2608aaa45309c77ac88fbfaa40e160b8c7892985.jpg",
            "followed": false,
            "vip_type": 2,
            "vip_statue": 1
        },
        "cover_type": 2,
        "cnt_info": {
            "collect": 87,
            "play": 313,
            "thumb_up": 138,
            "share": 2
        },
        "type": 11,
        "intro": "",
        "ctime": 1612699461,
        "mtime": 1644502129,
        "state": 0,
        "fav_state": 0,
        "like_state": 0,
        "media_count": 27
    }
}
```

</details>

# 获取收藏夹内视频id列表

> https://api.bilibili.com/x/v3/fav/resource/ids

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名      | 类型  | 必填  | 内容    | 备注  |
|----------|-----|-----|-------|-----|
| media_id | num | √   | 收藏夹id |     |
| platform | str |     | `web` |     |

## Json回复

### 根对象

| 字段名     | 类型    | 内容   | 备注   |
|---------|-------|------|------|
| code    | num   | 响应码  | 0：成功 |
| message | str   | 0    |      |
| ttl     | num   | 1    |      |
| data    | array | 信息本体 |      |

### `data`数组中的对象

| 字段名   | 类型  | 内容    | 备注  |
|-------|-----|-------|-----|
| id    | num | 视频AV号 |     |
| type  | num | `2`   |     |
| bv_id | str | 视频BV号 |     |
| bvid  | str | 视频BV号 |     |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/v3/fav/resource/ids?media_id=1172134631'
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
            "id": 893951834,
            "type": 2,
            "bv_id": "BV1NP4y1w7xX",
            "bvid": "BV1NP4y1w7xX"
        },
        {
            "id": 423913579,
            "type": 2,
            "bv_id": "BV1z3411j7tg",
            "bvid": "BV1z3411j7tg"
        },
        {
            "id": 211444690,
            "type": 2,
            "bv_id": "BV1ka411y7TT",
            "bvid": "BV1ka411y7TT"
        },
        {
            "id": 211457958,
            "type": 2,
            "bv_id": "BV1da411y757",
            "bvid": "BV1da411y757"
        },
        {
            "id": 678876532,
            "type": 2,
            "bv_id": "BV17m4y1Z7WH",
            "bvid": "BV17m4y1Z7WH"
        },
        {
            "id": 766219252,
            "type": 2,
            "bv_id": "BV1Yr4y1Y7vt",
            "bvid": "BV1Yr4y1Y7vt"
        },
        {
            "id": 551265567,
            "type": 2,
            "bv_id": "BV1Vq4y1c7D5",
            "bvid": "BV1Vq4y1c7D5"
        },
        {
            "id": 636427030,
            "type": 2,
            "bv_id": "BV1Bb4y177jD",
            "bvid": "BV1Bb4y177jD"
        },
        {
            "id": 893380157,
            "type": 2,
            "bv_id": "BV1UP4y177fs",
            "bvid": "BV1UP4y177fs"
        },
        {
            "id": 508989049,
            "type": 2,
            "bv_id": "BV1Ru41197QC",
            "bvid": "BV1Ru41197QC"
        },
        {
            "id": 678776271,
            "type": 2,
            "bv_id": "BV11m4y1o77Q",
            "bvid": "BV11m4y1o77Q"
        },
        {
            "id": 759565841,
            "type": 2,
            "bv_id": "BV1q64y1B7NF",
            "bvid": "BV1q64y1B7NF"
        },
        {
            "id": 289083348,
            "type": 2,
            "bv_id": "BV1vf4y1r7uV",
            "bvid": "BV1vf4y1r7uV"
        },
        {
            "id": 629053329,
            "type": 2,
            "bv_id": "BV1Dt4y1B7XF",
            "bvid": "BV1Dt4y1B7XF"
        },
        {
            "id": 799048549,
            "type": 2,
            "bv_id": "BV13y4y1Y7pz",
            "bvid": "BV13y4y1Y7pz"
        },
        {
            "id": 501703224,
            "type": 2,
            "bv_id": "BV1ZN411R72f",
            "bvid": "BV1ZN411R72f"
        },
        {
            "id": 289040110,
            "type": 2,
            "bv_id": "BV1Gf4y1r72i",
            "bvid": "BV1Gf4y1r72i"
        },
        {
            "id": 714078203,
            "type": 2,
            "bv_id": "BV1SX4y1N77m",
            "bvid": "BV1SX4y1N77m"
        },
        {
            "id": 886613303,
            "type": 2,
            "bv_id": "BV1tK4y1n725",
            "bvid": "BV1tK4y1n725"
        },
        {
            "id": 971604155,
            "type": 2,
            "bv_id": "BV18p4y1p7fQ",
            "bvid": "BV18p4y1p7fQ"
        },
        {
            "id": 629100762,
            "type": 2,
            "bv_id": "BV1dt4y1B7mB",
            "bvid": "BV1dt4y1B7mB"
        },
        {
            "id": 374095829,
            "type": 2,
            "bv_id": "BV13o4y197wh",
            "bvid": "BV13o4y197wh"
        },
        {
            "id": 246702017,
            "type": 2,
            "bv_id": "BV1ev411a7Kv",
            "bvid": "BV1ev411a7Kv"
        },
        {
            "id": 246575155,
            "type": 2,
            "bv_id": "BV1Bv411e7gr",
            "bvid": "BV1Bv411e7gr"
        },
        {
            "id": 288941965,
            "type": 2,
            "bv_id": "BV1kf4y167Br",
            "bvid": "BV1kf4y167Br"
        },
        {
            "id": 459230557,
            "type": 2,
            "bv_id": "BV1j5411E7B9",
            "bvid": "BV1j5411E7B9"
        },
        {
            "id": 971653786,
            "type": 2,
            "bv_id": "BV1ip4y1p7FB",
            "bvid": "BV1ip4y1p7FB"
        }
    ]
}
```

</details>