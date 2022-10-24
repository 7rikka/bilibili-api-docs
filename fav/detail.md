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