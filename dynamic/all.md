# 动态类型

| 类型                            | 说明            | 示例                                                              | 
|-------------------------------|---------------|-----------------------------------------------------------------|
| DYNAMIC_TYPE_NONE             | 无效动态          | [716510857084796964](https://t.bilibili.com/716510857084796964) |
| DYNAMIC_TYPE_FORWARD          | 动态转发          |                                                                 |
| DYNAMIC_TYPE_AV               | 投稿视频          |                                                                 |
| DYNAMIC_TYPE_PGC              | 剧集（番剧、电影、纪录片） |                                                                 |
| DYNAMIC_TYPE_COURSES          |               |                                                                 |
| DYNAMIC_TYPE_WORD             | 纯文字动态         | [718377531474968613](https://t.bilibili.com/718377531474968613) |
| DYNAMIC_TYPE_DRAW             | 带图动态          | [718384798557536290](https://t.bilibili.com/718384798557536290) |
| DYNAMIC_TYPE_ARTICLE          | 投稿专栏          | [718372214316990512](https://t.bilibili.com/718372214316990512) |
| DYNAMIC_TYPE_MUSIC            | 音乐            |                                                                 |
| DYNAMIC_TYPE_COMMON_SQUARE    | 装扮            | [551309621391003098](https://t.bilibili.com/551309621391003098) |
| DYNAMIC_TYPE_COMMON_VERTICAL  |               |                                                                 |
| DYNAMIC_TYPE_LIVE             | 直播间分享         | [216042859353895488](https://t.bilibili.com/216042859353895488) |
| DYNAMIC_TYPE_MEDIALIST        | 收藏夹           | [534428265320147158](https://t.bilibili.com/534428265320147158) |
| DYNAMIC_TYPE_COURSES_SEASON   | 课程            | [717906712866062340](https://t.bilibili.com/717906712866062340) |
| DYNAMIC_TYPE_COURSES_BATCH    |               |                                                                 |
| DYNAMIC_TYPE_AD               |               |                                                                 |
| DYNAMIC_TYPE_APPLET           |               |                                                                 |
| DYNAMIC_TYPE_SUBSCRIPTION     |               |                                                                 |
| DYNAMIC_TYPE_LIVE_RCMD        | 直播开播          | [718371505648435205](https://t.bilibili.com/718371505648435205) |
| DYNAMIC_TYPE_BANNER           |               |                                                                 |
| DYNAMIC_TYPE_UGC_SEASON       | 合集更新          | [718390979031203873](https://t.bilibili.com/718390979031203873) |
| DYNAMIC_TYPE_SUBSCRIPTION_NEW |               |                                                                 |

# 获取动态列表

> https://api.bilibili.com/x/polymer/web-dynamic/v1/feed/all

请求方式：`GET`

是否需要登录：`是`

## URL参数

| 参数名             | 类型  | 必填  | 内容     | 备注                                                        |
|-----------------|-----|-----|--------|-----------------------------------------------------------|
| timezone_offset | str |     | `-480` |                                                           |
| type            | str |     | 分类     | `all`：全部<br/>`video`：视频投稿<br/>`pgc`：追番追剧<br/>`article`：专栏 |
| offset          | num |     | 分页偏移量  | 翻页时使用                                                     |
| update_baseline | str |     | 更新基线   | 获取新动态时使用                                                  |
| page            | num |     | 页数     | 无效参数                                                      |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                  |
|---------|-----|------|---------------------|
| code    | num | 响应码  | 0：成功<br/>-101：账号未登录 |
| message | str |      |                     |
| ttl     | num | 1    |                     |
| data    | obj | 信息本体 |                     |

### `data`对象

| 字段名             | 类型    | 内容             | 备注                  |
|-----------------|-------|----------------|---------------------|
| has_more        | bool  | 是否有更多数据        |                     |
| items           | array | 数据数组           |                     |
| offset          | str   | 偏移量            | 等于`items`中最后一条记录的id |
| update_baseline | str   | 更新基线           | 等于`items`中第一条记录的id  |
| update_num      | num   | 本次获取获取到了多少条新动态 | 在更新基线以上的动态条数        |

### `data`对象 -> `items`数组中的对象

| 字段名     | 类型    | 内容   | 备注            |
|---------|-------|------|---------------|
| basic   | obj   |      |               |
| id_str  | str   |      |               |
| modules | obj   |      |               |
| type    | str   | 动态类型 | [动态类型](#动态类型) |
| visible | bool  |      |               |
| orig    | obj   |      |               |
| height  | num   |      |               |
| size    | num   |      |               |
| src     | str   |      |               |
| tags    | array |      |               |
| width   | num   |      |               |
| desc    | obj   |      |               |

### `data`对象 -> `items`数组中的对象 -> `basic`对象

| 字段名            | 类型  | 内容  | 备注                                                                                                                              |
|----------------|-----|-----|---------------------------------------------------------------------------------------------------------------------------------|
| comment_id_str | str |     | `DYNAMIC_TYPE_AV`：视频AV号<br/>`DYNAMIC_TYPE_LIVE_RCMD`：动态本身id<br/>`DYNAMIC_TYPE_DRAW`：(?)图片id<br/>`DYNAMIC_TYPE_ARTICLE`：专栏cvid   |
| comment_type   | num |     | 1：`DYNAMIC_TYPE_AV` `DYNAMIC_TYPE_PGC`<br/>11：`DYNAMIC_TYPE_DRAW`<br/>12：`DYNAMIC_TYPE_ARTICLE`<br/>17：`DYNAMIC_TYPE_LIVE_RCMD` |
| like_icon      | obj |     |                                                                                                                                 |
| rid_str        | str |     |                                                                                                                                 |

### `data`对象 -> `items`数组中的对象 -> `basic`对象 -> `like_icon`对象

| 字段名        | 类型  | 内容  | 备注  |
|------------|-----|-----|-----|
| action_url | str |     |     |
| end_url    | str |     |     |
| id         | num |     |     |
| start_url  | str |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象

| 字段名                | 类型  | 内容  | 备注  |
|--------------------|-----|-----|-----|
| module_author      | obj |     |     |
| module_dynamic     | obj |     |     |
| module_more        | obj |     |     |
| module_stat        | obj |     |     |
| module_interaction | obj |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_author`对象

| 字段名               | 类型   | 内容  | 备注  |
|-------------------|------|-----|-----|
| face              | str  |     |     |
| face_nft          | bool |     |     |
| following         | bool |     |     |
| jump_url          | str  |     |     |
| label             | str  |     |     |
| mid               | num  |     |     |
| name              | str  |     |     |
| pub_action        | str  |     |     |
| pub_time          | str  |     |     |
| pub_ts            | num  |     |     |
| type              | str  |     |     |
| decorate          | obj  |     |     |
| official_verify   | obj  |     |     |
| pendant           | obj  |     |     |
| pub_location_text | str  |     |     |
| vip               | obj  |     |     |
| nft_info          | obj  |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_author`对象 -> `decorate`对象

| 字段名      | 类型  | 内容  | 备注  |
|----------|-----|-----|-----|
| card_url | str |     |     |
| fan      | obj |     |     |
| id       | num |     |     |
| jump_url | str |     |     |
| name     | str |     |     |
| type     | num |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_author`对象 -> `decorate`对象 -> `fan`对象

| 字段名     | 类型   | 内容  | 备注  |
|---------|------|-----|-----|
| color   | str  |     |     |
| is_fan  | bool |     |     |
| num_str | str  |     |     |
| number  | num  |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_author`对象 -> `decorate`对象 -> `fan`对象 -> `official_verify`对象

| 字段名  | 类型  | 内容  | 备注  |
|------|-----|-----|-----|
| desc | str |     |     |
| type | num |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_author`对象 -> `decorate`对象 -> `fan`对象 -> `pendant`对象

| 字段名                 | 类型  | 内容  | 备注  |
|---------------------|-----|-----|-----|
| expire              | num |     |     |
| image               | str |     |     |
| image_enhance       | str |     |     |
| image_enhance_frame | str |     |     |
| name                | str |     |     |
| pid                 | num |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_author`对象 -> `decorate`对象 -> `fan`对象 -> `vip`对象

| 字段名                  | 类型  | 内容  | 备注  |
|----------------------|-----|-----|-----|
| avatar_subscript     | num |     |     |
| avatar_subscript_url | str |     |     |
| due_date             | num |     |     |
| label                | obj |     |     |
| nickname_color       | str |     |     |
| status               | num |     |     |
| theme_type           | num |     |     |
| type                 | num |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_author`对象 -> `decorate`对象 -> `fan`对象 -> `vip`对象 -> `label`对象

| 字段名                       | 类型   | 内容  | 备注  |
|---------------------------|------|-----|-----|
| bg_color                  | str  |     |     |
| bg_style                  | num  |     |     |
| border_color              | str  |     |     |
| img_label_uri_hans        | str  |     |     |
| img_label_uri_hans_static | str  |     |     |
| img_label_uri_hant        | str  |     |     |
| img_label_uri_hant_static | str  |     |     |
| label_theme               | str  |     |     |
| path                      | str  |     |     |
| text                      | str  |     |     |
| text_color                | str  |     |     |
| use_img_label             | bool |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_dynamic`对象

| 字段名        | 类型   | 内容  | 备注  |
|------------|------|-----|-----|
| additional | null |     |     |
| desc       | null |     |     |
| major      | obj  |     |     |
| topic      | null |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_dynamic`对象 -> `major`对象

| 字段名        | 类型  | 内容  | 备注  |
|------------|-----|-----|-----|
| type       | str |     |     |
| ugc_season | obj |     |     |
| live_rcmd  | obj |     |     |
| archive    | obj |     |     |
| draw       | obj |     |     |
| live       | obj |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_dynamic`对象 -> `major`对象 -> `ugc_season`对象

| 字段名             | 类型  | 内容  | 备注  |
|-----------------|-----|-----|-----|
| aid             | num |     |     |
| badge           | obj |     |     |
| cover           | str |     |     |
| desc            | str |     |     |
| disable_preview | num |     |     |
| duration_text   | str |     |     |
| jump_url        | str |     |     |
| stat            | obj |     |     |
| title           | str |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_dynamic`对象 -> `major`对象 -> `ugc_season`对象 -> `badge`对象

| 字段名      | 类型  | 内容  | 备注  |
|----------|-----|-----|-----|
| bg_color | str |     |     |
| color    | str |     |     |
| text     | str |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_dynamic`对象 -> `major`对象 -> `ugc_season`对象 -> `stat`对象

| 字段名     | 类型  | 内容  | 备注  |
|---------|-----|-----|-----|
| danmaku | str |     |     |
| play    | str |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_dynamic`对象 -> `major`对象 -> `live_rcmd`对象

| 字段名          | 类型  | 内容  | 备注  |
|--------------|-----|-----|-----|
| content      | str |     |     |
| reserve_type | num |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_dynamic`对象 -> `major`对象 -> `archive`对象

| 字段名             | 类型  | 内容  | 备注  |
|-----------------|-----|-----|-----|
| aid             | str |     |     |
| badge           | obj |     |     |
| bvid            | str |     |     |
| cover           | str |     |     |
| desc            | str |     |     |
| disable_preview | num |     |     |
| duration_text   | str |     |     |
| jump_url        | str |     |     |
| stat            | obj |     |     |
| title           | str |     |     |
| type            | num |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_dynamic`对象 -> `major`对象 -> `archive`对象 -> `badge`对象

| 字段名     | 类型    | 内容  | 备注  |
|---------|-------|-----|-----|

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_dynamic`对象 -> `major`对象 -> `archive`对象 -> `stat`对象

| 字段名             | 类型  | 内容  | 备注  |
|-----------------|-----|-----|-----|
| aid             | str |     |     |
| badge           | obj |     |     |
| bvid            | str |     |     |
| cover           | str |     |     |
| desc            | str |     |     |
| disable_preview | num |     |     |
| duration_text   | str |     |     |
| jump_url        | str |     |     |
| stat            | obj |     |     |
| title           | str |     |     |
| type            | num |     |     |
### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_dynamic`对象 -> `major`对象 -> `draw`对象

| 字段名   | 类型    | 内容  | 备注  |
|-------|-------|-----|-----|
| id    | num   |     |     |
| items | array |     |     |
### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_dynamic`对象 -> `major`对象 -> `live`对象

| 字段名          | 类型  | 内容  | 备注  |
|--------------|-----|-----|-----|
| badge        | obj |     |     |
| cover        | str |     |     |
| desc_first   | str |     |     |
| desc_second  | str |     |     |
| id           | num |     |     |
| jump_url     | str |     |     |
| live_state   | num |     |     |
| reserve_type | num |     |     |
| title        | str |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_more`对象

| 字段名               | 类型    | 内容  | 备注  |
|-------------------|-------|-----|-----|
| three_point_items | array |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_more`对象 -> `three_point_items`数组中的对象

| 字段名   | 类型  | 内容  | 备注  |
|-------|-----|-----|-----|
| label | str |     |     |
| type  | str |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_stat`对象

| 字段名     | 类型  | 内容  | 备注  |
|---------|-----|-----|-----|
| comment | obj |     |     |
| forward | obj |     |     |
| like    | obj |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_stat`对象 -> `comment`对象

| 字段名       | 类型   | 内容   | 备注            |
|-----------|------|------|---------------|
| count     | num  |      |               |
| forbidden | bool |      |               |
| hidden    | bool | 是否隐藏 | 直播类型动态会隐藏回复功能 |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_stat`对象 -> `forward`对象

| 字段名       | 类型   | 内容  | 备注  |
|-----------|------|-----|-----|
| count     | num  |     |     |
| forbidden | bool |     |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_stat`对象 -> `like`对象

| 字段名       | 类型   | 内容       | 备注  |
|-----------|------|----------|-----|
| count     | num  | 点赞数      |     |
| forbidden | bool |          |     |
| status    | bool | 当前用户是否点赞 |     |

### `data`对象 -> `items`数组中的对象 -> `modules`对象 -> `module_stat`对象 -> `module_interaction`对象

| 字段名   | 类型    | 内容  | 备注  |
|-------|-------|-----|-----|
| items | array |     |     |

### `data`对象 -> `items`数组中的对象 -> `orig`对象

| 字段名     | 类型    | 内容  | 备注  |
|---------|-------|-----|-----|

## 请求示例

### `SESSDATA`方式

```shell

```

### `access_key`方式

```shell

```

## 响应示例

<details>
<summary>点击查看</summary>

```json

```

</details>