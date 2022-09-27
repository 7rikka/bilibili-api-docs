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
| 7   | 综艺  |

##### `result`对象 -> `media`对象 -> `areas`数组中的对象

| 字段   | 类型  | 内容     | 备注                |
|------|-----|--------|-------------------|
| id   | num | 所属地区编号 | [地区编号列表](#地区编号列表) |
| name | str | 所属地区名称 |                   |

##### 地区编号列表

| 编号  | 名称   |
|-----|------|
| 1   | 中国大陆 |
| 2   | 日本   |
| 3   | 美国   |
| 4   | 英国   |
| 5   | 加拿大  |
| 6   | 中国香港 |
| 7   | 中国台湾 |
| 8   | 韩国   |
| 9   | 法国   |
| 10  | 泰国   |
| 13  | 西班牙  |
| 14  | 俄罗斯  |
| 15  | 德国   |
| 16  | 其他   |
| 24  | 匈牙利  |
| 27  | 印度   |
| 31  | 墨西哥  |
| 33  | 巴西   |
| 34  | 希腊   |
| 35  | 意大利  |
| 37  | 捷克   |
| 39  | 新西兰  |
| 41  | 比利时  |
| 43  | 澳大利亚 |
| 51  | 阿根廷  |
| 54  | 菲律宾  |

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