
<p align="center">
  <img src="https://raw.githubusercontent.com/UIGF-org/mihoyo-api-collect/main/files/images/logo.png" height="200">
  <br>
  <a href="https://github.com/UIGF-org/mihoyo-api-collect" style="text-decoration: none;">
    <img alt="GitHub repo size" src="https://img.shields.io/github/repo-size/UIGF-org/mihoyo-api-collect?style=flat-square">
  </a>
  <br>
  <a href="https://github.com/UIGF-org/mihoyo-api-collect/issues" style="text-decoration: none;">
    <img alt="GitHub issues" src="https://img.shields.io/github/issues/UIGF-org/mihoyo-api-collect?style=flat-square">
  </a>
  <a href="https://github.com/UIGF-org/mihoyo-api-collect/discussions" style="text-decoration: none;">
    <img alt="GitHub discussions" src="https://img.shields.io/github/discussions/UIGF-org/mihoyo-api-collect?color=%23555&style=flat-square">
  </a>
  <a href="https://github.com/UIGF-org/mihoyo-api-collect/graphs/contributors" style="text-decoration: none;">
    <img alt="GitHub contributors" src="https://img.shields.io/github/contributors/UIGF-org/mihoyo-api-collect?color=%23c0c0c0&style=flat-square">
  </a>
  <br>
  <a href="https://github.com/UIGF-org/mihoyo-api-collect/blob/master/LICENSE" style="text-decoration: none;">
    <img alt="Github license" src="https://img.shields.io/static/v1?style=flat-square&label=license&message=CC%20BY-NC%204.0&color=blueviolet">
  </a>
  <a href="https://github.com/UIGF-org/mihoyo-api-collect/commits/main" style="text-decoration: none;">
    <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/UIGF-org/mihoyo-api-collect?color=%23114514&style=flat-square">
  </a>
  <a href="https://github.com/UIGF-org/mihoyo-api-collect/stargazers" style="text-decoration: none;">
    <img alt="GitHub repo stars" src="https://img.shields.io/github/stars/UIGF-org/mihoyo-api-collect?color=%23aa4499&style=flat-square">
  </a>
  <a href="https://github.com/UIGF-org/mihoyo-api-collect/forks" style="text-decoration: none;">
    <img alt="GitHub forks" src="https://img.shields.io/github/forks/UIGF-org/mihoyo-api-collect?color=%23456789&style=flat-square">
  </a>
</p>

<h1 align="center">米哈游API</h1>
<p align="center">米游社、原神、崩坏</p>

---

目的是收集米哈游的米游社等应用、原神等游戏的API。

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

## 如何贡献文档

参阅[贡献指南](CONTRIBUTING.md)。

如有不理解的地方可以开启Issue。

---

## 目录

仅有部分内容，正在建设中……

已完结的文章会选中Checkbox。

- [x] [绕过检测与鉴权](other/authentication.md)
- [ ] [错误码](other/error_code.md)
- [ ] [各种ID对照表](other/id.md)
- [x] [游戏启动器信息](other/launcher.md)
---

### 米游社（HoYoLab，MiYouShe）

米游社的API几乎均为REST API结构。使用URL参数（URL Query，GET方式）或者JSON（POST方式）来传递参数，返回类型为JSON格式。使用HTTP不会强制301跳转至HTTPS协议通信，但是会返回401。

- [ ] [米游社](hoyolab)
  - [ ] [登录](hoyolab/login)
    - [x] [验证码登录](hoyolab/login/sms.md)
    - [x] [密码登录（米游社）](hoyolab/login/password_hoyolab.md)
    - [x] [密码登录（米哈游通行证）](hoyolab/login/password_passport.md)
    - [x] [扫码登录（GameToken）](hoyolab/login/qrcode_hk4e.md)
    - [x] [扫码登录（米游社）](hoyolab/login//qrcode_hoyolab.md)
  - [ ] [论坛](hoyolab/forum)
    - [ ] [基本信息](hoyolab/forum/info.md)
  - [ ] [文章](hoyolab/article)
    - [ ] [文章](hoyolab/article/article.md)
    - [ ] [文章操作](hoyolab/article/article_operation.md)
    - [ ] [公告](hoyolab/article/announcement.md)
  - [ ] [用户](hoyolab/user)
    - [ ] [用户信息](hoyolab/user/info.md)
    - [x] [用户Token](hoyolab/user/token.md)
    - [ ] [用户游戏信息](hoyolab/user/game_account_info.md)


---

### 《原神（Genshin Impact，Genshin，hk4e）》

关于《原神》的API。

<!-- 《原神》游戏内使用Socket进行通信，数据结构为Protobuf协议，并且已加密。 -->

查询玩家信息请查看[米游社](#米游社hoyolabmiyoushe)。

- [ ] [原神](genshin_impact)
  <!-- - [ ] [登录](genshin_impact/login)
    - [ ] [密码登录](genshin_impact/login/password.md)
    - [ ] [验证码登录](genshin_impact/login/sms.md)
  - [ ] [用户信息](genshin_impact/user)
    - [ ] [基本信息](genshin_impact/user/info.md) -->
  - [ ] [其它](genshin_impact/other/)
    - [ ] [公告](genshin_impact/other/announcement.md)
  - [ ] [第三方API](genshin_impact/thirdparty/)
    - [ ] [历史祈愿UP池](genshin_impact/thirdparty/historical_up_items.md)
    - [ ] [项目ID与名称的字典](genshin_impact/thirdparty/dictionary_of_item.md)

### 《崩坏：星穹铁道（Honkai: Star Rail，Star Rail，hkrpg）》

关于《崩坏：星穹铁道》的API。

查询玩家信息请查看[米游社](#米游社hoyolabmiyoushe)。

- [ ] [崩坏：星穹铁道](honkai_star_rail)
  - [ ] [其它](honkai_star_rail/other/)
    - [ ] [公告](honkai_star_rail/other/announcement.md)

<!--
---

### 《崩坏3（Honkai Impact，Honkai）》

《崩坏3》游戏内的API。

-->
---

## 贡献

[![contributors](https://opencollective.com/mihoyo-api-collect/contributors.svg?width=860&button=false)](https://github.com/UIGF-org/mihoyo-api-collect/graphs/contributors)

---

## 相关项目

- [Star Rail Warp Export](https://github.com/biuuu/star-rail-warp-export) - 星穹铁道跃迁记录导出工具。
- [Genshin Wish Export](https://github.com/biuuu/genshin-wish-export/) - 原神祈愿记录导出工具
- [Genshin Wish Analyzer](https://github.com/voderl/genshin-gacha-analyzer) - 原神祈愿记录分析器
- [Yunzai Bot](https://gitee.com/le-niao/Yunzai-Bot) - 原始云崽机器人，QQ群原神信息查询机器人
- [Miao Yunzai](https://github.com/yoimiya-kokomi/Miao-Yunzai) - “喵”版云崽机器人，QQ群原神信息和原神角色面板查询机器人
- [Snap.Hutao](https://github.com/DGP-Studio/Snap.Hutao) - 实用的开源多功能原神工具箱 🧰
- [Cocogoat](https://github.com/YuehaiTeam/cocogoat) - 原神成就记录与圣遗物管理
- [UIGF API](https://github.com/UIGF-org/UIGF-API) - 原神项目ID与项目名称互相转换API

- ~~[Genshin Player Query](https://github.com/Azure99/GenshinPlayerQuery) - 原神玩家信息查询~~ **已存档**
- ~~[Genshin Kits for Node.js](https://github.com/genshin-kit/genshin-kit-node) - Node.js原神玩家信息查询库~~ **已停止维护**
- ~~[Genshin Helper](https://github.com/y1ndan/genshinhelper2) - Python米游社API封装库~~ **已停止维护**
