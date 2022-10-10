# 获取预约信息

> https://api.bilibili.com/x/space/reservation?vmid=933478

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名  | 类型  | 必填  | 内容    | 备注  |
|------|-----|-----|-------|-----|
| vmid | num | √   | 用户uid |     |

## Json回复

### 根对象

| 字段名     | 类型    | 内容   | 备注   |
|---------|-------|------|------|
| code    | num   | 响应码  | 0：成功 |
| message | str   | 0    |      |
| ttl     | num   | 1    |      |
| data    | array | 信息本体 |      |

### `data`数组中的对象

| 字段名                  | 类型   | 内容         | 备注                |
|----------------------|------|------------|-------------------|
| sid                  | num  |            |                   |
| name                 | str  | 预约标题       |                   |
| total                | num  | 当前预约总人数    |                   |
| stime                | num  | 预约开始时间戳    | 单位：秒              |
| etime                | num  | 预约结束时间戳    | 单位：秒              |
| is_follow            | num  | 当前用户是否已预约  | 0：未预约<br/>1：已预约   |
| state                | num  | `100`      |                   |
| oid                  | str  | `空串`       |                   |
| type                 | num  | 预约类型       | 1：视频预约<br/>2：直播预约 |
| up_mid               | num  | 预约所属UP主uid |                   |
| reserve_record_ctime | num  | 第一次点预约的时间戳 | 单位：秒              |
| live_plan_start_time | num  | 直播计划开始时间戳  | 单位：秒              |
| show_total           | bool | 是否显示预约总数   |                   |
| subtitle             | str  | `空串`       |                   |
| attached_badge_text  | str  | `空串`       |                   |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/space/reservation?vmid=933478' \
-H 'cookie: SESSDATA=xxx'
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
      "sid": 470047,
      "name": "预告：策划",
      "total": 7902,
      "stime": 1646305965,
      "etime": 2147454847,
      "is_follow": 0,
      "state": 100,
      "oid": "",
      "type": 1,
      "up_mid": 933478,
      "reserve_record_ctime": 1665409554,
      "live_plan_start_time": 0,
      "show_total": true,
      "subtitle": "",
      "attached_badge_text": ""
    }
  ]
}
```

</details>

# 预约（通过动态中的按钮）

> https://api.vc.bilibili.com/dynamic_mix/v1/dynamic_mix/reserve_attach_card_button

请求方式：`POST`

是否需要登录：`是`

Content-Type：`application/x-www-form-urlencoded`

## FORM参数

| 参数名              | 类型  | 必填  | 内容        | 备注              |
|------------------|-----|-----|-----------|-----------------|
| cur_btn_status   | num |     | 操作类型      | 1：预约<br/>2：取消预约 |
| dynamic_id       | num |     | 动态id      |                 |
| attach_card_type | str |     | `reserve` |                 |
| reserve_total    | num |     | 提交前的预约总人数 |                 |
| reserve_id       | num | √   | 预约id      |                 |
| spmid            | str |     | `空串`      |                 |
| csrf             | str |     | 用户csrf    |                 |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                          |
|---------|-----|------|-----------------------------|
| code    | num | 响应码  | 0：成功<br/>7604003：操作失败，请稍后重试 |
| message | str | 0    |                             |
| ttl     | num | 1    |                             |
| data    | obj | 信息本体 |                             |

### `data`对象

| 字段名              | 类型   | 内容       | 备注                       |
|------------------|------|----------|--------------------------|
| btn_mode         | num  | `1`      |                          |
| final_btn_status | num  | 最终按钮状态   | 1：蓝色未按下状态<br/>2：灰色已经按下状态 |
| desc_update      | str  | 显示预约人数文案 |                          |
| reserve_update   | num  | 预约总人数    |                          |
| toast            | str  | 提示文案     |                          |
| has_activity     | bool | `false`  |                          |
| activity_url     | str  | `空串`     |                          |
| _gt_             | num  | `0`      |                          |

## 请求示例

### `SESSDATA`方式

```shell
curl -L -X POST 'https://api.vc.bilibili.com/dynamic_mix/v1/dynamic_mix/reserve_attach_card_button' \
-H 'cookie: SESSDATA=xxx' \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'cur_btn_status=1' \
--data-urlencode 'dynamic_id=633368592307453970' \
--data-urlencode 'attach_card_type=reserve' \
--data-urlencode 'reserve_total=66666' \
--data-urlencode 'reserve_id=470047' \
--data-urlencode 'spmid=' \
--data-urlencode 'csrf=xxx'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "code": 0,
  "msg": "",
  "message": "",
  "data": {
    "btn_mode": 1,
    "final_btn_status": 2,
    "desc_update": "6.6万人预约",
    "reserve_update": 66667,
    "toast": "预约成功，会在开始时提醒您",
    "has_activity": false,
    "activity_url": "",
    "_gt_": 0
  }
}
```

</details>