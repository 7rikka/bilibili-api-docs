# 搜索建议

> https://app.bilibili.com/x/car/search/suggest

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名        | 类型  | 必填  | 内容          | 备注             |
|------------|-----|-----|-------------|----------------|
| access_key | str |     |             | 可不登录，搜索建议会有所不同 |
| appkey     | str |     |             |                |
| build      | num |     |             |                |
| c_locale   | str |     |             |                |
| channel    | str |     |             |                |
| highlight  | num |     | 是否高亮显示搜索关键词 | 0：否<br/>1：是    |
| keyword    | num |     | 搜索关键词       |                |
| mobi_app   | str |     |             |                |
| platform   | str |     |             |                |
| s_locale   | str |     |             |                |
| ts         | num |     | 当前时间戳       | 单位：秒           |
| sign       | str |     |             |                |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名   | 类型    | 内容     | 备注  |
|-------|-------|--------|-----|
| items | array | 搜索建议列表 |     |
| args  | obj   |        |     |

### `data`对象 -> `items`数组中的对象

| 字段名       | 类型  | 内容         | 备注                                  |
|-----------|-----|------------|-------------------------------------|
| position  | num |            |                                     |
| title     | str | 显示的建议搜索关键词 | 如果`highlight = 0`，该字段将会和`keyword`相等 |
| from      | str | `search`   |                                     |
| keyword   | str | 建议搜索关键词    |                                     |
| term_type | num | `5`        |                                     |
| module_id | num | `1`        |                                     |

### `data`对象 -> `args`对象

| 字段名     | 类型  | 内容  | 备注  |
|---------|-----|-----|-----|
| trackid | str |     |     |

## 请求示例

```shell
curl -L -X GET 'https://app.bilibili.com/x/car/search/suggest?access_key=xxx&highlight=1&keyword=哔哩哔哩'
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
    "items": [
      {
        "position": 1,
        "title": "<em class=\"keyword\">哔哩哔哩</em>番剧出差",
        "from": "search",
        "keyword": "哔哩哔哩番剧出差",
        "term_type": 5,
        "module_id": 1
      },
      {
        "position": 2,
        "title": "<em class=\"keyword\">哔哩哔哩</em>直播",
        "from": "search",
        "keyword": "哔哩哔哩直播",
        "term_type": 5,
        "module_id": 1
      },
      {
        "position": 3,
        "title": "<em class=\"keyword\">哔哩哔哩</em>番剧",
        "from": "search",
        "keyword": "哔哩哔哩番剧",
        "term_type": 5,
        "module_id": 1
      },
      {
        "position": 4,
        "title": "<em class=\"keyword\">哔哩哔哩</em>英雄联盟赛事",
        "from": "search",
        "keyword": "哔哩哔哩英雄联盟赛事",
        "term_type": 5,
        "module_id": 1
      },
      {
        "position": 5,
        "title": "<em class=\"keyword\">哔哩哔哩</em>向前冲",
        "from": "search",
        "keyword": "哔哩哔哩向前冲",
        "term_type": 5,
        "module_id": 1
      },
      {
        "position": 6,
        "title": "<em class=\"keyword\">哔哩哔哩</em>漫画",
        "from": "search",
        "keyword": "哔哩哔哩漫画",
        "term_type": 5,
        "module_id": 1
      },
      {
        "position": 7,
        "title": "<em class=\"keyword\">哔哩哔哩</em>守望先锋赛事",
        "from": "search",
        "keyword": "哔哩哔哩守望先锋赛事",
        "term_type": 5,
        "module_id": 1
      },
      {
        "position": 8,
        "title": "<em class=\"keyword\">哔哩哔哩</em>数字藏品",
        "from": "search",
        "keyword": "哔哩哔哩数字藏品",
        "term_type": 5,
        "module_id": 1
      },
      {
        "position": 9,
        "title": "<em class=\"keyword\">哔哩哔哩</em>社区小管家",
        "from": "search",
        "keyword": "哔哩哔哩社区小管家",
        "term_type": 5,
        "module_id": 1
      },
      {
        "position": 10,
        "title": "<em class=\"keyword\">哔哩哔哩</em>大会员",
        "from": "search",
        "keyword": "哔哩哔哩大会员",
        "term_type": 5,
        "module_id": 1
      }
    ],
    "args": {
      "trackid": "5417260086249843846"
    }
  }
}
```

</details>

# 搜索

> https://app.bilibili.com/x/v2/car/search

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名        | 类型  | 必填  | 内容     | 备注                   |
|------------|-----|-----|--------|----------------------|
| access_key | str |     |        |                      |
| appkey     | str |     |        |                      |
| build      | num |     |        |                      |
| c_locale   | str |     |        |                      |
| channel    | str |     |        |                      |
| fnval      | num |     |        |                      |
| fnver      | num |     |        |                      |
| force_host | num |     |        |                      |
| keyword    | str |     | 搜索关键词  |                      |
| mobi_app   | str |     |        |                      |
| page_next  | str |     | 下一页的参数 | 例：`{"pn":2,"ps":20}` |
| platform   | str |     |        |                      |
| ps         | num |     | 分页大小   | 默认：20<br/>范围：[1,100] |
| qn         | num |     |        |                      |
| s_locale   | str |     |        |                      |
| ts         | num |     | 当前时间戳  | 单位：秒                 |
| sign       | str |     |        |                      |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注               |
|---------|-----|------|------------------|
| code    | num | 响应码  | 0：成功<br/>-10：-10 |
| message | str |      |                  |
| ttl     | num | 1    |                  |
| data    | obj | 信息本体 |                  |

### `data`对象

| 字段名       | 类型    | 内容       | 备注  |
|-----------|-------|----------|-----|
| items     | array | 查询到的视频结果 |     |
| up_items  | array | 查询到的用户结果 |     |
| page_next | obj   | 下一页查询参数  |     |
| has_next  | bool  | 是否有下一页   |     |

### `data`对象 -> `items`数组中的对象

| 字段名             | 类型   | 内容      | 备注                                    |
|-----------------|------|---------|---------------------------------------|
| item_type       | str  | 结果类型    | `ugc` `ogv`                           |
| item_id         | num  | `0`     |                                       |
| otype           | str  |         | `ugc` `pgc`                           |
| oid             | num  | 关联视频id  | `ogv`情况下为剧集season_id<br/>`ugc`情况下为av号 |
| cid             | num  | 视频cid   |                                       |
| url             | str  | 跳转播放url |                                       |
| title           | str  | 标题      |                                       |
| bg_color        | str  | `空串`    |                                       |
| cover           | str  | 封面      |                                       |
| landscape_cover | str  | 封面      | 剧集类型独有                                |
| badge           | obj  | 角标信息    | 剧集类型独有                                |
| author          | obj  | UP主信息   |                                       |
| play_count      | num  | 播放数     |                                       |
| danmaku_count   | num  | 弹幕数     |                                       |
| fav_count       | num  | 收藏数     |                                       |
| reply_count     | num  | 回复数     |                                       |
| duration        | num  | 视频长度    | 单位：秒 <br/>剧集类型固定为`0`                  |
| desc            | str  | 视频简介    |                                       |
| pubtime         | num  | 发布时间戳   | 单位：秒 <br/>剧集类型无此项                     |
| is_follow       | bool | `false` |                                       |
| is_like         | bool | `false` |                                       |
| sub_title       | str  | 副标题     |                                       |
| arc_count_show  | str  | `空串`    |                                       |
| hot_rate        | num  | `0`     |                                       |
| server_info     | str  | `空串`    |                                       |
| show_type       | num  | `0`     |                                       |
| label           |      | `null`  |                                       |
| catalog         |      | `null`  |                                       |
| score           | str  | `空串`    |                                       |

### `data`对象 -> `items`数组中的对象 -> `author`对象

| 字段名        | 类型   | 内容         | 备注  |
|------------|------|------------|-----|
| mid        | num  | 用户uid      |     |
| name       | str  | 用户名        |     |
| face       | str  | 头像         |     |
| fans_count | num  | 固定值：`0`    |     |
| relation   | null | 固定值：`null` |     |

### `data`对象 -> `items`数组中的对象 -> `badge`对象

| 字段名            | 类型  | 内容       | 备注     |
|----------------|-----|----------|--------|
| text           | str | 角标内容     |        |
| bg_color_day   | str | 背景颜色     | 日间模式   |
| bg_color_night | str | 背景颜色     | 夜间模式   |
| bg_style       | str | 背景颜色填充方式 | `fill` |

### `data`对象 -> `up_items`数组中的对象

| 字段名         | 类型  | 内容     | 备注  |
|-------------|-----|--------|-----|
| mid         | num | 用户uid  |     |
| name        | str | 用户名    |     |
| face        | str | 用户头像   |     |
| fans_count  | num | 用户粉丝数  |     |
| video_count | num | 用户投稿数  |     |
| desc        | str | 用户认证信息 |     |

### `data`对象 -> `page_next`对象

| 字段名 | 类型  | 内容       | 备注  |
|-----|-----|----------|-----|
| pn  | num | 下一页的页数   |     |
| ps  | num | 下一页的分页大小 |     |

## 请求示例

```shell
curl -L -X GET 'https://app.bilibili.com/x/v2/car/search?keyword=哔哩哔哩向前冲&ps=2'
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
    "items": [
      {
        "item_type": "ogv",
        "item_id": 0,
        "otype": "pgc",
        "oid": 41832,
        "cid": 640113,
        "url": "bilithings://player?aid=41832&cid=640113&goto=pgc&sourceType=",
        "title": "哔哩哔哩向前冲",
        "bg_color": "",
        "cover": "http://i0.hdslb.com/bfs/bangumi/image/0710616211b78b52b599de00ea42cc4b622cb9a1.png",
        "landscape_cover": "http://i0.hdslb.com/bfs/archive/1bb2d7e8e38ce8b4f6d95358f384621b54a47962.jpg",
        "badge": {
          "text": "出品",
          "bg_color_day": "#00C0FF",
          "bg_color_night": "#0B91BE",
          "bg_style": "fill"
        },
        "play_count": 223164716,
        "danmaku_count": 675893,
        "fav_count": 769150,
        "reply_count": 107434,
        "duration": 0,
        "desc": "全16集",
        "is_follow": false,
        "is_like": false,
        "sub_title": "76.9万追剧",
        "arc_count_show": "",
        "hot_rate": 0,
        "server_info": "",
        "show_type": 0,
        "label": null,
        "catalog": null,
        "score": ""
      },
      {
        "item_type": "ugc",
        "item_id": 0,
        "otype": "ugc",
        "oid": 303415947,
        "cid": 843290681,
        "url": "bilithings://player?aid=303415947&cid=843290681&goto=av&history_progress=0&player_height=1080&player_rotate=0&player_width=1920",
        "title": "第15期正片 复仇勇士卷土重来！【哔哩哔哩向前冲】",
        "bg_color": "",
        "cover": "http://i2.hdslb.com/bfs/archive/615be0e1440605103129939fef3c5336e2a2254d.jpg",
        "author": {
          "mid": 2053966364,
          "name": "哔哩哔哩向前冲",
          "face": "https://i2.hdslb.com/bfs/face/f90e4db73b1414a39378aff17ae2a765da02b66c.jpg",
          "fans_count": 0,
          "relation": null
        },
        "play_count": 1234654,
        "danmaku_count": 10066,
        "fav_count": 11,
        "reply_count": 518,
        "duration": 4851,
        "desc": "哔哩哔哩向前冲",
        "pubtime": 1664077800,
        "is_follow": false,
        "is_like": false,
        "sub_title": "",
        "arc_count_show": "",
        "hot_rate": 0,
        "server_info": "",
        "show_type": 0,
        "label": null,
        "catalog": null,
        "score": ""
      }
    ],
    "up_items": [
      {
        "mid": 2053966364,
        "name": "哔哩哔哩向前冲",
        "face": "https://i2.hdslb.com/bfs/face/f90e4db73b1414a39378aff17ae2a765da02b66c.jpg",
        "fans_count": 507342,
        "video_count": 844,
        "desc": "综艺《哔哩哔哩向前冲》节目官方账号"
      },
      {
        "mid": 130622717,
        "name": "我对哔哩向前冲",
        "face": "https://i2.hdslb.com/bfs/face/900a3689884b2d141bd8721d1f7dbd79e84c3b04.jpg",
        "fans_count": 16,
        "video_count": 4,
        "desc": ""
      },
      {
        "mid": 1161624420,
        "name": "哔哩向前冲c",
        "face": "https://i0.hdslb.com/bfs/face/member/noface.jpg",
        "fans_count": 14,
        "video_count": 1,
        "desc": ""
      }
    ],
    "page_next": {
      "pn": 2,
      "ps": 2
    },
    "has_next": true
  }
}
```

</details>