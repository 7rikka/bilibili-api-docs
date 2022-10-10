# 获取文集信息

> https://api.bilibili.com/x/article/list/web/articles

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名 | 类型  | 必填  | 内容   | 备注  |
|-----|-----|-----|------|-----|
| id  | num | √   | 文集id |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                               |
|---------|-----|------|----------------------------------|
| code    | num | 响应码  | 0：成功<br/>-400：请求错误<br/>-404：啥都木有 |
| message | str | 0    |                                  |
| ttl     | num | 1    |                                  |
| data    | obj | 信息本体 |                                  |

### `data`对象

| 字段名       | 类型    | 内容           | 备注  |
|-----------|-------|--------------|-----|
| list      | obj   | 文集信息         |     |
| articles  | array | 文章列表         |     |
| author    | obj   | 作者信息         |     |
| last      | obj   |              |     |
| attention | obj   | 当前用户是否关注文集作者 |     |

### `data`对象 -> `list`对象

| 字段名            | 类型  | 内容      | 备注   |
|----------------|-----|---------|------|
| id             | num | 文集id    |      |
| mid            | num | 作者uid   |      |
| name           | str | 文集名称    |      |
| image_url      | str | 封面      |      |
| update_time    | num | 最后更新时间戳 | 单位：秒 |
| ctime          | num | 创建时间戳   | 单位：秒 |
| publish_time   | num | 发布时间    | 单位：秒 |
| summary        | str | 简介      |      |
| words          | num | 总字数     |      |
| read           | num | 阅读量     |      |
| articles_count | num | 包含文章数   |      |
| state          | num | `1`     |      |
| reason         | str | `空串`    |      |
| apply_time     | str | `空串`    |      |
| check_time     | str | `空串`    |      |

### `data`对象 -> `articles`数组中的对象

| 字段名          | 类型    | 内容       | 备注   |
|--------------|-------|----------|------|
| id           | num   | 专栏文章id   |      |
| title        | str   | 标题       |      |
| state        | num   | `0`      |      |
| publish_time | num   | 发布时间戳    | 单位：秒 |
| words        | num   | 字数       |      |
| image_urls   | array |          |      |
| category     | obj   | 分类       |      |
| categories   | array | 分类       |      |
| summary      | str   | 摘要       |      |
| stats        | obj   | 专栏文章数据统计 |      |
| like_state   | num   |          |      |

### `data`对象 -> `articles`数组中的对象 -> `category`对象

| 字段名       | 类型  | 内容     | 备注  |
|-----------|-----|--------|-----|
| id        | num | 分类id   |     |
| parent_id | num | 父级分类id |     |
| name      | str | 分类名称   |     |

### `data`对象 -> `articles`数组中的对象 -> `categories`数组中的对象

| 字段名       | 类型  | 内容     | 备注  |
|-----------|-----|--------|-----|
| id        | num | 分类id   |     |
| parent_id | num | 父级分类id |     |
| name      | str | 分类名称   |     |

### `data`对象 -> `articles`数组中的对象 -> `stats`对象

| 字段名      | 类型  | 内容    | 备注    |
|----------|-----|-------|-------|
| view     | num | 浏览数   |       |
| favorite | num | 收藏数   |       |
| like     | num | 点赞数   |       |
| dislike  | num | 点踩数   | 恒为`0` |
| reply    | num | 回复数   |       |
| share    | num | 转发数   |       |
| coin     | num | 投币数   |       |
| dynamic  | num | 动态转发数 |       |

### `data`对象 -> `author`对象

| 字段名             | 类型  | 内容     | 备注  |
|-----------------|-----|--------|-----|
| mid             | num | 用户uid  |     |
| name            | str | 用户名    |     |
| face            | str | 头像     |     |
| pendant         | obj | 头像框信息  |     |
| official_verify | obj | 账号认证信息 |     |
| nameplate       | obj | 成就勋章信息 |     |
| vip             | obj | 大会员信息  |     |

### `data`对象 -> `articles`数组中的对象 -> `author`对象 -> `pendant`对象

| 字段名    | 类型  | 内容       | 备注  |
|--------|-----|----------|-----|
| pid    | num | 头像框id    |     |
| name   | str | 头像框名称    |     |
| image  | str | 头像框图片url |     |
| expire | num | 过期时间     |     |

### `data`对象 -> `articles`数组中的对象 -> `author`对象 -> `official_verify`对象

| 字段名  | 类型  | 内容   | 备注                           |
|------|-----|------|------------------------------|
| type | num | 是否认证 | -1：无<br />0：个人认证<br />1：机构认证 |
| desc | str | 认证备注 |                              |

### `data`对象 -> `articles`数组中的对象 -> `author`对象 -> `nameplate`对象

| 字段名         | 类型  | 内容      | 备注  |
|-------------|-----|---------|-----|
| nid         | num | 勋章id    |     |
| name        | str | 勋章名称    |     |
| image       | str | 勋章图标    |     |
| image_small | str | 勋章图标（小） |     |
| level       | str | 勋章等级    |     |
| condition   | str | 获取条件    |     |

### `data`对象 -> `articles`数组中的对象 -> `author`对象 -> `vip`对象

| 字段名              | 类型  | 内容         | 备注                              |
|------------------|-----|------------|---------------------------------|
| type             | num | 大会员类型      | 0：无<br />1：月大会员<br />2：年度及以上大会员 |
| status           | num | 大会员状态      | 0：无<br />1：有                    |
| due_date         | num | 大会员过期时间时间戳 | 单位：毫秒                           |
| vip_pay_type     | num | 支付类型       |                                 |
| theme_type       | num | `0`        |                                 |
| label            | obj | 大会员标签      |                                 |
| avatar_subscript | num | 是否显示大会员图标  | 0：不显示<br />1：显示                 |
| nickname_color   | str | 大会员昵称颜色    |                                 |

### `data`对象 -> `articles`数组中的对象 -> `author`对象 -> `vip`对象 -> `label`对象

| 字段名         | 类型  | 内容     | 备注                                                                                                                           |
|-------------|-----|--------|------------------------------------------------------------------------------------------------------------------------------|
| path        | str | `空串`   |                                                                                                                              |
| text        | str | 会员类型文案 | `大会员` `年度大会员` `十年大会员` `百年大会员` `最强绿鲤鱼`                                                                                        |
| label_theme | str | 会员标签   | vip：大会员<br />annual_vip：年度大会员<br />ten_annual_vip：十年大会员<br />hundred_annual_vip：百年大会员<br/>fools_day_hundred_annual_vip：最强绿鲤鱼 |

### `data`对象 -> `last`对象

| 字段名          | 类型    | 内容     | 备注   |
|--------------|-------|--------|------|
| id           | num   | 专栏文章id |      |
| title        | str   | 标题     |      |
| state        | num   | `0`    |      |
| publish_time | num   | 发布时间戳  | 单位：秒 |
| words        | num   | 字数     |      |
| image_urls   | array |        |      |
| category     | obj   | 分类     |      |
| categories   | array | 分类     |      |
| summary      | str   | 摘要     |      |

### `data`对象 -> `last`对象 -> `category`对象

| 字段名       | 类型  | 内容     | 备注  |
|-----------|-----|--------|-----|
| id        | num | 分类id   |     |
| parent_id | num | 父级分类id |     |
| name      | str | 分类名称   |     |

### `data`对象 -> `last`对象 -> `categories`数组中的对象

| 字段名       | 类型  | 内容     | 备注  |
|-----------|-----|--------|-----|
| id        | num | 分类id   |     |
| parent_id | num | 父级分类id |     |
| name      | str | 分类名称   |     |

## 请求示例

```shell
curl -L -X GET 'https://api.bilibili.com/x/article/list/web/articles?id=26407'
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
        "list": {
            "id": 26453,
            "mid": 2859372,
            "name": "杂谈",
            "image_url": "https://i0.hdslb.com/bfs/article/96d2b3d2a72e6497a011c885ab9245c51507ce18.png",
            "update_time": 1557303117,
            "ctime": 1537954625,
            "publish_time": 1557303168,
            "summary": "",
            "words": 10673,
            "read": 38366,
            "articles_count": 4,
            "state": 1,
            "reason": "",
            "apply_time": "",
            "check_time": ""
        },
        "articles": [
            {
                "id": 1145648,
                "title": "2018年名作之壁吧视频组招新",
                "state": 0,
                "publish_time": 1536737598,
                "words": 2385,
                "image_urls": [
                    "https://i0.hdslb.com/bfs/article/a5dfc3beafa4fd41d943f83cad784a1a88a5b638.jpg"
                ],
                "category": {
                    "id": 4,
                    "parent_id": 2,
                    "name": "动漫杂谈"
                },
                "categories": [
                    {
                        "id": 2,
                        "parent_id": 0,
                        "name": "动画"
                    },
                    {
                        "id": 4,
                        "parent_id": 2,
                        "name": "动漫杂谈"
                    }
                ],
                "summary": "名作之壁吧视频组是运营B站UP主“名作之壁吧”的幕后组织，视频内容主要围绕动画碟片销量，目前已有名家名作、预测打脸、大师之路、新番导视等代表作系列，还有目前正在筹备的动画年鉴系列。因为视频内容的范围拓",
                "stats": {
                    "view": 7461,
                    "favorite": 40,
                    "like": 775,
                    "dislike": 0,
                    "reply": 106,
                    "share": 55,
                    "coin": 51,
                    "dynamic": 0
                },
                "like_state": 0
            },
            {
                "id": 361873,
                "title": "从CloverWorks的诞生谈谈A-1 pictures的公司构成",
                "state": 0,
                "publish_time": 1523102847,
                "words": 3207,
                "image_urls": [
                    "https://i0.hdslb.com/bfs/article/2d56f1d598b9c932cadad4bb1bb8392bfec230e4.jpg"
                ],
                "category": {
                    "id": 4,
                    "parent_id": 2,
                    "name": "动漫杂谈"
                },
                "categories": [
                    {
                        "id": 2,
                        "parent_id": 0,
                        "name": "动画"
                    },
                    {
                        "id": 4,
                        "parent_id": 2,
                        "name": "动漫杂谈"
                    }
                ],
                "summary": "相信如果是对动画公司有所关注的人，最新都会听到一个名字：CloverWorks。这家新生的公司在4月将会制作《Darling in the franxx》后半部分与《女神异闻录5》——",
                "stats": {
                    "view": 21388,
                    "favorite": 559,
                    "like": 753,
                    "dislike": 0,
                    "reply": 441,
                    "share": 121,
                    "coin": 95,
                    "dynamic": 0
                },
                "like_state": 0
            },
            {
                "id": 1916504,
                "title": "19年一月新番 动画制片人、制作主任相关",
                "state": 0,
                "publish_time": 1548230152,
                "words": 2643,
                "image_urls": [
                    "https://i0.hdslb.com/bfs/article/70e3258b071e3864850f2da37e9ebccbdec97baa.jpg"
                ],
                "category": {
                    "id": 4,
                    "parent_id": 2,
                    "name": "动漫杂谈"
                },
                "categories": [
                    {
                        "id": 2,
                        "parent_id": 0,
                        "name": "动画"
                    },
                    {
                        "id": 4,
                        "parent_id": 2,
                        "name": "动漫杂谈"
                    }
                ],
                "summary": "组员阿群写的一月番动画制作人相关随笔哟~这季度新P和老铁组合都不少呢。这里随意记录一些看过的且有东西可讲的作品。1. 笑容的代价柳桥P这边时间飞船系列后拉着desk佐野弄这个。另一个desk福田和正（时间支配者desk、少女们向荒野进发desk辅佐）原属九组，应该是《时间支配者》后跳槽过来的。龙之子最近的话，金子未来升P后接手了后藤P的美妙TV系列，吉田P应该继续弄美妙男团相关，大松裕应该有新作在做（希望别又是短篇广告）。2. W'Z这两年菊池P上位以后，社长也只挂企画不下来了。Desk宗清辉+",
                "stats": {
                    "view": 5405,
                    "favorite": 75,
                    "like": 535,
                    "dislike": 0,
                    "reply": 37,
                    "share": 13,
                    "coin": 20,
                    "dynamic": 0
                },
                "like_state": 0
            },
            {
                "id": 2640614,
                "title": "19年春季新番 动画制片人、制作主任相关",
                "state": 0,
                "publish_time": 1557303168,
                "words": 2438,
                "image_urls": [
                    "https://i0.hdslb.com/bfs/article/a04bae480bef236366fe1ee4a1aafeb7231cfdbb.jpg"
                ],
                "category": {
                    "id": 4,
                    "parent_id": 2,
                    "name": "动漫杂谈"
                },
                "categories": [
                    {
                        "id": 2,
                        "parent_id": 0,
                        "name": "动画"
                    },
                    {
                        "id": 4,
                        "parent_id": 2,
                        "name": "动漫杂谈"
                    }
                ],
                "summary": "1.贤者之孙aniP：清水优人（春原庄的管理人），此季度双开设定制作：上野雄树，初次担任设定制作，清水P一手带大的新人制作动画制作：银链2.满脑子都是XX的青酱不能恋爱aniP：清水优人（春原庄的管理人）、金子逸人（银链社长）设定制作：芳賀さなえ（初次担任设定制作）动画制作：银链这季度银链双开，基本都是春原庄庄班人员（春原庄毕竟全本社回）。银链上次改组后，清水P、鬼塚P都单独表aniP了，怎么伏见哥哥却亡了，看看下部伊莉雅有没有机会3.川柳少女aniP：中川二郎（战斗女子高校、三颗星彩色冒险），",
                "stats": {
                    "view": 4112,
                    "favorite": 48,
                    "like": 511,
                    "dislike": 0,
                    "reply": 22,
                    "share": 5,
                    "coin": 18,
                    "dynamic": 0
                },
                "like_state": 0
            }
        ],
        "author": {
            "mid": 2859372,
            "name": "名作之壁吧",
            "face": "https://i0.hdslb.com/bfs/face/e864d7968e9c9f0a6255b0a751d8eebd591434fa.jpg",
            "pendant": {
                "pid": 0,
                "name": "",
                "image": "",
                "expire": 0
            },
            "official_verify": {
                "type": 0,
                "desc": "bilibili 知名UP主"
            },
            "nameplate": {
                "nid": 8,
                "name": "知名偶像",
                "image": "https://i0.hdslb.com/bfs/face/27a952195555e64508310e366b3e38bd4cd143fc.png",
                "image_small": "https://i2.hdslb.com/bfs/face/0497be49e08357bf05bca56e33a0637a273a7610.png",
                "level": "稀有勋章",
                "condition": "所有自制视频总播放数>=100万"
            },
            "vip": {
                "type": 1,
                "status": 0,
                "due_date": 0,
                "vip_pay_type": 0,
                "theme_type": 0,
                "label": {
                    "path": "",
                    "text": "",
                    "label_theme": ""
                },
                "avatar_subscript": 0,
                "nickname_color": ""
            }
        },
        "last": {
            "id": 0,
            "title": "",
            "state": 0,
            "publish_time": 0,
            "words": 0,
            "image_urls": [],
            "category": {
                "id": 0,
                "parent_id": 0,
                "name": ""
            },
            "categories": [],
            "summary": ""
        },
        "attention": false
    }
}
```

</details>