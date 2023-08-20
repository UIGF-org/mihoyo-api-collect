# 崩坏：星穹启动器
## 获取背景图等
`https://api-launcher.mihoyo.com/hkrpg_cn/mdk/launcher/api/content`
**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| key | str | 启动器key | |
| language | str | 语言 | 默认zh-cn |
| filter_adv | bool | 是否为简略信息 | 默认fasle |
| launcher_id | num | 启动器id | |

**JSON返回：**
根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| message | str | 返回消息 | |
| data | obj | 玩家信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| adv | obj | 玩家基础信息 | |
| banner | list | 游戏资讯 | |
| icon | list | 启动器侧边栏图标 | |
| post | list | 好像也是游戏资讯 | |
| qq | obj | 官方QQ群 | |
| more | obj | 未知 |  |
| links | obj | faq | |

`adv`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| background | str | 背景图URL | |
| icon | str | 版本热点图片URL | |
| url | str | 版本主题页 | |
| version | str | 背景图版本 | 背景图变动时会变大 |
| bg_checksum | str | 背景图哈希值 | 可能是md5 |

`banner`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| banner_id | str | 未知 | |
| name | null | 未知 | |
| img | str | 文章头图 | |
| url | str | 文章链接 | |
| order | str | 可能是排序 | 1-10之间 |

`icon`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| icon_id | str | 未知 | |
| img | str | 图标 | |
| url | str | 链接 | |
| title | str | 标题 | |
| tittle | str | 标题 | |
| qr_img | str | 二维码图片 | |
| qr_desc | str | 二维码描述 | |
| img_hover | str | 鼠标悬停图片 | |
| other_links | list | 未知 | 一般为空 |
| links | list | 链接列表 | 可能为空 |
| icon_link | str | 未知 | 一般为空 |

`post`对象：
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| post_id | str | 未知 | |
| type | str | 未知 | |
| title | str | 标题 | |
| show_time | str | 时间 | |
| url | str | 链接 | |
| tittle | str | 标题 | |
| order | str | 排序 | 1-12 |

`qq`对象：
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| number | str | QQ群号 | |
| name | str | 群名称 | |
| code | str | 群链接 | |
| qq_id | str | 未知 | |

`more`对象：
都说了未知了。
 
 `links`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| faq | str | faq链接 | |
| version | str | 未知 | 一般为1 |

