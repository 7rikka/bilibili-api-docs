# 获取国际电话区号列表

> https://passport.bilibili.com/x/passport-login/country

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名          | 类型  | 必填  | 内容        | 备注   |
|--------------|-----|-----|-----------|------|
| appkey       | str | √   |           |      |
| build        | num |     |           |      |
| buvid        | str |     |           |      |
| c_locale     | str |     | `zh_CN`   |      |
| channel      | str |     |           |      |
| disable_rcmd | num |     |           |      |
| local_id     | str |     |           |      |
| mobi_app     | str |     | `android` |      |
| platform     | str |     | `android` |      |
| s_locale     | str |     | `zh_CN`   |      |
| statistics   | str |     |           |      |
| ts           | num | √   | 当前时间戳     | 单位：秒 |
| sign         | str | √   |           |      |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名     | 类型    | 内容   | 备注  |
|---------|-------|------|-----|
| default | obj   | 默认选中 |     |
| list    | array |      |     |

### `data`对象 -> `default`对象

| 字段名          | 类型  | 内容      | 备注  |
|--------------|-----|---------|-----|
| id           | str | 记录id    |     |
| country_code | str | 国家&地区号  |     |
| cname        | str | 国家&地区名称 |     |

### `data`对象 -> `list`数组中的对象

| 字段名          | 类型  | 内容      | 备注  |
|--------------|-----|---------|-----|
| id           | str | 记录id    |     |
| country_code | str | 国家&地区号  |     |
| cname        | str | 国家&地区名称 |     |

## 请求示例

```shell
curl -L -X GET 'https://passport.bilibili.com/x/passport-login/country?appkey=783bbb7264451d82&ts=1664980868&sign=1d4aed275c4186b82bb45046ea790e4e'
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
    "default": {
      "id": 1,
      "country_code": "86",
      "cname": "中国大陆"
    },
    "list": [
      {
        "id": 1,
        "country_code": "86",
        "cname": "中国大陆"
      },
      {
        "id": 5,
        "country_code": "852",
        "cname": "中国香港特别行政区"
      },
      {
        "id": 2,
        "country_code": "853",
        "cname": "中国澳门特别行政区"
      },
      {
        "id": 3,
        "country_code": "886",
        "cname": "中国台湾"
      },
      {
        "id": 4,
        "country_code": "1",
        "cname": "美国"
      },
      {
        "id": 6,
        "country_code": "32",
        "cname": "比利时"
      },
      {
        "id": 7,
        "country_code": "61",
        "cname": "澳大利亚"
      },
      {
        "id": 8,
        "country_code": "33",
        "cname": "法国"
      },
      {
        "id": 9,
        "country_code": "1",
        "cname": "加拿大"
      },
      {
        "id": 10,
        "country_code": "81",
        "cname": "日本"
      },
      {
        "id": 11,
        "country_code": "65",
        "cname": "新加坡"
      },
      {
        "id": 12,
        "country_code": "82",
        "cname": "韩国"
      },
      {
        "id": 13,
        "country_code": "60",
        "cname": "马来西亚"
      },
      {
        "id": 14,
        "country_code": "44",
        "cname": "英国"
      },
      {
        "id": 15,
        "country_code": "39",
        "cname": "意大利"
      },
      {
        "id": 16,
        "country_code": "49",
        "cname": "德国"
      },
      {
        "id": 18,
        "country_code": "7",
        "cname": "俄罗斯"
      },
      {
        "id": 153,
        "country_code": "1681",
        "cname": "瓦利斯群岛和富图纳群岛"
      },
      {
        "id": 152,
        "country_code": "351",
        "cname": "葡萄牙"
      },
      {
        "id": 151,
        "country_code": "680",
        "cname": "帕劳"
      },
      {
        "id": 150,
        "country_code": "672",
        "cname": "诺福克岛"
      },
      {
        "id": 149,
        "country_code": "47",
        "cname": "挪威"
      },
      {
        "id": 148,
        "country_code": "683",
        "cname": "纽埃岛"
      },
      {
        "id": 147,
        "country_code": "234",
        "cname": "尼日利亚"
      },
      {
        "id": 146,
        "country_code": "227",
        "cname": "尼日尔"
      },
      {
        "id": 145,
        "country_code": "505",
        "cname": "尼加拉瓜"
      },
      {
        "id": 144,
        "country_code": "977",
        "cname": "尼泊尔"
      },
      {
        "id": 143,
        "country_code": "674",
        "cname": "瑙鲁"
      },
      {
        "id": 154,
        "country_code": "995",
        "cname": "格鲁吉亚"
      },
      {
        "id": 155,
        "country_code": "46",
        "cname": "瑞典"
      },
      {
        "id": 165,
        "country_code": "966",
        "cname": "沙特阿拉伯"
      },
      {
        "id": 164,
        "country_code": "259",
        "cname": "桑给巴尔岛"
      },
      {
        "id": 163,
        "country_code": "248",
        "cname": "塞舌尔共和国"
      },
      {
        "id": 162,
        "country_code": "357",
        "cname": "塞浦路斯"
      },
      {
        "id": 161,
        "country_code": "221",
        "cname": "塞内加尔"
      },
      {
        "id": 160,
        "country_code": "232",
        "cname": "塞拉利昂"
      },
      {
        "id": 159,
        "country_code": "684",
        "cname": "萨摩亚，东部"
      },
      {
        "id": 158,
        "country_code": "685",
        "cname": "萨摩亚，西部"
      },
      {
        "id": 157,
        "country_code": "503",
        "cname": "萨尔瓦多"
      },
      {
        "id": 156,
        "country_code": "41",
        "cname": "瑞士"
      },
      {
        "id": 166,
        "country_code": "239",
        "cname": "圣多美和普林西比"
      },
      {
        "id": 142,
        "country_code": "381",
        "cname": "南斯拉夫"
      },
      {
        "id": 141,
        "country_code": "27",
        "cname": "南非"
      },
      {
        "id": 128,
        "country_code": "222",
        "cname": "毛里塔尼亚"
      },
      {
        "id": 127,
        "country_code": "230",
        "cname": "毛里求斯"
      },
      {
        "id": 126,
        "country_code": "692",
        "cname": "马歇尔岛"
      },
      {
        "id": 125,
        "country_code": "596",
        "cname": "马提尼克岛"
      },
      {
        "id": 124,
        "country_code": "389",
        "cname": "马其顿"
      },
      {
        "id": 123,
        "country_code": "1670",
        "cname": "马里亚纳岛"
      },
      {
        "id": 122,
        "country_code": "223",
        "cname": "马里"
      },
      {
        "id": 121,
        "country_code": "265",
        "cname": "马拉维"
      },
      {
        "id": 120,
        "country_code": "356",
        "cname": "马耳他"
      },
      {
        "id": 119,
        "country_code": "960",
        "cname": "马尔代夫"
      },
      {
        "id": 129,
        "country_code": "976",
        "cname": "蒙古"
      },
      {
        "id": 130,
        "country_code": "1664",
        "cname": "蒙特塞拉特岛"
      },
      {
        "id": 140,
        "country_code": "264",
        "cname": "纳米比亚"
      },
      {
        "id": 139,
        "country_code": "52",
        "cname": "墨西哥"
      },
      {
        "id": 138,
        "country_code": "258",
        "cname": "莫桑比克"
      },
      {
        "id": 137,
        "country_code": "377",
        "cname": "摩纳哥"
      },
      {
        "id": 136,
        "country_code": "212",
        "cname": "摩洛哥"
      },
      {
        "id": 135,
        "country_code": "373",
        "cname": "摩尔多瓦"
      },
      {
        "id": 134,
        "country_code": "95",
        "cname": "缅甸"
      },
      {
        "id": 133,
        "country_code": "691",
        "cname": "密克罗尼西亚"
      },
      {
        "id": 132,
        "country_code": "51",
        "cname": "秘鲁"
      },
      {
        "id": 131,
        "country_code": "880",
        "cname": "孟加拉国"
      },
      {
        "id": 118,
        "country_code": "261",
        "cname": "马达加斯加"
      },
      {
        "id": 167,
        "country_code": "1784",
        "cname": "圣卢西亚"
      },
      {
        "id": 216,
        "country_code": "56",
        "cname": "智利"
      },
      {
        "id": 203,
        "country_code": "1876",
        "cname": "牙买加"
      },
      {
        "id": 202,
        "country_code": "963",
        "cname": "叙利亚"
      },
      {
        "id": 201,
        "country_code": "36",
        "cname": "匈牙利"
      },
      {
        "id": 200,
        "country_code": "225",
        "cname": "科特迪瓦"
      },
      {
        "id": 199,
        "country_code": "30",
        "cname": "希腊"
      },
      {
        "id": 198,
        "country_code": "34",
        "cname": "西班牙"
      },
      {
        "id": 197,
        "country_code": "998",
        "cname": "乌兹别克斯坦"
      },
      {
        "id": 196,
        "country_code": "598",
        "cname": "乌拉圭"
      },
      {
        "id": 195,
        "country_code": "380",
        "cname": "乌克兰"
      },
      {
        "id": 194,
        "country_code": "256",
        "cname": "乌干达"
      },
      {
        "id": 204,
        "country_code": "374",
        "cname": "亚美尼亚"
      },
      {
        "id": 205,
        "country_code": "967",
        "cname": "也门"
      },
      {
        "id": 215,
        "country_code": "350",
        "cname": "直布罗陀"
      },
      {
        "id": 214,
        "country_code": "235",
        "cname": "乍得"
      },
      {
        "id": 213,
        "country_code": "260",
        "cname": "赞比亚"
      },
      {
        "id": 212,
        "country_code": "84",
        "cname": "越南"
      },
      {
        "id": 211,
        "country_code": "962",
        "cname": "约旦"
      },
      {
        "id": 210,
        "country_code": "62",
        "cname": "印尼"
      },
      {
        "id": 209,
        "country_code": "91",
        "cname": "印度"
      },
      {
        "id": 208,
        "country_code": "972",
        "cname": "以色列"
      },
      {
        "id": 207,
        "country_code": "98",
        "cname": "伊朗"
      },
      {
        "id": 206,
        "country_code": "964",
        "cname": "伊拉克"
      },
      {
        "id": 193,
        "country_code": "673",
        "cname": "文莱"
      },
      {
        "id": 192,
        "country_code": "58",
        "cname": "委内瑞拉"
      },
      {
        "id": 191,
        "country_code": "1284",
        "cname": "维珍群岛(英属)"
      },
      {
        "id": 178,
        "country_code": "66",
        "cname": "泰国"
      },
      {
        "id": 177,
        "country_code": "252",
        "cname": "索马里"
      },
      {
        "id": 176,
        "country_code": "677",
        "cname": "所罗门群岛"
      },
      {
        "id": 175,
        "country_code": "597",
        "cname": "苏里南"
      },
      {
        "id": 174,
        "country_code": "249",
        "cname": "苏丹"
      },
      {
        "id": 173,
        "country_code": "268",
        "cname": "斯威士兰"
      },
      {
        "id": 172,
        "country_code": "386",
        "cname": "斯洛文尼亚"
      },
      {
        "id": 171,
        "country_code": "421",
        "cname": "斯洛伐克"
      },
      {
        "id": 170,
        "country_code": "94",
        "cname": "斯里兰卡"
      },
      {
        "id": 169,
        "country_code": "508",
        "cname": "圣皮埃尔和密克隆群岛"
      },
      {
        "id": 179,
        "country_code": "255",
        "cname": "坦桑尼亚"
      },
      {
        "id": 180,
        "country_code": "676",
        "cname": "汤加"
      },
      {
        "id": 190,
        "country_code": "1340",
        "cname": "维珍群岛(美属)"
      },
      {
        "id": 189,
        "country_code": "678",
        "cname": "瓦努阿图"
      },
      {
        "id": 188,
        "country_code": "690",
        "cname": "托克劳岛"
      },
      {
        "id": 187,
        "country_code": "993",
        "cname": "土库曼斯坦"
      },
      {
        "id": 186,
        "country_code": "90",
        "cname": "土耳其"
      },
      {
        "id": 185,
        "country_code": "688",
        "cname": "图瓦卢"
      },
      {
        "id": 184,
        "country_code": "216",
        "cname": "突尼斯"
      },
      {
        "id": 183,
        "country_code": "247",
        "cname": "阿森松岛"
      },
      {
        "id": 182,
        "country_code": "1868",
        "cname": "特立尼达和多巴哥"
      },
      {
        "id": 181,
        "country_code": "1649",
        "cname": "特克斯和凯科斯"
      },
      {
        "id": 168,
        "country_code": "378",
        "cname": "圣马力诺"
      },
      {
        "id": 67,
        "country_code": "594",
        "cname": "法属圭亚那"
      },
      {
        "id": 54,
        "country_code": "975",
        "cname": "不丹"
      },
      {
        "id": 53,
        "country_code": "267",
        "cname": "博茨瓦纳"
      },
      {
        "id": 52,
        "country_code": "501",
        "cname": "伯利兹"
      },
      {
        "id": 51,
        "country_code": "591",
        "cname": "玻利维亚"
      },
      {
        "id": 50,
        "country_code": "48",
        "cname": "波兰"
      },
      {
        "id": 49,
        "country_code": "387",
        "cname": "波黑"
      },
      {
        "id": 48,
        "country_code": "1787",
        "cname": "波多黎各"
      },
      {
        "id": 47,
        "country_code": "354",
        "cname": "冰岛"
      },
      {
        "id": 46,
        "country_code": "229",
        "cname": "贝宁"
      },
      {
        "id": 45,
        "country_code": "359",
        "cname": "保加利亚"
      },
      {
        "id": 55,
        "country_code": "226",
        "cname": "布基纳法索"
      },
      {
        "id": 56,
        "country_code": "257",
        "cname": "布隆迪"
      },
      {
        "id": 66,
        "country_code": "689",
        "cname": "法属波利尼西亚"
      },
      {
        "id": 65,
        "country_code": "298",
        "cname": "法罗岛"
      },
      {
        "id": 64,
        "country_code": "291",
        "cname": "厄立特里亚"
      },
      {
        "id": 63,
        "country_code": "593",
        "cname": "厄瓜多尔"
      },
      {
        "id": 62,
        "country_code": "1809",
        "cname": "多米尼加代表"
      },
      {
        "id": 61,
        "country_code": "1767",
        "cname": "多米尼加"
      },
      {
        "id": 60,
        "country_code": "228",
        "cname": "多哥"
      },
      {
        "id": 59,
        "country_code": "246",
        "cname": "迪戈加西亚岛"
      },
      {
        "id": 58,
        "country_code": "45",
        "cname": "丹麦"
      },
      {
        "id": 57,
        "country_code": "240",
        "cname": "赤道几内亚"
      },
      {
        "id": 44,
        "country_code": "1441",
        "cname": "百慕大群岛"
      },
      {
        "id": 43,
        "country_code": "375",
        "cname": "白俄罗斯"
      },
      {
        "id": 42,
        "country_code": "55",
        "cname": "巴西"
      },
      {
        "id": 29,
        "country_code": "353",
        "cname": "爱尔兰"
      },
      {
        "id": 28,
        "country_code": "251",
        "cname": "埃塞俄比亚"
      },
      {
        "id": 27,
        "country_code": "20",
        "cname": "埃及"
      },
      {
        "id": 26,
        "country_code": "994",
        "cname": "阿塞拜疆"
      },
      {
        "id": 25,
        "country_code": "968",
        "cname": "阿曼"
      },
      {
        "id": 24,
        "country_code": "971",
        "cname": "阿联酋"
      },
      {
        "id": 23,
        "country_code": "54",
        "cname": "阿根廷"
      },
      {
        "id": 22,
        "country_code": "93",
        "cname": "阿富汗"
      },
      {
        "id": 21,
        "country_code": "213",
        "cname": "阿尔及利亚"
      },
      {
        "id": 20,
        "country_code": "355",
        "cname": "阿尔巴尼亚"
      },
      {
        "id": 30,
        "country_code": "372",
        "cname": "爱沙尼亚"
      },
      {
        "id": 31,
        "country_code": "376",
        "cname": "安道尔"
      },
      {
        "id": 41,
        "country_code": "507",
        "cname": "巴拿马"
      },
      {
        "id": 40,
        "country_code": "973",
        "cname": "巴林"
      },
      {
        "id": 39,
        "country_code": "595",
        "cname": "巴拉圭"
      },
      {
        "id": 38,
        "country_code": "92",
        "cname": "巴基斯坦"
      },
      {
        "id": 37,
        "country_code": "1242",
        "cname": "巴哈马群岛"
      },
      {
        "id": 36,
        "country_code": "675",
        "cname": "巴布亚新几内亚"
      },
      {
        "id": 35,
        "country_code": "1246",
        "cname": "巴巴多斯"
      },
      {
        "id": 34,
        "country_code": "43",
        "cname": "奥地利"
      },
      {
        "id": 33,
        "country_code": "1268",
        "cname": "安提瓜岛和巴布达"
      },
      {
        "id": 32,
        "country_code": "244",
        "cname": "安哥拉"
      },
      {
        "id": 19,
        "country_code": "64",
        "cname": "新西兰"
      },
      {
        "id": 68,
        "country_code": "236",
        "cname": "非洲中部"
      },
      {
        "id": 117,
        "country_code": "40",
        "cname": "罗马尼亚"
      },
      {
        "id": 104,
        "country_code": "965",
        "cname": "科威特"
      },
      {
        "id": 103,
        "country_code": "269",
        "cname": "科摩罗"
      },
      {
        "id": 102,
        "country_code": "1345",
        "cname": "开曼群岛"
      },
      {
        "id": 101,
        "country_code": "974",
        "cname": "卡塔尔"
      },
      {
        "id": 100,
        "country_code": "237",
        "cname": "喀麦隆"
      },
      {
        "id": 99,
        "country_code": "262",
        "cname": "聚会岛"
      },
      {
        "id": 98,
        "country_code": "263",
        "cname": "津巴布韦"
      },
      {
        "id": 97,
        "country_code": "420",
        "cname": "捷克"
      },
      {
        "id": 96,
        "country_code": "855",
        "cname": "柬埔寨"
      },
      {
        "id": 95,
        "country_code": "241",
        "cname": "加蓬"
      },
      {
        "id": 105,
        "country_code": "385",
        "cname": "克罗地亚"
      },
      {
        "id": 106,
        "country_code": "254",
        "cname": "肯尼亚"
      },
      {
        "id": 116,
        "country_code": "250",
        "cname": "卢旺达"
      },
      {
        "id": 115,
        "country_code": "352",
        "cname": "卢森堡"
      },
      {
        "id": 114,
        "country_code": "218",
        "cname": "利比亚"
      },
      {
        "id": 113,
        "country_code": "231",
        "cname": "利比里亚"
      },
      {
        "id": 112,
        "country_code": "370",
        "cname": "立陶宛"
      },
      {
        "id": 111,
        "country_code": "961",
        "cname": "黎巴嫩"
      },
      {
        "id": 110,
        "country_code": "856",
        "cname": "老挝"
      },
      {
        "id": 109,
        "country_code": "266",
        "cname": "莱索托"
      },
      {
        "id": 108,
        "country_code": "371",
        "cname": "拉脱维亚"
      },
      {
        "id": 107,
        "country_code": "682",
        "cname": "库克岛"
      },
      {
        "id": 94,
        "country_code": "233",
        "cname": "加纳"
      },
      {
        "id": 93,
        "country_code": "245",
        "cname": "几内亚比绍"
      },
      {
        "id": 92,
        "country_code": "224",
        "cname": "几内亚"
      },
      {
        "id": 79,
        "country_code": "1473",
        "cname": "格林纳达"
      },
      {
        "id": 78,
        "country_code": "506",
        "cname": "哥斯达黎加"
      },
      {
        "id": 77,
        "country_code": "57",
        "cname": "哥伦比亚"
      },
      {
        "id": 76,
        "country_code": "243",
        "cname": "刚果(金)"
      },
      {
        "id": 75,
        "country_code": "242",
        "cname": "刚果"
      },
      {
        "id": 74,
        "country_code": "220",
        "cname": "冈比亚"
      },
      {
        "id": 73,
        "country_code": "500",
        "cname": "福克兰岛"
      },
      {
        "id": 72,
        "country_code": "238",
        "cname": "佛得角"
      },
      {
        "id": 71,
        "country_code": "358",
        "cname": "芬兰"
      },
      {
        "id": 70,
        "country_code": "679",
        "cname": "斐济"
      },
      {
        "id": 80,
        "country_code": "299",
        "cname": "格陵兰岛"
      },
      {
        "id": 81,
        "country_code": "53",
        "cname": "古巴"
      },
      {
        "id": 91,
        "country_code": "996",
        "cname": "吉尔吉斯斯坦"
      },
      {
        "id": 90,
        "country_code": "253",
        "cname": "吉布提"
      },
      {
        "id": 89,
        "country_code": "686",
        "cname": "基里巴斯"
      },
      {
        "id": 88,
        "country_code": "1808",
        "cname": "维克岛"
      },
      {
        "id": 87,
        "country_code": "504",
        "cname": "洪都拉斯"
      },
      {
        "id": 86,
        "country_code": "31",
        "cname": "荷兰"
      },
      {
        "id": 85,
        "country_code": "850",
        "cname": "朝鲜"
      },
      {
        "id": 84,
        "country_code": "509",
        "cname": "海地"
      },
      {
        "id": 83,
        "country_code": "1671",
        "cname": "关岛"
      },
      {
        "id": 82,
        "country_code": "590",
        "cname": "瓜德罗普岛"
      },
      {
        "id": 69,
        "country_code": "63",
        "cname": "菲律宾"
      }
    ]
  }
}
```

</details>