# 论坛文章

- [获取首页信息](#获取首页信息)
- [获取官方资讯](#获取官方资讯)
- [获取完整文章信息](#获取完整文章信息)

---

# 获取首页信息

_请求方式：GET_

`https://bbs-api-static.miyoushe.com/apihub/wapi/webHome`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| gids | num | 游戏ID | |
| page | num | 页数 | 若未指定则为第1页 |
| page_size | num | 每页文章数量<br/>1~50 | 若未指定或超出范围则为每页20篇 |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| retcode | num | 返回码<br/>1 未选择游戏 | |
| message | str | 返回消息 | |
| data | obj | 首页信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| carousels | arr | 头部切换的横幅信息 | 网页端 |
| recommended_posts | arr | 首页推荐文章 | |
| recommended_topics | obj | 首页推荐话题 | |
| fixed_posts | arr | 首页固定文章 | |
| selection_post_list | arr | 首页每月热榜 | |

`data`对象→`carousels`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| cover | str | 横幅图片 | |
| path | str | 横幅跳转链接 | |

`data`对象→`recommended_posts`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| post | obj | 文章信息 | |
| forum | obj | 所属分区信息 | |
| topics | arr | 文章话题信息 | |
| user | obj | 文章发布者信息 | |
| self_operation | | 待调查 | |
| stat | obj | 文章数据 | 均为0<br/>请使用：[获取完整文章信息](#获取完整文章信息) |
| cover | obj | 文章封面信息 | |
| image_list | arr | 文章中每张图片的信息 | |
| is_official_master | bool | 待调查 | |
| is_user_master | bool | 待调查 | |
| help_sys | obj | 待调查 | |
| vote_count | num | 文章点赞数量 | 为0<br/>请使用：[获取完整文章信息](#获取完整文章信息) |
| last_modify_time | num | 待调查 | |
| recommend_type | num | 待调查 | |
| collection | obj | 所属合集信息 | 为null<br/>请使用：[获取完整文章信息](#获取完整文章信息) |
| vod_list | 文章中每个视频的信息 | |

`data`对象→`recommended_posts`数组→对象→`post对象`：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| game_id | num | 游戏ID | |
| post_id | num | 文章ID | |
| f_forum_id | num | 所属分区ID | |
| uid | num | 文章发布者的UID | |
| subject | str | 文章标题 | |
| content | str | 简略的文章内容 | 获取完整内容请使用：[获取完整文章信息](#获取完整文章信息) |
| cover | str | 封面链接 | |
| view_type | num | 待调查 | |
| created_at | num | 文章创建的Unix时间戳 | |
| images | arr | 文章中每张图片的链接 | |
| post_status | obj | 文章状态数据 | |
| topic_ids | arr | 文章的话题的ID | |
| view_status | num | 待调查 | |
| max_floor | num | 待调查 | |
| is_original | num | 是否是原创文章<br/>1 原创 | |
| republish_authorization | num | 文章转载授权<br/>2 已开启创作声明，允许规范转载 | |
| reply_time | str | 文章评论时间 | |
| is_deleted | num | 文章是否已删除<br/>0 未删除 | |
| is_interactive | bool | 文章是否可交互（点赞、评论等） | |
| score | num | 待调查 | |

`data`对象→`recommended_posts`数组→对象→`post`对象→`post_status`对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| is_top | bool | 文章是否置顶 | |
| is_good | bool | 是否是精华文章 | |
| is_official | bool | 是否是官方发布的文章 | |

`data`对象→`recommended_posts`数组→对象→`forum`对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| id | num | 文章所属分区的ID | |
| name | str | 文章所属分区的名称 | |

`data`对象→`recommended_posts`数组→对象→`topics`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| id | num | 话题ID | |
| name | str | 话题名称 | |
| cover | str | 话题封面 | |
| content_type | num | 待调查 | |

`data`对象→`recommended_posts`数组→对象→`user`对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| uid | str | 文章发布者的UID | |
| nickname | str | 文章发布者的名称 | |
| introduce | str | 文章发布者的简介 | |
| avatar | num | 头像ID | |
| certification | obj | 认证信息 | |
| level_exp | obj | 等级和经验信息 | |
| avatar_url | str | 头像链接 | |
| pendant | str | 头像框链接 | |
| is_following | bool | 是否关注了你 | 需要鉴权，未鉴权则为false |
| is_followed | bool | 是否已关注 | 需要鉴权，未鉴权则为false |

`data`对象→`recommended_posts`数组→对象→`stat`对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| reply_num | num | 评论数量 | 为0 |
| view_num | num | 观看数量 | 为0 |
| like_num | num | 点赞数量 | 为0 |
| bookmark_num | num | 收藏数量 | 为0 |

`data`对象→`recommended_posts`数组→对象→`cover`对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| url | str | 文章封面链接 | |
| height | num | 文章封面高度 | |
| width | num | 文章封面宽度 | |
| format | str | 文章封面文件扩展名 | |
| size | str | 文章封面文件大小 | 字节 |
| crop | | 待调查 | |
| is_user_set_cover | bool | 是否是作者设置的封面 | |
| image_id | str | 图片ID | |
| entity_type | str | 待调查 | |
| entity_id | str | 待调查 | |

`data`对象→`recommended_posts`数组→对象→`image_list`对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| url | str | 文章封面链接 | |
| height | num | 文章封面高度 | |
| width | num | 文章封面宽度 | |
| format | str | 文章封面文件扩展名 | |
| size | str | 文章封面文件大小 | 字节 |
| crop | | 待调查 | |
| is_user_set_cover | bool | false | |
| image_id | str | 图片ID | |
| entity_type | str | 待调查 | |
| entity_id | str | 待调查 | |

`data`对象→`recommended_posts`数组→对象→`vod_list`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| id | str | 视频ID | |
| duration | num | 视频时长 | 毫秒 |
| cover | str | 视频封面链接 | |
| resolutions | arr | 视频分辨率列表 | |
| view_num | num | 视频播放数 | |
| transcoding_status | num | 待调查 | |
| review_status | num | 待调查 | |

`data`对象→`recommended_posts`数组→对象→`vod_list`数组→对象→`resolutions`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| url | str | 该清晰度的视频链接 | |
| definition | str | 清晰度文本 | |
| height | num | 该清晰度的视频的高度 | |
| width | num | 该清晰度的视频的宽度 | |
| bitrate | num | 该清晰度的视频的码率 | 未知单位 |
| size | str | 该清晰度的视频的大小 | 字节 |
| format | str | 该清晰度的视频的格式 | |
| label | str | 清晰度文本 | |

`data`对象→`recommended_topics`对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| list | arr | 话题信息 | |
| position | num | 推荐话题的位置 | |

`data`对象→`recommended_topics`对象→`list`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| id | num | 话题ID | |
| name | str | 话题名称 | |
| cover | str | 话题封面链接 | |
| desc | str | 话题描述 | 为空字符串 |
| is_focus | bool | 是否关注该话题 | 始终为false |
| view_num | num | 话题观看数 | 为0 |
| discuss_num | num | 话题讨论数 | 为0 |

`data`对象→`selection_post_list`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| post_id | str | 文章ID | |
| subject | str | 文章标题 | |
| forum_id | num | 所属论坛的ID | |
| forum_name | str | 所属论坛的名称 | |
| banner | str | 文章封面链接 | |
| view_type | num | 待调查 | | 


<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "carousels": [
      {
        "cover": "https://upload-bbs.miyoushe.com/upload/2023/01/29/834af3e4eda5251e6082750fc22edb63_8777643204760273855.png",
        "path": "https://webstatic.mihoyo.com/ys/event/e20230129-lantern-vqhoj8/index.html?game_biz=hk4e_cn&mhy_presentation_style=fullscreen&mhy_landscape=true&mhy_hide_status_bar=true&mhy_auth_required=true&utm_source=bbs&utm_medium=mys&utm_campaign=banner"
      },
      ...
    ],
    "recommended_posts": [
      {
        "post": {
          "game_id": 2,
          "post_id": "35089752",
          "f_forum_id": 43,
          "uid": "159922380",
          "subject": "蔷薇再开时第二天！全试用角色轻松拿满奖励攻略",
          "content": "UID ：100335197[图片]★活动时间：2023/01/31 10:00 ~ 2023/02/13 03:59(五天全解锁，也可以选择等五天后一起完成全部挑战小活动[图片]★参与条件：",
          "cover": "https://upload-bbs.miyoushe.com/upload/2023/02/01/159922380/e55509db76dab0d99ed28fcee9204bc0_8172512981975837842.jpg",
          "view_type": 1,
          "created_at": 1675213042,
          "images": [
            "https://upload-bbs.miyoushe.com/upload/2023/02/01/159922380/e55509db76dab0d99ed28fcee9204bc0_8172512981975837842.jpg",
            ...
          ],
          "post_status": {
            "is_top": false,
            "is_good": false,
            "is_official": false
          },
          "topic_ids": [
            236,
            357,
            405,
            425,
            947,
            1300
          ],
          "view_status": 1,
          "max_floor": 860,
          "is_original": 1,
          "republish_authorization": 2,
          "reply_time": "2023-02-05 09:40:12",
          "is_deleted": 0,
          "is_interactive": false,
          "score": 0
        },
        "forum": {
          "id": 43,
          "name": "攻略"
        },
        "topics": [
          {
            "id": 236,
            "name": "其他攻略",
            "cover": "https://upload-bbs.mihoyo.com/upload/2020/09/14/98dcbb80d92d523566755072a55a6ed1.png",
            "content_type": 3
          },
          {
            "id": 357,
            "name": "讨伐手册",
            "cover": "https://upload-bbs.mihoyo.com/upload/2020/09/14/acb13eaaad8e5c32a5fd3b3d02551614.png",
            "content_type": 2
          },
          {
            "id": 405,
            "name": "任务攻略",
            "cover": "https://upload-bbs.miyoushe.com/upload/2023/01/16/c5941f10bb2792ff40d88107f22ee935_2565180896808939451.png",
            "content_type": 2
          },
          {
            "id": 425,
            "name": "丽莎",
            "cover": "https://upload-bbs.mihoyo.com/upload/2020/11/25/87d31799fc896fe1128e2b4d7cafcafd.jpeg",
            "content_type": 1
          },
          {
            "id": 947,
            "name": "原神观测枢",
            "cover": "https://upload-bbs.mihoyo.com/upload/2022/02/14/8efc5670a3dd0467bf7fb1866bd5d203_2630690909080422615.png",
            "content_type": 2
          },
          {
            "id": 1300,
            "name": "蔷薇再开时",
            "cover": "https://upload-bbs.miyoushe.com/upload/2023/01/17/8dc22847a6730958d8acef2d49b23779_3259150493896385055.jpg",
            "content_type": 2
          }
        ],
        "user": {
          "uid": "159922380",
          "nickname": "李沐瑟",
          "introduce": "那啥，我能玩到游戏倒闭，萌新交流群798414372 ",
          "avatar": "100302",
          "gender": 0,
          "certification": {
            "type": 2,
            "label": "游戏领域作者、观测者、攻略作者"
          },
          "level_exp": {
            "level": 16,
            "exp": 80360
          },
          "avatar_url": "https://img-static.mihoyo.com/communityweb/upload/e92b5e783ae5ba9d372b4b14f8139a6a.png",
          "pendant": "https://upload-bbs.mihoyo.com/upload/2022/02/15/91e40b079e86bc6f93339be4f68038d1_4869129021901406468.png",
          "is_following": false,
          "is_followed": false
        },
        "self_operation": null,
        "stat": {
          "reply_num": 0,
          "view_num": 0,
          "like_num": 0,
          "bookmark_num": 0
        },
        "cover": {
          "url": "https://upload-bbs.miyoushe.com/upload/2023/02/01/159922380/e55509db76dab0d99ed28fcee9204bc0_8172512981975837842.jpg",
          "height": 600,
          "width": 1067,
          "format": "jpg",
          "size": "837613",
          "crop": null,
          "is_user_set_cover": true,
          "image_id": "122589789",
          "entity_type": "IMG_ENTITY_POST",
          "entity_id": "35089752"
        },
        "image_list": [
          {
            "url": "https://upload-bbs.miyoushe.com/upload/2023/02/01/159922380/e55509db76dab0d99ed28fcee9204bc0_8172512981975837842.jpg",
            "height": 600,
            "width": 1067,
            "format": "jpg",
            "size": "837613",
            "crop": null,
            "is_user_set_cover": false,
            "image_id": "122589789",
            "entity_type": "IMG_ENTITY_POST",
            "entity_id": "35089752"
          },
          ...
        ],
        "is_official_master": false,
        "is_user_master": false,
        "help_sys": {
          "top_up": null
        },
        "vote_count": 0,
        "last_modify_time": 0,
        "recommend_type": "",
        "collection": null,
        "vod_list": [
          {
            "id": "1620586068908748800",
            "duration": 242742,
            "cover": "https://upload-bbs.miyoushe.com/upload/2023/02/01/159922380/68a6611248ef8e1515ee63aa5483d2d2_3826365170291205335.jpg",
            "resolutions": [
              {
                "url": "https://vod-static.miyoushe.com/1/2023-02-01/43828081vodtranscq1500002267/f6f470f9243791579138374920/v.f270753.mp4",
                "definition": "480P",
                "height": 480,
                "width": 852,
                "bitrate": 597038,
                "size": "18114283",
                "format": ".mp4",
                "label": "480P"
              },
              {
                "url": "https://vod-static.miyoushe.com/1/2023-02-01/43828081vodtranscq1500002267/f6f470f9243791579138374920/v.f270754.mp4",
                "definition": "720P",
                "height": 720,
                "width": 1280,
                "bitrate": 2235841,
                "size": "67836002",
                "format": ".mp4",
                "label": "720P"
              },
              {
                "url": "https://vod-static.miyoushe.com/1/2023-02-01/43828081vodtranscq1500002267/f6f470f9243791579138374920/v.f270755.mp4",
                "definition": "1080P",
                "height": 1080,
                "width": 1920,
                "bitrate": 2796292,
                "size": "84840207",
                "format": ".mp4",
                "label": "1080P"
              }
            ],
            "view_num": 2035,
            "transcoding_status": 2,
            "review_status": 2
          }
        ]
      },
      ...
    ],
    "recommended_topics": {
      "list": [
        {
          "id": 1271,
          "name": "艾尔海森",
          "cover": "https://upload-bbs.miyoushe.com/upload/2022/12/15/889ce8e53fe5f84690ce304dc8c5dcbb_3093437298134130485.jpg",
          "desc": "",
          "is_focus": false,
          "view_num": 0,
          "discuss_num": 0
        },
        ...
      ],
      "position": 2
    },
    "fixed_posts": [],
    "selection_post_list": [
      {
        "post_id": "34160507",
        "subject": "原神周本收益分析，老周本BOSS还有打的必要吗",
        "forum_id": 43,
        "forum_name": "攻略",
        "banner": "https://upload-bbs.miyoushe.com/upload/2023/01/10/218792574/4f45a97be9a58d3c601fc88b41422e70_8341995634206658477.png",
        "view_type": 1
      },
      ...
    ]
  }
}
```
</details>


## 获取官方资讯

_请求方式：GET_

`https://bbs-api.miyoushe.com/post/wapi/getNewsList`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| gids | num | 游戏ID | |
| type | num | 资讯类型<br/>1 公告<br/>2 活动<br/>3 资讯 | |
| page_size | num | 每页文章数量<br/>1~50 | 若未指定或超出范围则为每页20篇 |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| retcode | num | 返回码<br/>1001 未指定类型<br/>1002 未指定唯一游戏 | |
| message | str | 返回消息 | |
| data | obj | 资讯信息 | |

`data`对象

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| list | arr | 资讯信息 | |
| last_id | num | 待调查 | |
| is_last | bool | 待调查 | |

`data`对象→`list`数组→对象：

<!-- | 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
|  -->


<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "list": [
      {
        "post": {
          "game_id": 2,
          "post_id": "35274951",
          "f_forum_id": 28,
          "uid": "75276539",
          "subject": "「星彩漫天」——《原神》烟花卡片分享H5正式上线",
          "content": "[图片]旅行者，你喜欢收集卡片吗？派蒙发现了一个好玩的东西！ 「星彩漫天」——《原神》烟花卡片分享H5正式上线。 >>点击前往「星彩漫天」网页活动<<〓活动时间〓卡片收集时间：2023年",
          "cover": "",
          "view_type": 1,
          "created_at": 1675569607,
          "images": [
            "https://upload-bbs.miyoushe.com/upload/2023/02/03/75276539/16038508c15654652a84a93886d9dec2_8099982150962629647.jpg"
          ],
          "post_status": {
            "is_top": false,
            "is_good": false,
            "is_official": true
          },
          "topic_ids": [],
          "view_status": 1,
          "max_floor": 3426,
          "is_original": 0,
          "republish_authorization": 0,
          "reply_time": "2023-02-05 15:19:16",
          "is_deleted": 0,
          "is_interactive": false,
          "structured_content": "[{\"insert\":\"\\n\"},{\"insert\":{\"image\":\"122952038\"}},{\"insert\":\"旅行者，你喜欢收集卡片吗？派蒙发现了一个好玩的东西！ \",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\\n\"},{\"insert\":\"「星彩漫天」——《原神》烟花卡片分享H5正式上线。 \",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"\\u003e\\u003e点击前往「\",\"attributes\":{\"link\":\"https://webstatic.mihoyo.com/ys/event/e20230205-firework-xm7wly/index.html?game_biz=hk4e_cn\\u0026mhy_presentation_style=fullscreen\\u0026mhy_auth_required=true\\u0026mhy_hide_status_bar=true\\u0026channel=mys\\u00260205\"}},{\"insert\":\"星彩漫天\",\"attributes\":{\"link\":\"https://webstatic.mihoyo.com/ys/event/e20230205-firework-xm7wly/index.html?game_biz=hk4e_cn\\u0026mhy_presentation_style=fullscreen\\u0026mhy_auth_required=true\\u0026mhy_hide_status_bar=true\\u0026channel=mys\\u00260205\"}},{\"insert\":\"」网页活动\\u003c\\u003c\",\"attributes\":{\"link\":\"https://webstatic.mihoyo.com/ys/event/e20230205-firework-xm7wly/index.html?game_biz=hk4e_cn\\u0026mhy_presentation_style=fullscreen\\u0026mhy_auth_required=true\\u0026mhy_hide_status_bar=true\\u0026channel=mys\\u00260205\"}},{\"insert\":\"\\n\\n\",\"attributes\":{\"align\":\"center\"}},{\"insert\":\"〓活动时间〓\",\"attributes\":{\"bold\":true,\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"卡片收集时间：2023年2月5日12:00:00-2023月2月11日23:59:59\",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"最终抽奖时间：2023年2月13日12:00:00\",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"奖励领取窗口：2023年2月5日12:00:00-2023月2月18日23:59:59\",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\\n\"},{\"insert\":\"〓参与条件〓\",\"attributes\":{\"bold\":true,\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\" 冒险等阶≥10级  \",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\\n\"},{\"insert\":\"〓活动简介〓 \",\"attributes\":{\"bold\":true,\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"活动期间，旅行者可以收集和交换烟花卡片，在拥有的烟花卡片种类达到一定条件后即可解锁抽奖功能，参与抽奖赢取实物或游戏内奖励。  \",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\\n\"},{\"insert\":\"〓活动玩法说明〓\",\"attributes\":{\"bold\":true,\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"1、活动期间，旅行者可以收集烟花卡片并放入背包，完成每日任务可以获得额外收集次数。 \",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"2、旅行者也可以通过烟花交换，将已拥有的卡片与好友换得尚未拥有的烟花卡片。 烟花交换将不会消耗已拥有的烟花卡片。\",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"3、烟花卡片类型共十一张。每次收集可获得随机一张卡片。 \",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"4、当旅行者拥有所有烟花卡片时，即可解锁抽奖资格，参与烟花抽奖，赢取更多实物奖励。 \",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\\n\"},{\"insert\":\"〓游戏奖励〓 \",\"attributes\":{\"bold\":true,\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"收集全部十一张卡牌后，即可领取原石等游戏奖励。 除参与烟花抽奖时抽取到的奖励之外，所有参与烟花抽奖的旅行者都将得到摩拉、精锻用魔矿等额外游戏奖励。\",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\\n\"},{\"insert\":\"〓活动注意事项〓\",\"attributes\":{\"bold\":true,\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"1、请各位旅行者登录米哈游通行证并绑定《原神》中的游戏角色参与活动，以保证活动奖励的正常发放与领取。 \",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"2、本次活动奖励不默认发放，请旅行者及时领取。 \",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\"},{\"insert\":\"3、在确认发奖资格并确认领取后，奖励将通过游戏内邮件发放，邮件有效期为30天，请注意查收。\",\"attributes\":{\"color\":\"#000000\"}},{\"insert\":\"\\n\"}]",
          "structured_content_rows": [],
          "review_id": 0,
          "is_profit": false,
          "is_in_profit": false,
          "updated_at": 1675581556,
          "deleted_at": 0,
          "pre_pub_status": 0,
          "cate_id": 0,
          "profit_post_status": -2,
          "audit_status": 0,
          "meta_content": "",
          "is_missing": false,
          "block_reply_img": 1,
          "is_showing_missing": false
        },
        "forum": {
          "id": 28,
          "name": "官方",
          "icon": "https://upload-bbs.mihoyo.com/upload/2020/04/05/1e49d332b6ca6dc3367801eea655dfdb.png",
          "game_id": 2,
          "forum_cate": null
        },
        "topics": [],
        "user": {
          "uid": "75276539",
          "nickname": "原神",
          "introduce": "",
          "avatar": "10011",
          "gender": 0,
          "certification": {
            "type": 1,
            "label": "原神官方账号"
          },
          "level_exp": {
            "level": 16,
            "exp": 107659
          },
          "is_following": false,
          "is_followed": false,
          "avatar_url": "https://img-static.mihoyo.com/avatar/avatar10011.png",
          "pendant": ""
        },
        "self_operation": {
          "attitude": 0,
          "is_collected": false
        },
        "stat": {
          "view_num": 437607,
          "reply_num": 5298,
          "like_num": 73584,
          "bookmark_num": 1380,
          "forward_num": 654
        },
        "help_sys": {
          "top_up": null,
          "top_n": [],
          "answer_num": 0
        },
        "cover": null,
        "image_list": [
          {
            "url": "https://upload-bbs.miyoushe.com/upload/2023/02/03/75276539/16038508c15654652a84a93886d9dec2_8099982150962629647.jpg",
            "height": 320,
            "width": 690,
            "format": "jpg",
            "size": "249835",
            "crop": null,
            "is_user_set_cover": false,
            "image_id": "122952038",
            "entity_type": "IMG_ENTITY_POST",
            "entity_id": "35274951"
          }
        ],
        "is_official_master": false,
        "is_user_master": false,
        "hot_reply_exist": false,
        "vote_count": 0,
        "last_modify_time": 0,
        "recommend_type": "",
        "collection": null,
        "vod_list": [],
        "is_block_on": false,
        "forum_rank_info": null,
        "link_card_list": [],
        "news_meta": {
          "activity_status": 1,
          "start_at_sec": "1675569600",
          "end_at_sec": "1676131140"
        }
      },
      ...
    ],
    "last_id": 1,
    "is_last": false
  }
}
```
</details>


## 获取完整文章信息

_请求方式：GET_

鉴权方式：
头部：`x-rpc-app_version`、`x-rpc-client_type`、`x-rpc-`

`https://bbs-api.miyoushe.com/post/wapi/getPostFull`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| gids | num | 游戏ID | |
| 

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| retcode | num | 返回码<br/>1 未选择游戏 | |
| message | str | 返回消息 | |
| data | obj | 首页信息 | |


<details>
<summary>查看示例</summary>

```json
```
</details>
