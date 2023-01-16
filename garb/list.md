# 装扮列表

> https://api.bilibili.com/x/garb/v2/mall/partition/item/list

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名       | 类型  | 必填  | 内容    | 备注                           |
|-----------|-----|-----|-------|------------------------------|
| group_id  | str |     | 分组id  |                              |
| part_id   | str | √   | 固定`6` |                              |
| pn        | str |     | 当前页数  |                              |
| ps        | str |     | 分页大小  | 默认`20`                       |
| sort_type | str |     | 排序方式  | 0：`默认`<br/>1：`销量`<br/>2：`最新` |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名  | 类型    | 内容   | 备注  |
|------|-------|------|-----|
| page | obj   | 分页信息 |     |
| list | array | 结果数组 |     |

### `data`对象 -> `page`对象

| 字段名   | 类型  | 内容   | 备注  |
|-------|-----|------|-----|
| total | num | 总记录数 |     |
| pn    | num | 当前页数 |     |
| ps    | num | 分页大小 |     |

### `data`对象 -> `list`数组中的对象

| 字段名              | 类型   | 内容     | 备注                                                           |
|------------------|------|--------|--------------------------------------------------------------|
| item_id          | num  |        |                                                              |
| name             | str  |        |                                                              |
| group_id         | num  |        |                                                              |
| group_name       | str  |        |                                                              |
| part_id          | num  |        |                                                              |
| state            | str  |        |                                                              |
| properties       | obj  |        |                                                              |
| current_activity | obj  | 折扣信息   |                                                              |
| current_sources  | null |        |                                                              |
| finish_sources   | null |        |                                                              |
| sale_left_time   | num  |        |                                                              |
| sale_time_end    | num  |        |                                                              |
| sale_surplus     | num  | 库存剩余   |                                                              |
| sale_count_desc  | str  | 已售数量描述 |                                                              |
| tag              | str  | 角标内容   | `空串`<br/>`粉丝套装已售罄`<br/>`即将下架`<br/>`即将售罄`<br/>`新品`<br/>`正在预约` |

### `data`对象 -> `list`数组中的对象 -> `properties`对象

| 字段名                        | 类型  | 内容                    | 备注  |
|----------------------------|-----|-----------------------|-----|
| desc                       | str | 装扮描述                  |     |
| fan_desc                   | str |                       |     |
| fan_id                     | str |                       |     |
| fan_item_ids               | str |                       |     |
| fan_mid                    | str |                       |     |
| fan_no_color               | str |                       |     |
| fan_recommend_desc         | str |                       |     |
| fan_recommend_jump_type    | str |                       |     |
| fan_recommend_jump_value   | str |                       |     |
| fan_share_image            | str |                       |     |
| gray_rule                  | str |                       |     |
| gray_rule_type             | str |                       |     |
| image_cover                | str |                       |     |
| image_cover_color          | str |                       |     |
| image_cover_long           | str |                       |     |
| image_desc                 | str |                       |     |
| is_hide                    | str |                       |     |
| item_id_card               | str |                       |     |
| item_id_emoji              | str |                       |     |
| item_id_pendant            | str |                       |     |
| item_id_thumbup            | str |                       |     |
| rank_investor_show         | str |                       |     |
| sale_bp_forever_raw        | str |                       |     |
| sale_bp_pm_raw             | str |                       |     |
| sale_buy_num_limit         | str |                       |     |
| sale_quantity              | str |                       |     |
| sale_quantity_limit        | str |                       |     |
| sale_region_ip_limit       | str | 销售区域限制                |     |
| sale_reserve_switch        | str | `true`                |     |
| sale_time_begin            | str |                       |     |
| sale_type                  | str | `pay`                 |     |
| suit_card_type             | str | `multi_img` `big_img` |     |
| type                       | str | `ip` `up`             |     |
| realname_auth              | str |                       |     |
| rank_investor_name         | str |                       |     |
| sale_time_end              | str |                       |     |
| pub_btn_plus_color         | str |                       |     |
| pub_btn_shade_color_bottom | str |                       |     |
| pub_btn_shade_color_top    | str |                       |     |
| related_words              | str |                       |     |
| item_base_intro_image      | str |                       |     |

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
curl -L -X GET 'https://api.bilibili.com/x/garb/v2/mall/partition/item/list?part_id=6&pn=1&ps=1'
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
        "page": {
            "total": 453,
            "pn": 1,
            "ps": 1
        },
        "list": [
            {
                "item_id": 32296,
                "name": "EveOneCat2",
                "group_id": 46,
                "group_name": "EveOneCat2",
                "part_id": 6,
                "state": "active",
                "properties": {
                    "desc": "猫在用看似滑稽很的方式来展示人类世界的宇宙，或是说，猫猫正在展示它们所认为的，人类世界的宇宙应有的样子。",
                    "fan_desc": "EveOneCat2",
                    "fan_id": "EveOneCat2",
                    "fan_item_ids": "32264,32256,32263,32262,32260,32261",
                    "fan_mid": "6457791",
                    "fan_no_color": "#f35543",
                    "fan_recommend_desc": "猫在用看似滑稽很的方式来展示人类世界的宇宙，或是说，猫猫正在展示它们所认为的，人类世界的宇宙应有的样子。",
                    "fan_recommend_jump_type": "url",
                    "fan_recommend_jump_value": "https://space.bilibili.com/6457791?from=search&seid=14208507792597677991&spm_id_from=333.337.0.0",
                    "fan_share_image": "https://i0.hdslb.com/bfs/garb/item/209cac9335f92e2aa928a0d480a3e203bb79c110.png",
                    "gray_rule": "true",
                    "gray_rule_type": "all",
                    "image_cover": "https://i0.hdslb.com/bfs/garb/item/af6ab166af22ed45d429bfde4e3962bb78f270c8.png",
                    "image_cover_color": "#3a63ad",
                    "image_cover_long": "https://i0.hdslb.com/bfs/garb/item/580e50bbcc3b4082affb041ba11f4a76ae7fe465.png",
                    "image_desc": "https://i0.hdslb.com/bfs/garb/item/2e7c8b79c3fa8fd3dfd70652f73c932d8ee97590.png",
                    "is_hide": "false",
                    "item_id_card": "32258",
                    "item_id_emoji": "32266",
                    "item_id_pendant": "32257",
                    "item_id_thumbup": "32259",
                    "rank_investor_show": "false",
                    "sale_bp_forever_raw": "5900",
                    "sale_bp_pm_raw": "800",
                    "sale_buy_num_limit": "100",
                    "sale_quantity": "1000000",
                    "sale_quantity_limit": "true",
                    "sale_region_ip_limit": "全球",
                    "sale_reserve_switch": "false",
                    "sale_time_begin": "1632567600",
                    "sale_type": "pay",
                    "suit_card_type": "multi_img",
                    "type": "ip"
                },
                "current_activity": null,
                "current_sources": null,
                "finish_sources": null,
                "sale_left_time": -41285583,
                "sale_time_end": -1673853183,
                "sale_surplus": 810298,
                "sale_count_desc": "10万+",
                "tag": ""
            }
        ]
    }
}
```

</details>