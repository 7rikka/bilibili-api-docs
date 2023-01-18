# 查询直播间封禁状态

> https://api.live.bilibili.com/room/v1/Room/getBannedInfo

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名    | 类型  | 必填  | 内容    | 备注  |
|--------|-----|-----|-------|-----|
| roomid | str | √   | 直播间id |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注               |
|---------|-----|------|------------------|
| code    | num | 响应码  | 0：成功<br/>1：房间不存在 |
| msg     | str |      |                  |
| message | str |      |                  |
| data    | obj | 信息本体 |                  |

### `data`对象

| 字段名       | 类型  | 内容  | 备注                          |
|-----------|-----|-----|-----------------------------|
| lock_till | num |     | 0：未封禁<br/>-1：永久封禁<br/>-2：封禁 |

#### 示例

| lock_till | url                                                                                           |
|-----------|-----------------------------------------------------------------------------------------------|
| -1        | [580794](https://live.bilibili.com/580794)<br/>[23094995](https://live.bilibili.com/23094995) |
| -2        | [5432670](https://live.bilibili.com/5432670)                                                  |

## 请求示例

```shell
curl -L -X GET 'https://api.live.bilibili.com/room/v1/Room/getBannedInfo?roomid=3'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "code": 0,
  "msg": "ok",
  "message": "ok",
  "data": {
    "lock_till": 0
  }
}
```

</details>