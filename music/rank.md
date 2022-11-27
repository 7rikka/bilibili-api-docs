# 全站音乐榜

> https://music.bilibili.com/pc/rank

# 获取音乐榜所有分期数据

> https://api.bilibili.com/x/copyright-music-publicity/toplist/all_period

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名       | 类型  | 必填  | 内容     | 备注  |
|-----------|-----|-----|--------|-----|
| csrf      | str |     | 用户csrf |     |
| list_type | str | √   | `1`    |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名  | 类型  | 内容   | 备注  |
|------|-----|------|-----|
| list | obj | 数据列表 |     |

### `data`对象 -> `list`对象

| 字段名  | 类型    | 内容      | 备注  |
|------|-------|---------|-----|
| 2022 | array | 2022年数据 |     |

### `data`对象 -> `list`对象 -> `2022`数组中的对象

| 字段名          | 类型  | 内容    | 备注   |
|--------------|-----|-------|------|
| ID           | num | 记录id  |      |
| priod        | num | 期数    |      |
| publish_time | num | 发布时间戳 | 单位：秒 |

## 请求示例

```shell
curl --location --request GET 'https://api.bilibili.com/x/copyright-music-publicity/toplist/all_period?list_type=1'
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
    "list": {
      "2022": [
        {
          "ID": 28,
          "priod": 24,
          "publish_time": 1669370757
        },
        {
          "ID": 26,
          "priod": 23,
          "publish_time": 1668766987
        },
        {
          "ID": 22,
          "priod": 22,
          "publish_time": 1668163419
        },
        {
          "ID": 21,
          "priod": 21,
          "publish_time": 1667558276
        },
        {
          "ID": 20,
          "priod": 20,
          "publish_time": 1666951199
        },
        {
          "ID": 19,
          "priod": 19,
          "publish_time": 1666346399
        },
        {
          "ID": 18,
          "priod": 18,
          "publish_time": 1665741599
        },
        {
          "ID": 17,
          "priod": 17,
          "publish_time": 1665136799
        },
        {
          "ID": 16,
          "priod": 16,
          "publish_time": 1664531999
        },
        {
          "ID": 15,
          "priod": 15,
          "publish_time": 1663927199
        },
        {
          "ID": 14,
          "priod": 14,
          "publish_time": 1663322399
        },
        {
          "ID": 13,
          "priod": 13,
          "publish_time": 1662717599
        },
        {
          "ID": 12,
          "priod": 12,
          "publish_time": 1662113559
        },
        {
          "ID": 11,
          "priod": 11,
          "publish_time": 1661508657
        },
        {
          "ID": 10,
          "priod": 10,
          "publish_time": 1660903199
        },
        {
          "ID": 9,
          "priod": 9,
          "publish_time": 1660298400
        },
        {
          "ID": 8,
          "priod": 8,
          "publish_time": 1659693599
        },
        {
          "ID": 7,
          "priod": 7,
          "publish_time": 1659088799
        },
        {
          "ID": 6,
          "priod": 6,
          "publish_time": 1658483999
        },
        {
          "ID": 5,
          "priod": 5,
          "publish_time": 1657879200
        },
        {
          "ID": 4,
          "priod": 4,
          "publish_time": 1657274399
        },
        {
          "ID": 3,
          "priod": 3,
          "publish_time": 1656669600
        },
        {
          "ID": 2,
          "priod": 2,
          "publish_time": 1656064800
        },
        {
          "ID": 1,
          "priod": 1,
          "publish_time": 1655460091
        }
      ]
    }
  }
}
```

</details>