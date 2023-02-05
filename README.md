
<h1 align="center">米哈游API</h1>
<p align="center">米游社、原神、崩坏</p>

---

<!-- <h3 align="center">野生API文档</h3> -->

目的是收集米哈游的米游社、原神、崩坏等应用、游戏的API。

---

**声明**：

1. 本项目遵守 CC-BY-NC 4.0 协议，禁止一切商业使用，如需转载请注明作者 ID
2. **请勿滥用，本项目仅用于学习和测试！请勿滥用，本项目仅用于学习和测试！请勿滥用，本项目仅用于学习和测试！**
3. 利用本项目提供的接口、文档等造成不良影响及后果与本人无关
4. 由于本项目的特殊性，可能随时停止开发或删档
5. 本项目为开源项目，不接受任何形式的催单和索取行为，更不容许存在付费内容

---

暂时还缺少内容，正在建设中……

已完结的文章会选中Checkbox。

- [ ] [鉴权](other/authentication.md)
- [ ] [错误码](other/error_code.md)
- [ ] [各种ID对照表](other/id.md)

---

米游社（HoYoLab，MiYouShe）

米游社的API几乎均为REST API结构。使用URL参数（URL Query，GET方式）或者JSON（POST方式）来传递参数，返回类型为JSON格式。使用HTTP不会强制301跳转至HTTPS协议通信，但是会返回401。

- [ ] [米游社](hoyolab)
  - [ ] [登录](hoyolab/login)
    - [ ] [密码登录](hoyolab/login/password.md)
    - [ ] [验证码登录](hoyolab/login/sms.md)
  - [ ] [论坛](hoyolab/forum)
    - [ ] [基本信息](hoyolab/forum/info.md)
  - [ ] [文章](hoyolab/article)
    - [ ] [文章](hoyolab/article/article.md)
    - [ ] [公告](hoyolab/article/announcement.md)
    - [ ] [文章操作](hoyolab/article/article_operation.md)
  - [ ] [用户](hoyolab/user)
    - [ ] [用户信息](hoyolab/user/info.md)
    - [ ] [用户游戏信息](hoyolab/user/game_info.md)

---

《原神（Genshin Impact，Genshin，hk4e）》

《原神》游戏内的API。

- [ ] [原神](genshin_impact)
  - [ ] [登录](genshin_impact/login)
    - [ ] [密码登录](genshin_impact/login/password.md)
    - [ ] [验证码登录](genshin_impact/login/sms.md)
  - [ ] [用户信息](genshin_impact/user)
    - [ ] [基本信息](genshin_impact/user/info.md)
    - [ ] [深境螺旋信息](genshin_impact/user/spiral_abyss.md)
    - [ ] [角色信息](genshin_impact/user/characters.md)
  <!-- - [ ] [公告](genshin_impact/announcement/)
    - [ ] [官方公告](hoyolab/article/announcement.md) -->

---




