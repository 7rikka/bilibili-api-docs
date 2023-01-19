# 清晰度代码

| 代码    | 说明  |
|-------|-----|
| 30000 | 杜比  |
| 20000 | 4K  |
| 10000 | 原画  |
| 400   | 蓝光  |
| 250   | 超清  |
| 150   | 高清  |
| 80    | 流畅  |

# 获取直播间信息

> https://api.live.bilibili.com/xlive/web-room/v2/index/getRoomPlayInfo

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名      | 类型  | 必填  | 内容    | 备注                                             |
|----------|-----|-----|-------|------------------------------------------------|
| room_id  | num | √   | 直播间id |                                                |
| protocol | str | √   | 直播协议  | 0：http_stream<br/>1：http_hls<br/>可多选, 使用英文逗号分隔 |
| format   | str | √   | 格式    | 0：flv<br/>1：ts<br/>2：fmp4<br/>可多选, 使用英文逗号分隔    |
| codec    | str | √   | 编码格式  | 0：AVC<br/>1：HEVC<br/>可多选, 使用英文逗号分隔             |
| qn       | num |     | 清晰度编码 | 默认`150`<br/>[清晰度代码](#清晰度代码)                    |
| platform | str |     | `web` |                                                |
| ptype    | num |     | `8`   |                                                |
| dolby    | num |     | `5`   |                                                |
| panorama | num |     | `1`   |                                                |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                    |
|---------|-----|------|-----------------------|
| code    | num | 响应码  | 0：成功<br/>1002002：参数错误 |
| message | str | 0    |                       |
| ttl     | num | 1    |                       |
| data    | obj | 信息本体 |                       |

### `data`对象

| 字段名               | 类型    | 内容        | 备注                        |
|-------------------|-------|-----------|---------------------------|
| room_id           | num   | 直播间id     |                           |
| short_id          | num   | 直播间短id    |                           |
| uid               | num   | 主播uid     |                           |
| is_hidden         | bool  | 直播间是否被隐藏  |                           |
| is_locked         | bool  | 直播间是否被锁定  |                           |
| is_portrait       | bool  | 是否竖屏      |                           |
| live_status       | num   | 直播状态      | 0：未开播<br/>1：直播中<br/>2：轮播中 |
| hidden_till       | num   | 隐藏结束时间    |                           |
| lock_till         | num   | 封禁结束时间    | 秒级时间戳                     |
| encrypted         | bool  | 直播间为加密直播间 |                           |
| pwd_verified      | bool  | 是否通过密码验证  | 当`encrypted`为`true`时才有意义  |
| live_time         | num   | 本次开播时间    | 秒级时间戳                     |
| room_shield       | num   |           |                           |
| all_special_types | array |           |                           |
| playurl_info      | obj   | 直播流信息     |                           |

### `data`对象 -> `playurl_info`对象

| 字段名       | 类型  | 内容  | 备注  |
|-----------|-----|-----|-----|
| conf_json | str |     |     |
| playurl   | obj |     |     |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象

| 字段名       | 类型    | 内容    | 备注  |
|-----------|-------|-------|-----|
| cid       | num   | 直播间id |     |
| g_qn_desc | array | 清晰度列表 |     |
| stream    | array | 直播流信息 |     |
| p2p_data  | obj   |       |     |
| dolby_qn  |       |       |     |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `g_qn_desc`数组中的对象

| 字段名       | 类型  | 内容    | 备注              |
|-----------|-----|-------|-----------------|
| qn        | num | 清晰度代码 | [清晰度代码](#清晰度代码) |
| desc      | str | 清晰度描述 |                 |
| hdr_desc  | str |       |                 |
| attr_desc |     |       |                 |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `stream`数组中的对象

| 字段名           | 类型    | 内容   | 备注  |
|---------------|-------|------|-----|
| protocol_name | str   | 协议名  |     |
| format        | array | 格式列表 |     |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `stream`数组中的对象 -> `format`数组中的对象

| 字段名         | 类型    | 内容   | 备注  |
|-------------|-------|------|-----|
| format_name | str   | 格式名  |     |
| codec       | array | 编码列表 |     |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `stream`数组中的对象 -> `format`数组中的对象 -> `codec`数组中的对象

| 字段名        | 类型    | 内容        | 备注              |
|------------|-------|-----------|-----------------|
| codec_name | str   | 编码名       |                 |
| current_qn | num   | 当前清晰度编码   | [清晰度代码](#清晰度代码) |
| accept_qn  | array | 可用清晰度编码列表 | [清晰度代码](#清晰度代码) |
| base_url   | str   | 播放源路径     |                 |
| url_info   | array | 域名信息列表    |                 |
| hdr_qn     | null  |           |                 |
| dolby_type | num   |           |                 |
| attr_name  | str   |           |                 |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `stream`数组中的对象 -> `format`数组中的对象 -> `codec`数组中的对象 -> `url_info`数组中的对象

| 字段名        | 类型  | 内容    | 备注  |
|------------|-----|-------|-----|
| host       | str | 域名    |     |
| extra      | str | URL参数 |     |
| stream_ttl | num |       |     |

### `data`对象 -> `playurl_info`对象 -> `playurl`对象 -> `p2p_data`对象

| 字段名       | 类型   | 内容  | 备注  |
|-----------|------|-----|-----|
| p2p       | bool |     |     |
| p2p_type  | num  |     |     |
| m_p2p     | bool |     |     |
| m_servers | null |     |     |

## 请求示例

```shell
curl -L -X GET 'https://api.live.bilibili.com/xlive/web-room/v2/index/getRoomPlayInfo?room_id=3&protocol=0,1&format=0,1,2&codec=0,1&qn=10000'
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
    "room_id": 23058,
    "short_id": 3,
    "uid": 11153765,
    "is_hidden": false,
    "is_locked": false,
    "is_portrait": false,
    "live_status": 1,
    "hidden_till": 0,
    "lock_till": 0,
    "encrypted": false,
    "pwd_verified": true,
    "live_time": 1671425336,
    "room_shield": 1,
    "all_special_types": [],
    "playurl_info": {
      "conf_json": "{\"cdn_rate\":10000,\"report_interval_sec\":150}",
      "playurl": {
        "cid": 23058,
        "g_qn_desc": [
          {
            "qn": 30000,
            "desc": "杜比",
            "hdr_desc": "",
            "attr_desc": null
          },
          {
            "qn": 20000,
            "desc": "4K",
            "hdr_desc": "",
            "attr_desc": null
          },
          {
            "qn": 10000,
            "desc": "原画",
            "hdr_desc": "",
            "attr_desc": null
          },
          {
            "qn": 400,
            "desc": "蓝光",
            "hdr_desc": "HDR",
            "attr_desc": null
          },
          {
            "qn": 250,
            "desc": "超清",
            "hdr_desc": "HDR",
            "attr_desc": null
          },
          {
            "qn": 150,
            "desc": "高清",
            "hdr_desc": "",
            "attr_desc": null
          },
          {
            "qn": 80,
            "desc": "流畅",
            "hdr_desc": "",
            "attr_desc": null
          }
        ],
        "stream": [
          {
            "protocol_name": "http_stream",
            "format": [
              {
                "format_name": "flv",
                "codec": [
                  {
                    "codec_name": "avc",
                    "current_qn": 10000,
                    "accept_qn": [
                      10000,
                      150
                    ],
                    "base_url": "/live-bvc/462997/live_11153765_9369560.flv?",
                    "url_info": [
                      {
                        "host": "https://cn-hbcd-cu-02-20.bilivideo.com",
                        "extra": "expires=1674103815&pt=web&deadline=1674103815&len=0&oi=1963941079&platform=web&qn=10000&trid=1000061f434c07ac4f4184820bfb141e75e8&uipk=100&uipv=100&nbs=1&uparams=cdn,deadline,len,oi,platform,qn,trid,uipk,uipv,nbs&cdn=cn-gotcha01&upsig=f494aa9e92e24943061fe5082494ec44&sk=33541455720f64c7671bc1480acfb176&p2p_type=1&src=57345&sl=1&free_type=0&sid=cn-hbcd-cu-02-20&chash=1&sche=ban&score=12&pp=rtmp&machinezone=jd&source=onetier&trace=0&site=92e80b6f3ebfd393e7d1c1e2e648d9c1&order=1",
                        "stream_ttl": 3600
                      }
                    ],
                    "hdr_qn": null,
                    "dolby_type": 0,
                    "attr_name": ""
                  }
                ]
              }
            ]
          },
          {
            "protocol_name": "http_hls",
            "format": [
              {
                "format_name": "ts",
                "codec": [
                  {
                    "codec_name": "avc",
                    "current_qn": 10000,
                    "accept_qn": [
                      10000,
                      150
                    ],
                    "base_url": "/live-bvc/462997/live_11153765_9369560.m3u8?",
                    "url_info": [
                      {
                        "host": "https://cn-hbcd-cu-02-20.bilivideo.com",
                        "extra": "expires=1674103815&len=0&oi=1963941079&pt=web&qn=10000&trid=1003061f434c07ac4f4184820bfb141e75e8&sigparams=cdn,expires,len,oi,pt,qn,trid&cdn=cn-gotcha01&sign=4f9bcec18e3afdca04b31ffb285ec915&sk=33541455720f64c7671bc1480acfb176&p2p_type=1&src=57345&sl=1&free_type=0&sid=cn-hbcd-cu-02-20&chash=1&sche=ban&score=12&pp=rtmp&machinezone=jd&source=onetier&trace=0&site=92e80b6f3ebfd393e7d1c1e2e648d9c1&order=1",
                        "stream_ttl": 3600
                      }
                    ],
                    "hdr_qn": null,
                    "dolby_type": 0,
                    "attr_name": ""
                  }
                ]
              },
              {
                "format_name": "fmp4",
                "codec": [
                  {
                    "codec_name": "avc",
                    "current_qn": 10000,
                    "accept_qn": [
                      10000,
                      150
                    ],
                    "base_url": "/live-bvc/462997/live_11153765_9369560/index.m3u8?",
                    "url_info": [
                      {
                        "host": "https://cn-hbcd-cu-02-20.bilivideo.com",
                        "extra": "expires=1674103815&len=0&oi=1963941079&pt=web&qn=10000&trid=1007061f434c07ac4f4184820bfb141e75e8&sigparams=cdn,expires,len,oi,pt,qn,trid&cdn=cn-gotcha01&sign=cc57dce528316d8389f2f34e7bd15f5c&sk=a99391b8b4d5779b2e32e41dbc989d2d&flvsk=33541455720f64c7671bc1480acfb176&p2p_type=1&src=57345&sl=1&free_type=0&sid=cn-hbcd-cu-02-20&chash=1&sche=ban&bvchls=1&score=12&pp=rtmp&machinezone=jd&source=onetier&trace=0&site=92e80b6f3ebfd393e7d1c1e2e648d9c1&order=1",
                        "stream_ttl": 3600
                      },
                      {
                        "host": "https://c1--cn-gotcha208.bilivideo.com",
                        "extra": "expires=1674103815&len=0&oi=1963941079&pt=web&qn=10000&trid=1007061f434c07ac4f4184820bfb141e75e8&sigparams=cdn,expires,len,oi,pt,qn,trid&cdn=cn-gotcha208&sign=2ff96adf5056c8dbee546955260fc2df&sk=a99391b8b4d5779b2e32e41dbc989d2d&p2p_type=1&src=57345&sl=1&free_type=0&pp=rtmp&machinezone=jd&source=onetier&trace=0&site=92e80b6f3ebfd393e7d1c1e2e648d9c1&order=2",
                        "stream_ttl": 3600
                      }
                    ],
                    "hdr_qn": null,
                    "dolby_type": 0,
                    "attr_name": ""
                  }
                ]
              }
            ]
          }
        ],
        "p2p_data": {
          "p2p": true,
          "p2p_type": 1,
          "m_p2p": false,
          "m_servers": null
        },
        "dolby_qn": null
      }
    }
  }
}
```

</details>