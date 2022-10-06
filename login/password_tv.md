# 获取公钥和盐值

> https://passport.snm0516.aisee.tv/x/passport-tv-login/key

请求方式：`GET`

是否需要登录：`否`

## URL参数

| 参数名               | 类型   | 必填  | 内容    | 备注   |
|-------------------|------|-----|-------|------|
| appkey            | str  |     |       |      |
| bili_local_id     | str  |     |       |      |
| brand             | str  |     |       |      |
| build             | num  |     |       |      |
| buvid             | str  |     |       |      |
| channel           | str  |     |       |      |
| cpu               | str  |     |       |      |
| device            | str  |     |       |      |
| device_id         | str  |     |       |      |
| device_name       | str  |     |       |      |
| device_platform   | str  |     |       |      |
| explor_attr       | num  |     |       |      |
| fingerprint       | str  |     |       |      |
| fourk             | num  |     |       |      |
| guest_access_key  | str  |     |       |      |
| guest_id          | num  |     |       |      |
| guid              | str  |     |       |      |
| local_fingerprint | str  |     |       |      |
| local_id          | str  |     |       |      |
| memory            | num  |     |       |      |
| mobi_app          | str  |     |       |      |
| mode_switch       | bool |     |       |      |
| model             | str  |     |       |      |
| mpi_id            | str  |     |       |      |
| mpi_model         | str  |     |       |      |
| mpi_type          | str  |     |       |      |
| networkstate      | str  |     |       |      |
| platform          | str  |     |       |      |
| resource_id       | str  |     |       |      |
| statistics        | str  |     |       |      |
| sys_ver           | num  |     |       |      |
| teenager_mode     | num  |     |       |      |
| ts                | num  |     | 当前时间戳 | 单位：秒 |
| tv_brand          | str  |     |       |      |
| uid               | num  |     |       |      |
| sign              | str  |     |       |      |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注   |
|---------|-----|------|------|
| code    | num | 响应码  | 0：成功 |
| message | str | 0    |      |
| ttl     | num | 1    |      |
| data    | obj | 信息本体 |      |

### `data`对象

| 字段名  | 类型  | 内容     | 备注  |
|------|-----|--------|-----|
| hash | str | 密码盐值   |     |
| key  | str | rsa 公钥 |     |

## 请求示例

```shell
curl -L -X GET 'https://passport.snm0516.aisee.tv/x/passport-tv-login/key'
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
    "hash": "de6e8bb6d83cd936",
    "key": "-----BEGIN PUBLIC KEY-----\nMIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDjb4V7EidX/ym28t2ybo0U6t0n\n6p4ej8VjqKHg100va6jkNbNTrLQqMCQCAYtXMXXp2Fwkk6WR+12N9zknLjf+C9sx\n/+l48mjUU8RqahiFD1XT/u2e0m2EN029OhCgkHx3Fc/KlFSIbak93EH/XlYis0w+\nXl69GV6klzgxW6d2xQIDAQAB\n-----END PUBLIC KEY-----"
  }
}
```

</details>

# 账号密码登录

> https://passport.snm0516.aisee.tv/x/passport-tv-login/login

请求方式：`POST`

是否需要登录：`否`

Content-Type：`application/x-www-form-urlencoded`

## URL参数

| 参数名               | 类型   | 必填  | 内容      | 备注       |
|-------------------|------|-----|---------|----------|
| appkey            | str  | √   |         |          |
| bili_local_id     | str  |     |         |          |
| brand             | str  |     |         |          |
| build             | num  |     |         |          |
| buvid             | str  |     |         |          |
| channel           | str  |     |         |          |
| code              | str  |     |         |          |
| cpu               | str  |     |         |          |
| device            | str  |     |         |          |
| device_id         | str  |     |         |          |
| device_name       | str  |     |         |          |
| device_platform   | str  |     |         |          |
| device_tourist_id | num  |     |         |          |
| explor_attr       | num  |     |         |          |
| extend            | str  |     |         |          |
| fingerprint       | str  |     |         |          |
| fourk             | num  |     |         |          |
| guest_access_key  | str  |     |         |          |
| guest_id          | num  |     |         |          |
| guid              | str  |     |         |          |
| local_fingerprint | str  |     |         |          |
| local_id          | str  | √   |         |          |
| login_session_id  | str  |     |         |          |
| memory            | num  |     |         |          |
| mobi_app          | str  |     |         |          |
| mode_switch       | bool |     |         |          |
| model             | str  |     |         |          |
| mpi_id            | str  |     |         |          |
| mpi_model         | str  |     |         |          |
| mpi_type          | str  |     |         |          |
| networkstate      | str  |     |         |          |
| password          | str  | √   | 加密后的密码  |          |
| platform          | str  |     |         |          |
| resource_id       | str  |     |         |          |
| spm_id            | str  |     |         |          |
| statistics        | str  |     |         |          |
| sys_ver           | num  |     |         |          |
| teenager_mode     | num  |     |         |          |
| token             | str  | √   | 密钥的hash |          |
| ts                | num  | √   | 当前时间戳   | 单位：秒     |
| tv_brand          | str  |     |         |          |
| uid               | num  |     |         |          |
| username          | str  | √   | 登录用户名   | 手机号或邮箱地址 |
| sign              | str  |     |         |          |

## Json回复

### 根对象

| 字段名     | 类型  | 内容   | 备注                                                                                                                                       |
|---------|-----|------|------------------------------------------------------------------------------------------------------------------------------------------|
| code    | num | 响应码  | 0：成功<br/>-629：用户名或密码错误<br/>86036：您的账号存在异常行为，请到 bilibili 手机端完成验证登录，再重新尝试登录<br/>86041：设备超过次数限制,请尝试扫码登录.<br/>86048：密码错误超过次数限制,请尝试扫码登录或短信登录. |
| message | str |      |                                                                                                                                          |
| ttl     | num | 1    |                                                                                                                                          |
| data    | obj | 信息本体 |                                                                                                                                          |

### `data`对象

| 字段名 | 类型  | 内容  | 备注  |
|-----|-----|-----|-----|
| xxx | str |     |     |

## 请求示例

```shell
curl -L -X POST 'https://passport.snm0516.aisee.tv/x/passport-tv-login/login?password=xxx&local_id=11&sign=xxx&appkey=4409e2ce8ffd12b8&token=xxx&ts=1664534298&username=xxx'
```

## 响应示例

<details>
<summary>点击查看</summary>

```json

```

</details>

# 密码加密示例

## Java实现

```java
import cn.hutool.core.codec.Base64;

import javax.crypto.Cipher;
import java.security.KeyFactory;
import java.security.PublicKey;
import java.security.spec.X509EncodedKeySpec;

public class Test {
    public static void main(String[] args) throws Exception {
        //用户密码
        String password = "abcdef";
        //获取到的证书内容
        String key = "-----BEGIN PUBLIC KEY-----\nMIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDjb4V7EidX/ym28t2ybo0U6t0n\n6p4ej8VjqKHg100va6jkNbNTrLQqMCQCAYtXMXXp2Fwkk6WR+12N9zknLjf+C9sx\n/+l48mjUU8RqahiFD1XT/u2e0m2EN029OhCgkHx3Fc/KlFSIbak93EH/XlYis0w+\nXl69GV6klzgxW6d2xQIDAQAB\n-----END PUBLIC KEY-----\n";
        //获取到的盐值
        String hash = "bb73382121594c46";
        String[] split = key.strip().split("\n");
        String newKey = split[1] + split[2] + split[3] + split[4];
        //进行加密
        KeyFactory keyFactory = KeyFactory.getInstance("RSA");
        X509EncodedKeySpec keySpec = new X509EncodedKeySpec(Base64.decode(newKey));
        PublicKey publicKey = keyFactory.generatePublic(keySpec);
        Cipher cipher = Cipher.getInstance(keyFactory.getAlgorithm());
        cipher.init(Cipher.PUBLIC_KEY, publicKey);
        byte[] bytes = cipher.doFinal((hash + password).getBytes());
        String encode = Base64.encode(bytes);
        System.out.println(encode);
    }
}
```