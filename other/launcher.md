# 游戏启动器信息

- [游戏启动器信息](#游戏启动器信息)
  - [获取推荐内容](#获取推荐内容)
  - [获取游戏资源文件信息](#获取游戏资源文件信息)
  - [获取用户协议](#获取用户协议)
---

## 获取推荐内容

_请求方式：GET_

《原神》国服：`https://sdk-static.mihoyo.com/hk4e_cn/mdk/launcher/api/content`

《原神》国际服：`https://hk4e-launcher-static.hoyoverse.com/hk4e_global/mdk/launcher/api/content`

《崩坏：星穹铁道》国服：`https://api-launcher.mihoyo.com/hkrpg_cn/mdk/launcher/api/content`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| key | str | 启动器Key | |
| launcher_id | num | 启动器ID | |
| language | str | 返回文本语言的国家代码 | 国服仅支持中文（zh-cn） |
| filter_adv | bool | 是否不获取资讯信息 | 留空则返回所有信息，即`false` |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码<br>-204 请求参数`launcher_id`的值无效<br>-205 请求参数`key`的值无效 | |
| message | str | 返回消息 | |
| data | obj | 推荐信息 | 若请求参数中的`language`为不支持的语言，则所有数据均为空与空数组 |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| adv | obj | 背景图片信息 | |
| banner | arr | 游戏资讯 | |
| icon | arr | 启动器侧边栏图标及其信息 | |
| post | arr | 最近的官方资讯文章信息 | |
| qq | obj | 官方QQ群信息 | |
| more | obj | 待调查 | |
| links | obj | 常见问题页面的URL | |

`data`对象→`adv`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| background | str | 背景图片的URL | 文件名中“_”字符前为该图片的MD5校验码 |
| icon | str | 版本热点按钮图片的URL | |
| url | str | 版本专题内容页面的URL | |
| version | str | 背景图版本 | |
| bg_checksum | str | 待调查 | 疑似为背景图片的校验码，但经过比对后，发现其与MD5和任何哈希散列算法通过图片内容生成的值无法匹配 |

`data`对象→`banner`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| banner_id | str | 待调查 | |
| name | str | 待调查 | 似乎总是为空字符串 |
| img | str | 文章封面图片的URL | |
| url | str | 文章页面的URL | |
| order | str | 文章滚动的排序值 | 范围为1-10 |

`data`对象→`icon`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| icon_id | str | 待调查 | |
| img | str | 图标URL | |
| url | str | 该图标将会跳转至的URL | |
| title | str | 二维码下方按钮的文本 | |
| tittle | str | 与`title`字段的内容相同 | |
| qr_img | str | 二维码图片URL | |
| qr_desc | str | 二维码下方描述的文本 | |
| img_hover | str | 鼠标悬停时显示图标的URL | |
| other_links | arr | 待调查 | 似乎总是为空数组 |
| links | arr | 二维码下方按钮的跳转URL | |
| icon_link | str | 待调查 | 总是为空字符串 |

`data`对象→`icon`数组→对象→`links`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| title | str | 按钮内文本 | |
| url | str | 按钮将跳转的URL | |

`data`对象→`post`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| post_id | str | 待调查 | |
| type | str | 米游社文章类型 | |
| title | str | 文章标题 | |
| show_time | str | 文章发布的时间 | 格式为“月/日” |
| url | str | 文章链接 | |
| tittle | str | 与`title`字段的内容相同 | |
| order | str | 列表排序值 | 范围为1-12 |

`data`对象→`qq`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| qq_id | str | 待调查 | |
| number | str | QQ群号 | |
| name | str | QQ群名称 | |
| code | str | QQ群URL | URL经过Unicode转义 |
 
`data`对象→`links`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| faq | str | 常见问题页面的URL | |
| version | str | 待调查 | 总是为1 |

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "adv": {
      "background": "https://launcher-webstatic.mihoyo.com/launcher-public/2023/08/14/7f92b296633974293b1cc9ced73952f9_2267874619055857570.png",
      "icon": "https://launcher-webstatic.mihoyo.com/launcher-public/2023/08/14/5d0d835da94aaf76f6c41a0a51cd51af_3635147868632833439.png",
      "url": "https://webstatic.mihoyo.com/ys/event/e20210601blue_post/vert.html?page_sn=d5dda66067224184\\u0026bbs_presentation_style=fullscreen\\u0026utm_source=game\\u0026utm_medium=ys\\u0026utm_campaign=bt",
      "version": "308",
      "bg_checksum": "8b375f844058d43255c33e2e4e71483a"
    },
    "banner": [
      {
        "banner_id": "64df45b948f1ddd6ee9b3fd2",
        "name": "",
        "img": "https://launcher-webstatic.mihoyo.com/launcher-public/2023/08/18/7c65cb9f5367e6b06ae1051c2c16f3a2_7403794543422733768.jpg",
        "url": "https://www.miyoushe.com/ys/article/42537480",
        "order": "7"
      },
      ...
    ],
    "icon": [
      {
        "icon_id": "5f5b7ca3b10d9a70d0e47d86",
        "img": "https://webstatic.mihoyo.com/upload/operation_location/2020/09/11/41dbaf011ef6fd782450e6b59255d410_2396120149109972020.png",
        "tittle": "加入QQ群",
        "url": "https://ys.mihoyo.com/launcher/18/zh-cn/qq?api_url=https%3A%2F%2Fapi-sdk.mihoyo.com%2Fhk4e_cn\\u0026prev=false",
        "qr_img": "",
        "qr_desc": "",
        "img_hover": "https://webstatic.mihoyo.com/upload/operation_location/2020/09/11/d9b6a36596d49e8c2b262f3db8b271d9_6971507594010738352.png",
        "other_links": [],
        "title": "加入QQ群",
        "icon_link": "https://ys.mihoyo.com/launcher/18/zh-cn/qq?api_url=https%3A%2F%2Fapi-sdk.mihoyo.com%2Fhk4e_cn\\u0026prev=false",
        "links": [
          {
            "title": "加入QQ群",
            "url": "https://ys.mihoyo.com/launcher/18/zh-cn/qq?api_url=https%3A%2F%2Fapi-sdk.mihoyo.com%2Fhk4e_cn\\u0026prev=false"
          },
          ...
        ]
      },
      ...
    ],
    "post": [
      {
        "post_id": "64e587f248f1ddd6ee9b3fe9",
        "type": "POST_TYPE_INFO",
        "tittle": "《原神》枫丹实机画面展示片｜Gamescom 2023",
        "url": "https://www.miyoushe.com/ys/article/42711525",
        "show_time": "08/23",
        "order": "11",
        "title": "《原神》枫丹实机画面展示片｜Gamescom 2023"
      },
      ...
    ],
    "qq": [
      {
        "qq_id": "5fe2a761b15384c3e4621420",
        "name": "原神官方玩家群11",
        "number": "512047400",
        "code": "https://jq.qq.com/?_wv=1027\\u0026k=4dhAg811"
      },
      ...
    ],
    "more": {
      "activity_link": "",
      "announce_link": "",
      "info_link": "",
      "news_link": "",
      "trends_link": "",
      "supply_link": "",
      "tools_link": ""
    },
    "links": {
      "faq": "https://bbs.mihoyo.com/ys/article/4004423",
      "version": "1"
    }
  }
}
```
</details>

## 获取游戏资源文件信息

_请求方式：GET_

《原神》国服：`https://sdk-static.mihoyo.com/hk4e_cn/mdk/launcher/api/resource`

《原神》国际服：`https://hk4e-launcher-static.hoyoverse.com/hk4e_global/mdk/launcher/api/resource`

《崩坏：星穹铁道》国服：`https://api-launcher.mihoyo.com/hkrpg_cn/mdk/launcher/api/resource`


**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| key | str | 启动器Key | |
| launcher_id | num | 启动器ID | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| message | str | 返回消息 | |
| data | obj | 资源信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| game | obj | 游戏主要资源信息 | |
| plugin | obj | 游戏运行库信息 | |
| web_url | str | 启动器下载页面URL | |
| force_update | | 待调查 | |
| pre_download_game | | 待调查 |
| sdk | | 待调查 |
| deprecated_packages | arr | 已弃用游戏资源文件的文件名与MD5值 | |
| deprecated_files | arr | 已弃用游戏文件的文件名与MD5值 | |

`data`对象→`game`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| latest | obj | 最新版本文件信息 | |
| diffs | arr | 一些旧版本至当前版本的增量文件信息 | |

`data`对象→`game`对象→`latest`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| version | str | 最新游戏版本 | |
| name | str | 文件名称 | 总是为空字符串 |
| path | str | 空字符串 | 根据`diffs`数组→对象→`path`字段的规律，本应为文件URL，但是被`segments`字段取代 |
| size | str | 文件解压后的大小 | |
| md5 | str | 该文件的MD5值 | |
| voice_packs | arr | 所有语音包信息 | 《崩坏：星穹铁道》为空数组 |
| decompressed_path | str | 待调查 | |
| segments | arr | 游戏资源压缩文件各分卷的信息 | 《崩坏：星穹铁道》为空数组 |
| package_size | str | 压缩包文件大小 | |
| entry | str | 游戏启动程序的文件名 | |

`data`对象→`game`对象→`latest`对象→`voice_packs`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| language | str | 语音资源对应的语言代码 | |
| path | str | 该资源文件的URL | |
| name | str | 语音包文件名称 | 总是为空字符串 |
| size | str | 文件解压后的大小 | |
| package_size | str | 压缩包文件大小 | |
| md5 | str | 文件的MD5值 | |

`data`对象→`game`对象→`latest`对象→`segments`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| path | str | 该资源文件的URL | |
| md5 | str | 文件的MD5值 | |
| package_size | str | 压缩包文件大小 | |

`data`对象→`game`对象→`diffs`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| name | str | 文件名 | |
| version | str | 该增量包修补的旧版本 | |
| path | str | 该增量包的URL | |
| size | str | 文件解压后的大小 | |
| md5 | str | 文件的MD5值 | |
| package_size | str | 压缩包文件大小 | |
| is_recommended_update | bool | 待调查 | |
| voice_packs | obj | 所有语音增量包信息 | 《崩坏：星穹铁道》为空 |

`data`对象→`game`对象→`diffs`数组→`voice_packs`数组→对象：

与`data`对象→`game`对象→`latest`对象→`voice_packs`数组→对象的结构相同

`data`对象→`plugin`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| plugins | arr | 运行库信息 | |
| version | str | 运行库版本 | |

`data`对象→`plugin`对象→`plugins`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| name | str | 运行库文件名 | |
| path | str | 运行库文件URL | |
| md5 | str | 文件的MD5值 | |
| version | str | 该文件的版本 | 总是为空字符串 |
| size | str | 文件大小 | |
| entry | str | 运行库安装程序的文件名 | 可能为空字符串 |

`data`对象→`game`对象→`deprecated_packages`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| name | str | 文件名 | |
| md5 | str | 文件的MD5值 | |

`data`对象→`game`对象→`deprecated_files`数组→对象：

与`data`对象→`game`对象→`deprecated_packages`数组→对象的结构相同

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "game": {
      "latest": {
        "name": "",
        "version": "4.0.0",
        "path": "",
        "size": "120599654462",
        "md5": "3c70931b5ae61d89abe0403dff2365ef",
        "entry": "YuanShen.exe",
        "voice_packs": [
          {
            "language": "zh-cn",
            "name": "",
            "path": "https://autopatchcn.yuanshen.com/client_app/download/pc_zip/20230804185703_R1La3H9xIH1hBiHJ/Audio_Chinese_4.0.0.zip",
            "size": "22459851756",
            "md5": "690b7cf26d12ffdad839027f2ed75914",
            "package_size": "11224682998"
          },
          ...
        ],
        "decompressed_path": "https://autopatchcn.yuanshen.com/client_app/download/pc_zip/20230804185703_R1La3H9xIH1hBiHJ/ScatteredFiles",
        "segments": [
          {
            "path": "https://autopatchcn.yuanshen.com/client_app/download/pc_zip/20230804185703_R1La3H9xIH1hBiHJ/YuanShen_4.0.0.zip.001",
            "md5": "7da1c2721272ffa2d0df2a14ca9b7885",
            "package_size": "10737418240"
          },
          ...
        ],
        "package_size": "60294584351"
      },
      "diffs": [
        {
          "name": "game_3.8.0_4.0.0_hdiff_h2FAbmpdS1P3OQ6r.zip",
          "version": "3.8.0",
          "path": "https://autopatchcn.yuanshen.com/client_app/update/hk4e_cn/18/game_3.8.0_4.0.0_hdiff_h2FAbmpdS1P3OQ6r.zip",
          "size": "67793295222",
          "md5": "42BA351D7B2ED6058E3BC19AC88EF639",
          "is_recommended_update": false,
          "voice_packs": [
            {
              "language": "zh-cn",
              "name": "zh-cn_3.8.0_4.0.0_hdiff_q7JUo5yfuLOYZVFE.zip",
              "path": "https://autopatchcn.yuanshen.com/client_app/update/hk4e_cn/18/zh-cn_3.8.0_4.0.0_hdiff_q7JUo5yfuLOYZVFE.zip",
              "size": "1436148319",
              "md5": "30438FBF20AE9C7706D78C76DBBA38AF",
              "package_size": "658001593"
            },
            ...
          ],
          "package_size": "33699060276"
        },
        ...
      ]
    },
    "plugin": {
      "plugins": [
        {
          "name": "DXSETUP.zip",
          "version": "",
          "path": "https://autopatchcn.yuanshen.com/client_app/plugins/DXSETUP.zip",
          "size": "100647892",
          "md5": "CA2AC3835D7D7DA6CB8624FEFB177083",
          "entry": "",
          "package_size": "0"
        },
        ...
      ],
      "version": "1"
    },
    "web_url": "https://ys.mihoyo.com/launcher",
    "force_update": null,
    "pre_download_game": null,
    "deprecated_packages": [
      {
        "name": "YuanShen_4.0.0.zip.001",
        "md5": "7da1c2721272ffa2d0df2a14ca9b7885"
      },
      ...
    ],
    "sdk": null,
    "deprecated_files": [
      {
        "name": "YuanShen_Data/Plugins/PCGameSDK.dll",
        "md5": ""
      },
      ...
    ]
  }
}
```
</details>

## 获取用户协议

_请求方式：GET_

《原神》国服：`https://sdk-static.mihoyo.com/hk4e_cn/mdk/launcher/api/protocol`

《原神》国际服：`https://hk4e-launcher-static.hoyoverse.com/hk4e_global/mdk/launcher/api/protocol`

《崩坏：星穹铁道》国服：`https://api-launcher.mihoyo.com/hkrpg_cn/mdk/launcher/api/protocol`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| key | str | 启动器Key | |
| launcher_id | num | 启动器ID | |
| language | str | 返回文本语言的国家代码 | 国服仅支持中文（zh-cn） |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| message | str | 返回消息 | |
| data | obj | 用户协议以及用户协议版本 | 若请求参数中的`language`为不支持的语言，则所有数据均为空与空数组 |

`data`对象：
| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| protocol | str | 用户协议 | 为HTML |
| title | str | 用户协议标题 | |
| agreement_version | str | 用户协议版本 | 一般为当前游戏版本 |

<details>
<summary>查看示例</summary>
```json
{
    "retcode": 0,
    "message": "OK",
    "data": {
        "protocol": "<p style=\"white-space: pre-wrap;\"><span style=\"color:rgba(0,0,0,1)\">Effective Date: July 5, 2023</span></p>\n\n<p style=\"white-space: pre-wrap; min-height: 1.5em; text-align: justify;\"><span style=\"color:rgba(0,0,0,1)\"> </span></p>\n\n<p style=\"white-space: pre-wrap; text-align: justify;\"><span style=\"color:rgba(0,0,0,1)\">PLEASE READ THESE TERMS OF SERVICE CAREFULLY, INCLUDING OUR PRIVACY POLICY.</span></p>\n\n<p style=\"white-space: pre-wrap; text-align: justify;\"><span style=\"color:rgba(0,0,0,1)\">This Terms of Service (&#34;Agreement&#34;) is a legally binding agreement between COGNOSPHERE PTE. LTD. (&#34;COGNOSPHERE,&#34; &#34;we,&#34; &#34;our,&#34; or &#34;us&#34;) and you (&#34;you&#34; or &#34;User&#34;). This Agreement governs your use of or access to COGNOSPHERE Game(s), our online website, any game-specific site, software systems, customer support, social media, community channels and/or any other online services provided by COGNOSPHERE and by any of our authorized third party (collectively the &#34;COGNOSPHERE ...",
        "title": "Terms of Service",
        "agreement_version": "4.0"
    }
}
```

</details>