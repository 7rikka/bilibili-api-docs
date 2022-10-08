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