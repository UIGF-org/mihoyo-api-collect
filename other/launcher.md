# 启动器api
### 获取显示内容
原神：`https://sdk-static.mihoyo.com/hk4e_cn/mdk/launcher/api/content`
<br>
崩坏:星穹铁道：`https://api-launcher.mihoyo.com/hkrpg_cn/mdk/launcher/api/content`

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

`data`对象→`adv`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| background | str | 背景图URL | |
| icon | str | 版本热点图片URL | |
| url | str | 版本主题页 | |
| version | str | 背景图版本 | 背景图变动时会变大 |
| bg_checksum | str | 背景图哈希值 | 可能是md5 |

`data`对象→`banner`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| banner_id | str | 未知 | |
| name | null | 未知 | |
| img | str | 文章头图 | |
| url | str | 文章链接 | |
| order | str | 可能是排序 | 1-10之间 |

`data`对象→`icon`数组→对象：

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

`data`对象→`post`数组→对象：
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| post_id | str | 未知 | |
| type | str | 未知 | |
| title | str | 标题 | |
| show_time | str | 时间 | |
| url | str | 链接 | |
| tittle | str | 标题 | |
| order | str | 排序 | 1-12 |

`data`对象→`qq`对象：
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| number | str | QQ群号 | |
| name | str | 群名称 | |
| code | str | 群链接 | |
| qq_id | str | 未知 | |

`data`对象→`more`对象：
都说了未知了。
 
`data`对象→`links`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| faq | str | faq链接 | |
| version | str | 未知 | 一般为1 |

### 获取游戏下载链接

原神：`https://sdk-static.mihoyo.com/hk4e_cn/mdk/launcher/api/resource`
<br>
崩坏：星穹铁道：`https://api-launcher.mihoyo.com/hkrpg_cn/mdk/launcher/api/resource`


**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| key | str | 启动器key | |
| launcher_id | num | 启动器id | |

**JSON返回：**
根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| message | str | 返回消息 | |
| data | obj | 玩家信息 | |

`data`对象→`game`对象：
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| latest | obj | 最新版本 | |
| diffs | obj | 增量包 | |
| web_url | str | 启动器首页？ | |
| force_update | null | 未知 | |
| pre_download_game | null | 未知 |
| deprecated_packages | obj | 压缩包MD5 | |
| sdk | null | 未知 |
| deprecated_files | obj | 压缩包内部分文件MD5 | |

`data`对象→`game`对象→`latest`对象：
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| version | str | 版本号 | |
| name | str | 版本名称 | 一般为空 |
| path | str | 下载链接 | |
| size | str | 解压后文件大小 | 单位为B |
| md5 | str | 文件md5 | |
| voice_packs | obj | 语音包列表 | 崩坏：星穹铁道为空 |
| decompressed_path | str | 未知 | |
| segments | obj | 分卷压缩包列表 | 崩坏：星穹铁道为空 |
| package_size | 压缩包体积 | 单位为B |
| entry | str | 游戏入口 | |

`data`对象→`game`对象→`latest`对象→`voice_packs`数组→对象：
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| language | str | 语言 | |
| path | str | 下载链接 | |
| name | str | 语音包名称 | 一般为空 |
| size | str | 解压后文件大小 | 单位为B |
| package_size | 压缩包体积 | 单位为B |
| md5 | str | 文件md5 | |

`data`对象→`game`对象→`latest`对象→`segments`数组→对象：
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| path | str | 下载链接 | |
| md5 | str | 文件md5 | |
| package_size | 压缩包体积 | 单位为B |

`data`对象→`game`对象→`diffs`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| name | str | 文件名 | |
| version | str | 旧文件版本号 | |
| path | str | 下载链接 | |
| size | str | 解压后文件大小 | 单位为B |
| md5 | str | 文件md5 | |
| package_size | 压缩包体积 | 单位为B |
| is_recommended_update | bool | 未知 | |
| voice_packs | obj | 语音包列表 | 崩坏：星穹铁道为空 |

`data`对象→`game`对象→`diffs`数组→`voice_packs`数组→对象：

同`data`对象→`game`对象→`latest`对象→`voice_packs`数组→对象

`data`对象→`plugin`对象：
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| plugins | obj | 插件列表? | |
| version | str | 版本号? | |

`data`对象→`plugin`对象→`plugins`数组→对象：
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| name | str | 插件名称? | |
| path | str | 下载链接 | |
| md5 | str | 文件md5 | |
| version | str | 文件版本号 | |
| size | str | 文件大小 | 单位为B |
| entry | str | 入口文件 | 可能为空 |

`data`对象→`game`对象→`deprecated_packages`数组→对象：
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| name | str | 文件名 | |
| md5 | str | 文件md5 | |

`data`对象→`game`对象→`deprecated_files`数组→对象：
<br>
同：`data`对象→`game`对象→`deprecated_packages`数组→对象：