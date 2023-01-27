# b站上传速度测试页面

> https://member.bilibili.com/preupload?r=ping

# upos可用上传cdn

| 线路       | zone | upcdn |
|----------|------|-------|
| sz-bda2  | sz   | bda2  |
| sz-qn    | sz   | qn    |
| cs-bda2  | cs   | bda2  |
| cs-qn    | cs   | qn    |
| cs-qnhk  | cs   | qnhk  |
| cs-bldsa | cs   | bldsa |

# 获取上传参数

> https://member.bilibili.com/preupload

请求方式：`GET`

是否需要登录：`是`

鉴权方式：`SESSDATA`

## URL参数

### kodo方式

| 参数名        | 类型  | 必填  | 内容     | 备注            |
|------------|-----|-----|--------|---------------|
| name       | str | √   | 视频文件名  |               |
| size       | str | √   | 视频文件大小 | 单位：字节         |
| r          | str | √   | 上传方式   | `upos`        |
| os         | str |     |        | `upos`        |
| upcdn      | str |     |        |               |
| zone       | str |     |        |               |
| profile    | str |     |        | `ugcupos/bup` |
| ssl        | str |     |        | `0`           |
| version    | str |     |        | `2.10.4.0`    |
| build      | str |     |        | `2100400`     |
| webVersion | str |     |        | `2.0.0`       |

## Json回复

### 根对象

| 字段名           | 类型    | 内容      | 备注         |
|---------------|-------|---------|------------|
| OK            | num   | `1`     |            |
| bili_filename | str   | 唯一文件id  | `在投稿中需要此值` |
| biz_id        | num   | 视频cid   |            |
| endpoint      | str   | 上传地址域名  |            |
| fetch_headers | obj   | 请求头信息   |            |
| fetch_url     | str   | 确认url   |            |
| fetch_urls    | array | 确认url列表 |            |
| key           | str   | 唯一文件名   |            |
| uptoken       | str   | 上传token |            |

### `fetch_headers`对象

| 字段名                 | 类型  | 内容                       | 备注  |
|---------------------|-----|--------------------------|-----|
| X-Upos-Auth         | str | 请求头`X-Upos-Auth`         |     |
| X-Upos-Fetch-Source | str | 请求头`X-Upos-Fetch-Source` |     |

## 请求示例

```shell
curl --location --request GET 'https://member.bilibili.com/preupload?name=xxx&r=kodo&profile=ugcupos%2Fbup&size=3023228' \
--header 'cookie: SESSDATA=xxx'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "OK": 1,
  "bili_filename": "********************************",
  "biz_id": 10086,
  "endpoint": "//upload-na0.qbox.me",
  "fetch_headers": {
    "X-Upos-Auth": "access_id=**********&cdn=bvcupcdnkodobm&os=kodo&sign=********************************&timestamp=**********.***&uid=*******&uip=***.**.***.***&uport=*****&use_dqp=0",
    "X-Upos-Fetch-Source": "https://bvcupcdnkodobm.qbox.me/n230125ko32zdci13t6byaq8c5tdsnva.mp4"
  },
  "fetch_url": "//upos-cs-upcdnqn.bilivideo.com/ugc/********************************.mp4?biz_id=*********&fetch=&name=a.mp4&output=json&profile=ugcupos%2Ffetch",
  "fetch_urls": [
    "//upos-cs-upcdnqn.bilivideo.com/ugc/********************************.mp4?biz_id=*********&fetch=&name=a.mp4&output=json&profile=ugcupos%2Ffetch",
    "//upos-cs-upcdnws.bilivideo.com/ugc/********************************.mp4?biz_id=*********&fetch=&name=a.mp4&output=json&profile=ugcupos%2Ffetch"
  ],
  "key": "********************************.mp4",
  "uptoken": "****************************************:***************************=:************************************************************************************************************************************"
}
```

</details>