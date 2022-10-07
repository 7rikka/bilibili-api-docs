# 获取视频播放流

> https://api.snm0516.aisee.tv/x/tv/playurl

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名              | 类型   | 必填  | 内容                 | 备注                     |
|------------------|------|-----|--------------------|------------------------|
| access_key       | str  |     |                    |                        |
| appkey           | str  |     |                    |                        |
| brand            | str  |     |                    |                        |
| build            | num  | √   | `105400`           | 不填只会获得durl             |
| channel          | str  |     |                    |                        |
| cid              | num  | √   | 视频cid              |                        |
| cpu              | str  |     |                    |                        |
| device_name      | str  |     |                    |                        |
| drm_tech_type    | num  |     |                    |                        |
| explor_attr      | num  |     |                    |                        |
| fnval            | num  | √   |                    |                        |
| fnver            | num  |     |                    |                        |
| force_host       | num  |     |                    |                        |
| fourk            | num  |     |                    |                        |
| from_outside     | num  |     |                    |                        |
| guest_access_key | str  |     |                    |                        |
| guest_id         | num  |     |                    |                        |
| memory           | num  |     |                    |                        |
| mobi_app         | str  | √   | 固定值：android_tv_yst | 不填只会获得durl             |
| mode_switch      | bool |     |                    |                        |
| model            | str  |     |                    |                        |
| mpi_id           | str  |     |                    |                        |
| mpi_model        | str  |     |                    |                        |
| mpi_type         | str  |     |                    |                        |
| object_id        | num  |     |                    |                        |
| platform         | str  | √   | 固定值：`android`      | 不传会报-10403错误。。后台代码写错了？ |
| playurl_type     | num  | √   | 固定值：`2`            |                        |
| qn               | num  | √   | 最高清晰度编号            |                        |
| resource_id      | str  |     |                    |                        |
| source_type      | num  |     |                    |                        |
| statistics       | str  |     |                    |                        |
| sys_ver          | num  |     |                    |                        |
| teenager_mode    | num  |     |                    |                        |
| ts               | num  |     |                    |                        |
| tv_brand         | str  |     |                    |                        |
| uid              | num  |     |                    |                        |
| sign             | str  |     |                    |                        |

## FORM参数

| 参数名 | 类型  | 必填  | 内容  | 备注  |
|-----|-----|-----|-----|-----|
| xxx | str |     |     |     |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                      |
|---------|-----|------|-----------------------------------------|
| code    | num | 响应码  | 0：成功<br/>-10403：啊哦。。该内容不支持Android平台播放哦！ |
| message | str | 0    |                                         |
| ttl     | num | 1    |                                         |
| data    | obj | 信息本体 |                                         |

### `data`对象

| 字段名 | 类型  | 内容  | 备注  |
|-----|-----|-----|-----|
| xxx | str |     |     |

## 请求示例

```shell

```

## 响应示例

<details>
<summary>点击查看</summary>

```json

```
</details>