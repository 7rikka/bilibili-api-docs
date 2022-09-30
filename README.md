<h1 align="center">哔哩哔哩 API文档</h1>
<p align="center">
    <a href="https://github.com/7rikka/bilibili-api-docs/issues" style="text-decoration:none">
        <img src="https://img.shields.io/github/issues/7rikka/bilibili-api-docs.svg" alt="GitHub issues"/>
    </a>
    <a href="https://github.com/7rikka/bilibili-api-docs/stargazers" style="text-decoration:none" >
        <img src="https://img.shields.io/github/stars/7rikka/bilibili-api-docs.svg" alt="GitHub stars"/>
    </a>
    <a href="https://github.com/7rikka/bilibili-api-docs/network" style="text-decoration:none" >
        <img src="https://img.shields.io/github/forks/7rikka/bilibili-api-docs.svg" alt="GitHub forks"/>
    </a>
</p>

---

**目录**

- [ ] [名词解释](md/description.md)
- [X] [App端sign签名生成方法](md/app_sign.md)
- [ ] [App端参数列表](md/params.md)
- [ ] [响应码收集](code.md)
- [ ] Web端
  - [ ] 剧集
    - [X] [获取剧集基本信息](bangumi/info.md#获取剧集基本信息)
    - [X] [获取剧集分集信息](bangumi/info.md#获取剧集分集信息)
- [ ] APP端
  - [ ] 登录
    - [ ] [获取登录二维码]()
    - [ ] [获取二维码扫描状态]()
- [ ] TV端
  - [ ] 登录
    - [X] 二维码登录
      - [X] [获取登录二维码](login/qr_tv.md#获取登录二维码)
      - [X] [获取二维码扫描状态](login/qr_tv.md#获取二维码扫描状态)
    - [X] 短信登录
      - [X] [申请发送短信](login/sms_tv.md#申请发送短信)
      - [X] [使用短信验证码登录](login/sms_tv.md#使用短信验证码登录)
    - [X] 账号密码登录
      - [X] [获取公钥和盐值](login/password_tv.md#获取公钥和盐值)
      - [X] [账号密码登录](login/password_tv.md#账号密码登录)
      - [X] [密码加密示例](login/password_tv.md#密码加密示例)
    - [X] [查询token有效时间](login/info.md#查询token有效时间)
- [ ] 车机端
  - [X] 登录
    - [X] 二维码登录
      - [X] [获取登录二维码](login/qr_car.md#获取登录二维码)
      - [X] [获取二维码扫描状态](login/qr_car.md#获取二维码扫描状态)
    - [X] [退出登录](login/logout_car.md#退出登录)
