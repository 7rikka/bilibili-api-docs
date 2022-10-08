# 获取用户信息

> https://api.bilibili.com/x/space/acc/info?mid=523637998

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名      | 类型  | 必填  | 内容      | 备注  |
|----------|-----|-----|---------|-----|
| mid      | num | √   | 用户id    |     |
| token    | str |     | `空串`    |     |
| platform | str |     | `web`   |     |
| jsonp    | str |     | `jsonp` |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名              | 类型   | 内容             | 备注                |
|------------------|------|----------------|-------------------|
| mid              | num  | 用户uid          |                   |
| name             | str  | 昵称             |                   |
| sex              | str  | 性别             | 可选：`男` `女` `保密`   |
| face             | str  | 头像             |                   |
| face_nft         | num  | 是否为ntf头像       | 0：否<br/>1：是       |
| face_nft_type    | num  |                | 0,1               |
| sign             | str  | 个人签名           |                   |
| rank             | num  | `10000`        |                   |
| level            | num  | 当前等级           |                   |
| jointime         | num  | 注册时间           | 此接口返回恒为`0`        |
| moral            | num  | 节操值            | 此接口返回恒为`0`        |
| silence          | num  | 是否处于禁言状态       | 0：否<br/>1：是       |
| coins            | num  | 硬币数            | 只可查看本人数据，其他人恒为`0` |
| fans_badge       | bool | 是否开通粉丝勋章       |                   |
| fans_medal       | obj  | 粉丝勋章信息         |                   |
| official         | obj  | 账号认证信息         |                   |
| vip              | obj  | 大会员信息          |                   |
| pendant          | obj  | 头像框信息          |                   |
| nameplate        | obj  | 成就勋章信息         |                   |
| user_honour_info | obj  |                |                   |
| is_followed      | bool | 当前登录用户是否关注了该用户 |                   |
| top_photo        | str  | 空间头图url        |                   |
| theme            | obj  | `空对象`          |                   |
| sys_notice       | obj  | 系统通知信息         |                   |
| live_room        | obj  | 直播间信息          |                   |
| birthday         | str  | 生日             | 格式：MM-DD          |
| school           | obj  | 学校信息           |                   |
| profession       | obj  |                |                   |
| tags             | null |                |                   |
| series           | obj  |                |                   |
| is_senior_member | num  | 是否为硬核会员        | 0：否<br />1：是      |
| mcn_info         | null |                |                   |
| gaia_res_type    | num  |                |                   |
| gaia_data        | null |                |                   |
| is_risk          | bool |                |                   |
| elec             | obj  | 充电信息           |                   |

### `data`对象 -> `fans_medal`对象

| 字段名   | 类型   | 内容       | 备注  |
|-------|------|----------|-----|
| show  | bool | 是否显示粉丝勋章 |     |
| wear  | bool | 是否佩戴粉丝勋章 |     |
| medal | obj  | 粉丝勋章信息   |     |

### `data`对象 -> `fans_medal`对象 -> `medal`对象

| 字段名                | 类型  | 内容           | 备注               |
|--------------------|-----|--------------|------------------|
| uid                | num | 用户uid        |                  |
| target_id          | num | 粉丝勋章所属UP的uid |                  |
| medal_id           | num | 粉丝勋章id       |                  |
| level              | num | 粉丝勋章等级       |                  |
| medal_name         | str | 粉丝勋章名称       |                  |
| medal_color        | num | 颜色           |                  |
| intimacy           | num | 当前亲密度        |                  |
| next_intimacy      | num | 下一等级所需亲密度    |                  |
| day_limit          | num | 每日亲密度获取上限    |                  |
| today_feed         | num | 今日已获得亲密度     |                  |
| medal_color_start  | num | 粉丝勋章颜色       | 十进制数，可转为十六进制颜色代码 |
| medal_color_end    | num | 粉丝勋章颜色       | 十进制数，可转为十六进制颜色代码 |
| medal_color_border | num | 粉丝勋章边框颜色     | 十进制数，可转为十六进制颜色代码 |
| is_lighted         | num | `1`          |                  |
| light_status       | num | `1`          |                  |
| wearing_status     | num | 当前是否佩戴       | 0：未佩戴<br />1：已佩戴 |
| score              | num |              |                  |

### `data`对象 -> `official`对象

| 字段名   | 类型  | 内容   | 备注                                      |
|-------|-----|------|-----------------------------------------|
| role  | num | 认证类型 | 0：无<br />1 2 7 9：个人认证<br />3 4 5 6：机构认证 |
| title | str | 认证信息 |                                         |
| desc  | str | 认证备注 |                                         |
| type  | num | 是否认证 | -1：无<br />0：个人认证<br />1：机构认证            |

### `data`对象 -> `vip`对象

| 字段名                  | 类型  | 内容         | 备注                                           |
|----------------------|-----|------------|----------------------------------------------|
| type                 | num | 大会员类型      | 0：无<br />1：月大会员<br />2：年度及以上大会员              |
| status               | num | 大会员状态      | 0：无<br />1：有                                 |
| due_date             | num | 大会员过期时间时间戳 | 单位：毫秒                                        |
| vip_pay_type         | num | 支付类型       |                                              |
| theme_type           | num | `0`        |                                              |
| label                | obj | 大会员标签      |                                              |
| avatar_subscript     | num | 是否显示大会员图标  | 0：不显示<br />1：显示                              |
| nickname_color       | str | 大会员昵称颜色    |                                              |
| role                 | num | 大角色类型      | 1：月度大会员<br/>3：年度大会员<br/>7：十年大会员<br/>15：百年大会员 |
| avatar_subscript_url | str | 大会员角标地址    |                                              |
| tv_vip_status        | num | 电视大会员状态    | 0：未开通                                        |
| tv_vip_pay_type      | num | 电视大会员支付类型  |                                              |

### `data`对象 -> `vip`对象 -> `label`对象

| 字段名                       | 类型   | 内容       | 备注                                                                                                                           |
|---------------------------|------|----------|------------------------------------------------------------------------------------------------------------------------------|
| path                      | str  | `空串`     |                                                                                                                              |
| text                      | str  | 会员类型文案   | `大会员` `年度大会员` `十年大会员` `百年大会员` `最强绿鲤鱼`                                                                                        |
| label_theme               | str  | 会员标签     | vip：大会员<br />annual_vip：年度大会员<br />ten_annual_vip：十年大会员<br />hundred_annual_vip：百年大会员<br/>fools_day_hundred_annual_vip：最强绿鲤鱼 |
| text_color                | str  | 用户名文字颜色  | `#FFFFFF`                                                                                                                    |
| bg_style                  | num  | `1`      |                                                                                                                              |
| bg_color                  | str  | 会员标签背景颜色 |                                                                                                                              |
| border_color              | str  | `空串`     |                                                                                                                              |
| use_img_label             | bool | `true`   |                                                                                                                              |
| img_label_uri_hans        | str  | `空串`     |                                                                                                                              |
| img_label_uri_hant        | str  | `空串`     |                                                                                                                              |
| img_label_uri_hans_static | str  | 大会员牌子图片  | 简体版                                                                                                                          |
| img_label_uri_hant_static | str  | 大会员牌子图片  | 繁体版                                                                                                                          |

### `data`对象 -> `pendant`对象

| 字段名                 | 类型  | 内容       | 备注  |
|---------------------|-----|----------|-----|
| pid                 | num | 头像框id    |     |
| name                | str | 头像框名称    |     |
| image               | str | 头像框图片url |     |
| expire              | num | 过期时间     |     |
| image_enhance       | str | 头像框图片url |     |
| image_enhance_frame | str | `空串`     |     |

### `data`对象 -> `nameplate`对象

| 字段名         | 类型  | 内容      | 备注  |
|-------------|-----|---------|-----|
| nid         | num | 勋章id    |     |
| name        | str | 勋章名称    |     |
| image       | str | 勋章图标    |     |
| image_small | str | 勋章图标（小） |     |
| level       | str | 勋章等级    |     |
| condition   | str | 获取条件    |     |

### `data`对象 -> `user_honour_info`对象

| 字段名    | 类型    | 内容  | 备注  |
|--------|-------|-----|-----|
| mid    | num   |     |     |
| colour | null  |     |     |
| tags   | array |     |     |

### `data`对象 -> `sys_notice`对象

| 字段名         | 类型  | 内容   | 备注  |
|-------------|-----|------|-----|
| id          | num | id   |     |
| content     | str | 显示文案 |     |
| url         | str | 跳转地址 |     |
| notice_type | num | `1`  |     |
| icon        | str | 前缀图标 |     |
| text_color  | str | 文字颜色 |     |
| bg_color    | str | 背景颜色 |     |

### `data`对象 -> `live_room`对象

| 字段名            | 类型  | 内容  | 备注  |
|----------------|-----|-----|-----|
| roomStatus     | num |     |     |
| liveStatus     | num |     |     |
| url            | str |     |     |
| title          | str |     |     |
| cover          | str |     |     |
| roomid         | num |     |     |
| roundStatus    | num |     |     |
| broadcast_type | num |     |     |
| watched_show   | obj |     |     |

### `data`对象 -> `school`对象

| 字段名  | 类型  | 内容   | 备注  |
|------|-----|------|-----|
| name | str | 大学名称 |     |

### `data`对象 -> `profession`对象

| 字段名        | 类型  | 内容  | 备注  |
|------------|-----|-----|-----|
| name       | str |     |     |
| department | str |     |     |
| title      | str |     |     |
| is_show    | num |     |     |

### `data`对象 -> `series`对象

| 字段名                 | 类型   | 内容  | 备注  |
|---------------------|------|-----|-----|
| user_upgrade_status | num  |     |     |
| show_upgrade_window | bool |     |     |

### `data`对象 -> `elec`对象

| 字段名       | 类型  | 内容  | 备注  |
|-----------|-----|-----|-----|
| show_info | obj |     |     |

### `data`对象 -> `elec`对象 -> `show_info`对象

| 字段名      | 类型   | 内容      | 备注               |
|----------|------|---------|------------------|
| show     | bool | 是否开通了充电 |                  |
| state    | num  | 状态      | -1：未开通<br/>1：已开通 |
| title    | str  | `空串`    |                  |
| icon     | str  | `空串`    |                  |
| jump_url | str  | `空串`    |                  |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/space/acc/info?mid=523637998'
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
    "mid": 523637998,
    "name": "小灰灰之声",
    "sex": "保密",
    "face": "https://i1.hdslb.com/bfs/face/031317cc2c8d765bc897d32171ed09daf08f6ee9.jpg",
    "face_nft": 0,
    "face_nft_type": 0,
    "sign": "在下灰灰，欢迎大家和我做朋友↖(^ω^)↗",
    "rank": 10000,
    "level": 6,
    "jointime": 0,
    "moral": 0,
    "silence": 0,
    "coins": 0,
    "fans_badge": true,
    "fans_medal": {
      "show": true,
      "wear": true,
      "medal": {
        "uid": 523637998,
        "target_id": 31832612,
        "medal_id": 157607,
        "level": 14,
        "medal_name": "喜糖儿",
        "medal_color": 12478086,
        "intimacy": 4874,
        "next_intimacy": 15000,
        "day_limit": 1500,
        "today_feed": 100,
        "medal_color_start": 12478086,
        "medal_color_end": 12478086,
        "medal_color_border": 12478086,
        "is_lighted": 1,
        "light_status": 1,
        "wearing_status": 1,
        "score": 49775
      }
    },
    "official": {
      "role": 0,
      "title": "",
      "desc": "",
      "type": -1
    },
    "vip": {
      "type": 2,
      "status": 1,
      "due_date": 1725206400000,
      "vip_pay_type": 1,
      "theme_type": 0,
      "label": {
        "path": "",
        "text": "年度大会员",
        "label_theme": "annual_vip",
        "text_color": "#FFFFFF",
        "bg_style": 1,
        "bg_color": "#FB7299",
        "border_color": "",
        "use_img_label": true,
        "img_label_uri_hans": "https://i0.hdslb.com/bfs/activity-plat/static/20220608/e369244d0b14644f5e1a06431e22a4d5/0DFy9BHgwE.gif",
        "img_label_uri_hant": "",
        "img_label_uri_hans_static": "https://i0.hdslb.com/bfs/vip/8d7e624d13d3e134251e4174a7318c19a8edbd71.png",
        "img_label_uri_hant_static": "https://i0.hdslb.com/bfs/activity-plat/static/20220614/e369244d0b14644f5e1a06431e22a4d5/uckjAv3Npy.png"
      },
      "avatar_subscript": 1,
      "nickname_color": "#FB7299",
      "role": 3,
      "avatar_subscript_url": "",
      "tv_vip_status": 1,
      "tv_vip_pay_type": 0
    },
    "pendant": {
      "pid": 994,
      "name": "格兰芬多",
      "image": "https://i1.hdslb.com/bfs/face/2dee633139ce7c6b0dca657236240cc399c090be.png",
      "expire": 0,
      "image_enhance": "https://i1.hdslb.com/bfs/face/2dee633139ce7c6b0dca657236240cc399c090be.png",
      "image_enhance_frame": ""
    },
    "nameplate": {
      "nid": 3,
      "name": "白银殿堂",
      "image": "https://i2.hdslb.com/bfs/face/f6a31275029365ae5dc710006585ddcf1139bde1.png",
      "image_small": "https://i1.hdslb.com/bfs/face/b09cdb4c119c467cf2d15db5263b4f539fa6e30b.png",
      "level": "高级勋章",
      "condition": "单个自制视频总播放数>=10万"
    },
    "user_honour_info": {
      "mid": 0,
      "colour": null,
      "tags": []
    },
    "is_followed": false,
    "top_photo": "http://i0.hdslb.com/bfs/space/cb1c3ef50e22b6096fde67febe863494caefebad.png",
    "theme": {},
    "sys_notice": {},
    "live_room": {
      "roomStatus": 1,
      "liveStatus": 0,
      "url": "https://live.bilibili.com/23256525?broadcast_type=0&is_room_feed=1",
      "title": "一小时看完筐出胜利！",
      "cover": "http://i0.hdslb.com/bfs/live/new_room_cover/e260d19c44e278244cba9eb8673169f1e2c8719f.jpg",
      "roomid": 23256525,
      "roundStatus": 0,
      "broadcast_type": 0,
      "watched_show": {
        "switch": true,
        "num": 2,
        "text_small": "2",
        "text_large": "2人看过",
        "icon": "https://i0.hdslb.com/bfs/live/a725a9e61242ef44d764ac911691a7ce07f36c1d.png",
        "icon_location": "",
        "icon_web": "https://i0.hdslb.com/bfs/live/8d9d0f33ef8bf6f308742752d13dd0df731df19c.png"
      }
    },
    "birthday": "08-08",
    "school": {
      "name": ""
    },
    "profession": {
      "name": "",
      "department": "",
      "title": "",
      "is_show": 0
    },
    "tags": null,
    "series": {
      "user_upgrade_status": 3,
      "show_upgrade_window": false
    },
    "is_senior_member": 1,
    "mcn_info": null,
    "gaia_res_type": 0,
    "gaia_data": null,
    "is_risk": false,
    "elec": {
      "show_info": {
        "show": true,
        "state": 1,
        "title": "",
        "icon": "",
        "jump_url": ""
      }
    }
  }
}
```

</details>

# 系统提示（sys_notice）示例

| id  | content                                         | url | notice_type | 示例用户                                                                                            |
|-----|-------------------------------------------------|-----|-------------|-------------------------------------------------------------------------------------------------|
| 8   | 该用户存在较大争议，请谨慎甄别其内容                              |     | 1           | [28062215](https://space.bilibili.com/28062215)                                                 |
| 11  | 该账号涉及合约争议，暂冻结其账号功能使用。详见公告->                     |     | 1           |
| 20  | 请允许我们在此献上最后的告别，以此纪念其在哔哩哔哩留下的回忆与足迹。请点此查看纪念账号相关说明 |     | 2           |
| 22  | 该账号涉及合约诉讼，封禁其账号使用。                              |     |
| 24  | 该账号涉及合约争议，暂冻结其账号功能使用。                           |     | 1           | [291229008](https://space.bilibili.com/291229008)                                               |
| 25  | 该用户涉及严重指控，暂冻结其账号功能使用                            |     | 1           |                                                                                                 |
| 31  | 该用户涉及严重指控，暂冻结其账号功能使用                            |     | 1           | [22439273](https://space.bilibili.com/22439273)                                                 |
| 36  | 该账户存在争议，请谨慎甄别                                   |     | 1           | [198297](https://space.bilibili.com/198297)<br/>[18149131](https://space.bilibili.com/18149131) |

# rank

| UID    | rank  |
|--------|-------|
| 124416 | 20000 |
| 16765  | 20000 |
| 3351   | 25000 |