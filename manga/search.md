# 漫画搜索（APP端）

> https://manga.bilibili.com/twirp/search.v1.Search/SearchKeyword

请求方式：`POST`

是否需要登录：`否`

Content-Type：`application/json`

## JSON参数

| 参数名      | 类型  | 必填 | 内容    | 备注 |
|----------|-----|----|-------|----|
| keyword  | str |    | 搜索关键词 |    |
| pageNum  | num |    | 页数    |    |
| pageSize | num |    | 分页大小  |    |

## Json回复

### 根对象

| 字段名  | 类型  | 内容   | 备注   |
|------|-----|------|------|
| code | num | 响应码  | 0：成功 |
| msg  | str |      |      |
| data | obj | 信息本体 |      |

### `data`对象

| 字段名        | 类型  | 内容   | 备注 |
|------------|-----|------|----|
| comic_data | obj | 漫画信息 |    |
| novel_data | obj | 小说信息 |    |

### `data`对象 -> `comic_data`对象

| 字段名        | 类型    | 内容     | 备注 |
|------------|-------|--------|----|
| list       | array | 漫画信息列表 |    |
| total_page | num   |        |    |
| total_num  | num   | 搜索总条数  |    |
| recommends | array |        |    |
| similar    | str   |        |    |
| jump       | null  |        |    |
| se_id      | str   |        |    |
| banner     | obj   |        |    |

### `data`对象 -> `comic_data`对象 -> `list`数组中的对象

| 字段名             | 类型    | 内容   | 备注              |
|-----------------|-------|------|-----------------|
| id              | num   | 漫画id |                 |
| title           | str   | 显示标题 |                 |
| square_cover    | str   | 方形封面 |                 |
| vertical_cover  | str   | 纵向封面 |                 |
| author_name     | array | 作者名称 |                 |
| styles          | array | 漫画风格 |                 |
| is_finish       | num   | 是否完结 | 0：未完结<br/>1：已完结 |
| allow_wait_free | bool  |      |                 |
| discount_type   | num   |      |                 |
| type            | num   |      |                 |
| wiki            | obj   |      |                 |

### `data`对象 -> `comic_data`对象 -> `list`数组中的对象 -> `author_name`数组中的对象

| 字段名 | 类型 | 内容 | 备注 |
|-----|----|----|----|

### `data`对象 -> `comic_data`对象 -> `list`数组中的对象 -> `styles`数组中的对象

| 字段名 | 类型 | 内容 | 备注 |
|-----|----|----|----|

### `data`对象 -> `comic_data`对象 -> `list`数组中的对象 -> `wiki`对象

| 字段名            | 类型    | 内容 | 备注 |
|----------------|-------|----|----|
| id             | num   |    |    |
| title          | str   |    |    |
| origin_title   | str   |    |    |
| vertical_cover | str   |    |    |
| producer       | str   |    |    |
| author_name    | array |    |    |
| publish_time   | str   |    |    |
| frequency      | str   |    |    |

### `data`对象 -> `comic_data`对象 -> `list`数组中的对象 -> `wiki`对象 -> `author_name`数组中的对象

| 字段名 | 类型 | 内容 | 备注 |
|-----|----|----|----|

### `data`对象 -> `comic_data`对象 -> `banner`对象

| 字段名   | 类型  | 内容 | 备注 |
|-------|-----|----|----|
| icon  | str |    |    |
| title | str |    |    |
| url   | str |    |    |

### `data`对象 -> `novel_data`对象

| 字段名   | 类型    | 内容 | 备注 |
|-------|-------|----|----|
| total | num   |    |    |
| list  | array |    |    |

### `data`对象 -> `novel_data`对象 -> `list`数组中的对象

| 字段名           | 类型  | 内容 | 备注 |
|---------------|-----|----|----|
| novel_id      | num |    |    |
| title         | str |    |    |
| v_cover       | str |    |    |
| finish_status | num |    |    |
| status        | num |    |    |
| discount_type | num |    |    |
| numbers       | num |    |    |
| style         | obj |    |    |
| evaluate      | str |    |    |
| author        | str |    |    |

### `data`对象 -> `novel_data`对象 -> `list`数组中的对象 -> `style`对象

| 字段名  | 类型  | 内容 | 备注 |
|------|-----|----|----|
| id   | num |    |    |
| name | str |    |    |

## 请求示例

```shell
curl -L -X POST 'https://manga.bilibili.com/twirp/search.v1.Search/SearchKeyword' \
-H 'content-type: application/json; charset=utf-8' \
--data-raw '{"keyword":"孤独摇滚","pageNum":1,"pageSize":20}'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json
{
  "code": 0,
  "msg": "",
  "data": {
    "comic_data": {
      "list": [
        {
          "id": 29763,
          "title": "<em class=\"keyword\">孤独摇滚!</em>",
          "square_cover": "https://i0.hdslb.com/bfs/manga-static/cdd62626f24669fb32afdbed51ab886c6c726906.jpg",
          "vertical_cover": "https://i0.hdslb.com/bfs/manga-static/a5d57f7886af467f6a2e2a74db6b44928bc99fdf.jpg",
          "author_name": [
            "浜路晶",
            "芳文社"
          ],
          "styles": [
            "都市"
          ],
          "is_finish": 0,
          "allow_wait_free": false,
          "discount_type": 0,
          "type": 0,
          "wiki": {
            "id": 0,
            "title": "",
            "origin_title": "",
            "vertical_cover": "",
            "producer": "",
            "author_name": [
              "浜路晶",
              "芳文社"
            ],
            "publish_time": "",
            "frequency": ""
          }
        },
        {
          "id": 24545,
          "title": "<em class=\"keyword\">孤</em><em class=\"keyword\">独</em>的小象",
          "square_cover": "http://i0.hdslb.com/bfs/bangumi/7361583ff59064e9fd6132456a5fc8247352406d.jpg",
          "vertical_cover": "http://i0.hdslb.com/bfs/bangumi/1a9961ec0a56e4d67dae8ff7435275f67431bbff.jpg",
          "author_name": [
            "火山映画"
          ],
          "styles": [
            "现代"
          ],
          "is_finish": 1,
          "allow_wait_free": false,
          "discount_type": 0,
          "type": 0,
          "wiki": {
            "id": 0,
            "title": "",
            "origin_title": "",
            "vertical_cover": "",
            "producer": "",
            "author_name": [
              "火山映画"
            ],
            "publish_time": "",
            "frequency": ""
          }
        },
        {
          "id": 26065,
          "title": "寂寞的阔少",
          "square_cover": "http://i0.hdslb.com/bfs/manga-static/dfc60dd5d0b420d61545ec31ae58154c7ccfb4f4.jpg",
          "vertical_cover": "http://i0.hdslb.com/bfs/manga-static/d445f6074a5bc5caeb22dfb6fda09bae51f09a3e.jpg",
          "author_name": [
            "秋乃七海",
            "禾林"
          ],
          "styles": [
            "西幻"
          ],
          "is_finish": 1,
          "allow_wait_free": false,
          "discount_type": 0,
          "type": 0,
          "wiki": {
            "id": 0,
            "title": "",
            "origin_title": "",
            "vertical_cover": "",
            "producer": "",
            "author_name": [
              "秋乃七海",
              "禾林"
            ],
            "publish_time": "",
            "frequency": ""
          }
        },
        {
          "id": 29588,
          "title": "旅途的蓝与幻想",
          "square_cover": "https://i0.hdslb.com/bfs/manga-static/25cda2b93432eafd1a5a28561f2b50cfac461e10.jpg",
          "vertical_cover": "https://i0.hdslb.com/bfs/manga-static/3d676173a0438594b40996326598093ab2ad0935.jpg",
          "author_name": [
            "<em class=\"keyword\">孤</em><em class=\"keyword\">独</em>的guan测者"
          ],
          "styles": [
            "西幻"
          ],
          "is_finish": 0,
          "allow_wait_free": false,
          "discount_type": 0,
          "type": 0,
          "wiki": {
            "id": 0,
            "title": "",
            "origin_title": "",
            "vertical_cover": "",
            "producer": "",
            "author_name": [
              "<em class=\"keyword\">孤</em><em class=\"keyword\">独</em>的guan测者"
            ],
            "publish_time": "",
            "frequency": ""
          }
        },
        {
          "id": 30190,
          "title": "<em class=\"keyword\">孤</em><em class=\"keyword\">独</em>精灵医师的诊察记录~圣女骑士团和治愈奇迹~",
          "square_cover": "https://i0.hdslb.com/bfs/manga-static/bbc887817f13a43d5ff0644e4060965c12650a07.jpg",
          "vertical_cover": "https://i0.hdslb.com/bfs/manga-static/d41a0c2f34e2055bbc265c06c80252e9e174eee6.jpg",
          "author_name": [
            "橘由宇",
            "十话",
            "角川集团"
          ],
          "styles": [
            "奇幻"
          ],
          "is_finish": 0,
          "allow_wait_free": false,
          "discount_type": 0,
          "type": 0,
          "wiki": {
            "id": 0,
            "title": "",
            "origin_title": "",
            "vertical_cover": "",
            "producer": "",
            "author_name": [
              "橘由宇",
              "十话",
              "角川集团"
            ],
            "publish_time": "",
            "frequency": ""
          }
        }
      ],
      "total_page": 0,
      "total_num": 5,
      "recommends": [],
      "similar": "",
      "jump": null,
      "se_id": "52177a42b3950471",
      "banner": {
        "icon": "",
        "title": "",
        "url": ""
      }
    },
    "novel_data": {
      "total": 84,
      "list": [
        {
          "novel_id": 10865,
          "title": "亿万<em class=\"keyword\">孤</em><em class=\"keyword\">独</em>",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/3644581ee29c6e994b62655954d5c63d69534e3b.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 447561,
          "style": {
            "id": 261,
            "name": "都市"
          },
          "evaluate": "邻居和亲戚们也不与他们家来往，他感到了极度<em class=\"keyword\">孤独</em>，\n他一度想在险峻的华山上独自离去，幸亏遇见了一对身患绝症的中年夫妻，女儿也刚因白血病去世。",
          "author": "雨正浓"
        },
        {
          "novel_id": 11642,
          "title": "超级系统我在异界有座城",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/0a8f47e11937a35452dc141b6495919b6d95269e.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 309888,
          "style": {
            "id": 237,
            "name": "玄幻"
          },
          "evaluate": "比如你会看到一群精灵正在打着麻将，牛头人正唱着<em class=\"keyword\">摇滚</em>乐队的歌曲，还有那些天天买着彩票，妄图中一等奖的地精。\n《简介无力，请看正文。》\n推荐两本老书。\n《僵尸至尊纵横异界》《超级APP三界神仙斗地主》！",
          "author": "惜缘1314"
        },
        {
          "novel_id": 5063,
          "title": "逃离深渊",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/da4768443cdac483c16cbab50ae7f103d09c10d7.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 1005876,
          "style": {
            "id": 261,
            "name": "都市"
          },
          "evaluate": "尽管被命运抛弃，哪怕被孑然一身，所幸还有<em class=\"keyword\">孤独</em>作伴。一个来自猛鬼地狱的小男孩，爬出了深渊，却无法逃离命运的牵绊，努力逃出命运的魔爪，渴望融入平凡的世界，可惜，这并不是他脱离<em class=\"keyword\">孤独</em>的理由。",
          "author": "麦浪摆渡人"
        },
        {
          "novel_id": 776,
          "title": "异界逍遥游",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/ee788892f62ebc94933e0c668a13e0aec97a854e.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 165005,
          "style": {
            "id": 237,
            "name": "玄幻"
          },
          "evaluate": "<em class=\"keyword\">孤独</em>水寒，一个来自于二十一世纪星球的后生小子，在睡觉中居然神奇的穿越道了另一个世界：“修炼之境”，这是一个修炼武的世界，只有不断的修炼才能成为一个强者。",
          "author": "抚琴的琴"
        },
        {
          "novel_id": 12789,
          "title": "无上仙尊重生玄幻",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/64b33ddb0eea96f878268ce04e168818a7472b28.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 132164,
          "style": {
            "id": 237,
            "name": "玄幻"
          },
          "evaluate": "仙人魔念转世重生\n这一世，不求长生<em class=\"keyword\">孤独</em>，只求逍遥！",
          "author": "慢一步疯子"
        },
        {
          "novel_id": 10540,
          "title": "第三人格",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/2947968fc7a9a96b5486d8d331d90da76c452b2d.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 500811,
          "style": {
            "id": 242,
            "name": "奇幻"
          },
          "evaluate": "镜子里的怪物 穿着与我同样的衣服 他向我诉说的是无尽的<em class=\"keyword\">孤独</em> ​​​…",
          "author": "奈何孤人"
        },
        {
          "novel_id": 6202,
          "title": "人本来就是<em class=\"keyword\">孤</em><em class=\"keyword\">独</em>",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/d54bc8ce3fbcfb793715f5488bec5ef9158dcbe8.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 320717,
          "style": {
            "id": 20,
            "name": "都市青春"
          },
          "evaluate": "所谓人生，要么把人心掏空，要么使人心发疯。",
          "author": "昼眠"
        },
        {
          "novel_id": 477,
          "title": "暖之爱",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/bbaffbf02185c9ab8d5335c104d7b096e33a3d50.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 173360,
          "style": {
            "id": 20,
            "name": "都市青春"
          },
          "evaluate": "凌风和韩菲只是艺人与制作人关系而已，凌风很受韩菲的照顾，给了他极大的信心要在<em class=\"keyword\">摇滚</em>之都的终极对决上取的胜利。",
          "author": "洛儿"
        },
        {
          "novel_id": 11585,
          "title": "伴月记",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/a7af56b880d7bf2e3db32e005e0c7d5729ae6017.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 319852,
          "style": {
            "id": 261,
            "name": "都市"
          },
          "evaluate": "最明亮的便是月球，<em class=\"keyword\">孤独</em>？自有陪伴相守的人！日月星辰，生死相依，这故事好长，好长……",
          "author": "凤飞凰随"
        },
        {
          "novel_id": 5978,
          "title": "盛夏秋实",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/7a0358e8e004e1be76df80bfcae575788b1f0687.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 429538,
          "style": {
            "id": 20,
            "name": "都市青春"
          },
          "evaluate": "在同一公司没有更多交流的两个人，因为一次不可预料的英雄救“美”，由此开始了一场关于三个<em class=\"keyword\">孤独</em>之人的寂寞盛宴。",
          "author": "云后夕阳"
        },
        {
          "novel_id": 430,
          "title": "突然的爱很幸福",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/45b3707e6fb27ddee8247bd4abad29cc434f9f4d.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 161333,
          "style": {
            "id": 20,
            "name": "都市青春"
          },
          "evaluate": "那一天，天气很好，突然，走来了一个25岁上下的靓女，这个女人叫做<em class=\"keyword\">孤独</em>琦琦，不但长得漂亮，还性感迷人，身材很好啊。",
          "author": "水波荡漾"
        },
        {
          "novel_id": 6147,
          "title": "无缝地带",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/ddfff9c5194004610afa003308290c9eec2509da.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 345652,
          "style": {
            "id": 261,
            "name": "都市"
          },
          "evaluate": "这不是一个谍战故事，而是一个多重身份的共产党员超级特工林重，在泯灭人性之地进行潜伏和抗日放火的<em class=\"keyword\">孤独</em>的、多面的间谍生涯和矛盾人性。",
          "author": "李枭"
        },
        {
          "novel_id": 4268,
          "title": "蛮荒崛起",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/f3973a250b8524b467eb856ebce7a4126b1f8b12.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 216241,
          "style": {
            "id": 237,
            "name": "玄幻"
          },
          "evaluate": "上古的传说，诸神的迷局，神墟中的禁地……\n当第五<em class=\"keyword\">孤独</em>站在蛮荒之巅，抬眼域外，才发现，所谓蛮荒，不过是牢笼而已。\n征伐，才刚刚开始！",
          "author": "问荒"
        },
        {
          "novel_id": 8914,
          "title": "永生战神",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/f8584926bfde927c9ba0da5e146708d8e2486a8b.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 916536,
          "style": {
            "id": 237,
            "name": "玄幻"
          },
          "evaluate": "世间沧桑轮回，看着人类生生死死，他却不死不伤不老不灭，万年<em class=\"keyword\">孤独</em>是他的诅咒，傲世九重，逆天而行，最终他只是想要一个陪伴他的同类而已……",
          "author": "逆流"
        },
        {
          "novel_id": 11013,
          "title": "妖怪售卖店",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/641c2446fc355cb216ef0b80d42441ff9a49a125.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 414493,
          "style": {
            "id": 261,
            "name": "都市"
          },
          "evaluate": "你可相信前世，你可愿意预见未来，你可想摆脱命运；说起来你可能不信，这个世界上有妖怪存在；这是一部基于爱情，推理，奇幻于一体的小说，你可愿意<em class=\"keyword\">孤独</em>",
          "author": "洛祁枫"
        },
        {
          "novel_id": 13607,
          "title": "再度囧婚",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/9bdf8615d712d14befb5426010dd925c07f469d2.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 1012817,
          "style": {
            "id": 20,
            "name": "都市青春"
          },
          "evaluate": "芹芹想回头，但恋爱现实让她越走越远……\n几个恋爱情人寻花问柳，让她感到<em class=\"keyword\">孤独</em>，对以往情人眷恋。。。。。，他们能否死复燃。。。。。。\n昨天大学生活刚强的她，今日已经变得柔弱。。。。。",
          "author": "石胜明"
        },
        {
          "novel_id": 1183,
          "title": "葬你入棺",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/1240865a32515533253afeaca971582667bd65f6.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 767288,
          "style": {
            "id": 261,
            "name": "都市"
          },
          "evaluate": "自一出生，我就是“棺材仔”冥冥中注定我<em class=\"keyword\">孤独</em>一生。 棺材铺里阴气重，所以我单身了20年。 可却阴差阳错，娶得一千金小姐，乃是鬼妻， 我的人生观，瞬间崩溃了....",
          "author": "半饮残酒"
        },
        {
          "novel_id": 15816,
          "title": "甜妻要乖：不良总裁请走开",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/8f72d4fb5855193dd1a1a71609ad7fd03b2439e0.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 300081,
          "style": {
            "id": 20,
            "name": "都市青春"
          },
          "evaluate": "本来抱着<em class=\"keyword\">孤独</em>终老的心，却被人“骗”婚。\n只是这个老公怎么有点怪？\n苏小白怒斥着躺在床上的某人：“你干什么？不要忘了我们的约法三章！”\n某人一脸无辜：“乖，做戏要做得像一点，不然会露馅的。”",
          "author": "南途"
        },
        {
          "novel_id": 5364,
          "title": "天际",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/54c96e36d788c99503a9d0eade3ee6161bbf03e9.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 783746,
          "style": {
            "id": 2,
            "name": "古代言情"
          },
          "evaluate": "可任他一世风骨、一生<em class=\"keyword\">孤独</em>——到头来，也怕动了情。被拐卖的少女与天际史上最伟大的法师",
          "author": "校长是亲妈"
        },
        {
          "novel_id": 1079,
          "title": "女神的极品护卫",
          "v_cover": "https://i0.hdslb.com/bfs/manga-static/8e85e0d8771522b4c3d1df01642cbcdfeebd3769.jpg",
          "finish_status": 2,
          "status": 1,
          "discount_type": 0,
          "numbers": 1858579,
          "style": {
            "id": 261,
            "name": "都市"
          },
          "evaluate": "九死一生回到都市，林<em class=\"keyword\">孤独</em>来到凤城，准备照顾好兄弟的姐姐，弥补内心的痛苦，却接到老家伙的命令，让他成了美女总裁的贴身保镖，本以为轻松搞定的任务，却不想牵扯出一个巨大的阴谋…… 且看小保镖如何称霸华夏，走向世界",
          "author": "心不载马"
        }
      ]
    }
  }
}
```

</details>