# 获取直播间信息

> https://api.live.bilibili.com/xlive/web-room/v2/index/getRoomPlayInfo

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名      | 类型  | 必填  | 内容  | 备注  |
|----------|-----|-----|-----|-----|
| room_id  | num |     |     |     |
| protocol | str |     |     |     |
| format   | str |     |     |     |
| codec    | str |     |     |     |
| qn       | num |     |     |     |
| platform | str |     |     |     |
| ptype    | num |     |     |     |
| dolby    | num |     |     |     |
| panorama | num |     |     |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名               | 类型    | 内容       | 备注              |
|-------------------|-------|----------|-----------------|
| room_id           | num   | 直播间id    |                 |
| short_id          | num   | 直播间短id   |                 |
| uid               | num   | 主播UID    |                 |
| is_hidden         | bool  |          |                 |
| is_locked         | bool  | 直播间是否被封禁 |                 |
| is_portrait       | bool  |          |                 |
| live_status       | num   | 直播状态     | 1：直播中<br/>2：未开播 |
| hidden_till       | num   |          |                 |
| lock_till         | num   | 封禁结束时间   | 秒级时间戳           |
| encrypted         | bool  |          |                 |
| pwd_verified      | bool  |          |                 |
| live_time         | num   | 本次开播时间   | 秒级时间戳           |
| room_shield       | num   |          |                 |
| all_special_types | array |          |                 |
| playurl_info      | obj   | 直播流信息    |                 |

### `data`对象 -> `playurl_info`对象

| 字段名       | 类型  | 内容  | 备注  |
|-----------|-----|-----|-----|
| conf_json | str |     |     |
| playurl   | obj |     |     |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象

| 字段名       | 类型    | 内容  | 备注  |
|-----------|-------|-----|-----|
| cid       | num   |     |     |
| g_qn_desc | array |     |     |
| stream    | array |     |     |
| p2p_data  | obj   |     |     |
| dolby_qn  | null  |     |     |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `g_qn_desc`数组中的对象

| 字段名       | 类型   | 内容  | 备注  |
|-----------|------|-----|-----|
| qn        | num  |     |     |
| desc      | str  |     |     |
| hdr_desc  | str  |     |     |
| attr_desc | null |     |     |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `stream`数组中的对象

| 字段名           | 类型    | 内容  | 备注  |
|---------------|-------|-----|-----|
| protocol_name | str   |     |     |
| format        | array |     |     |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `stream`数组中的对象 -> `format`数组中的对象

| 字段名         | 类型    | 内容  | 备注  |
|-------------|-------|-----|-----|
| format_name | str   |     |     |
| codec       | array |     |     |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `stream`数组中的对象 -> `format`数组中的对象 -> `codec`数组中的对象

| 字段名        | 类型    | 内容  | 备注  |
|------------|-------|-----|-----|
| codec_name | str   |     |     |
| current_qn | num   |     |     |
| accept_qn  | array |     |     |
| base_url   | str   |     |     |
| url_info   | array |     |     |
| hdr_qn     | null  |     |     |
| dolby_type | num   |     |     |
| attr_name  | str   |     |     |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `stream`数组中的对象 -> `format`数组中的对象 -> `codec`数组中的对象 -> `accept_qn`数组中的对象

| 字段名 | 类型  | 内容  | 备注  |
|-----|-----|-----|-----|

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `stream`数组中的对象 -> `format`数组中的对象 -> `codec`数组中的对象 -> `url_info`数组中的对象

| 字段名        | 类型  | 内容  | 备注  |
|------------|-----|-----|-----|
| host       | str |     |     |
| extra      | str |     |     |
| stream_ttl | num |     |     |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `p2p_data`对象

| 字段名       | 类型   | 内容  | 备注  |
|-----------|------|-----|-----|
| p2p       | bool |     |     |
| p2p_type  | num  |     |     |
| m_p2p     | bool |     |     |
| m_servers | null |     |     |

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