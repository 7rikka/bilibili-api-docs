# 一键三连

> https://api.bilibili.com/x/web-interface/archive/like/triple

请求方式：`POST`

是否需要登录：`是`

Content-Type：`application/x-www-form-urlencoded`

## FORM参数

| 参数名    | 类型  | 必填  | 内容           | 备注       |
|--------|-----|-----|--------------|----------|
| aid    | num | √   | 视频av号        | av,bv二选一 |
| bvid   | str | √   | 视频bv号        | av,bv二选一 |
| csrf   | str | √   | 用户csrf       |          |
| eab_x  | str |     | `2`          |          |
| ramval | str |     | `3`          |          |
| source | str |     | `web_normal` |          |
| ga     | num |     | `1`          |          |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                                    |
|---------|-----|------|-------------------------------------------------------|
| code    | num | 响应码  | 0：成功<br/>-101：账号未登录<br/>-111：csrf 校验失败<br/> -400：请求错误 |
| message | str |      |                                                       |
| ttl     | num | 1    |                                                       |
| data    | obj | 信息本体 |                                                       |

### `data`对象

| 字段名           | 类型   | 内容      | 备注  |
|---------------|------|---------|-----|
| like          | bool | 点赞是否成功  |     |
| coin          | bool | 投币是否成功  |     |
| fav           | bool | 收藏是否成功  |     |
| multiply      | num  | `0`     |     |
| is_risk       | bool | `false` |     |
| gaia_res_type | num  | `0`     |     |
| gaia_data     |      | `null`  |     |

## 请求示例

```shell
curl -L -X POST 'https://api.bilibili.com/x/web-interface/archive/like/triple' \
-H 'cookie:  SESSDATA=xxx' \
-H 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'aid=xxx' \
--data-urlencode 'csrf=xxx'
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
    "like": true,
    "coin": true,
    "fav": true,
    "multiply": 0,
    "is_risk": false,
    "gaia_res_type": 0,
    "gaia_data": null
  }
}
```

</details>