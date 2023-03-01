# ACTIVITY_MATCH_GIFT

## 字段

## 示例数据

```json

```

# ANCHOR_LOT_AWARD

## 字段

## 示例数据

```json```

# ANCHOR_LOT_CHECKSTATUS

## 字段

## 示例数据

```json```

# ANCHOR_LOT_END

## 字段

## 示例数据

```json```

# ANCHOR_LOT_START

## 字段

## 示例数据

```json```

# AREA_RANK_CHANGED

## 字段

## 示例数据

```json```

# BOX_ACTIVITY_START

## 字段

## 示例数据

```json```

# CHANGE_ROOM_INFO

## 字段

## 示例数据

```json```

# CHASE_FRAME_SWITCH

## 字段

## 示例数据

```json```

# COMBO_SEND

## 字段

## 示例数据

```json```

# COMMON_NOTICE_DANMAKU

## 字段

## 示例数据

```json```

# CUT_OFF

## 字段

## 示例数据

```json```

# DANMU_AGGREGATION

## 字段

## 示例数据

```json```

# DANMU_GIFT_LOTTERY_AWARD

## 字段

## 示例数据

```json```

# DANMU_GIFT_LOTTERY_END

## 字段

## 示例数据

```json```

# DANMU_GIFT_LOTTERY_START

## 字段

## 示例数据

```json```

# DANMU_MSG

## 字段

## 示例数据

```json```

# DANMU_TAG_CHANGE

## 字段

## 示例数据

```json```

# ENTRY_EFFECT

## 字段

## 示例数据

```json```

# ENTRY_EFFECT_MUST_RECEIVE

## 字段

## 示例数据

```json```

# FULL_SCREEN_SPECIAL_EFFECT

## 字段

## 示例数据

```json```

# GIFT_PANEL_PLAN

## 字段

## 示例数据

```json```

# GIFT_STAR_PROCESS

## 字段

## 示例数据

```json```

# GOTO_BUY_FLOW

## 字段

## 示例数据

```json```

# GUARD_ACHIEVEMENT_ROOM

## 字段

## 示例数据

```json```

# GUARD_BENEFIT_RECEIVE

## 字段

## 示例数据

```json```

# GUARD_BUY

## 字段

## 示例数据

```json```

# GUARD_HONOR_THOUSAND

## 字段

## 示例数据

```json```

# GUARD_LOTTERY_START

## 字段

## 示例数据

```json```

# GUARD_WINDOWS_OPEN

## 字段

## 示例数据

```json```

# HOT_RANK_CHANGED_V2

## 字段

## 示例数据

```json```

# HOT_RANK_SETTLEMENT_V2

## 字段

## 示例数据

```json```

# HOT_ROOM_NOTIFY

## 字段

## 示例数据

```json```

# HOUR_RANK_AWARDS

## 字段

## 示例数据

```json```

# INTERACT_WORD

## 字段

### 根对象

| 字段名  | 类型  | 内容 | 备注 |
|------|-----|----|----|
| cmd  | str |    |    |
| data | obj |    |    |

### 根对象 -> `data`对象

| 字段名            | 类型    | 内容 | 备注 |
|----------------|-------|----|----|
| contribution   | obj   |    |    |
| core_user_type | num   |    |    |
| dmscore        | num   |    |    |
| fans_medal     | obj   |    |    |
| identities     | array |    |    |
| is_spread      | num   |    |    |
| msg_type       | num   |    |    |
| privilege_type | num   |    |    |
| roomid         | num   |    |    |
| score          | num   |    |    |
| spread_desc    | str   |    |    |
| spread_info    | str   |    |    |
| tail_icon      | num   |    |    |
| timestamp      | num   |    |    |
| trigger_time   | num   |    |    |
| uid            | num   |    |    |
| uname          | str   |    |    |
| uname_color    | str   |    |    |

### 根对象 -> `data`对象 -> `contribution`对象

| 字段名   | 类型  | 内容 | 备注 |
|-------|-----|----|----|
| grade | num |    |    |

### 根对象 -> `data`对象 -> `fans_medal`对象

| 字段名                | 类型  | 内容 | 备注 |
|--------------------|-----|----|----|
| anchor_roomid      | num |    |    |
| guard_level        | num |    |    |
| icon_id            | num |    |    |
| is_lighted         | num |    |    |
| medal_color        | num |    |    |
| medal_color_border | num |    |    |
| medal_color_end    | num |    |    |
| medal_color_start  | num |    |    |
| medal_level        | num |    |    |
| medal_name         | str |    |    |
| score              | num |    |    |
| special            | str |    |    |
| target_id          | num |    |    |

### 根对象 -> `data`对象 -> `identities`数组中的对象

| 字段名 | 类型 | 内容 | 备注 |
|-----|----|----|----|

## 示例数据

```json
{
  "cmd": "INTERACT_WORD",
  "data": {
    "contribution": {
      "grade": 0
    },
    "core_user_type": 0,
    "dmscore": 16,
    "fans_medal": {
      "anchor_roomid": 22889484,
      "guard_level": 0,
      "icon_id": 0,
      "is_lighted": 0,
      "medal_color": 12478086,
      "medal_color_border": 12632256,
      "medal_color_end": 12632256,
      "medal_color_start": 12632256,
      "medal_level": 15,
      "medal_name": "鲸呆",
      "score": 82500,
      "special": "",
      "target_id": 591892279
    },
    "identities": [
      1
    ],
    "is_spread": 0,
    "msg_type": 1,
    "privilege_type": 0,
    "roomid": 24530513,
    "score": 1677652271926,
    "spread_desc": "",
    "spread_info": "",
    "tail_icon": 0,
    "timestamp": 1677652271,
    "trigger_time": 1677652270788228600,
    "uid": 483651568,
    "uname": "莲香清梦",
    "uname_color": ""
  }
}
```

# LIKE_INFO_V3_CLICK

## 字段

## 示例数据

```json```

# LIKE_INFO_V3_UPDATE

## 字段

## 示例数据

```json```

# LIKE_SO_HOT

## 字段

## 示例数据

```json```

# LITTLE_MESSAGE_BOX

## 字段

## 示例数据

```json```

# LITTLE_TIPS

## 字段

## 示例数据

```json```

# LIVE

## 字段

## 示例数据

```json```

# LIVE_INTERACTIVE_GAME

## 字段

## 示例数据

```json```

# LIVE_INTERNAL_ROOM_LOGIN

## 字段

## 示例数据

```json```

# LIVE_MULTI_VIEW_CHANGE

## 字段

## 示例数据

```json```

# LIVE_OPEN_PLATFORM_CLOUD_GAME

## 字段

## 示例数据

```json```

# LIVE_OPEN_PLATFORM_GAME

## 字段

## 示例数据

```json```

# LIVE_PANEL_CHANGE_CONTENT

## 字段

## 示例数据

```json```

# LIVE_PLAYER_LOG_RECYCLE

## 字段

## 示例数据

```json```

# LOL_ACTIVITY

## 字段

## 示例数据

```json```

# MATCH_TEAM_GIFT_RANK

## 字段

## 示例数据

```json```

# MESSAGEBOX_USER_GAIN_MEDAL

## 字段

## 示例数据

```json```

# MESSAGEBOX_USER_MEDAL_CHANGE

## 字段

## 示例数据

```json```

# MESSAGEBOX_USER_MEDAL_COMPENSATION

## 字段

## 示例数据

```json```

# MILESTONE_UPDATE_EVENT

## 字段

## 示例数据

```json```

# MULTI_VOICE_OPERATIN

## 字段

## 示例数据

```json```

# MULTI_VOICE_STATUS_SYNC

## 字段

## 示例数据

```json```

# NOTICE_MSG

## 字段

## 示例数据

```json```

# ONLINE_RANK_COUNT

## 字段

## 示例数据

```json```

# ONLINE_RANK_TOP3

## 字段

## 示例数据

```json```

# ONLINE_RANK_V2

## 字段

## 示例数据

```json```

# PK_AGAIN

## 字段

## 示例数据

```json```

# PK_BATTLE_CRIT

## 字段

## 示例数据

```json```

# PK_BATTLE_END

## 字段

## 示例数据

```json```

# PK_BATTLE_FINAL_PROCESS

## 字段

## 示例数据

```json```

# PK_BATTLE_GIFT

## 字段

## 示例数据

```json```

# PK_BATTLE_PRE_NEW

## 字段

## 示例数据

```json```

# PK_BATTLE_PROCESS_NEW

## 字段

## 示例数据

```json```

# PK_BATTLE_PRO_TYPE

## 字段

## 示例数据

```json```

# PK_BATTLE_PUNISH_END

## 字段

## 示例数据

```json```

# PK_BATTLE_RANK_CHANGE

## 字段

## 示例数据

```json```

# PK_BATTLE_SETTLE_NEW

## 字段

## 示例数据

```json```

# PK_BATTLE_SETTLE_V2

## 字段

## 示例数据

```json```

# PK_BATTLE_SPECIAL_GIFT

## 字段

## 示例数据

```json```

# PK_BATTLE_START_NEW

## 字段

## 示例数据

```json```

# PK_BATTLE_VIDEO_PUNISH_BEGIN

## 字段

## 示例数据

```json```

# PK_BATTLE_VIDEO_PUNISH_END

## 字段

## 示例数据

```json```

# PK_BATTLE_VOTES_ADD

## 字段

## 示例数据

```json```

# PK_END

## 字段

## 示例数据

```json```

# PK_LOTTERY_START

## 字段

## 示例数据

```json```

# PK_MATCH

## 字段

## 示例数据

```json```

# PK_MIC_END

## 字段

## 示例数据

```json```

# PK_PRE

## 字段

## 示例数据

```json```

# PK_PROCESS

## 字段

## 示例数据

```json```

# PK_SETTLE

## 字段

## 示例数据

```json```

# PK_START

## 字段

## 示例数据

```json```

# PLAY_TAG

## 字段

## 示例数据

```json```

# PLAY_TOGETHER

## 字段

## 示例数据

```json```

# POPULARITY_RED_POCKET_NEW

## 字段

## 示例数据

```json```

# POPULARITY_RED_POCKET_START

## 字段

## 示例数据

```json```

# POPULARITY_RED_POCKET_WINNER_LIST

## 字段

## 示例数据

```json```

# POPULAR_RANK_CHANGED

## 字段

## 示例数据

```json```

# PREPARING

## 字段

## 示例数据

```json```

# RAFFLE_END

## 字段

## 示例数据

```json```

# RAFFLE_START

## 字段

## 示例数据

```json```

# RANK_REM

## 字段

## 示例数据

```json```

# RECOMMEND_CARD

## 字段

## 示例数据

```json```

# RED_POCKET_START

## 字段

## 示例数据

```json```

# REENTER_LIVE_ROOM

## 字段

## 示例数据

```json```

# ROOM_ADMINS

## 字段

## 示例数据

```json```

# ROOM_BANNER

## 字段

## 示例数据

```json```

# ROOM_BLOCK_INTO

## 字段

## 示例数据

```json```

# ROOM_BLOCK_MSG

## 字段

## 示例数据

```json```

# ROOM_CHANGE

## 字段

## 示例数据

```json```

# ROOM_KICKOUT

## 字段

## 示例数据

```json```

# ROOM_LIMIT

## 字段

## 示例数据

```json```

# ROOM_LOCK

## 字段

## 示例数据

```json```

# ROOM_RANK

## 字段

## 示例数据

```json```

# ROOM_REAL_TIME_MESSAGE_UPDATE

## 字段

## 示例数据

```json```

# ROOM_REFRESH

## 字段

## 示例数据

```json```

# ROOM_SILENT_OFF

## 字段

## 示例数据

```json```

# ROOM_SILENT_ON

## 字段

## 示例数据

```json```

# ROOM_SKIN_MSG

## 字段

## 示例数据

```json```

# Revenue_PayLimit

## 字段

## 示例数据

```json```

# SEND_GIFT

## 字段

## 示例数据

```json```

# SEND_GIFT_V2

## 字段

## 示例数据

```json```

# SEND_TOP

## 字段

## 示例数据

```json```

# SHOPPING_CART_SHOW

## 字段

## 示例数据

```json```

# SPECIAL_GIFT

## 字段

## 示例数据

```json```

# STARLIVE_PK_MSG

## 字段

## 示例数据

```json```

# STOP_LIVE_ROOM_LIST

## 字段

## 示例数据

```json```

# SUPER_CHAT_AUDIT

## 字段

## 示例数据

```json```

# SUPER_CHAT_ENTRANCE

## 字段

## 示例数据

```json```

# SUPER_CHAT_MESSAGE

## 字段

## 示例数据

```json```

# SUPER_CHAT_MESSAGE_DELETE

## 字段

## 示例数据

```json```

# SUPER_CHAT_MESSAGE_JPN

## 字段

### 根对象

| 字段名    | 类型  | 内容 | 备注 |
|--------|-----|----|----|
| cmd    | str |    |    |
| data   | obj |    |    |
| roomid | str |    |    |

### `data`对象

| 字段名                     | 类型  | 内容 | 备注 |
|-------------------------|-----|----|----|
| id                      | str |    |    |
| uid                     | str |    |    |
| price                   | num |    |    |
| rate                    | num |    |    |
| message                 | str |    |    |
| message_jpn             | str |    |    |
| is_ranked               | num |    |    |
| background_image        | str |    |    |
| background_color        | str |    |    |
| background_icon         | str |    |    |
| background_price_color  | str |    |    |
| background_bottom_color | str |    |    |
| ts                      | num |    |    |
| token                   | str |    |    |
| medal_info              | obj |    |    |
| user_info               | obj |    |    |
| time                    | num |    |    |
| start_time              | num |    |    |
| end_time                | num |    |    |
| gift                    | obj |    |    |

### `data`对象 -> `medal_info`对象

| 字段名           | 类型  | 内容 | 备注 |
|---------------|-----|----|----|
| icon_id       | num |    |    |
| target_id     | num |    |    |
| special       | str |    |    |
| anchor_uname  | str |    |    |
| anchor_roomid | num |    |    |
| medal_level   | num |    |    |
| medal_name    | str |    |    |
| medal_color   | str |    |    |

### `data`对象 -> `user_info`对象

| 字段名         | 类型  | 内容 | 备注 |
|-------------|-----|----|----|
| uname       | str |    |    |
| face        | str |    |    |
| face_frame  | str |    |    |
| guard_level | num |    |    |
| user_level  | num |    |    |
| level_color | str |    |    |
| is_vip      | num |    |    |
| is_svip     | num |    |    |
| is_main_vip | num |    |    |
| title       | str |    |    |
| manager     | num |    |    |

### `data`对象 -> `gift`对象

| 字段名       | 类型  | 内容 | 备注 |
|-----------|-----|----|----|
| num       | num |    |    |
| gift_id   | num |    |    |
| gift_name | str |    |    |

## 示例数据

```json
{
  "cmd": "SUPER_CHAT_MESSAGE_JPN",
  "data": {
    "id": "6575310",
    "uid": "1312331587",
    "price": 30,
    "rate": 1000,
    "message": "想听 天马座的幻想",
    "message_jpn": "ペガサスの幻想を聞きたい",
    "is_ranked": 1,
    "background_image": "https://i0.hdslb.com/bfs/live/a712efa5c6ebc67bafbe8352d3e74b820a00c13e.png",
    "background_color": "#EDF5FF",
    "background_icon": "",
    "background_price_color": "#7497CD",
    "background_bottom_color": "#2A60B2",
    "ts": 1677642780,
    "token": "C44CDD5C",
    "medal_info": {
      "icon_id": 0,
      "target_id": 57871034,
      "special": "",
      "anchor_uname": "栀小朵",
      "anchor_roomid": 23246736,
      "medal_level": 32,
      "medal_name": "朵不知",
      "medal_color": "#2d0855"
    },
    "user_info": {
      "uname": "栀小朵的鼠土圭丶垚",
      "face": "https://i1.hdslb.com/bfs/face/c16280ebd4a0f1564618b0589c057aaae284d5ad.jpg",
      "face_frame": "",
      "guard_level": 0,
      "user_level": 40,
      "level_color": "#a068f1",
      "is_vip": 0,
      "is_svip": 0,
      "is_main_vip": 0,
      "title": "0",
      "manager": 0
    },
    "time": 60,
    "start_time": 1677642780,
    "end_time": 1677642840,
    "gift": {
      "num": 1,
      "gift_id": 12000,
      "gift_name": "醒目留言"
    }
  },
  "roomid": "22901614"
}
```

# THERMAL_STORM_DANMU_BEGIN

## 字段

## 示例数据

```json```

# THERMAL_STORM_DANMU_CANCEL

## 字段

## 示例数据

```json```

# THERMAL_STORM_DANMU_OVER

## 字段

## 示例数据

```json```

# THERMAL_STORM_DANMU_UPDATE

## 字段

## 示例数据

```json```

# TRADING_SCORE

## 字段

## 示例数据

```json```

# TV_END

## 字段

## 示例数据

```json```

# TV_START

## 字段

## 示例数据

```json```

# USER_PANEL_RED_ALARM

## 字段

## 示例数据

```json```

# USER_TITLE_GET

## 字段

## 示例数据

```json```

# USER_TOAST_MSG

## 字段

## 示例数据

```json```

# VIDEO_CONNECTION_JOIN_END

## 字段

## 示例数据

```json```

# VIDEO_CONNECTION_JOIN_START

## 字段

## 示例数据

```json```

# VIDEO_CONNECTION_MSG

## 字段

## 示例数据

```json```

# VIDEO_CONNECTION_START

## 字段

## 示例数据

```json```

# VOICE_JOIN_LIST

## 字段

## 示例数据

```json```

# VOICE_JOIN_ROOM_COUNT_INFO

## 字段

## 示例数据

```json```

# VOICE_JOIN_STATUS

## 字段

## 示例数据

```json```

# VTR_GIFT_LOTTERY

## 字段

## 示例数据

```json```

# WARNING

## 字段

## 示例数据

```json```

# WATCHED_CHANGE

## 字段

## 示例数据

```json```

# WATCH_LPL_EXPIRED

## 字段

## 示例数据

```json```

# WEB_REPORT_CONTROL

## 字段

## 示例数据

```json```

# WIDGET_BANNER

## 字段

## 示例数据

```json```

# WIDGET_GIFT_STAR_PROCESS

## 字段

## 示例数据

```json```

# WIN_ACTIVITY

## 字段

## 示例数据

```json```

# WIN_ACTIVITY_USER

## 字段

## 示例数据

```json```

# room_admin_entrance

## 字段

## 示例数据

```json```