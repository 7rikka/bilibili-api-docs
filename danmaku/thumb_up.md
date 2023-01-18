# 点赞弹幕

> https://api.bilibili.com/x/v2/dm/thumbup/add

请求方式：`POST`

是否需要登录：`是`

鉴权方式：`SESSDATA`

Content-Type：`application/x-www-form-urlencoded`

## URL参数

| 参数名              | 类型  | 必填  | 内容     | 备注              |
|------------------|-----|-----|--------|-----------------|
| op               | str | √   | 操作类型   | 1：点赞<br/>2：取消点赞 |
| dmid             | str | √   | 弹幕id   |                 |
| oid              | str | √   | 视频cid  |                 |
| platform         | str |     |        |                 |
| polaris_appid    | str |     |        |                 |
| polaris_platfrom | str |     |        |                 |
| spmid            | str |     |        |                 |
| from_spmid       | str |     |        |                 |
| csrf             | str | √   | 用户csrf |                 |

## Json回复

### 根对象

| 字段名     | 类型  | 内容  | 备注                                                                                                                                          |
|---------|-----|-----|---------------------------------------------------------------------------------------------------------------------------------------------|
| code    | num | 响应码 | 0：成功<br/>-101：账号未登录<br/>-111：csrf 校验失败<br/>-400：请求错误<br/>-404：啥都木有<br/>36106：该弹幕已被删除<br/>36805：该视频禁止点赞弹幕<br/>65004：取消赞失败 未点赞过<br/>65006：已赞过 |
| message | str | 0   |                                                                                                                                             |
| ttl     | num | 1   |                                                                                                                                             |

## 请求示例

```shell
curl -L -X POST 'https://api.bilibili.com/x/v2/dm/thumbup/add?op=1&dmid=xxx&oid=xxx&csrf=xxx' \
-H 'Cookie: SESSDATA=xxx;'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "code": 0,
  "message": "0",
  "ttl": 1
}
```

</details>