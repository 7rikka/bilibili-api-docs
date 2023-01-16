# 搜索装扮

> https://api.bilibili.com/x/garb/v2/mall/home/search

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名      | 类型  | 必填  | 内容    | 备注  |
|----------|-----|-----|-------|-----|
| key_word | str | √   | 搜索关键词 |     |
| pn       | str |     |       |     |
| pn       | str |     |       |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名   | 类型    | 内容   | 备注  |
|-------|-------|------|-----|
| list  | array | 结果数组 |     |
| pn    | num   | 当前页数 |     |
| ps    | num   | 分页大小 |     |
| total | num   | 总记录数 |     |

### `data`对象 -> `list`数组中的对象

| 字段名              | 类型   | 内容     | 备注        |
|------------------|------|--------|-----------|
| item_id          | num  |        |           |
| name             | str  |        |           |
| group_id         | num  |        |           |
| group_name       | str  |        |           |
| part_id          | num  |        |           |
| state            | str  |        |           |
| properties       | obj  |        |           |
| current_activity | null | 折扣信息   |           |
| current_sources  | null |        |           |
| finish_sources   | null |        |           |
| sale_left_time   | num  |        |           |
| sale_time_end    | num  |        |           |
| sale_surplus     | num  | 库存剩余   |           |
| sale_count_desc  | str  | 已售数量描述 |           |
| tag              | str  | 角标内容   | `粉丝套装已售罄` |

### `data`对象 -> `list`数组中的对象 -> `properties`对象

| 字段名                      | 类型  | 内容                    | 备注          |
|--------------------------|-----|-----------------------|-------------|
| desc                     | str | 装扮描述                  |             |
| fan_desc                 | str |                       |             |
| fan_id                   | str |                       |             |
| fan_item_ids             | str |                       |             |
| fan_mid                  | str |                       |             |
| fan_no_color             | str |                       |             |
| fan_recommend_desc       | str |                       |             |
| fan_recommend_jump_type  | str | `url` `uid`           |             |
| fan_recommend_jump_value | str |                       |             |
| fan_share_image          | str |                       |             |
| gray_rule                | str | `true`                |             |
| gray_rule_type           | str | `all`                 |             |
| image_cover              | str |                       |             |
| image_cover_color        | str |                       |             |
| image_cover_long         | str |                       |             |
| image_desc               | str |                       |             |
| is_hide                  | str | `false`               |             |
| item_id_card             | str |                       |             |
| item_id_emoji            | str |                       |             |
| item_id_thumbup          | str |                       |             |
| rank_investor_show       | str |                       |             |
| realname_auth            | str | `false`               |             |
| sale_bp_forever_raw      | str |                       |             |
| sale_bp_pm_raw           | str |                       |             |
| sale_buy_num_limit       | str |                       |             |
| sale_quantity            | str |                       |             |
| sale_quantity_limit      | str | `true` `false`        |             |
| sale_region_ip_limit     | str | 销售区域限制                | `全球` `大陆地区` |
| sale_reserve_switch      | str | `true` `false`        |             |
| sale_time_begin          | str |                       |             |
| sale_type                | str | `pay`                 |             |
| suit_card_type           | str | `multi_img` `big_img` |             |
| type                     | str | `ip` `up`             |             |

### `data`对象 -> `list`数组中的对象 -> `current_activity`对象

| 字段名              | 类型   | 内容  | 备注  |
|------------------|------|-----|-----|
| type             | str  |     |     |
| time_limit       | bool |     |     |
| time_left        | num  |     |     |
| tag              | str  |     |     |
| price_bp_month   | num  |     |     |
| price_bp_forever | num  |     |     |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/garb/v2/mall/home/search?key_word=初音&pn=1&ps=1'
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
        "item_id": 44245,
        "name": "初音未来圣诞快乐",
        "group_id": 47,
        "group_name": "初音未来圣诞快乐",
        "part_id": 6,
        "state": "active",
        "properties": {
          "desc": "派对已开启，一起跟初音未来欢度圣诞吧！圣诞装的MIKU有没有戳到你呢？",
          "fan_desc": "初音未来圣诞快乐",
          "fan_id": "初音未来圣诞快乐",
          "fan_item_ids": "44244,44683,44684,44685",
          "fan_mid": "399918500",
          "fan_no_color": "#f0393d",
          "fan_recommend_desc": "“初音未来”是一款由日本Crypton Future Media公司研发出的声库合成“软件”，通过输入歌词和旋律后任何人都可以让她唱歌。",
          "fan_recommend_jump_type": "url",
          "fan_recommend_jump_value": "https://space.bilibili.com/399918500?spm_id_from=333.337.0.0",
          "fan_share_image": "https://i0.hdslb.com/bfs/garb/item/ea6fc960e2f23707b8ad9e7dc1784b1f6f3a2335.jpg",
          "gray_rule": "true",
          "gray_rule_type": "all",
          "image_cover": "https://i0.hdslb.com/bfs/garb/item/a7eaa4c5c0944a8cfc0c43fdde25e2c8cf201034.jpg",
          "image_cover_color": "#b32d45",
          "image_cover_long": "https://i0.hdslb.com/bfs/garb/item/97aeaf46282ed5b72c8b38cc082ecd844157931c.jpg",
          "image_desc": "https://i0.hdslb.com/bfs/garb/item/8b0850fa4da6b6f1b2a31408431b463b02ab4c29.jpg",
          "is_hide": "false",
          "item_id_card": "44243",
          "item_id_emoji": "44682",
          "rank_investor_show": "false",
          "realname_auth": "false",
          "sale_bp_forever_raw": "3500",
          "sale_bp_pm_raw": "800",
          "sale_buy_num_limit": "100",
          "sale_quantity": "139000",
          "sale_quantity_limit": "true",
          "sale_region_ip_limit": "全球",
          "sale_reserve_switch": "true",
          "sale_time_begin": "1671966000",
          "sale_type": "pay",
          "suit_card_type": "big_img",
          "type": "up"
        },
        "current_activity": null,
        "current_sources": null,
        "finish_sources": null,
        "sale_left_time": -1885382,
        "sale_time_end": -1673851382,
        "sale_surplus": 126916,
        "sale_count_desc": "1万+",
        "tag": ""
      }
    ],
    "pn": 1,
    "ps": 1,
    "total": 3
  }
}
```

</details>