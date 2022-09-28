# 获取剧集基本信息

> http://api.bilibili.com/pgc/review/user

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名      | 类型  | 必填  | 内容        | 备注  |
|----------|-----|-----|-----------|-----|
| media_id | num |     | 剧集mediaId |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                    |
|---------|-----|------|---------------------------------------|
| code    | num | 响应码  | 0：success<br/>-400：请求错误<br/>-404：啥都木有 |
| message | str |      |                                       |
| result  | obj | 信息本体 |                                       |

### `result`对象

| 字段名    | 类型  | 内容     | 备注                                            |
|--------|-----|--------|-----------------------------------------------|
| media  | obj | 剧集信息   |                                               |
| review | obj | 用户操作信息 | 需要登录并且设置`Refer`符合`http(s)://*.bilibili.com`格式 |

#### `result`对象 -> `media`对象

| 字段                 | 类型    | 内容        | 备注                |
|--------------------|-------|-----------|-------------------|
| areas              | array | 地区        |                   |
| cover              | str   | 封面图片url   |                   |
| horizontal_picture | str   | 横板封面图片url |                   |
| media_id           | num   | 剧集mdid    |                   |
| new_ep             | obj   | 最新一话信息    |                   |
| rating             | obj   | 评分信息      |                   |
| season_id          | num   | 剧集ssid    |                   |
| share_url          | url   | 剧集详情页连接   |                   |
| title              | str   | 标题        |                   |
| type               | num   | 剧集类型id    | [剧集类型列表](#剧集类型列表) |
| type_name          | str   | 剧集类型      |                   |

#### 剧集类型列表

| 编号  | 名称  |
|-----|-----|
| 1   | 番剧  |
| 2   | 电影  |
| 3   | 纪录片 |
| 4   | 国创  |
| 5   | 电视剧 |
| 6   | 漫画  |
| 7   | 综艺  |

##### `result`对象 -> `media`对象 -> `areas`数组中的对象

| 字段   | 类型  | 内容     | 备注                |
|------|-----|--------|-------------------|
| id   | num | 所属地区编号 | [地区编号列表](#地区编号列表) |
| name | str | 所属地区名称 |                   |

##### 地区编号列表

| 编号  | 名称    |
|-----|-------|
| 1   | 中国大陆  |
| 2   | 日本    |
| 3   | 美国    |
| 4   | 英国    |
| 5   | 加拿大   |
| 6   | 中国香港  |
| 7   | 中国台湾  |
| 8   | 韩国    |
| 9   | 法国    |
| 10  | 泰国    |
| 12  | 新加坡   |
| 13  | 西班牙   |
| 14  | 俄罗斯   |
| 15  | 德国    |
| 16  | 其他    |
| 17  | 丹麦    |
| 18  | 乌克兰   |
| 19  | 以色列   |
| 20  | 伊朗    |
| 22  | 克罗地亚  |
| 23  | 冰岛    |
| 24  | 匈牙利   |
| 25  | 南非    |
| 26  | 印尼    |
| 27  | 印度    |
| 30  | 土耳其   |
| 31  | 墨西哥   |
| 32  | 委内瑞拉  |
| 33  | 巴西    |
| 34  | 希腊    |
| 35  | 意大利   |
| 36  | 挪威    |
| 37  | 捷克    |
| 39  | 新西兰   |
| 40  | 智利    |
| 41  | 比利时   |
| 42  | 波兰    |
| 43  | 澳大利亚  |
| 44  | 爱尔兰   |
| 45  | 瑞典    |
| 46  | 瑞士    |
| 47  | 芬兰    |
| 48  | 苏联    |
| 49  | 荷兰    |
| 51  | 阿根廷   |
| 53  | 古巴    |
| 54  | 菲律宾   |
| 55  | 哈萨克斯坦 |

##### `result`对象 -> `media`对象 -> `new_ep`对象

| 字段         | 类型  | 内容        | 备注       |
|------------|-----|-----------|----------|
| id         | num | 最新一话的epId |          |
| index      | str | 最新一话的短标题  |          |
| index_show | str | 最新一话显示的名称 | 例：`全12话` |

##### `result`对象 -> `media`中的`rating`对象：

| 字段    | 类型  | 内容     | 备注  |
|-------|-----|--------|-----|
| count | num | 总计评分人数 |     |
| score | num | 评分     |     |

#### `result`对象 -> `media`对象

| 字段      | 类型  | 内容  | 备注  |
|---------|-----|-----|-----|
| is_coin | num | `1` |     |
| is_open | num | `1` |     |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/pgc/review/user?media_id=4340' \
-H 'cookie: SESSDATA=xxx' \
-H 'referer: https://www.bilibili.com'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "code": 0,
  "message": "success",
  "result": {
    "media": {
      "areas": [
        {
          "id": 2,
          "name": "日本"
        }
      ],
      "cover": "http://i0.hdslb.com/bfs/bangumi/image/9b2fadeebea37c5da20ec9215fc4056caee69584.jpg",
      "horizontal_picture": "http://i0.hdslb.com/bfs/bangumi/image/9b2fadeebea37c5da20ec9215fc4056caee69584.jpg",
      "media_id": 4340,
      "new_ep": {
        "id": 329015,
        "index": "13",
        "index_show": "全13话"
      },
      "rating": {
        "count": 42892,
        "score": 9.8
      },
      "season_id": 4340,
      "share_url": "https://www.bilibili.com/bangumi/media/md4340",
      "title": "中二病也要谈恋爱！",
      "type": 1,
      "type_name": "番剧"
    },
    "review": {
      "is_coin": 1,
      "is_open": 1
    }
  }
}
```
</details>

# 获取剧集分集信息

> https://api.bilibili.com/pgc/web/season/section

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名       | 类型  | 必填  | 内容         | 备注  |
|-----------|-----|-----|------------|-----|
| season_id | str | √   | 剧集seasonId |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                      |
|---------|-----|------|-------------------------|
| code    | num | 响应码  | 0：success<br/>-404：啥都木有 |
| message | str |      |                         |
| result  | obj | 信息本体 |                         |

### `result`对象

| 字段名          | 类型    | 内容     | 备注  |
|--------------|-------|--------|-----|
| main_section | obj   | 正片信息   |     |
| section      | array | 花絮、PV等 |     |

#### `result`对象 -> `main_section`对象

| 字段       | 类型    | 内容                           | 备注  |
|----------|-------|------------------------------|-----|
| episodes | array | 分集信息                         |     |
| id       | num   | 分组id                         |     |
| type     | num   | 0：正片<br/>1：PV&其他<br/>2：OP&ED |     |
| title    | str   |                              |     |

#### `result`对象 -> `main_section`对象 -> `episodes`数组中的对象

| 字段          | 类型  | 内容        | 备注  |
|-------------|-----|-----------|-----|
| aid         | num | 视频av号     |     |
| badge       | str |           |     |
| badge_info  | obj |           |     |
| badge_type  | num | `0`       |     |
| cid         | num | 分集cid     |     |
| cover       | str | 分集封面      |     |
| from        | str | `bangumi` |     |
| id          | num | 分集epId    |     |
| is_premiere | num | 0         |     |
| long_title  | str | 长标题       |     |
| share_url   | str | 分集播放页url  |     |
| status      | num | 2         |     |
| title       | str | 短标题       |     |
| vid         | str |           |     |

##### `result`对象 -> `main_section`对象 -> `episodes`数组中的对象 -> `badge_info`对象

| 字段             | 类型  | 内容        | 备注  |
|----------------|-----|-----------|-----|
| bg_color       | str | `#FB7299` |     |
| bg_color_night | str | `#BB5B76` |     |
| text           | str | `空串`      |     |

`section`数组中的对象：

**同`main_section`对象**

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/pgc/web/season/section?season_id=4340'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "code": 0,
  "message": "success",
  "result": {
    "main_section": {
      "episodes": [
        {
          "aid": 968620643,
          "badge": "",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": ""
          },
          "badge_type": 0,
          "cid": 202261238,
          "cover": "http://i0.hdslb.com/bfs/archive/8175958db30ee1758955ef2165119c225273c36c.jpg",
          "from": "bangumi",
          "id": 329002,
          "is_premiere": 0,
          "long_title": "邂逅的…邪王真眼",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329002",
          "status": 2,
          "title": "1",
          "vid": ""
        },
        {
          "aid": 286113704,
          "badge": "会员",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": "会员"
          },
          "badge_type": 0,
          "cid": 202261408,
          "cover": "http://i0.hdslb.com/bfs/archive/1f1a3ee4b2a6a68412cbbbcf2e3c3b45467faad2.jpg",
          "from": "bangumi",
          "id": 329003,
          "is_premiere": 0,
          "long_title": "旋律的…圣调理人",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329003",
          "status": 13,
          "title": "2",
          "vid": ""
        },
        {
          "aid": 968611756,
          "badge": "会员",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": "会员"
          },
          "badge_type": 0,
          "cid": 202261668,
          "cover": "http://i0.hdslb.com/bfs/archive/cb287c8f6d072e77cb9f211b4b444aa7bfeccd94.jpg",
          "from": "bangumi",
          "id": 329004,
          "is_premiere": 0,
          "long_title": "异端的…双马尾 ",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329004",
          "status": 13,
          "title": "3",
          "vid": ""
        },
        {
          "aid": 753505705,
          "badge": "会员",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": "会员"
          },
          "badge_type": 0,
          "cid": 202261811,
          "cover": "http://i0.hdslb.com/bfs/archive/d96eceb234598902edddf9c6776b3a6d5ae8a0ca.jpg",
          "from": "bangumi",
          "id": 329005,
          "is_premiere": 0,
          "long_title": "可恨的…黑暗圣典",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329005",
          "status": 13,
          "title": "4",
          "vid": ""
        },
        {
          "aid": 838564013,
          "badge": "会员",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": "会员"
          },
          "badge_type": 0,
          "cid": 202261974,
          "cover": "http://i0.hdslb.com/bfs/archive/1d58718ec2bf13ada507632cf47c1b0b88b13cd8.jpg",
          "from": "bangumi",
          "id": 329006,
          "is_premiere": 0,
          "long_title": "束缚的…十字架",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329006",
          "status": 13,
          "title": "5",
          "vid": ""
        },
        {
          "aid": 838540312,
          "badge": "会员",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": "会员"
          },
          "badge_type": 0,
          "cid": 202262199,
          "cover": "http://i0.hdslb.com/bfs/archive/d9d6192d387572370f42703fddcde45cc3282203.jpg",
          "from": "bangumi",
          "id": 329007,
          "is_premiere": 0,
          "long_title": "赎罪的…救世主 ",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329007",
          "status": 13,
          "title": "6",
          "vid": ""
        },
        {
          "aid": 541111336,
          "badge": "会员",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": "会员"
          },
          "badge_type": 0,
          "cid": 202262504,
          "cover": "http://i0.hdslb.com/bfs/archive/25855ee7c7b08afe24745af9f991b5311d6e3ce9.jpg",
          "from": "bangumi",
          "id": 329009,
          "is_premiere": 0,
          "long_title": "追忆的…失乐园",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329009",
          "status": 13,
          "title": "7",
          "vid": ""
        },
        {
          "aid": 201078068,
          "badge": "会员",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": "会员"
          },
          "badge_type": 0,
          "cid": 202262652,
          "cover": "http://i0.hdslb.com/bfs/archive/283eb404287b9fa2dcc24822c0620a43a928ee96.jpg",
          "from": "bangumi",
          "id": 329010,
          "is_premiere": 0,
          "long_title": "仅属于两人的…逃避之旅",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329010",
          "status": 13,
          "title": "8",
          "vid": ""
        },
        {
          "aid": 498514272,
          "badge": "会员",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": "会员"
          },
          "badge_type": 0,
          "cid": 202262795,
          "cover": "http://i0.hdslb.com/bfs/archive/fb12d0c47defca3774f8b2b26a8f5786aa4d818b.jpg",
          "from": "bangumi",
          "id": 329011,
          "is_premiere": 0,
          "long_title": "混沌的…初恋烦恼 ",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329011",
          "status": 13,
          "title": "9",
          "vid": ""
        },
        {
          "aid": 583547991,
          "badge": "会员",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": "会员"
          },
          "badge_type": 0,
          "cid": 202262932,
          "cover": "http://i0.hdslb.com/bfs/archive/3bb68c63b74221e368b6d951aecfdd3034869f7d.jpg",
          "from": "bangumi",
          "id": 329012,
          "is_premiere": 0,
          "long_title": "圣母的…便当盒",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329012",
          "status": 13,
          "title": "10",
          "vid": ""
        },
        {
          "aid": 841108727,
          "badge": "会员",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": "会员"
          },
          "badge_type": 0,
          "cid": 202263084,
          "cover": "http://i0.hdslb.com/bfs/archive/a0ab0d00f8c8000046b91c5b4ec6ca6bc2d35ff4.jpg",
          "from": "bangumi",
          "id": 329013,
          "is_premiere": 0,
          "long_title": "单翼的…堕天使",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329013",
          "status": 13,
          "title": "11",
          "vid": ""
        },
        {
          "aid": 371010992,
          "badge": "会员",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": "会员"
          },
          "badge_type": 0,
          "cid": 202263295,
          "cover": "http://i0.hdslb.com/bfs/archive/080b90595d875bd15f2a619ea05178c666134507.jpg",
          "from": "bangumi",
          "id": 329014,
          "is_premiere": 0,
          "long_title": "终天之契约",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329014",
          "status": 13,
          "title": "12",
          "vid": ""
        },
        {
          "aid": 926068856,
          "badge": "会员",
          "badge_info": {
            "bg_color": "#FB7299",
            "bg_color_night": "#BB5B76",
            "text": "会员"
          },
          "badge_type": 0,
          "cid": 202263430,
          "cover": "http://i0.hdslb.com/bfs/archive/c87f7a21b505b847c9feff96cb761e8701620cb7.jpg",
          "from": "bangumi",
          "id": 329015,
          "is_premiere": 0,
          "long_title": "闪光的…圣爆诞祭  ",
          "share_url": "https://www.bilibili.com/bangumi/play/ep329015",
          "status": 13,
          "title": "13",
          "vid": ""
        }
      ],
      "id": 21274,
      "title": "正片",
      "type": 0
    },
    "section": []
  }
}
```
</details>