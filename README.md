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
  - [ ] 登录
    - [X] 二维码登录
      - [X] [获取登录二维码](login/qr_web.md#获取登录二维码)
      - [X] [获取二维码扫描状态](login/qr_web.md#获取二维码扫描状态)
    - [ ] 账号密码登录
    - [ ] 短信登录
    - [ ] 微信登录
    - [ ] QQ登录
    - [ ] 微博登录
    - [X] [退出登录](login/logout_web.md#退出登录)
  - [ ] 剧集
    - [X] [获取剧集基本信息](bangumi/info.md#获取剧集基本信息)
    - [X] [获取剧集分集信息](bangumi/info.md#获取剧集分集信息)
    - [X] [获取视频播放流](bangumi/playurl_web.md#获取视频播放流)
  - [ ] 视频
    - [ ] [获取视频播放流](video/playurl_web.md#获取视频播放流)
    - [X] [一键三连](video/triple_web.md#一键三连)
  - [ ] 专栏
    - [X] [获取用户专栏文章列表](article/list.md#获取用户专栏文章列表)
    - [X] [获取用户专栏文集列表](article/list.md#获取用户专栏文集列表)
    - [X] [获取专栏推荐文章](article/recommends.md#获取专栏推荐文章)
    - [X] [专栏排行榜](article/rank.md#专栏排行榜)
    - [X] [获取文集信息](article/readlist.md#获取文集信息)
  - [ ] 课程
    - [ ] [获取视频播放流]()
  - [ ] 大会员
    - [X] 卡券兑换
      - [X] [查询卡券状态](vip/privilege.md#查询卡券状态)
      - [X] [兑换卡券](vip/privilege.md#兑换卡券)
  - [ ] 用户
    - [X] [关注/取消关注用户](user/relation.md#关注取消关注用户)
  - [ ] 空间
    - [X] [获取预约信息](space/reservation.md#获取预约信息)
- [ ] APP端
  - [ ] 登录
    - [ ] 账号密码登录
    - [X] 短信登录
      - [X] [获取国际电话区号列表](login/sms_app.md#获取国际电话区号列表)
      - [X] [申请发送短信](login/sms_app.md#申请发送短信)
      - [X] [使用短信验证码登录](login/sms_app.md#使用短信验证码登录)
    - [ ] 退出登录
  - [ ] 大会员
    - [ ] 大积分中心
      - [ ] 首页
      - [X] [大积分签到](vip/sign.md#大积分签到)
      - [X] [大积分中心首页](vip/point.md#大积分中心首页)
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
    - [X] [查询token有效时间](login/info_tv.md#查询token有效时间)
  - [ ] 通知
  - [ ] 设置
    - [X] [获取个人隐私设置](setting/setting_tv.md#获取个人隐私设置)
    - [X] [修改个人隐私选项](setting/setting_tv.md#修改个人隐私选项)
  - [ ] 分区
    - [X] [获取分区列表](regin/regin_tv.md#获取分区列表)
- [ ] 车机端
  - [X] 登录
    - [X] 二维码登录
      - [X] [获取登录二维码](login/qr_car.md#获取登录二维码)
      - [X] [获取二维码扫描状态](login/qr_car.md#获取二维码扫描状态)
    - [X] [退出登录](login/logout_car.md#退出登录)
  - [ ] 搜索
    - [X] [搜索建议](search/search_car.md#搜索建议)
    - [X] [搜索](search/search_car.md#搜索)
- [ ] 其他
  - [X] [获取当前时间戳](other/now.md#获取当前时间戳)