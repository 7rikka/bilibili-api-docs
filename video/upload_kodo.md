# 获取上传参数

> https://member.bilibili.com/preupload

请求方式：`GET`

是否需要登录：`是`

鉴权方式：`SESSDATA`

## URL参数

### kodo方式

| 参数名        | 类型  | 必填  | 内容     | 备注                                                                              |
|------------|-----|-----|--------|---------------------------------------------------------------------------------|
| name       | str | √   | 视频文件名  |                                                                                 |
| size       | str | √   | 视频文件大小 | 单位：字节                                                                           |
| r          | str | √   | 上传方式   | `kodo`                                                                          |
| os         | str |     |        | `kodo`                                                                          |
| bucket     | str |     |        | 已知可用值：`bvcupcdnkodohd` `bvcupcdnkodobm`<br/>默认：`bvcupcdnkodohd`                 |
| profile    | str | √   |        | 已知可用值：`ugcupos/bup` `ugcupos/bupfetch` `ugcupos/fetch` `ugcfx/bup` `fxmeta/bup` |
| ssl        | str |     |        | `0`                                                                             |
| version    | str |     |        | `2.11.0`                                                                        |
| build      | str |     |        | `2110000`                                                                       |
| webVersion | str |     |        | `2.0.0`                                                                         |

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

# 上传分块

> https: + {endpoint} + /mkblk/ + {分块总字节数}

例如 `endpoint` 为 `//upload-na0.qbox.me`，分块字节数为 `3023228`，则上传地址为 `https://upload-na0.qbox.me/mkblk/3023228`

`mkblk`应该为`make block`

请求方式：`POST`

Content-Type：`application/octet-stream`

## HEADER参数

| 参数名           | 类型  | 必填  | 内容      | 备注                         |
|---------------|-----|-----|---------|----------------------------|
| Authorization | str | √   | 上传token | `UpToken XXXXXXXXXXX`      |
| Content-Type  | str | √   | 内容类型    | `application/octet-stream` |

## BODY内容

`分块的二进制内容，分块大小为4MB`

## Json回复

### 根对象

| 字段名        | 类型  | 内容     | 备注     |
|------------|-----|--------|--------|
| ctx        | str |        |        |
| checksum   | str |        |        |
| crc32      | num |        |        |
| offset     | num |        |        |
| host       | str |        |        |
| expired_at | num | 有效期时间戳 | 有效期为7天 |

## 请求示例

```shell

```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "ctx": "xxx",
  "checksum": "xxx",
  "crc32": 2502997942,
  "offset": 3023228,
  "host": "https://upload-na0.qbox.me",
  "expired_at": 1675332417
}
```

</details>

# 结束分块上传

> https: + {endpoint} + /mkfile/ + {文件总字节数} + /key/ + base64(key)

`mkfile`应该为`make file`

请求方式：`POST`

Content-Type：`application/json`

## HEADER参数

| 参数名           | 类型  | 必填  | 内容                    | 备注  |
|---------------|-----|-----|-----------------------|-----|
| Authorization | str | √   | `UpToken XXXXXXXXXXX` |     |

## BODY内容

`每个分块上传结果的ctx，按照顺序使用英文逗号连接的字符串`

## Json回复

### 根对象

| 字段名  | 类型  | 内容    | 备注  |
|------|-----|-------|-----|
| hash | str |       |     |
| key  | str | 唯一文件名 |     |

## 请求示例

```shell
curl --location --request POST 'https://upload-na0.qbox.me/mkfile/3023228/key/xxx' \
--header 'authorization: UpToken xxx' \
--header 'Content-Type: text/plain' \
--data-raw 'xxx'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "hash": "xxx",
  "key": "xxx"
}
```

</details>

# 通知主站拉取视频

> https: + {fetch_url}

请求方式：`POST`

Content-Type：`application/x-www-form-urlencoded`

## HEADER参数

| 参数名                 | 类型  | 必填  | 内容                       | 备注  |
|---------------------|-----|-----|--------------------------|-----|
| X-Upos-Auth         | str | √   | 请求头`X-Upos-Auth`         |     |
| X-Upos-Fetch-Source | str | √   | 请求头`X-Upos-Fetch-Source` |     |

## URL参数

| 参数名     | 类型  | 必填  | 内容              | 备注  |
|---------|-----|-----|-----------------|-----|
| fetch   | str | √   | `空`             |     |
| name    | str | √   | 视频原始文件名         |     |
| output  | str | √   | `json`          |     |
| profile | str | √   | `ugcupos/fetch` |     |
| biz_id  | str | √   | 视频biz_id        |     |

## Json回复

### 根对象

| 字段名  | 类型  | 内容         | 备注  |
|------|-----|------------|-----|
| OK   | num | `1`        |     |
| info | str | `Success.` |     |

## 请求示例

```shell
curl --location --request POST 'https://upos-cs-upcdnqn.bilivideo.com/ugc/xxxxxxx?fetch=&name=xxxxx&output=json&profile=ugcupos%2Ffetch&biz_id=xxx' \
--header 'X-Upos-Auth: xxx' \
--header 'X-Upos-Fetch-Source: xxx'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "OK": 1,
  "info": "Success."
}
```

</details>