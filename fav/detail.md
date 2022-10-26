# 页面地址

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
| face       | str  | UP主头像  |                                 |
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

# 获取收藏夹内视频详细信息

> https://api.bilibili.com/x/v3/fav/resource/infos

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名        | 类型  | 必填  | 内容     | 备注                                                              |
|------------|-----|-----|--------|-----------------------------------------------------------------|
| resources  | str | √   | 查询参数   | 通过[获取收藏夹内视频id列表](#获取收藏夹内视频id列表)返回结果生成，格式为`id:type`，使用英文逗号连接的字符串 |
| platform   | str |     | `web`  |                                                                 |
| folder_mid | num |     | 收藏夹id  |                                                                 |
| folder_id  | num |     | UP主UID |                                                                 |

## Json回复

### 根对象

| 字段名     | 类型    | 内容   | 备注   |
|---------|-------|------|------|
| code    | num   | 响应码  | 0：成功 |
| message | str   | 0    |      |
| ttl     | num   | 1    |      |
| data    | array | 信息本体 |      |

### `data`数组中的对象

| 字段名      | 类型   | 内容    | 备注                                      |
|----------|------|-------|-----------------------------------------|
| id       | num  | 指向id  | 2：视频AV号<br/>12：音频AUID<br/>24：剧集SeasonId |
| type     | num  | 视频类型  | 2：视频<br/>12：音频<br/>24：剧集                |
| title    | str  | 标题    |                                         |
| cover    | str  | 封面    |                                         |
| intro    | str  | 简介    |                                         |
| page     | num  | 分p数   |                                         |
| duration | num  | 长度    | 单位：秒                                    |
| upper    | obj  | UP主信息 |                                         |
| attr     | num  | 属性位   | 0：正常<br/>9：已失效                          |
| cnt_info | obj  | 统计信息  |                                         |
| link     | str  | 播放链接  |                                         |
| ctime    | num  | 上传时间  |                                         |
| pubtime  | num  | 发布时间  |                                         |
| fav_time | num  | 收藏时间  |                                         |
| bv_id    | str  | 视频BV号 |                                         |
| bvid     | str  | 视频BV号 |                                         |
| season   | null |       |                                         |
| ogv      | null |       |                                         |
| ugc      | obj  |       |                                         |

### `data`数组中的对象 -> `upper`对象

| 字段名  | 类型  | 内容     | 备注  |
|------|-----|--------|-----|
| mid  | num | UP主UID |     |
| name | str | UP主名称  |     |
| face | str | UP主头像  |     |

### `data`数组中的对象 -> `cnt_info`对象

| 字段名     | 类型  | 内容  | 备注  |
|---------|-----|-----|-----|
| collect | num | 收藏数 |     |
| play    | num | 播放数 |     |
| danmaku | num | 点赞数 |     |

### `data`数组中的对象 -> `ugc`对象

| 字段名       | 类型  | 内容        | 备注  |
|-----------|-----|-----------|-----|
| first_cid | num | 第一个分p的cid |     |

### `data`数组中的对象 -> `ogv`对象

| 字段名       | 类型  |     | 内容         | 备注  |
|-----------|-----|-----|------------|-----|
| type_name | str |     | 剧集类型名称     |     |
| type_id   | num |     | 剧集类型id     |     |
| season_id | num |     | 剧集seasonId |     |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/v3/fav/resource/infos?resources=893951834:2,423913579:2,211444690:2,211457958:2,678876532:2,766219252:2,551265567:2,636427030:2,893380157:2,508989049:2,678776271:2,759565841:2,289083348:2,629053329:2,799048549:2,501703224:2,289040110:2,714078203:2,886613303:2,971604155:2'
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
            "title": "【泛式生贺·描改手书】星期一的忧郁（诶嘿酱永远单推！！）",
            "cover": "http://i2.hdslb.com/bfs/archive/9de62df037b585af287655ecc03f540b66e97b1a.jpg",
            "intro": "原作：┗|∵|┓ 月曜日の憂鬱/天月 feat. HoneyWorks（sm35367532）\n使用翻唱曲：Nako-av59496948（已授权）\n描改绘图：贰圆です\n视频后期：阿瓜\n\n泛哥哥生日快乐！！！\n因为是社畜，这个手书真的花了好久的时间【泪目】特别感觉阿瓜帮我制作成了视频，没有阿瓜就没有这个视频。\n也特别谢谢Nako小姐姐的翻唱~~。\n希望阿泛能喜欢这个手书，祝阿泛天天开心身体健康【比心】",
            "page": 1,
            "duration": 123,
            "upper": {
                "mid": 880754,
                "name": "贰圆です",
                "face": "https://i2.hdslb.com/bfs/face/070345212181c667bbef1ed954169c70ba840b98.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 2618,
                "play": 41840,
                "danmaku": 57
            },
            "link": "bilibili://video/893951834",
            "ctime": 1644422732,
            "pubtime": 1644422732,
            "fav_time": 0,
            "bv_id": "BV1NP4y1w7xX",
            "bvid": "BV1NP4y1w7xX",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 505137655
            }
        },
        {
            "id": 423913579,
            "type": 2,
            "title": "【泛式/生贺mep】妄想税",
            "cover": "http://i2.hdslb.com/bfs/archive/373389940d7658c77f3a1ffce0705ad04439a7b9.jpg",
            "intro": "主催：朽木Naityks\n制作：下播型泛式录播组\n绘制：千千里\n制作协力：顺其自燃 滑稽型泛式 cat39 工程师也要取材\n特别鸣谢：主播丶潜质 牧羊迪 超高校级的卷毛\nBGM：妄想税 - DECO＊27,初音ミク\n本家：BV1Cs411f7DA\n参考：BV1u7411q71S BV17v411a7p2 BV1WW411x7tv BV1Wa411q7Jb",
            "page": 1,
            "duration": 85,
            "upper": {
                "mid": 6964677,
                "name": "朽木Naityks",
                "face": "https://i0.hdslb.com/bfs/face/6c16bf34a4079cbb96cfe670524923e38b4005de.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 3595,
                "play": 147091,
                "danmaku": 163
            },
            "link": "bilibili://video/423913579",
            "ctime": 1644420462,
            "pubtime": 1644422405,
            "fav_time": 0,
            "bv_id": "BV1z3411j7tg",
            "bvid": "BV1z3411j7tg",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 506634114
            }
        },
        {
            "id": 211444690,
            "type": 2,
            "title": "【泛竹手书 || 泛式2022生贺】ミライチズ-未来蓝图",
            "cover": "http://i0.hdslb.com/bfs/archive/1d0c4f2c245c1edd97c02a987ae15454dbfadf87.jpg",
            "intro": "原曲：BV1cS4y117So\n（请不要去原曲底下评论，也不要在评论区发无关信息）\n祝泛式2022年生日快乐！\n之前一直是视频粉丝，去年才开始看直播然后沉迷其中一发不可收拾hhhh\n非常喜欢阿泛和竹鱼姐！祝阿泛新的一岁里能少点破事！有更多时间能做想做的事情！\n祝阿泛和竹鱼姐天天开心！\n\n特别感谢参演的﻿@下播型泛式录播组 ",
            "page": 1,
            "duration": 241,
            "upper": {
                "mid": 493491,
                "name": "很普通的Pikari",
                "face": "https://i0.hdslb.com/bfs/face/8cda7fc598d9cec65cafb536a97c90740adbf7f2.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 4567,
                "play": 127985,
                "danmaku": 187
            },
            "link": "bilibili://video/211444690",
            "ctime": 1644454825,
            "pubtime": 1644454811,
            "fav_time": 0,
            "bv_id": "BV1ka411y7TT",
            "bvid": "BV1ka411y7TT",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 505167924
            }
        },
        {
            "id": 211457958,
            "type": 2,
            "title": "【泛式/2022生贺】那什么的泛八爷",
            "cover": "http://i1.hdslb.com/bfs/archive/92150b94ea278ab1a2de966346d8e9bc09b243fd.png",
            "intro": "描改手书：BV1Ds411S7d2\r\nBGM：小西克幸 - なんかのさなぎ\r\n祝泛老师生日快乐！\r\n祝阿泛和竹鱼姐永远幸福！",
            "page": 1,
            "duration": 156,
            "upper": {
                "mid": 30311024,
                "name": "暖风吹喵",
                "face": "https://i2.hdslb.com/bfs/face/b7252226f7b91dacf258834380355e1d5e644957.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 247,
                "play": 6770,
                "danmaku": 49
            },
            "link": "bilibili://video/211457958",
            "ctime": 1644423732,
            "pubtime": 1644426029,
            "fav_time": 0,
            "bv_id": "BV1da411y757",
            "bvid": "BV1da411y757",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 505153214
            }
        },
        {
            "id": 678876532,
            "type": 2,
            "title": "【泛式2022生贺】直播中的泛哥哥【手书】",
            "cover": "http://i2.hdslb.com/bfs/archive/90ce094b79fb47cf12005527422c8a1b37912d6a.jpg",
            "intro": "再贴一次原视频素材：\nBV1oK4y197bH\nBV1xK4y1J7pS\nBV15y4y1T7zb\nBV1h54y1W72w\n\nidea来源：はとくべ樣\n【YouTube】https://www.youtube.com/channel/UClgnCQJmkwUytgEHu-32OQA\n【Twitter】https://twitter.com/hatocube\n\n泛哥哥生日快乐！！\n\n（以下是无关紧要碎碎念：第一次做手书献给了大鼻子叔叔（bushi) 我根本不会画画，绘画水平是让小学美术老师都头疼的程度，（",
            "page": 1,
            "duration": 304,
            "upper": {
                "mid": 23556492,
                "name": "脚底板好痛",
                "face": "https://i0.hdslb.com/bfs/face/7132f6bb2207759f6cc4adeb0d2cd9aa5b5b1c68.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 583,
                "play": 15991,
                "danmaku": 48
            },
            "link": "bilibili://video/678876532",
            "ctime": 1644306097,
            "pubtime": 1644422405,
            "fav_time": 0,
            "bv_id": "BV17m4y1Z7WH",
            "bvid": "BV17m4y1Z7WH",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 503967733
            }
        },
        {
            "id": 766219252,
            "type": 2,
            "title": "【泛式生贺手书】我，稻草人",
            "cover": "http://i0.hdslb.com/bfs/archive/cb6f3e1ce1c07b67abebb1d8bc64aa727f505953.jpg",
            "intro": "祝泛泛生日快乐！\n本家：sm32788993 （站内搬运：BV1nW41147ad ）\n原作：あめのむらくもP\n原唱：GUMI",
            "page": 1,
            "duration": 193,
            "upper": {
                "mid": 24344133,
                "name": "依尔芙琳Elfring",
                "face": "https://i0.hdslb.com/bfs/face/2f87a2347878de001fcaeac5d070719887f9618a.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 28,
                "play": 746,
                "danmaku": 1
            },
            "link": "bilibili://video/766219252",
            "ctime": 1644422407,
            "pubtime": 1644422405,
            "fav_time": 0,
            "bv_id": "BV1Yr4y1Y7vt",
            "bvid": "BV1Yr4y1Y7vt",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 499859795
            }
        },
        {
            "id": 551265567,
            "type": 2,
            "title": "诶嘿酱，我真的好喜欢你啊！【泛式生贺|仿麦德】",
            "cover": "http://i2.hdslb.com/bfs/archive/5e5b40b76e3d2dcd54530614fac044d3b64dd713.jpg",
            "intro": "感谢一年来为诶嘿酱画图的太太们！今天带大家回顾一下可爱的一岁诶嘿酱（>_<）\n顺便祝泛式生日快乐吧。\n----------------------------------\n第一次做MAD，只能当学生纯抄了\n本家BV1U54y117gq（姚姐2022年新生报到（）\n\n\n画师从前至后依次为：\n路人乙_lry、清凇凇、南斯拉夫蜥蜴、空_iceeeee、北冥海岸、AsunaWhite空白、YOYO麻薯、顺其自燃、冰冰冰冰冰释、贰圆です、DODO-SUPER11、御水银秋、权凛子、阿沐木沐木、阳戈不是秧歌、九条凛奏",
            "page": 1,
            "duration": 89,
            "upper": {
                "mid": 87809529,
                "name": "順其自燃LQR",
                "face": "https://i0.hdslb.com/bfs/face/ca6ba7b994b0feedd2607303393f02272894f58a.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 571,
                "play": 18703,
                "danmaku": 49
            },
            "link": "bilibili://video/551265567",
            "ctime": 1644262014,
            "pubtime": 1644381017,
            "fav_time": 0,
            "bv_id": "BV1Vq4y1c7D5",
            "bvid": "BV1Vq4y1c7D5",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 503716160
            }
        },
        {
            "id": 636427030,
            "type": 2,
            "title": "【泛式/生贺手书】Colors",
            "cover": "http://i2.hdslb.com/bfs/archive/f6e5e6b98e4119d9767412a59c7cd1c249568152.jpg",
            "intro": "技术力低下的小屑手书、、还请多多包涵\n希望米娜看的开心\n祝阿泛生日快乐 天天开心 和竹鱼姐百年好合\n祝大家新年快乐ww",
            "page": 1,
            "duration": 47,
            "upper": {
                "mid": 30038791,
                "name": "晴颜颜颜AKiA",
                "face": "https://i1.hdslb.com/bfs/face/c1755d5a0c498ccb5f0dd5b80d0da8c840661b99.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 65,
                "play": 1253,
                "danmaku": 2
            },
            "link": "bilibili://video/636427030",
            "ctime": 1644452422,
            "pubtime": 1644459607,
            "fav_time": 0,
            "bv_id": "BV1Bb4y177jD",
            "bvid": "BV1Bb4y177jD",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 504421723
            }
        },
        {
            "id": 893380157,
            "type": 2,
            "title": "【泛式生贺】如果曾经的他从未这样选择",
            "cover": "http://i0.hdslb.com/bfs/archive/672b4931cc42eac2cae5fb8120e40f4331ae2716.jpg",
            "intro": "我感觉这个视频是我做过最牛的视频了（\n素材都是国外的，因为国内的素材真难搞\n祝阿泛生日快乐！！",
            "page": 1,
            "duration": 336,
            "upper": {
                "mid": 19535532,
                "name": "-向泽-",
                "face": "https://i0.hdslb.com/bfs/face/8b7baa8ce77db40f97623e39b69c972d45933805.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 129,
                "play": 2925,
                "danmaku": 2
            },
            "link": "bilibili://video/893380157",
            "ctime": 1644228003,
            "pubtime": 1644228000,
            "fav_time": 0,
            "bv_id": "BV1UP4y177fs",
            "bvid": "BV1UP4y177fs",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 493862379
            }
        },
        {
            "id": 508989049,
            "type": 2,
            "title": "【泛式/生贺】年度切片整活",
            "cover": "http://i2.hdslb.com/bfs/archive/39d50eaee42449517979d9a75f2fb6fde71a7610.jpg",
            "intro": "做的真的烂 但我人也麻了\n\n祝泛鸽鸽生日快乐",
            "page": 1,
            "duration": 413,
            "upper": {
                "mid": 38320710,
                "name": "九月浪",
                "face": "https://i0.hdslb.com/bfs/face/fedefd1bc387727d3b3a8f9c6ffc3d42c1f6b2a0.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 71,
                "play": 2699,
                "danmaku": 7
            },
            "link": "bilibili://video/508989049",
            "ctime": 1644419909,
            "pubtime": 1644419909,
            "fav_time": 0,
            "bv_id": "BV1Ru41197QC",
            "bvid": "BV1Ru41197QC",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 505514484
            }
        },
        {
            "id": 678776271,
            "type": 2,
            "title": "【泛式／生贺2022】初春弦光",
            "cover": "http://i0.hdslb.com/bfs/archive/7d65ec481c620eaa933c61b4124440772508d444.jpg",
            "intro": "因为选歌困难最后还是选了录播组去年的歌的屑（\n边学AE边做的，所以看起来会有些粗糙，希望大家可以看下去\n素材来源：@下播型泛式录播组  \n分镜借鉴：@姚努力ovo@Arices丶",
            "page": 1,
            "duration": 155,
            "upper": {
                "mid": 281047536,
                "name": "银杏叶ginkgo",
                "face": "https://i0.hdslb.com/bfs/face/a8210221be205f67e45bd04e8dbb9ddc27d4d616.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 136,
                "play": 4755,
                "danmaku": 13
            },
            "link": "bilibili://video/678776271",
            "ctime": 1644466216,
            "pubtime": 1644466215,
            "fav_time": 0,
            "bv_id": "BV11m4y1o77Q",
            "bvid": "BV11m4y1o77Q",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 502599237
            }
        },
        {
            "id": 759565841,
            "type": 2,
            "title": "【泛式400万粉贺】梦想舞台",
            "cover": "http://i2.hdslb.com/bfs/archive/1b60504514ba3c3161bdb503fc1cad8dad4a805f.jpg",
            "intro": "恭喜泛哥哥400万粉！感谢一直以来的陪伴\n用了一部分录播组的画面，录播组yyds",
            "page": 1,
            "duration": 271,
            "upper": {
                "mid": 19535532,
                "name": "-向泽-",
                "face": "https://i0.hdslb.com/bfs/face/8b7baa8ce77db40f97623e39b69c972d45933805.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 396,
                "play": 11669,
                "danmaku": 27
            },
            "link": "bilibili://video/759565841",
            "ctime": 1627827535,
            "pubtime": 1627827535,
            "fav_time": 0,
            "bv_id": "BV1q64y1B7NF",
            "bvid": "BV1q64y1B7NF",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 380937841
            }
        },
        {
            "id": 289083348,
            "type": 2,
            "title": "燈火的命題",
            "cover": "http://i1.hdslb.com/bfs/archive/160928257af42fd14040b7c1c139a939e0ff755e.jpg",
            "intro": "主催：下播型泛式录播组\n主要绘制：千千里\n分镜：星名一 朽木Naityks\n制作协力：朽木Naityks 牧羊迪 吃年 工程师也要取材 风见无景\n特别感谢：AsunaWhite Blood_Puppet 泛式\nBGM：灯火的命题-メガテラ・ゼロ\n分镜参考：しょー",
            "page": 1,
            "duration": 204,
            "upper": {
                "mid": 27688592,
                "name": "星名三九",
                "face": "https://i2.hdslb.com/bfs/face/967d0890b33271ea512ec9c3ea5acb77aef93d0b.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 7180,
                "play": 201832,
                "danmaku": 1233
            },
            "link": "bilibili://video/289083348",
            "ctime": 1612873789,
            "pubtime": 1612886411,
            "fav_time": 0,
            "bv_id": "BV1vf4y1r7uV",
            "bvid": "BV1vf4y1r7uV",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 295461089
            }
        },
        {
            "id": 629053329,
            "type": 2,
            "title": "【泛式生贺】回顾2020，与你相遇好幸运",
            "cover": "http://i0.hdslb.com/bfs/archive/2c107567b82c06bb2c7d719e6e58ee200e4f9a49.jpg",
            "intro": "恭喜泛哥哥生日快乐！新的一年也要多加努力！\n同时衷心感谢下播组大佬工程师也要取材的支持与帮助，有了他才有了这期视频\nBGM:透明ガール SINGER：NONA REEVES",
            "page": 1,
            "duration": 28,
            "upper": {
                "mid": 14436401,
                "name": "色切子",
                "face": "https://i2.hdslb.com/bfs/face/d6f30a06cdc5bb22d3a6124b013f35d5ba5c6e7e.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 379,
                "play": 11697,
                "danmaku": 20
            },
            "link": "bilibili://video/629053329",
            "ctime": 1612539059,
            "pubtime": 1612695616,
            "fav_time": 0,
            "bv_id": "BV1Dt4y1B7XF",
            "bvid": "BV1Dt4y1B7XF",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 293413288
            }
        },
        {
            "id": 799048549,
            "type": 2,
            "title": "【泛式2021年生贺】太陽系デスコ",
            "cover": "http://i1.hdslb.com/bfs/archive/1cc4aa09d02a18d8b5c71fa66ec805e6609d1cb4.jpg",
            "intro": "祝泛式生日快乐！！又喜欢了你一年！\n因为我画画十分慢的缘故，此手书花了我3个月的时间，我在回看一遍视频，发现画风变化的我自己都不认识\n然后也没什么话讲了，就祝视频对面的大家天天开心，然后祝泛式可以越来越好吧！！",
            "page": 1,
            "duration": 202,
            "upper": {
                "mid": 146085146,
                "name": "摸呀摸呀笋干sun",
                "face": "https://i2.hdslb.com/bfs/face/8cfa51dfd7074f0bc1a27678d27e48c8215ea6a8.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 233,
                "play": 5112,
                "danmaku": 7
            },
            "link": "bilibili://video/799048549",
            "ctime": 1612936810,
            "pubtime": 1612936809,
            "fav_time": 0,
            "bv_id": "BV13y4y1Y7pz",
            "bvid": "BV13y4y1Y7pz",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 295268379
            }
        },
        {
            "id": 501703224,
            "type": 2,
            "title": "【生贺/手书】泛式来了哦！",
            "cover": "http://i0.hdslb.com/bfs/archive/1932c0f9ec488226dbb23544ff64e4aa9ee39206.jpg",
            "intro": "泛鸽鸽生日快乐！\n因为这几天生病了所以只完成了原计划的一半（没错我原计划就是只做1分50秒我太懒了）\n画画技术不行只能做描改啦，希望明年能做一个完成度更高的生贺！\n好多话想说呀但又不想太矫情，祝泛鸽鸽和竹鱼姐一切顺利万事顺遂！❤\n本家：BV1bW411r7XU sm33897535",
            "page": 1,
            "duration": 74,
            "upper": {
                "mid": 54824578,
                "name": "极玉_",
                "face": "https://i1.hdslb.com/bfs/face/5acd5dd600dc7e03fcdd67ae5611eb51fe6de709.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 172,
                "play": 6166,
                "danmaku": 11
            },
            "link": "bilibili://video/501703224",
            "ctime": 1612952425,
            "pubtime": 1612952425,
            "fav_time": 0,
            "bv_id": "BV1ZN411R72f",
            "bvid": "BV1ZN411R72f",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 295906479
            }
        },
        {
            "id": 289040110,
            "type": 2,
            "title": "【2021泛式生贺/手书】Blessing（阿泛生日快乐！）",
            "cover": "http://i0.hdslb.com/bfs/archive/08355cdb6b100de211e4cd25c66c046454a75efa.jpg",
            "intro": "祝阿泛生日快乐！！\n第一次做手书投稿，做的很简陋很粗糙，还请多多包涵！",
            "page": 1,
            "duration": 81,
            "upper": {
                "mid": 12966850,
                "name": "-多读书_多看报-",
                "face": "https://i1.hdslb.com/bfs/face/571cb3eeffa8fcea2134533ec0afc08145ad6236.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 213,
                "play": 6551,
                "danmaku": 38
            },
            "link": "bilibili://video/289040110",
            "ctime": 1612799347,
            "pubtime": 1612799347,
            "fav_time": 0,
            "bv_id": "BV1Gf4y1r72i",
            "bvid": "BV1Gf4y1r72i",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 295063925
            }
        },
        {
            "id": 714078203,
            "type": 2,
            "title": "【泛式生贺】Trust Me",
            "cover": "http://i0.hdslb.com/bfs/archive/c5e60f8bc50c60d33e1a60107b4662dbefa7266e.jpg",
            "intro": "泛式生日快乐！还有新年快乐！\n画得很潦草，凑合看（",
            "page": 1,
            "duration": 90,
            "upper": {
                "mid": 4633422,
                "name": "枯炎",
                "face": "https://i0.hdslb.com/bfs/face/85816bb33c2d11c37476020188457872eb16cef3.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 246,
                "play": 4981,
                "danmaku": 13
            },
            "link": "bilibili://video/714078203",
            "ctime": 1612886419,
            "pubtime": 1612886411,
            "fav_time": 0,
            "bv_id": "BV1SX4y1N77m",
            "bvid": "BV1SX4y1N77m",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 295343117
            }
        },
        {
            "id": 886613303,
            "type": 2,
            "title": "【2021泛式生贺手书】淡色漂浮",
            "cover": "http://i2.hdslb.com/bfs/archive/29fc5ed44a085495d9a4fb25e07f6767ff4d7f68.jpg",
            "intro": "勉强赶上了的生贺，祝阿泛生日快乐！\n第一次做手书，技术力和图力都很有限，画完了发现与其说是泛式生贺手书不如说是泛竹cp手书（笑）\n感谢Cat39在制作过程中提供的建议和帮助，也感谢每一个我直播画手书时陪伴着我的人。\n最后也祝大家新年快乐！",
            "page": 1,
            "duration": 109,
            "upper": {
                "mid": 38808836,
                "name": "次伞tks_Channel",
                "face": "https://i2.hdslb.com/bfs/face/5e2f4cfc12ae7ba46bfb311d046d4f397b3a3afa.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 310,
                "play": 4351,
                "danmaku": 14
            },
            "link": "bilibili://video/886613303",
            "ctime": 1612937716,
            "pubtime": 1612937716,
            "fav_time": 0,
            "bv_id": "BV1tK4y1n725",
            "bvid": "BV1tK4y1n725",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 295784652
            }
        },
        {
            "id": 971604155,
            "type": 2,
            "title": "【泛式生贺/手书】 Feel Special",
            "cover": "http://i1.hdslb.com/bfs/archive/83acf17d5f30c821aa1556483618bf3a82b3eadc.jpg",
            "intro": "BGM:单相思——Aimer\n孩子第一次做手术 别骂了别骂了（）\n三连什么的就拜托各位了！QAQ\n最后再次祝泛八爷生快！！",
            "page": 1,
            "duration": 98,
            "upper": {
                "mid": 366073095,
                "name": "云朵月亮_",
                "face": "https://i0.hdslb.com/bfs/face/02b44d165298f897dc76df0f71e95d407f988105.jpg"
            },
            "attr": 0,
            "cnt_info": {
                "collect": 49,
                "play": 921,
                "danmaku": 3
            },
            "link": "bilibili://video/971604155",
            "ctime": 1612852784,
            "pubtime": 1612852784,
            "fav_time": 0,
            "bv_id": "BV18p4y1p7fQ",
            "bvid": "BV18p4y1p7fQ",
            "season": null,
            "ogv": null,
            "ugc": {
                "first_cid": 295301766
            }
        }
    ]
}
```

</details>