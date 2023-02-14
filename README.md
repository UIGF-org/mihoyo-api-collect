

<p align="center">
  <img src="https://raw.githubusercontent.com/Kamisato-Ayaka-233/mihoyo-api-collect/main/files/images/top.jpg" height="200">
  <br/><br/>
  <img alt="GitHub repo size" src="https://img.shields.io/github/repo-size/Kamisato-Ayaka-233/mihoyo-api-collect?style=flat-square">
  <br/>
  <img alt="GitHub issues" src="https://img.shields.io/github/issues/Kamisato-Ayaka-233/mihoyo-api-collect?style=flat-square">
  <img alt="GitHub Discussions" src="https://img.shields.io/github/discussions/Kamisato-Ayaka-233/mihoyo-api-collect?color=%23555&style=flat-square">
  <br/>
  <img alt="GitHub contributors" src="https://img.shields.io/github/contributors/Kamisato-Ayaka-233/mihoyo-api-collect?color=%23c0c0c0&style=flat-square">
  <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/Kamisato-Ayaka-233/mihoyo-api-collect?color=%23114514&style=flat-square">
  <img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/Kamisato-Ayaka-233/mihoyo-api-collect?color=%23aa4499&style=flat-square">
  <img alt="GitHub forks" src="https://img.shields.io/github/forks/Kamisato-Ayaka-233/mihoyo-api-collect?color=%23456789&style=flat-square">
</p>


<h1 align="center">米哈游API</h1>
<p align="center">米游社、原神、崩坏</p>

---

目的是收集米哈游的米游社、原神、崩坏等应用、游戏的API。

---

## 声明

1. 本项目遵守CC-BY-NC 4.0协议，禁止一切商业使用，如需转载请注明作者及原文档地址。
2. **请勿滥用，本项目仅用于学习和测试！**  
**请勿滥用，本项目仅用于学习和测试！**  
**请勿滥用，本项目仅用于学习和测试！**  
3. 利用本项目提供的接口、文档等造成不良影响及后果与本人无关。
4. 由于本项目的特殊性，可能随时停止编写或删档。
5. 本项目为开源项目，不接受任何形式的催单和索取行为，更不容许存在付费内容。

---

## 目录

仅有部分内容，正在建设中……

已完结的文章会选中Checkbox。

- [ ] [鉴权](other/authentication.md)
- [ ] [错误码](other/error_code.md)
- [ ] [各种ID对照表](other/id.md)

---

### 米游社（HoYoLab，MiYouShe）

米游社的API几乎均为REST API结构。使用URL参数（URL Query，GET方式）或者JSON（POST方式）来传递参数，返回类型为JSON格式。使用HTTP不会强制301跳转至HTTPS协议通信，但是会返回401。

- [ ] [米游社](hoyolab)
  - [ ] [登录](hoyolab/login)
    - [ ] [密码登录](hoyolab/login/password.md)
    - [ ] [验证码登录](hoyolab/login/sms.md)
  - [ ] [论坛](hoyolab/forum)
    - [ ] [基本信息](hoyolab/forum/info.md)
  - [ ] [文章](hoyolab/article)
    - [ ] [文章](hoyolab/article/article.md)
    - [ ] [文章操作](hoyolab/article/article_operation.md)
    - [ ] [公告](hoyolab/article/announcement.md)
  - [ ] [用户](hoyolab/user)
    - [ ] [用户信息](hoyolab/user/info.md)
    - [ ] [用户游戏信息](hoyolab/user/game_account_info.md)

---

### 《原神（Genshin Impact，Genshin，hk4e）》

《原神》游戏内的API。

<!-- 《原神》游戏内使用Socket进行通信，数据结构为Protobuf协议，并且已加密。 -->

查询玩家信息请查看[米游社](#米游社hoyolabmiyoushe)。

- [ ] [原神](genshin_impact)
  - [ ] [登录](genshin_impact/login)
    - [ ] [密码登录](genshin_impact/login/password.md)
    - [ ] [验证码登录](genshin_impact/login/sms.md)
  - [ ] [用户信息](genshin_impact/user)
    - [ ] [基本信息](genshin_impact/user/info.md)
  - [ ] [其它](genshin_impact/other/)
    - [ ] [公告](genshin_impact/other/announcement.md)


<!--
---

### 《崩坏3（Honkai Impact，Honkai）》

《崩坏3》游戏内的API。

-->

---

## 相关项目

* [Genshin Kits for Node.js](https://github.com/genshin-kit/genshin-kit-node) - Node.js原神玩家信息查询库。


