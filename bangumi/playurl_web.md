# 获取视频播放流

**此接口是剧集解析专用接口，无法解析普通视频**

> https://api.bilibili.com/pgc/player/web/playurl

请求方式：`GET`

是否需要登录：`否`

请求参数参考：[(WEB端)获取视频播放流](../video/playurl_web.md)

## URL参数

| 参数名           | 类型  | 必填  | 内容        | 备注                                                               |
|---------------|-----|-----|-----------|------------------------------------------------------------------|
| avid          | num |     |           |                                                                  |
| cid           | num | √   | 视频cid     | cid，ep_id二选一                                                     |
| qn            | num |     | 视频最高清晰度代码 | 默认80(1080p)<br/>[视频流清晰度代码列表](../video/playurl_web.md#视频流清晰度代码列表) |
| fnver         | num |     | 固定值：`0`   |                                                                  |
| fnval         | num |     | 视频格式参数    |                                                                  |
| fourk         | num |     | 是否获取4K清晰度 |                                                                  |
| ep_id         | num | √   | 视频epid    | cid，ep_id二选一                                                     |
| session       | str |     |           |                                                                  |
| from_client   | str |     | `BROWSER` |                                                                  |
| drm_tech_type | num |     | `2`       |                                                                  |

## Json回复

### 根对象

| 字段名     | 类型  | 内容        | 备注   |
|---------|-----|-----------|------|
| code    | num | 响应码       | 0：成功 |
| message | str | `success` |      |
| result  | obj |           |      |

### `result`对象

| 字段名                | 类型    | 内容                                    | 备注                                           |
|--------------------|-------|---------------------------------------|----------------------------------------------|
| accept_format      | str   | 视频支持的格式列表                             | 取决于`fnval`和`fourk`                           |
| code               | num   | `0`                                   |                                              |
| seek_param         | str   | 固定值：`start`                           |                                              |
| is_preview         | num   | `0`                                   |                                              |
| fnval              | num   | 请求时的`fnval`                           |                                              |
| video_project      | bool  | `true`                                |                                              |
| fnver              | num   | 请求时的`fnver`                           |                                              |
| type               | str   | `DASH` `MP4` `FLV`                    |                                              |
| bp                 | num   | 当前用户是否已承包                             | 0：未承包<br/>1：已承包                              |
| result             | str   | `suee`                                |                                              |
| seek_type          | str   | offset：`DASH`、`FLV`<br/> second：`mp4` |                                              |
| vip_type           | num   | 当前用户大会员类型                             | 1：月度大会员<br/>2：年度大会员                          |
| from               | str   | `local`                               |                                              |
| video_codecid      | num   | 默认选择视频流的编码类型                          | [视频编码格式代码](../video/playurl_web.md#视频编码格式代码) |
| record_info        | obj   | 备案信息                                  |                                              |
| is_drm             | bool  | `false`                               |                                              |
| no_rexcode         | num   | `0`                                   |                                              |
| format             | str   | 前端播放器显示最高的视频格式                        |                                              |
| support_formats    | array | 支持格式的详细信息                             |                                              |
| message            | str   | `空串`                                  |                                              |
| accept_quality     | array | 视频支持的分辨率代码列表                          | 取决于`fnval`和`fourk`                           |
| quality            | num   | 前端播放器显示最高的视频清晰度代码                     |                                              |
| timelength         | num   | 视频长度                                  | 单位：毫秒                                        |
| has_paid           | bool  | `false`                               |                                              |
| vip_status         | num   | 当前用户是否是大会员                            | 0：不是<br/>1：是                                 |
| dash               | obj   | `DASH`格式返回的视频流和音频流信息                  |                                              |
| clip_info_list     | array | `空数组`                                 |                                              |
| accept_description | array | 视频支持的分辨率列表                            | 取决于`fnval`和`fourk`                           |
| status             | num   | `2`                                   |                                              |

#### `result`对象 -> `dash`对象

| 字段名             | 类型    | 内容        | 备注   |
|-----------------|-------|-----------|------|
| duration        | num   | 视频长度      | 单位：秒 |
| minBufferTime   | num   | `1.5`     |      |
| min_buffer_time | num   | `1.5`     |      |
| video           | array | 视频流信息     |      |
| audio           | array | 音频流信息     |      |
| dolby           | obj   | 杜比全景声音轨信息 |      |

#### `result`对象 -> `dash`对象 -> `video`数组中的对象

| 字段名            | 类型    | 内容         | 备注                                           |
|----------------|-------|------------|----------------------------------------------|
| start_with_sap | num   | `1`        |                                              |
| bandwidth      | num   | 所需最低带宽     |                                              |
| sar            | str   | `1:1`      |                                              |
| backupUrl      | array | 备用音频流url列表 |                                              |
| codecs         | str   | 编码类型       |                                              |
| base_url       | str   | 默认视频流url   |                                              |
| backup_url     | array | 备用音频流url列表 |                                              |
| segment_base   | obj   |            |                                              |
| mimeType       | str   | 格式类型       |                                              |
| frame_rate     | str   | 帧率         |                                              |
| SegmentBase    | obj   |            |                                              |
| frameRate      | str   | 帧率         |                                              |
| codecid        | num   | 视频编码格式代码   | [视频编码格式代码](../video/playurl_web.md#视频编码格式代码) |
| baseUrl        | str   | 默认视频流url   |                                              |
| size           | num   | 文件大小       |                                              |
| mime_type      | str   | 格式类型       |                                              |
| width          | num   | 视频宽度       |                                              |
| startWithSAP   | num   | `1`        |                                              |
| id             | num   | 视频清晰度代码    | [视频流清晰度代码列表](#视频流清晰度代码列表)                    |
| height         | num   | 视频高度       |                                              |
| md5            | str   | `空串`       |                                              |

#### `result`对象 -> `dash`对象 -> `audio`数组中的对象

| 字段名            | 类型    | 内容         | 备注                                           |
|----------------|-------|------------|----------------------------------------------|
| start_with_sap | num   | `1`        |                                              |
| bandwidth      | num   | 所需最低带宽     |                                              |
| sar            | str   | `1:1`      |                                              |
| backupUrl      | array | 备用音频流url列表 |                                              |
| codecs         | str   | 编码类型       |                                              |
| base_url       | str   | 默认视频流url   |                                              |
| backup_url     | array | 备用音频流url列表 |                                              |
| segment_base   | obj   |            |                                              |
| mimeType       | str   | 格式类型       |                                              |
| frame_rate     | str   | 帧率         |                                              |
| SegmentBase    | obj   |            |                                              |
| frameRate      | str   | 帧率         |                                              |
| codecid        | num   | 视频编码格式代码   | [视频编码格式代码](../video/playurl_web.md#视频编码格式代码) |
| baseUrl        | str   | 默认视频流url   |                                              |
| size           | num   | 文件大小       |                                              |
| mime_type      | str   | 格式类型       |                                              |
| width          | num   | 视频宽度       |                                              |
| startWithSAP   | num   | `1`        |                                              |
| id             | num   | 视频清晰度代码    | [视频流清晰度代码列表](#视频流清晰度代码列表)                    |
| height         | num   | 视频高度       |                                              |
| md5            | str   | `空串`       |                                              |

#### `result`对象 -> `dash`对象 -> `dolby`对象

| 字段名   | 类型    | 内容   | 备注  |
|-------|-------|------|-----|
| audio | array | 音轨列表 |     |
| type  | num   | `0`  |     |

#### `result`对象 -> `dash`对象 -> `video`/`audio`数组中的对象 -> `segment_base`对象

| 字段名            | 类型  | 内容  | 备注  |
|----------------|-----|-----|-----|
| initialization | str |     |     |
| index_range    | str |     |     |

#### `result`对象 -> `support_formats`数组中的对象

| 字段名             | 类型    | 内容       | 备注                                               |
|-----------------|-------|----------|--------------------------------------------------|
| display_desc    | str   | 格式描述     |                                                  |
| superscript     | str   |          |                                                  |
| need_login      | bool  | 是否需要登录   |                                                  |
| codecs          | array | 可用编码格式列表 |                                                  |
| format          | str   | 视频格式     |                                                  |
| description     | str   | 格式描述     |                                                  |
| need_vip        | bool  | 是否需要大会员  |                                                  |
| quality         | num   | 视频清晰度代码  | [视频流清晰度代码列表](../video/playurl_web.md#视频流清晰度代码列表) |
| new_description | str   | 格式描述     |                                                  |

## 请求示例

**需要设置Referer为`http(s)://*.bilibili.com`，否则无法获取1080P以上的流信息。**

```shell
curl -L -X GET 'https://api.bilibili.com/pgc/player/web/playurl?cid=7076198&qn=127&fnver=0&fnval=4048' \
-H 'cookie: SESSDATA=xxx' \
-H 'referer: http://www.bilibili.com'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "code": 0,
  "message": "success",
  "result": {
    "accept_format": "hdflv2,flv,flv720,flv480,mp4",
    "code": 0,
    "seek_param": "start",
    "is_preview": 0,
    "fnval": 4048,
    "video_project": true,
    "fnver": 0,
    "type": "DASH",
    "bp": 1,
    "result": "suee",
    "seek_type": "offset",
    "vip_type": 2,
    "from": "local",
    "video_codecid": 7,
    "record_info": {
      "record_icon": "",
      "record": "登记号：10417060172092207"
    },
    "is_drm": false,
    "no_rexcode": 0,
    "format": "hdflv2",
    "support_formats": [
      {
        "display_desc": "4K",
        "superscript": "",
        "need_login": true,
        "codecs": [
          "avc1.640032",
          "hev1.1.6.L153.90"
        ],
        "format": "hdflv2",
        "description": "超清 4K",
        "need_vip": true,
        "quality": 120,
        "new_description": "4K 超清"
      },
      {
        "display_desc": "1080P",
        "superscript": "",
        "need_login": true,
        "codecs": [
          "av01.0.08M.08.0.110.01.01.01.0",
          "avc1.640028",
          "hev1.1.6.L120.90"
        ],
        "format": "flv",
        "description": "高清 1080P",
        "quality": 80,
        "new_description": "1080P 高清"
      },
      {
        "display_desc": "720P",
        "superscript": "",
        "need_login": true,
        "codecs": [
          "av01.0.05M.08.0.110.01.01.01.0",
          "avc1.64001F",
          "hev1.1.6.L120.90"
        ],
        "format": "flv720",
        "description": "高清 720P",
        "quality": 64,
        "new_description": "720P 高清"
      },
      {
        "display_desc": "480P",
        "superscript": "",
        "codecs": [
          "av01.0.04M.08.0.110.01.01.01.0",
          "avc1.64001E",
          "hev1.1.6.L120.90"
        ],
        "format": "flv480",
        "description": "清晰 480P",
        "quality": 32,
        "new_description": "480P 清晰"
      },
      {
        "display_desc": "360P",
        "superscript": "",
        "codecs": [
          "av01.0.01M.08.0.110.01.01.01.0",
          "avc1.64001E",
          "hev1.1.6.L120.90"
        ],
        "format": "mp4",
        "description": "流畅 360P",
        "quality": 16,
        "new_description": "360P 流畅"
      }
    ],
    "message": "",
    "accept_quality": [
      120,
      80,
      64,
      32,
      16
    ],
    "quality": 120,
    "timelength": 1502076,
    "has_paid": false,
    "vip_status": 1,
    "dash": {
      "duration": 1503,
      "minBufferTime": 1.5,
      "min_buffer_time": 1.5,
      "video": [
        {
          "start_with_sap": 1,
          "bandwidth": 5409920,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/98/61/7076198/7076198_sr2-1-100035.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=cosbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=369592605da5162702b5b80cef44a5d0&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=676671&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/98/61/7076198/7076198_sr2-1-100035.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=cosbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=c10fe955b64a89c27c7bef23370518b1&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=676671&logo=40000000"
          ],
          "codecs": "avc1.640032",
          "base_url": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/98/61/7076198/7076198_sr2-1-100035.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=coso1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=21f27b4ab5b94ca20171160576912bff&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=676671&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/98/61/7076198/7076198_sr2-1-100035.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=cosbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=369592605da5162702b5b80cef44a5d0&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=676671&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/98/61/7076198/7076198_sr2-1-100035.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=cosbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=c10fe955b64a89c27c7bef23370518b1&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=676671&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-997",
            "index_range": "998-4629"
          },
          "mimeType": "video/mp4",
          "frame_rate": "23.810",
          "SegmentBase": {
            "Initialization": "0-997",
            "indexRange": "998-4629"
          },
          "frameRate": "23.810",
          "codecid": 7,
          "baseUrl": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/98/61/7076198/7076198_sr2-1-100035.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=coso1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=21f27b4ab5b94ca20171160576912bff&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=676671&logo=80000000",
          "size": 1015684259,
          "mime_type": "video/mp4",
          "width": 2560,
          "startWithSAP": 1,
          "id": 120,
          "height": 1920,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 2467436,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_sr2-1-100036.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=60c8b9de47c1d8dcb469992569ef5b5f&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=308626&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_sr2-1-100036.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=66984aa96448c5568b70fafb2ec04726&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=308626&logo=40000000"
          ],
          "codecs": "hev1.1.6.L153.90",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_sr2-1-100036.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=6e7b689f61d7cc55a0a678a5ae23a6a2&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=308626&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_sr2-1-100036.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=60c8b9de47c1d8dcb469992569ef5b5f&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=308626&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_sr2-1-100036.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=66984aa96448c5568b70fafb2ec04726&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=308626&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-1062",
            "index_range": "1063-4694"
          },
          "mimeType": "video/mp4",
          "frame_rate": "24.390",
          "SegmentBase": {
            "Initialization": "0-1062",
            "indexRange": "1063-4694"
          },
          "frameRate": "24.390",
          "codecid": 12,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_sr2-1-100036.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=6e7b689f61d7cc55a0a678a5ae23a6a2&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=308626&logo=80000000",
          "size": 463248535,
          "mime_type": "video/mp4",
          "width": 2560,
          "startWithSAP": 1,
          "id": 120,
          "height": 1920,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 1290685,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30080.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=122da91b5b49ea4b77419de44ee8f2ae&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=161441&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30080.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=ef0fbca20fa902fa40836c92851c3304&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=161441&logo=40000000"
          ],
          "codecs": "avc1.640028",
          "base_url": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30080.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=upos&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=476621dc7e3fcbf713b9731da6e1f45e&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=161441&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30080.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=122da91b5b49ea4b77419de44ee8f2ae&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=161441&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30080.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=ef0fbca20fa902fa40836c92851c3304&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=161441&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-976",
            "index_range": "977-4608"
          },
          "mimeType": "video/mp4",
          "frame_rate": "24.390",
          "SegmentBase": {
            "Initialization": "0-976",
            "indexRange": "977-4608"
          },
          "frameRate": "24.390",
          "codecid": 7,
          "baseUrl": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30080.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=upos&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=476621dc7e3fcbf713b9731da6e1f45e&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=161441&logo=80000000",
          "size": 242323555,
          "mime_type": "video/mp4",
          "width": 1280,
          "startWithSAP": 1,
          "id": 80,
          "height": 960,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 461015,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30077.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=10bc8f1c0328ffaf7903aad8e9b69bce&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=57662&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30077.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=3ab416ae86f6f921e63ab591264fdd2a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=57662&logo=40000000"
          ],
          "codecs": "hev1.1.6.L120.90",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30077.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=b4a15393f271b0a0f30f3f74f19f73b8&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=57662&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30077.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=10bc8f1c0328ffaf7903aad8e9b69bce&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=57662&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30077.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=3ab416ae86f6f921e63ab591264fdd2a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=57662&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-1042",
            "index_range": "1043-4674"
          },
          "mimeType": "video/mp4",
          "frame_rate": "23.810",
          "SegmentBase": {
            "Initialization": "0-1042",
            "indexRange": "1043-4674"
          },
          "frameRate": "23.810",
          "codecid": 12,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30077.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=b4a15393f271b0a0f30f3f74f19f73b8&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=57662&logo=80000000",
          "size": 86550858,
          "mime_type": "video/mp4",
          "width": 1280,
          "startWithSAP": 1,
          "id": 80,
          "height": 960,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 583415,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100026.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=d0565811b08431a7e924f1f81a2c777a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=73186&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100026.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=de4dfa68e30da65791ce9330b58ac027&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=73186&logo=40000000"
          ],
          "codecs": "av01.0.08M.08.0.110.01.01.01.0",
          "base_url": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100026.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=upos&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=75236fb8597e1752aba0ad749e41f5c1&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=73186&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100026.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=d0565811b08431a7e924f1f81a2c777a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=73186&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100026.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=de4dfa68e30da65791ce9330b58ac027&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=73186&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-923",
            "index_range": "1300-4943"
          },
          "mimeType": "video/mp4",
          "frame_rate": "23.976",
          "SegmentBase": {
            "Initialization": "0-923",
            "indexRange": "1300-4943"
          },
          "frameRate": "23.976",
          "codecid": 13,
          "baseUrl": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100026.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=upos&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=75236fb8597e1752aba0ad749e41f5c1&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=73186&logo=80000000",
          "size": 109853118,
          "mime_type": "video/mp4",
          "width": 1280,
          "startWithSAP": 1,
          "id": 80,
          "height": 960,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 1290767,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30064.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=5bf32bfac108bee32d1dd3caf2e76eb6&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=161451&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30064.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=438df44ed33294405346a8d70350fd30&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=161451&logo=40000000"
          ],
          "codecs": "avc1.64001F",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30064.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=a7c023c2d8e9bf2ede68602cd42e7935&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=161451&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30064.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=5bf32bfac108bee32d1dd3caf2e76eb6&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=161451&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30064.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=438df44ed33294405346a8d70350fd30&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=161451&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-976",
            "index_range": "977-4608"
          },
          "mimeType": "video/mp4",
          "frame_rate": "24.390",
          "SegmentBase": {
            "Initialization": "0-976",
            "indexRange": "977-4608"
          },
          "frameRate": "24.390",
          "codecid": 7,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30064.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=a7c023c2d8e9bf2ede68602cd42e7935&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=161451&logo=80000000",
          "size": 242339014,
          "mime_type": "video/mp4",
          "width": 960,
          "startWithSAP": 1,
          "id": 64,
          "height": 720,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 255694,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30066.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=5fbae38ceb616a7ed088a4ce089ff068&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=31981&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30066.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=7acaf72776e26f5a7d8ddd0dfe3ed4f8&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=31981&logo=40000000"
          ],
          "codecs": "hev1.1.6.L120.90",
          "base_url": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30066.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=upos&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=268574bc3ab1ba3f39314a8bf2c8cbeb&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=31981&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30066.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=5fbae38ceb616a7ed088a4ce089ff068&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=31981&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30066.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=7acaf72776e26f5a7d8ddd0dfe3ed4f8&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=31981&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-1040",
            "index_range": "1041-4672"
          },
          "mimeType": "video/mp4",
          "frame_rate": "23.810",
          "SegmentBase": {
            "Initialization": "0-1040",
            "indexRange": "1041-4672"
          },
          "frameRate": "23.810",
          "codecid": 12,
          "baseUrl": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30066.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=upos&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=268574bc3ab1ba3f39314a8bf2c8cbeb&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=31981&logo=80000000",
          "size": 48004012,
          "mime_type": "video/mp4",
          "width": 960,
          "startWithSAP": 1,
          "id": 64,
          "height": 720,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 566485,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100024.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=7fda2b1acd1669153214a80591a0b50a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=71069&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100024.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=79baf3eb2c24205ef0044e673ae763ea&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=71069&logo=40000000"
          ],
          "codecs": "av01.0.05M.08.0.110.01.01.01.0",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100024.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=494b8539f87f4768872eb0226c833094&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=71069&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100024.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=7fda2b1acd1669153214a80591a0b50a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=71069&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100024.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=79baf3eb2c24205ef0044e673ae763ea&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=71069&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-923",
            "index_range": "1300-4943"
          },
          "mimeType": "video/mp4",
          "frame_rate": "23.976",
          "SegmentBase": {
            "Initialization": "0-923",
            "indexRange": "1300-4943"
          },
          "frameRate": "23.976",
          "codecid": 13,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100024.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=494b8539f87f4768872eb0226c833094&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=71069&logo=80000000",
          "size": 106674619,
          "mime_type": "video/mp4",
          "width": 960,
          "startWithSAP": 1,
          "id": 64,
          "height": 720,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 509089,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=991b963fff2b9e4679cac3e39f6f060d&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=63677&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=6c0b84d40ab4f4dfcf790e28ea2cbef8&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=63677&logo=40000000"
          ],
          "codecs": "avc1.64001E",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=9f372ca230452e3ad598e9c40c49b0d0&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=63677&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=991b963fff2b9e4679cac3e39f6f060d&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=63677&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=6c0b84d40ab4f4dfcf790e28ea2cbef8&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=63677&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-976",
            "index_range": "977-4608"
          },
          "mimeType": "video/mp4",
          "frame_rate": "24.390",
          "SegmentBase": {
            "Initialization": "0-976",
            "indexRange": "977-4608"
          },
          "frameRate": "24.390",
          "codecid": 7,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=9f372ca230452e3ad598e9c40c49b0d0&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=63677&logo=80000000",
          "size": 95580487,
          "mime_type": "video/mp4",
          "width": 640,
          "startWithSAP": 1,
          "id": 32,
          "height": 480,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 176786,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30033.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=59fbd5a6bb5b9b6f8d711f0210ac7035&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=22111&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30033.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=312dfc09630fd61274c48efced538eef&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=22111&logo=40000000"
          ],
          "codecs": "hev1.1.6.L120.90",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30033.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=bdd4714c71d95409f9ccb6d2d0596acd&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=22111&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30033.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=59fbd5a6bb5b9b6f8d711f0210ac7035&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=22111&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30033.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=312dfc09630fd61274c48efced538eef&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=22111&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-1040",
            "index_range": "1041-4672"
          },
          "mimeType": "video/mp4",
          "frame_rate": "23.810",
          "SegmentBase": {
            "Initialization": "0-1040",
            "indexRange": "1041-4672"
          },
          "frameRate": "23.810",
          "codecid": 12,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30033.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=bdd4714c71d95409f9ccb6d2d0596acd&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=22111&logo=80000000",
          "size": 33189900,
          "mime_type": "video/mp4",
          "width": 640,
          "startWithSAP": 1,
          "id": 32,
          "height": 480,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 235289,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100023.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=cosbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=19bf8c580742b58ec1fc9952a0f461df&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=29644&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100023.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=cosbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=0a1dd79f61de9f2aa5798ce2946766ca&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=29644&logo=40000000"
          ],
          "codecs": "av01.0.04M.08.0.110.01.01.01.0",
          "base_url": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100023.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=coso1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=526099dc6a88130d8bd6c869a6014290&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=29644&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100023.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=cosbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=19bf8c580742b58ec1fc9952a0f461df&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=29644&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100023.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=cosbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=0a1dd79f61de9f2aa5798ce2946766ca&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=29644&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-923",
            "index_range": "1300-4943"
          },
          "mimeType": "video/mp4",
          "frame_rate": "23.976",
          "SegmentBase": {
            "Initialization": "0-923",
            "indexRange": "1300-4943"
          },
          "frameRate": "23.976",
          "codecid": 13,
          "baseUrl": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100023.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=coso1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=526099dc6a88130d8bd6c869a6014290&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=29644&logo=80000000",
          "size": 44495934,
          "mime_type": "video/mp4",
          "width": 640,
          "startWithSAP": 1,
          "id": 32,
          "height": 480,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 307348,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30011.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=ea70b5145663f3f5c3c4959d83cc2866&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=38442&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30011.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=7f24403a9a348eaa877239f32978a057&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=38442&logo=40000000"
          ],
          "codecs": "hev1.1.6.L120.90",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30011.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=a2676d9e8a2f50ee0e489186674b0de5&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=38442&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30011.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=ea70b5145663f3f5c3c4959d83cc2866&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=38442&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30011.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=7f24403a9a348eaa877239f32978a057&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=38442&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-1041",
            "index_range": "1042-4673"
          },
          "mimeType": "video/mp4",
          "frame_rate": "23.810",
          "SegmentBase": {
            "Initialization": "0-1041",
            "indexRange": "1042-4673"
          },
          "frameRate": "23.810",
          "codecid": 12,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8x3-1-30011.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=a2676d9e8a2f50ee0e489186674b0de5&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=38442&logo=80000000",
          "size": 57701491,
          "mime_type": "video/mp4",
          "width": 480,
          "startWithSAP": 1,
          "id": 16,
          "height": 360,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 346158,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30016.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=a9531483588989718955542973a15583&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=43298&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30016.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=66bf25d1e04870526eeeab43ba636728&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=43298&logo=40000000"
          ],
          "codecs": "avc1.64001E",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30016.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=2d2312854193cde08f090fbeab7ca466&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=43298&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30016.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=a9531483588989718955542973a15583&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=43298&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30016.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=66bf25d1e04870526eeeab43ba636728&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=43298&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-985",
            "index_range": "986-4617"
          },
          "mimeType": "video/mp4",
          "frame_rate": "24.390",
          "SegmentBase": {
            "Initialization": "0-985",
            "indexRange": "986-4617"
          },
          "frameRate": "24.390",
          "codecid": 7,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30016.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=2d2312854193cde08f090fbeab7ca466&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=43298&logo=80000000",
          "size": 64990607,
          "mime_type": "video/mp4",
          "width": 480,
          "startWithSAP": 1,
          "id": 16,
          "height": 360,
          "md5": ""
        },
        {
          "start_with_sap": 1,
          "bandwidth": 202806,
          "sar": "1:1",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100022.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=79b71d7139cbff309ed413ffeeda420c&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=25581&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100022.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=f2f688a86cf5348c5bf9951b85ba4dca&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=25581&logo=40000000"
          ],
          "codecs": "av01.0.01M.08.0.110.01.01.01.0",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100022.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=7b7e975f87e3bd243b0b8cbfde40a049&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=25581&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100022.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=79b71d7139cbff309ed413ffeeda420c&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=25581&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100022.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=f2f688a86cf5348c5bf9951b85ba4dca&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=25581&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-923",
            "index_range": "1300-4943"
          },
          "mimeType": "video/mp4",
          "frame_rate": "23.976",
          "SegmentBase": {
            "Initialization": "0-923",
            "indexRange": "1300-4943"
          },
          "frameRate": "23.976",
          "codecid": 13,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-100022.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=7b7e975f87e3bd243b0b8cbfde40a049&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=25581&logo=80000000",
          "size": 38397629,
          "mime_type": "video/mp4",
          "width": 480,
          "startWithSAP": 1,
          "id": 16,
          "height": 360,
          "md5": ""
        }
      ],
      "audio": [
        {
          "start_with_sap": 0,
          "bandwidth": 193686,
          "sar": "",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30280.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=c58656f9ef4ac1fc0a5cb06ed0ec7040&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=24212&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30280.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=f64b1560f0ac549c1c803c29749bfa01&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=24212&logo=40000000"
          ],
          "codecs": "mp4a.40.2",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30280.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=04f418033865cb9fa3c5b07b1aa16fcb&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=24212&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30280.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=c58656f9ef4ac1fc0a5cb06ed0ec7040&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=24212&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30280.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=f64b1560f0ac549c1c803c29749bfa01&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=24212&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-907",
            "index_range": "908-4551"
          },
          "mimeType": "audio/mp4",
          "frame_rate": "",
          "SegmentBase": {
            "Initialization": "0-907",
            "indexRange": "908-4551"
          },
          "frameRate": "",
          "codecid": 0,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30280.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=04f418033865cb9fa3c5b07b1aa16fcb&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=24212&logo=80000000",
          "size": 36366489,
          "mime_type": "audio/mp4",
          "width": 0,
          "startWithSAP": 0,
          "id": 30280,
          "height": 0,
          "md5": ""
        },
        {
          "start_with_sap": 0,
          "bandwidth": 67269,
          "sar": "",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30216.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=692d72d0534fa8bce6da0acb2877247b&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=8409&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30216.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=6e500a64eb263f1b9e2816a2a5412ad3&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=8409&logo=40000000"
          ],
          "codecs": "mp4a.40.2",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30216.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=4ba8167e88fdd0a48d75f570b67bc530&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=8409&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30216.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=692d72d0534fa8bce6da0acb2877247b&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=8409&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30216.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwbbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=6e500a64eb263f1b9e2816a2a5412ad3&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=8409&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-941",
            "index_range": "942-4585"
          },
          "mimeType": "audio/mp4",
          "frame_rate": "",
          "SegmentBase": {
            "Initialization": "0-941",
            "indexRange": "942-4585"
          },
          "frameRate": "",
          "codecid": 0,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30216.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=hwo1bv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=4ba8167e88fdd0a48d75f570b67bc530&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=8409&logo=80000000",
          "size": 12630407,
          "mime_type": "audio/mp4",
          "width": 0,
          "startWithSAP": 0,
          "id": 30216,
          "height": 0,
          "md5": ""
        },
        {
          "start_with_sap": 0,
          "bandwidth": 132759,
          "sar": "",
          "backupUrl": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30232.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=cb414dca94b21fa7e958d7aa9fba201b&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=16595&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30232.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=088625e102a6b40bff1aeb0e955fac52&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=16595&logo=40000000"
          ],
          "codecs": "mp4a.40.2",
          "base_url": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30232.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=upos&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=5430aa82d503071ea14d8732d77c6b66&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=16595&logo=80000000",
          "backup_url": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30232.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=cb414dca94b21fa7e958d7aa9fba201b&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=1&bw=16595&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30232.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=alibbv&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=088625e102a6b40bff1aeb0e955fac52&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=1&bw=16595&logo=40000000"
          ],
          "segment_base": {
            "initialization": "0-907",
            "index_range": "908-4551"
          },
          "mimeType": "audio/mp4",
          "frame_rate": "",
          "SegmentBase": {
            "Initialization": "0-907",
            "indexRange": "908-4551"
          },
          "frameRate": "",
          "codecid": 0,
          "baseUrl": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/98/61/7076198/7076198_da8-1-30232.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664790596&gen=playurlv2&os=upos&oi=663750228&trid=72394dfc119f42d2a21402878335b073p&mid=*******&platform=pc&upsig=5430aa82d503071ea14d8732d77c6b66&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=1&bw=16595&logo=80000000",
          "size": 24926810,
          "mime_type": "audio/mp4",
          "width": 0,
          "startWithSAP": 0,
          "id": 30232,
          "height": 0,
          "md5": ""
        }
      ],
      "dolby": {
        "audio": [],
        "type": 0
      }
    },
    "clip_info_list": [],
    "accept_description": [
      "超清 4K",
      "高清 1080P",
      "高清 720P",
      "清晰 480P",
      "流畅 360P"
    ],
    "status": 2
  }
}
```

</details>