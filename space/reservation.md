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