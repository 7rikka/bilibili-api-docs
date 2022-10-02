# 视频流清晰度代码列表

| 代码  | 说明          | AVC编码 | HEVC编码 | AV1编码 | format代码   | 格式                 | 备注  |
|-----|-------------|-------|--------|-------|------------|--------------------|-----|
| 6   | 240P 极速     | √     |        |       | mp4        | `MP4`              |     |
| 16  | 360P 流畅     | √     | √      | √     | mp4        | `DASH` `FLV` `MP4` |     |
| 32  | 480P 清晰     | √     | √      | √     | flv480     | `DASH` `FLV`       |     |
| 48  | 720P 高清     | √     |        |       | hdmp4      | `MP4`              |     |
| 64  | 720P 高清     | √     | √      | √     | flv720     | `DASH` `FLV`       |     |
| 74  | 720P60 高帧率  | √     | √      |       | flv720_p60 | `DASH` `FLV`       |     |
| 80  | 1080P 高清    | √     | √      | √     | flv        | `DASH` `FLV`       |     |
| 112 | 1080P 高码率   | √     | √      | √     | hdflv2     | `DASH` `FLV`       |     |
| 116 | 1080P60 高帧率 | √     | √      | √     | flv_p60    | `DASH` `FLV`       |     |
| 120 | 4K 超清       | √     | √      | √     | hdflv2     | `DASH` `FLV`       |     |
| 125 | HDR 真彩      |       | √      |       | hdflv2     | `DASH`             |     |
| 126 | 杜比视界        |       | √      |       | hdflv2     | `DASH`             |     |
| 127 | 8K 超高清      | √     | √      | √     | hdflv2     | `DASH`             |     |

# 关于无损音轨

获取`DASH`格式，可在`flac`字段获取无损音轨

示例：[BV1hG41147Wx](https://www.bilibili.com/video/BV1hG41147Wx)

# 视频流格式fnval代码列表

该代码为二进制属性位，如需组合功能需要使用`OR`运算结合一下数值

| 值    | 含义         | 备注                                         |
|------|------------|--------------------------------------------|
| 0    | 获取`FLV`格式  | 只有`AVC`编码，文件后缀为`flv`，音视频`不分离`              |
| 1    | 获取`MP4`格式  | 只有`AVC`编码，文件后缀为`mp4`，音视频`不分离`              |
| 16   | 获取`DASH`格式 | 有`AVC`、`HEVC`和`AV1`三种编码，文件后缀为`m4s`，音视频`分离` |
| 64   | 获取`真彩 HDR` | 配合`qn >= 125`获取真彩HDR片源                     |
| 128  | 获取`4K 超清`  | 配合`qn >= 120`获取4K超清片源                      |
| 256  | 获取`杜比全景声`  | 必须为`DASH`格式                                |
| 512  | 获取`杜比视界`   | 必须为`DASH`格式                                |
| 1024 | 获取`8K 超高清` | 必须为`DASH`格式，需要`qn=127`                     |
| 2048 | 获取`AV1`编码  | 必须为`DASH`格式                                |

# 注意事项

1.有关视频格式

`FLV`、`MP4`和`DASH`任选其一，默认是`FLV`

2.有关杜比视界

`杜比视界`和`杜比全景声`是分开的，前者是视频流，后者是音频流，可以只获取视频流或者音频流

3.有关4K

获取4K清晰度可以选`(fnval & 128 = 128) & (qn >= 120)` 或者 `fourk = 1` 两种条件任选其一，都可以获取到4K清晰度

# 常用fnval

`FLV`格式：0 + 64 + 128 + 256 + 512 + 1024 + 2048 = `4032`

`MP4`格式：1 + 64 + 128 + 256 + 512 + 1024 + 2048 = `4033`

`DASH`格式：16 + 64 + 128 + 256 + 512 + 1024 + 2048 = `4048`

# 视频编码格式代码

| 值   | 含义     | 备注  |
|-----|--------|-----|
| 7   | AVC编码  |     |
| 12  | HEVC编码 |     |
| 13  | AV1编码  |     |

# 音频流音质代码

| 值     | 含义       |
|-------|----------|
| 30216 | 64K      |
| 30232 | 132K     |
| 30280 | 192K以上   |
| 30250 | 杜比全景声    |
| 30251 | Hi-Res无损 |

# 获取视频播放流

> https://api.bilibili.com/x/player/playurl

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名     | 类型  | 必填  | 内容        | 备注                                       |
|---------|-----|-----|-----------|------------------------------------------|
| avid    | num | √   | 视频av号     | av号，bv号二选一                               |
| bvid    | str | √   | 视频bv号     | av号，bv号二选一                               |
| cid     | num | √   | 视频的cid    |                                          |
| qn      | num |     | 视频最高清晰度代码 | 默认64(720p)<br/>[视频流清晰度代码列表](#视频流清晰度代码列表) |
| fnver   | num |     | 固定值：`0`   |                                          |
| fnval   | num |     | 视频格式参数    |                                          |
| fourk   | num |     | 是否获取4K清晰度 |                                          |
| session | str |     |           |                                          |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名                | 类型    | 内容                                    | 备注                 |
|--------------------|-------|---------------------------------------|--------------------|
| from               | str   | `local`                               |                    |
| result             | str   | `suee`                                |                    |
| message            | str   | `空串`                                  |                    |
| quality            | num   | 前端播放器显示最高的视频清晰度代码                     |                    |
| format             | str   | 前端播放器显示最高的视频格式                        |                    |
| timelength         | num   | 视频长度                                  | 单位：毫秒              |
| accept_format      | str   | 视频支持的格式列表                             | 取决于`fnval`和`fourk` |
| accept_description | array | 视频支持的分辨率列表                            | 取决于`fnval`和`fourk` |
| accept_quality     | array | 视频支持的分辨率代码列表                          | 取决于`fnval`和`fourk` |
| video_codecid      | num   | 默认选择视频流的编码id                          |                    |
| seek_param         | str   | 固定值：`start`                           |                    |
| seek_type          | str   | offset：`DASH`、`FLV`<br/> second：`mp4` |                    |
| durl               | obj   | `FLV`或`MP4`格式返回的视频信息                  |                    |
| dash               | obj   | `DASH`格式返回的视频流和音频流信息                  |                    |
| support_formats    | array | 支持格式的详细信息                             |                    |
| high_format        |       | `null`                                |                    |
| last_play_time     | num   | 上次播放进度                                | 单位：毫秒              |
| last_play_cid      | num   | 上次播放分p的cid                            |                    |

#### `data`对象 -> `dash`对象

| 字段名             | 类型    | 内容        | 备注   |
|-----------------|-------|-----------|------|
| duration        | num   | 视频长度      | 单位：秒 |
| minBufferTime   | num   | `1.5`     |      |
| min_buffer_time | num   | `1.5`     |      |
| video           | array | 视频流信息     |      |
| audio           | array | 音频流信息     |      |
| dolby           | null  | 杜比全景声音轨信息 |      |
| flac            | null  | 无损音轨信息    |      |

##### `data`对象 -> `dash`对象 -> `video`数组中的对象

| 字段名            | 类型    | 内容       | 备注                        |
|----------------|-------|----------|---------------------------|
| id             | num   | 视频清晰度代码  | [视频流清晰度代码列表](#视频流清晰度代码列表) |
| baseUrl        | str   | 默认视频流url |                           |
| base_url       | str   | 默认视频流url |                           |
| backupUrl      | array | 备用视频流url |                           |
| backup_url     | array | 备用视频流url |                           |
| bandwidth      | num   | 所需最低带宽   |                           |
| mimeType       | str   | 格式类型     |                           |
| mime_type      | str   | 格式类型     |                           |
| codecs         | str   | 编码类型     |                           |
| width          | num   | 视频高度     |                           |
| height         | num   | 视频宽度     |                           |
| frameRate      | str   | 帧率       |                           |
| frame_rate     | str   | 帧率       |                           |
| sar            | str   | `1:1`    |                           |
| startWithSap   | num   | `1`      |                           |
| start_with_sap | num   | `1`      |                           |
| SegmentBase    | obj   |          |                           |
| segment_base   | obj   |          |                           |
| codecid        | num   | 视频编码格式代码 | [视频编码格式代码](#视频编码格式代码)     |

##### `data`对象 -> `dash`对象 -> `audio`数组中的对象

| 字段名            | 类型    | 内容         | 备注                  |
|----------------|-------|------------|---------------------|
| id             | num   | 音频音质代码     | [音频流音质代码](#音频流音质代码) |
| baseUrl        | str   | 默认音频流url   |                     |
| base_url       | str   | 默认音频流url   |                     |
| backupUrl      | array | 备用音频流url列表 |                     |
| backup_url     | array | 备用音频流url列表 |                     |
| bandwidth      | num   | 所需最低带宽     |                     |
| mimeType       | str   | 格式类型       |                     |
| mime_type      | str   | 格式类型       |                     |
| codecs         | str   | 编码类型       |                     |
| width          | num   | `0`        |                     |
| height         | num   | `0`        |                     |
| frameRate      | str   | `空串`       |                     |
| frame_rate     | str   | `空串`       |                     |
| sar            | str   | `空串`       |                     |
| startWithSap   | num   | `0`        |                     |
| start_with_sap | num   | `0`        |                     |
| SegmentBase    | obj   |            |                     |
| segment_base   | obj   |            |                     |
| codecid        | num   | `0`        |                     |

##### `data`对象 -> `dash`对象 -> `video`/`audio`数组中的对象 -> `segment_base`对象

| 字段名            | 类型  | 内容  | 备注  |
|----------------|-----|-----|-----|
| initialization | str |     |     |
| index_range    | str |     |     |

##### `data`对象 -> `dash`对象 -> `dolby`对象

| 字段    | 类型    | 内容      | 备注  |
|-------|-------|---------|-----|
| type  | num   | 固定值：`2` |     |
| audio | array | 杜比音轨列表  |     |

##### `data`对象 -> `dash`对象 -> `dolby`对象 -> `audio`数组中的对象

| 字段           | 类型    | 内容                | 备注    |
|--------------|-------|-------------------|-------|
| id           | num   | 音轨代码，固定为：`30250`  |       |
| base_url     | str   | 音频流url            |       |
| backup_url   | array | 音频流备用url列表        |       |
| bandwidth    | num   | 音频所需最低带宽          |       |
| mime_type    | num   | 音频格式类型            |       |
| codecs       | num   | 音频编码信息，固定为：`ec-3` |       |
| segment_base | obj   |                   |       |
| size         | num   | 音轨文件大小            | 单位：字节 |

##### `data`对象 -> `dash`对象 -> `flac`对象

| 字段      | 类型   | 内容                     | 备注  |
|---------|------|------------------------|-----|
| display | bool | 是否在播放器显示切换Hi-Res无损音轨按钮 |     |
| audio   | obj  | 音频流信息                  |     |

#### `data`对象 -> `support_formats`数组中的对象

| 字段名             | 类型    | 内容       | 备注                        |
|-----------------|-------|----------|---------------------------|
| quality         | num   | 视频清晰度代码  | [视频流清晰度代码列表](#视频流清晰度代码列表) |
| format          | str   | 视频格式     |                           |
| new_description | str   | 格式描述     |                           |
| display_desc    | str   | 格式描述     |                           |
| superscript     | str   |          |                           |
| codecs          | array | 可用编码格式列表 |                           |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/player/playurl?avid=934637444&cid=455439756&qn=127&fnver=0&fnval=4048' \
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
  "data": {
    "from": "local",
    "result": "suee",
    "message": "",
    "quality": 127,
    "format": "hdflv2",
    "timelength": 192810,
    "accept_format": "hdflv2,hdflv2,hdflv2,flv,flv720,flv480,mp4",
    "accept_description": [
      "超高清 8K",
      "超清 4K",
      "高清 1080P+",
      "高清 1080P",
      "高清 720P",
      "清晰 480P",
      "流畅 360P"
    ],
    "accept_quality": [
      127,
      120,
      112,
      80,
      64,
      32,
      16
    ],
    "video_codecid": 12,
    "seek_param": "start",
    "seek_type": "offset",
    "dash": {
      "duration": 193,
      "minBufferTime": 1.5,
      "min_buffer_time": 1.5,
      "video": [
        {
          "id": 127,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-30127.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=8b5697f6c4cc3fe6efbad175a42486b0&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=2545181&logo=80000000",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-30127.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=8b5697f6c4cc3fe6efbad175a42486b0&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=2545181&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-30127.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=2da94cec73efd282f4c429e8b9152b30&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=2545181&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-30127.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=f7306f71be88c057d461e3fbec13f9e8&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=2545181&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-30127.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=2da94cec73efd282f4c429e8b9152b30&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=2545181&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-30127.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=f7306f71be88c057d461e3fbec13f9e8&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=2545181&logo=40000000"
          ],
          "bandwidth": 20281170,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "hev1.1.6.L180.90",
          "width": 8192,
          "height": 4320,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1:1",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-1166",
            "indexRange": "1167-1666"
          },
          "segment_base": {
            "initialization": "0-1166",
            "index_range": "1167-1666"
          },
          "codecid": 12
        },
        {
          "id": 127,
          "baseUrl": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=coso1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=12ef59f4ee9bf526ac570a902e077c6e&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=1207778&logo=80000000",
          "base_url": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=coso1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=12ef59f4ee9bf526ac570a902e077c6e&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=1207778&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=9d7ab6b2b0361bca57a99937d98e11af&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=1207778&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=9a524eefa7734091f2227a8092c28f2d&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=1207778&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=9d7ab6b2b0361bca57a99937d98e11af&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=1207778&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=9a524eefa7734091f2227a8092c28f2d&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=1207778&logo=40000000"
          ],
          "bandwidth": 9623112,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "av01.0.16M.08.0.110.01.01.01.0",
          "width": 8192,
          "height": 4320,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1:1",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-940",
            "indexRange": "993-1492"
          },
          "segment_base": {
            "initialization": "0-940",
            "index_range": "993-1492"
          },
          "codecid": 13
        },
        {
          "id": 120,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30120.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=0b97d90a02e30eefdaaab4097b6638fa&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=1376427&logo=80000000",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30120.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=0b97d90a02e30eefdaaab4097b6638fa&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=1376427&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30120.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=3071ae3ce17ccc4d625a3a17b325db79&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=1376427&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30120.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=0c3081cdca616bf95c288bb014ba10eb&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=1376427&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30120.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=3071ae3ce17ccc4d625a3a17b325db79&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=1376427&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30120.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=0c3081cdca616bf95c288bb014ba10eb&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=1376427&logo=40000000"
          ],
          "bandwidth": 10968001,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "avc1.640033",
          "width": 4096,
          "height": 2160,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1:1",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-995",
            "indexRange": "996-1495"
          },
          "segment_base": {
            "initialization": "0-995",
            "index_range": "996-1495"
          },
          "codecid": 7
        },
        {
          "id": 120,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30121.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=f9cdf43dc14f805d93c30be0e91ef755&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=613771&logo=80000000",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30121.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=f9cdf43dc14f805d93c30be0e91ef755&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=613771&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30121.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=76749cbd26df1be7d95a1a3760974258&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=613771&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30121.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=b0258a3c9f1c0f3f556a520cd9375ad2&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=613771&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30121.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=76749cbd26df1be7d95a1a3760974258&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=613771&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30121.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=b0258a3c9f1c0f3f556a520cd9375ad2&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=613771&logo=40000000"
          ],
          "bandwidth": 4890810,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "hev1.1.6.L153.90",
          "width": 4096,
          "height": 2160,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1:1",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-1159",
            "indexRange": "1160-1659"
          },
          "segment_base": {
            "initialization": "0-1159",
            "index_range": "1160-1659"
          },
          "codecid": 12
        },
        {
          "id": 120,
          "baseUrl": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100029.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=upos&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=d0d093125f0d5c6fe06491b5972ac224&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=641785&logo=80000000",
          "base_url": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100029.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=upos&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=d0d093125f0d5c6fe06491b5972ac224&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=641785&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100029.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=fa3d014bbf656b7acf251519685d76ff&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=641785&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100029.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=461ca53bc1ca899550954f1b2cdbeb95&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=641785&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100029.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=fa3d014bbf656b7acf251519685d76ff&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=641785&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100029.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=461ca53bc1ca899550954f1b2cdbeb95&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=641785&logo=40000000"
          ],
          "bandwidth": 5113022,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "av01.0.12M.08.0.110.01.01.01.0",
          "width": 4096,
          "height": 2160,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1:1",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-940",
            "indexRange": "993-1492"
          },
          "segment_base": {
            "initialization": "0-940",
            "index_range": "993-1492"
          },
          "codecid": 13
        },
        {
          "id": 112,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30112.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=8a0411077b0e2fe601198cdf450d42e1&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=608670&logo=80000000",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30112.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=8a0411077b0e2fe601198cdf450d42e1&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=608670&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30112.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=6fb02407683067871b45fedd328ff32b&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=608670&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30112.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=e4cbad904d283e08c192e0a4266af31b&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=608670&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30112.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=6fb02407683067871b45fedd328ff32b&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=608670&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30112.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=e4cbad904d283e08c192e0a4266af31b&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=608670&logo=40000000"
          ],
          "bandwidth": 4850164,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "avc1.640032",
          "width": 2048,
          "height": 1080,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1:1",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-996",
            "indexRange": "997-1496"
          },
          "segment_base": {
            "initialization": "0-996",
            "index_range": "997-1496"
          },
          "codecid": 7
        },
        {
          "id": 112,
          "baseUrl": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30102.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=coso1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=0c6e015549d1decfddabf4df3313086f&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=175660&logo=80000000",
          "base_url": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30102.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=coso1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=0c6e015549d1decfddabf4df3313086f&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=175660&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30102.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=0964d4ceb0850340d2da39dafcd12b5f&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=175660&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30102.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=105e8350945b6a33c335a5e07b1b1365&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=175660&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30102.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=0964d4ceb0850340d2da39dafcd12b5f&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=175660&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30102.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=105e8350945b6a33c335a5e07b1b1365&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=175660&logo=40000000"
          ],
          "bandwidth": 1399742,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "hev1.1.6.L150.90",
          "width": 2048,
          "height": 1080,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1:1",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-1158",
            "indexRange": "1159-1658"
          },
          "segment_base": {
            "initialization": "0-1158",
            "index_range": "1159-1658"
          },
          "codecid": 12
        },
        {
          "id": 112,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100027.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=8b01d1230b07e69a68b431fd050b5c60&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=182183&logo=80000000",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100027.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=8b01d1230b07e69a68b431fd050b5c60&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=182183&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100027.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=b0707c369dda2f4ba57e9ada7b9d9fd4&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=182183&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100027.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=f6d298601df9c8154e094e943d62c6d1&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=182183&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100027.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=b0707c369dda2f4ba57e9ada7b9d9fd4&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=182183&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100027.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=f6d298601df9c8154e094e943d62c6d1&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=182183&logo=40000000"
          ],
          "bandwidth": 1450700,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "av01.0.08M.08.0.110.01.01.01.0",
          "width": 2048,
          "height": 1080,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1:1",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-939",
            "indexRange": "992-1491"
          },
          "segment_base": {
            "initialization": "0-939",
            "index_range": "992-1491"
          },
          "codecid": 13
        },
        {
          "id": 80,
          "baseUrl": "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30080.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=0afeb86fec93002cc28942a7e160fc15&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=208792&logo=80000000",
          "base_url": "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30080.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=0afeb86fec93002cc28942a7e160fc15&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=208792&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30080.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=0afeb86fec93002cc28942a7e160fc15&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=208792&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30080.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=79da9193759f91350e6285a91449a4f6&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=208792&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30080.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=0afeb86fec93002cc28942a7e160fc15&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=208792&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30080.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=79da9193759f91350e6285a91449a4f6&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=208792&logo=40000000"
          ],
          "bandwidth": 1663753,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "avc1.640032",
          "width": 2048,
          "height": 1080,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1:1",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-996",
            "indexRange": "997-1496"
          },
          "segment_base": {
            "initialization": "0-996",
            "index_range": "997-1496"
          },
          "codecid": 7
        },
        {
          "id": 80,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30077.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=1fa04289ab0b1a00d19f53f5ea8c7324&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=113154&logo=80000000",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30077.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=1fa04289ab0b1a00d19f53f5ea8c7324&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=113154&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30077.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=91221d9d33d77667a898698a493fed4a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=113154&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30077.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=323fc495a45e1aa0a4b4b7c99ca4536a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=113154&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30077.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=91221d9d33d77667a898698a493fed4a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=113154&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30077.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=323fc495a45e1aa0a4b4b7c99ca4536a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=113154&logo=40000000"
          ],
          "bandwidth": 901664,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "hev1.1.6.L150.90",
          "width": 2048,
          "height": 1080,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1:1",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-1158",
            "indexRange": "1159-1658"
          },
          "segment_base": {
            "initialization": "0-1158",
            "index_range": "1159-1658"
          },
          "codecid": 12
        },
        {
          "id": 80,
          "baseUrl": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100026.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=coso1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=9938eedb4ed7940f88d24352cb72d78e&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=108250&logo=80000000",
          "base_url": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100026.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=coso1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=9938eedb4ed7940f88d24352cb72d78e&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=108250&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100026.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=22a071ff34f0fe2021745d1e672ebfb2&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=108250&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100026.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=d0da489e1908e065e8b7024b330137dc&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=108250&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100026.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=22a071ff34f0fe2021745d1e672ebfb2&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=108250&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100026.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=d0da489e1908e065e8b7024b330137dc&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=108250&logo=40000000"
          ],
          "bandwidth": 861574,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "av01.0.08M.08.0.110.01.01.01.0",
          "width": 2048,
          "height": 1080,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1:1",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-939",
            "indexRange": "992-1491"
          },
          "segment_base": {
            "initialization": "0-939",
            "index_range": "992-1491"
          },
          "codecid": 13
        },
        {
          "id": 64,
          "baseUrl": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30064.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=coso1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=385ca4f3b9193a83fe1a3e78f277e31c&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=139846&logo=80000000",
          "base_url": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30064.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=coso1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=385ca4f3b9193a83fe1a3e78f277e31c&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=139846&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30064.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=3dc236892d613d75c74fac0635314fa1&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=139846&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30064.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=5d6071304535e79882f398f722e66cc5&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=139846&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30064.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=3dc236892d613d75c74fac0635314fa1&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=139846&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30064.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=5d6071304535e79882f398f722e66cc5&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=139846&logo=40000000"
          ],
          "bandwidth": 1114363,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "avc1.640028",
          "width": 1364,
          "height": 720,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1024:1023",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-999",
            "indexRange": "1000-1499"
          },
          "segment_base": {
            "initialization": "0-999",
            "index_range": "1000-1499"
          },
          "codecid": 7
        },
        {
          "id": 64,
          "baseUrl": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30066.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=upos&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=8dbb746148d0357ca6a69da0260069c9&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=48178&logo=80000000",
          "base_url": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30066.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=upos&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=8dbb746148d0357ca6a69da0260069c9&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=48178&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30066.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=76badc95dcabe00849881f99cff3edf9&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=48178&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30066.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=5c42c7d6df3b1c31e55792be629c26a6&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=48178&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30066.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=76badc95dcabe00849881f99cff3edf9&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=48178&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30066.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=5c42c7d6df3b1c31e55792be629c26a6&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=48178&logo=40000000"
          ],
          "bandwidth": 383908,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "hev1.1.6.L120.90",
          "width": 1364,
          "height": 720,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1024:1023",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-1163",
            "indexRange": "1164-1663"
          },
          "segment_base": {
            "initialization": "0-1163",
            "index_range": "1164-1663"
          },
          "codecid": 12
        },
        {
          "id": 64,
          "baseUrl": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100024.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=upos&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=bc959f9a18a293c510aa1c80b852a4c2&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=90230&logo=80000000",
          "base_url": "https://upos-sz-estgoss.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100024.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=upos&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=bc959f9a18a293c510aa1c80b852a4c2&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=90230&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100024.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=b2b51928d153078a04a72f136f95a2a7&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=90230&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100024.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=51e73e42d2c1c960ce9bcf80bcf19883&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=90230&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100024.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=b2b51928d153078a04a72f136f95a2a7&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=90230&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100024.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=51e73e42d2c1c960ce9bcf80bcf19883&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=90230&logo=40000000"
          ],
          "bandwidth": 717979,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "av01.0.05M.08.0.110.01.01.01.0",
          "width": 1364,
          "height": 720,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1024:1023",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-939",
            "indexRange": "992-1491"
          },
          "segment_base": {
            "initialization": "0-939",
            "index_range": "992-1491"
          },
          "codecid": 13
        },
        {
          "id": 32,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=5e51c579d0e3e32d66f003df1109ef71&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=63317&logo=80000000",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=5e51c579d0e3e32d66f003df1109ef71&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=63317&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=968cd15beae47d73262f7b929e3d0963&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=63317&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=8bfd9ed6455d9485df0827c8dcdbcff3&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=63317&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=968cd15beae47d73262f7b929e3d0963&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=63317&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30032.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=8bfd9ed6455d9485df0827c8dcdbcff3&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=63317&logo=40000000"
          ],
          "bandwidth": 504542,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "avc1.64001F",
          "width": 910,
          "height": 480,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "4096:4095",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-999",
            "indexRange": "1000-1499"
          },
          "segment_base": {
            "initialization": "0-999",
            "index_range": "1000-1499"
          },
          "codecid": 7
        },
        {
          "id": 32,
          "baseUrl": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30033.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=coso1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=cec61c7751592d089cf2056719dd962a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=28323&logo=80000000",
          "base_url": "https://upos-sz-mirrorcoso1.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30033.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=coso1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=cec61c7751592d089cf2056719dd962a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=28323&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30033.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=e074dda6da3bf12b36e6f39d2c23e5fa&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=28323&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30033.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=3b3dd6a59d4d59bb09d51753827fef81&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=28323&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorcos.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30033.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=e074dda6da3bf12b36e6f39d2c23e5fa&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=28323&logo=40000000",
            "https://upos-sz-mirrorcosb.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30033.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=cosbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=3b3dd6a59d4d59bb09d51753827fef81&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=28323&logo=40000000"
          ],
          "bandwidth": 225697,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "hev1.1.6.L120.90",
          "width": 910,
          "height": 480,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "4096:4095",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-1163",
            "indexRange": "1164-1663"
          },
          "segment_base": {
            "initialization": "0-1163",
            "index_range": "1164-1663"
          },
          "codecid": 12
        },
        {
          "id": 32,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100023.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=8395693a815cb889776c16a40ef58ba2&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=45147&logo=80000000",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100023.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=8395693a815cb889776c16a40ef58ba2&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=45147&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100023.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=e6675b5dbeb5d74af07424fa7a600be7&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=45147&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100023.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=cbc2d0df96865e6849d1fcadb3ea0ba6&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=45147&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100023.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=e6675b5dbeb5d74af07424fa7a600be7&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=45147&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100023.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=cbc2d0df96865e6849d1fcadb3ea0ba6&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=45147&logo=40000000"
          ],
          "bandwidth": 358736,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "av01.0.04M.08.0.110.01.01.01.0",
          "width": 910,
          "height": 480,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "4096:4095",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-939",
            "indexRange": "992-1491"
          },
          "segment_base": {
            "initialization": "0-939",
            "index_range": "992-1491"
          },
          "codecid": 13
        },
        {
          "id": 16,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30011.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=43b86de0e648a561c15649b9afb5b6d7&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=38389&logo=80000000",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30011.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=43b86de0e648a561c15649b9afb5b6d7&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=38389&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30011.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=84f816e74e383c840da709d0ef3af2b4&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=38389&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30011.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=1acda22b77d28f6075f8b267c9c4e918&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=38389&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30011.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=84f816e74e383c840da709d0ef3af2b4&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=38389&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_x2-1-30011.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=1acda22b77d28f6075f8b267c9c4e918&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=38389&logo=40000000"
          ],
          "bandwidth": 305906,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "hev1.1.6.L120.90",
          "width": 682,
          "height": 360,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1024:1023",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-1063",
            "indexRange": "1064-1563"
          },
          "segment_base": {
            "initialization": "0-1063",
            "index_range": "1064-1563"
          },
          "codecid": 12
        },
        {
          "id": 16,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30016.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=549701bf5033bbf4d06166c9831cfe1a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=28281&logo=80000000",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30016.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=549701bf5033bbf4d06166c9831cfe1a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=28281&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30016.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=9147eaa0af18fd627bb3fded773f01ea&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=28281&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30016.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=f7be789c2f6d949c48d5a6f664d366e6&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=28281&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30016.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=9147eaa0af18fd627bb3fded773f01ea&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=28281&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30016.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=f7be789c2f6d949c48d5a6f664d366e6&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=28281&logo=40000000"
          ],
          "bandwidth": 225362,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "avc1.64001E",
          "width": 682,
          "height": 360,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1024:1023",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-1007",
            "indexRange": "1008-1507"
          },
          "segment_base": {
            "initialization": "0-1007",
            "index_range": "1008-1507"
          },
          "codecid": 7
        },
        {
          "id": 16,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100022.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=af7fe97e008fa40efb5fc2cc4e1108cf&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=24565&logo=80000000",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100022.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=af7fe97e008fa40efb5fc2cc4e1108cf&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=24565&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100022.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=9707ad4b2433599c238bfd1086908597&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=24565&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100022.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=458bc3fc5d5fda77af9b54208c4544f0&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=24565&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100022.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=9707ad4b2433599c238bfd1086908597&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=24565&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756-1-100022.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=458bc3fc5d5fda77af9b54208c4544f0&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=24565&logo=40000000"
          ],
          "bandwidth": 194731,
          "mimeType": "video/mp4",
          "mime_type": "video/mp4",
          "codecs": "av01.0.01M.08.0.110.01.01.01.0",
          "width": 682,
          "height": 360,
          "frameRate": "25",
          "frame_rate": "25",
          "sar": "1024:1023",
          "startWithSap": 1,
          "start_with_sap": 1,
          "SegmentBase": {
            "Initialization": "0-939",
            "indexRange": "992-1491"
          },
          "segment_base": {
            "initialization": "0-939",
            "index_range": "992-1491"
          },
          "codecid": 13
        }
      ],
      "audio": [
        {
          "id": 30280,
          "baseUrl": "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30280.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=2adea27810ceccdf1536adf66fa3e25a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=24769&logo=80000000",
          "base_url": "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30280.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=2adea27810ceccdf1536adf66fa3e25a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=24769&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30280.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=2adea27810ceccdf1536adf66fa3e25a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=24769&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30280.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=b6f51a5a0579b1ea5e5f69fb3225bc1f&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=24769&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30280.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=2adea27810ceccdf1536adf66fa3e25a&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=24769&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30280.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=b6f51a5a0579b1ea5e5f69fb3225bc1f&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=24769&logo=40000000"
          ],
          "bandwidth": 197324,
          "mimeType": "audio/mp4",
          "mime_type": "audio/mp4",
          "codecs": "mp4a.40.2",
          "width": 0,
          "height": 0,
          "frameRate": "",
          "frame_rate": "",
          "sar": "",
          "startWithSap": 0,
          "start_with_sap": 0,
          "SegmentBase": {
            "Initialization": "0-907",
            "indexRange": "908-1407"
          },
          "segment_base": {
            "initialization": "0-907",
            "index_range": "908-1407"
          },
          "codecid": 0
        },
        {
          "id": 30216,
          "baseUrl": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30216.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=1e456e977006d1be4d1ce16b3687ec69&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=8453&logo=80000000",
          "base_url": "https://upos-sz-mirrorhwo1.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30216.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwo1bv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=1e456e977006d1be4d1ce16b3687ec69&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=8453&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30216.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=cd9293ce3c22d82abb51c620c4df47c1&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=8453&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30216.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=bb6d83b313057f441ec993fea6cd22f8&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=8453&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorhw.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30216.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=cd9293ce3c22d82abb51c620c4df47c1&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=8453&logo=40000000",
            "https://upos-sz-mirrorhwb.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30216.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=hwbbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=bb6d83b313057f441ec993fea6cd22f8&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=8453&logo=40000000"
          ],
          "bandwidth": 67340,
          "mimeType": "audio/mp4",
          "mime_type": "audio/mp4",
          "codecs": "mp4a.40.2",
          "width": 0,
          "height": 0,
          "frameRate": "",
          "frame_rate": "",
          "sar": "",
          "startWithSap": 0,
          "start_with_sap": 0,
          "SegmentBase": {
            "Initialization": "0-941",
            "indexRange": "942-1441"
          },
          "segment_base": {
            "initialization": "0-941",
            "index_range": "942-1441"
          },
          "codecid": 0
        },
        {
          "id": 30232,
          "baseUrl": "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30232.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=a462eb228abea32aaf11494f55275ced&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=16670&logo=80000000",
          "base_url": "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30232.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=a462eb228abea32aaf11494f55275ced&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=0,3&agrr=0&bw=16670&logo=80000000",
          "backupUrl": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30232.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=a462eb228abea32aaf11494f55275ced&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=16670&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30232.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=a59a2b07ccba74fc479310988c09ae38&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=16670&logo=40000000"
          ],
          "backup_url": [
            "https://upos-sz-mirrorali.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30232.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=a462eb228abea32aaf11494f55275ced&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=1,3&agrr=0&bw=16670&logo=40000000",
            "https://upos-sz-mirroralib.bilivideo.com/upgcxcode/56/97/455439756/455439756_nb2-1-30232.m4s?e=ig8euxZM2rNcNbdlhoNvNC8BqJIzNbfqXBvEqxTEto8BTrNvN0GvT90W5JZMkX_YN0MvXg8gNEV4NC8xNEV4N03eN0B5tZlqNxTEto8BTrNvNeZVuJ10Kj_g2UB02J0mN0B5tZlqNCNEto8BTrNvNC7MTX502C8f2jmMQJ6mqF2fka1mqx6gqj0eN0B599M=&uipk=5&nbs=1&deadline=1664715840&gen=playurlv2&os=alibbv&oi=663750228&trid=baeb477295f543148fb5c1f382e7e237u&mid=*******&platform=pc&upsig=a59a2b07ccba74fc479310988c09ae38&uparams=e,uipk,nbs,deadline,gen,os,oi,trid,mid,platform&bvc=vod&nettype=0&orderid=2,3&agrr=0&bw=16670&logo=40000000"
          ],
          "bandwidth": 132801,
          "mimeType": "audio/mp4",
          "mime_type": "audio/mp4",
          "codecs": "mp4a.40.2",
          "width": 0,
          "height": 0,
          "frameRate": "",
          "frame_rate": "",
          "sar": "",
          "startWithSap": 0,
          "start_with_sap": 0,
          "SegmentBase": {
            "Initialization": "0-907",
            "indexRange": "908-1407"
          },
          "segment_base": {
            "initialization": "0-907",
            "index_range": "908-1407"
          },
          "codecid": 0
        }
      ],
      "dolby": null,
      "flac": null
    },
    "support_formats": [
      {
        "quality": 127,
        "format": "hdflv2",
        "new_description": "8K 超高清",
        "display_desc": "8K",
        "superscript": "",
        "codecs": [
          "av01.0.16M.08.0.110.01.01.01.0",
          "hev1.1.6.L180.90"
        ]
      },
      {
        "quality": 120,
        "format": "hdflv2",
        "new_description": "4K 超清",
        "display_desc": "4K",
        "superscript": "",
        "codecs": [
          "av01.0.12M.08.0.110.01.01.01.0",
          "avc1.640033",
          "hev1.1.6.L153.90"
        ]
      },
      {
        "quality": 112,
        "format": "hdflv2",
        "new_description": "1080P 高码率",
        "display_desc": "1080P",
        "superscript": "高码率",
        "codecs": [
          "av01.0.08M.08.0.110.01.01.01.0",
          "avc1.640032",
          "hev1.1.6.L150.90"
        ]
      },
      {
        "quality": 80,
        "format": "flv",
        "new_description": "1080P 高清",
        "display_desc": "1080P",
        "superscript": "",
        "codecs": [
          "av01.0.08M.08.0.110.01.01.01.0",
          "avc1.640032",
          "hev1.1.6.L150.90"
        ]
      },
      {
        "quality": 64,
        "format": "flv720",
        "new_description": "720P 高清",
        "display_desc": "720P",
        "superscript": "",
        "codecs": [
          "av01.0.05M.08.0.110.01.01.01.0",
          "avc1.640028",
          "hev1.1.6.L120.90"
        ]
      },
      {
        "quality": 32,
        "format": "flv480",
        "new_description": "480P 清晰",
        "display_desc": "480P",
        "superscript": "",
        "codecs": [
          "av01.0.04M.08.0.110.01.01.01.0",
          "avc1.64001F",
          "hev1.1.6.L120.90"
        ]
      },
      {
        "quality": 16,
        "format": "mp4",
        "new_description": "360P 流畅",
        "display_desc": "360P",
        "superscript": "",
        "codecs": [
          "av01.0.01M.08.0.110.01.01.01.0",
          "avc1.64001E",
          "hev1.1.6.L120.90"
        ]
      }
    ],
    "high_format": null,
    "last_play_time": 11000,
    "last_play_cid": 455439756
  }
}
```

</details>