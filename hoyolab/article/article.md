

# 论坛文章

- [获取首页信息](#获取首页信息)
- [获取官方资讯](#获取官方资讯)
- [获取完整文章信息](#获取完整文章信息)
- [获取文章评论信息](#获取文章评论信息)

---

## 获取首页信息

_请求方式：GET_

`https://bbs-api-static.miyoushe.com/apihub/wapi/webHome`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| gids | num | 游戏ID | |
| page | num | 页数 | 若未指定则为第1页 |
| page_size | num | 每页文章数量，范围为1-50 | 若未指定或超出范围则为每页20篇 |

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
| view_type               | num  | 文章呈现类型<br />1 内容以文字类文章为主<br />2 内容以图片类文章为主<br />5 内容以视频类文章为主 | 文字类文章示例：[【V3.8攻略·七圣召唤】万叶、烟绯、坎蒂丝新卡一图流解读！-原神社区-米游社 (miyoushe.com)](https://www.miyoushe.com/ys/article/41059886)<br />图片类文章示例：[「可莉」头像 一起来玩吧~~~~【观测枢】-原神社区-米游社 (miyoushe.com)](https://www.miyoushe.com/ys/article/41214610)<br />视频类文章示例：[【欢愉一夏主题视频】3.8游园会BGM神还原~(观测枢)-原神社区-米游社 (miyoushe.com)](https://www.miyoushe.com/ys/article/41175339) |
| created_at | num | 文章创建的Unix时间戳 | |
| images | arr | 文章中每张图片的链接 | |
| post_status | obj | 文章状态数据 | |
| topic_ids | arr | 文章的话题的ID | |
| view_status | num | 待调查 |  |
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
| view_type  | num  | 文章呈现类型<br />1 内容以文字类文章为主<br />2 内容以图片类文章为主<br />5 内容以视频类文章为主 | 文字类文章示例：[【V3.8攻略·七圣召唤】万叶、烟绯、坎蒂丝新卡一图流解读！-原神社区-米游社 (miyoushe.com)](https://www.miyoushe.com/ys/article/41059886)<br />图片类文章示例：[「可莉」头像 一起来玩吧~~~~【观测枢】-原神社区-米游社 (miyoushe.com)](https://www.miyoushe.com/ys/article/41214610)<br />视频类文章示例：[【欢愉一夏主题视频】3.8游园会BGM神还原~(观测枢)-原神社区-米游社 (miyoushe.com)](https://www.miyoushe.com/ys/article/41175339) |


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
| retcode | num | 返回码<br/>1001 参数`type`不正确<br/>1002 参数`gids`不正确 | |
| message | str | 返回消息 | |
| data | obj | 资讯信息 | |

`data`对象

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| list | arr | 资讯信息 | |
| last_id | num | 待调查 | |
| is_last | bool | 待调查 | |

`data`对象→`list`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
|  |  |  |  |


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
          "post_id": "39530410",
          "f_forum_id": 28,
          "uid": "384454482",
          "subject": "「原神赛事解说主持招募」计划启动",
          "content": "▌「原神赛事解说主持招募」计划启动亲爱的旅行者，请查收这份招募指南！即日起至5月28日，原神赛事将开启首批解说主持招募报名如果你正在寻找演艺的契机，不如一起开启一段崭新的冒险吧！★ 期待",
          "cover": "",
          "view_type": 1,
          "created_at": 1684555284,
          "images": [
            "https://upload-bbs.miyoushe.com/upload/2023/05/20/384454482/316ebd6113fd3923768a73e4d097a296_7231734090118733998.jpg"
          ],
          "post_status": {
            "is_top": false,
            "is_good": false,
            "is_official": true
          },
          "topic_ids": [
            1264
          ],
          "view_status": 1,
          "max_floor": 38,
          "is_original": 0,
          "republish_authorization": 0,
          "reply_time": "2023-05-20 15:40:55",
          "is_deleted": 0,
          "is_interactive": false,
          "structured_content": "[{\"insert\":\"▌「原神赛事解说主持招募」计划启动\\n\\n亲爱的旅行者，请查收这份招募指南！\\n\\n即日起至5月28日，原神赛事将开启首批解说主持招募报名\\n如果你正在寻找演艺的契机，不如一起开启一段崭新的冒险吧！\\n\\n★ 期待看见在舞台上闪耀的大家！\\n\"},{\"insert\":{\"image\":\"136156250\"}},{\"insert\":\"\\n\\n\"}]",
          "structured_content_rows": [],
          "review_id": 0,
          "is_profit": false,
          "is_in_profit": false,
          "updated_at": 1684568455,
          "deleted_at": 0,
          "pre_pub_status": 0,
          "cate_id": 0,
          "profit_post_status": -2,
          "audit_status": 0,
          "meta_content": "",
          "is_missing": false,
          "block_reply_img": 1,
          "is_showing_missing": false,
          "block_latest_reply_time": 0,
          "selected_comment": 0
        },
        "forum": {
          "id": 28,
          "name": "官方",
          "icon": "https://upload-bbs.mihoyo.com/upload/2020/04/05/1e49d332b6ca6dc3367801eea655dfdb.png",
          "game_id": 2,
          "forum_cate": null
        },
        "topics": [
          {
            "id": 1264,
            "name": "七圣召唤",
            "cover": "https://upload-bbs.miyoushe.com/upload/2022/11/25/fbab7b47dce9d09cb1f06557531ac9a1_1617410903526086645.jpg",
            "is_top": false,
            "is_good": false,
            "is_interactive": false,
            "game_id": 0,
            "content_type": 2
          }
        ],
        "user": {
          "uid": "384454482",
          "nickname": "原神赛事",
          "introduce": "",
          "avatar": "101070",
          "gender": 0,
          "certification": {
            "type": 1,
            "label": "原神赛事官方账号"
          },
          "level_exp": {
            "level": 3,
            "exp": 172
          },
          "is_following": false,
          "is_followed": false,
          "avatar_url": "https://bbs-static.miyoushe.com/static/2023/05/12/b85ea3822de881e64920ffdf3d8aed77_1765242819614536153.png",
          "pendant": ""
        },
        "self_operation": {
          "attitude": 0,
          "is_collected": false
        },
        "stat": {
          "view_num": 2524,
          "reply_num": 54,
          "like_num": 439,
          "bookmark_num": 7,
          "forward_num": 5
        },
        "help_sys": {
          "top_up": null,
          "top_n": [],
          "answer_num": 0
        },
        "cover": null,
        "image_list": [
          {
            "url": "https://upload-bbs.miyoushe.com/upload/2023/05/20/384454482/316ebd6113fd3923768a73e4d097a296_7231734090118733998.jpg",
            "height": 2817,
            "width": 1000,
            "format": "jpg",
            "size": "1294054",
            "crop": null,
            "is_user_set_cover": false,
            "image_id": "136156250",
            "entity_type": "IMG_ENTITY_POST",
            "entity_id": "39530410",
            "is_deleted": false
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
          "activity_status": 0,
          "start_at_sec": "0",
          "end_at_sec": "0"
        }
      }
    ],
    "last_id": 1,
    "is_last": false
  }
}
```
</details>


## 获取完整文章信息

_请求方式：GET_

> _需要验证请求头_

网页：`https://bbs-api.miyoushe.com/post/wapi/getPostFull`
应用：`https://bbs-api.miyoushe.com/post/api/getPostFull`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| post_id | num | 文章ID | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| retcode | num | 返回码<br>1101 参数`post_id`对应的文章不存在 | |
| message | str | 返回消息 | |
| data | obj | 文章信息 | |

`data`对象→`post`对象：

| 字段               | 类型        | 内容                       | 备注                                |
| ------------------ | ----------- | -------------------------- | ----------------------------------- |
| post               | obj         | 文章内容                   |                                     |
| forum              | obj         | 板块信息                   |                                     |
| topics             | obj         | 文章的标签                 |                                     |
| user               | obj         | 发布者的信息               |                                     |
| stat               | obj         | 文章统计信息               |                                     |
| help_sys           | null        | 待调查                     |                                     |
| cover              | null \| obj | 文章封面                   | 若发布者未设置封面，则该项为null    |
| last_modify_time   | num         | 该文章的上次修改时间       | 时间为unix时间戳，视频类文章可能为0 |
| vod_list           | arr         | 视频的分片信息             | 非视频类文章的长度为0               |
| link_card_list     | arr         | 该文章所含的链接卡片的信息 |                                     |
| help_sys           | null        | 待调查                     |                                     |
| is_official_master | bool        | 待调查                     |                                     |
| is_user_master     | bool        | 待调查                     |                                     |
| hot_reply_exist    | bool        | 待调查                     |                                     |
| vote_count         | num         | 待调查                     |                                     |
| recommend_type     | str         | 待调查                     |                                     |
| collection         | arr         | 合集信息                   |                                     |
| is_block_on        | bool        | 待调查                     |                                     |
| forum_rank_info    | null        | 待调查                     |                                     |
| news_meta          | null        | 待调查                     |                                     |

`data`对象→`post`对象→`post`对象：

| 字段                    | 类型 | 内容                                                         | 备注                                                         |
| ----------------------- | ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| game_id                 | num  | 游戏id                                                       |                                                              |
| post_id                 | str  | 文章id                                                       |                                                              |
| f_forum_id              | num  | 板块id                                                       |                                                              |
| uid                     | str  | 发布者的uid                                                  |                                                              |
| subject                 | str  | 文章标题                                                     |                                                              |
| content                 | str  | 文章内容                                                     | 内容为html结构                                               |
| cover                   | str  | 文章封面                                                     | 若发布者未设置封面，则该项为空字符串                         |
| view_type               | num  | 文章呈现类型<br />1 内容以文字类文章为主<br />2 内容以图片类文章为主<br />5 内容以视频类文章为主 | 文字类文章示例：[【V3.8攻略·七圣召唤】万叶、烟绯、坎蒂丝新卡一图流解读！-原神社区-米游社 (miyoushe.com)](https://www.miyoushe.com/ys/article/41059886)<br />图片类文章示例：[「可莉」头像 一起来玩吧~~~~【观测枢】-原神社区-米游社 (miyoushe.com)](https://www.miyoushe.com/ys/article/41214610)<br />视频类文章示例：[【欢愉一夏主题视频】3.8游园会BGM神还原~(观测枢)-原神社区-米游社 (miyoushe.com)](https://www.miyoushe.com/ys/article/41175339) |
| created_at              | num  | 文章发布时间                                                 | 时间为unix时间戳                                             |
| image                   | arr  | 文章中出现的图片                                             |                                                              |
| post_status             | obj  | 文章状态                                                     |                                                              |
| topic_ids               | arr  | 文章所涉及到的标签id                                         |                                                              |
| view_status             | num  | 待调查                                                       |                                                              |
| max_floor               | num  | 待调查                                                       |                                                              |
| is_original             | num  | 是否为原创内容                                               |                                                              |
| republish_authorization | num  | 待调查                                                       |                                                              |
| reply_time              | str  | 最后一次的回复时间                                           |                                                              |
| is_deleted              | num  | 是否被删除                                                   |                                                              |
| is_interactive          | bool | 是否为互动内容                                               |                                                              |
| structured_content      | str  | 结构化的内容                                                 | 可使用json解析器对其进行解析                                 |
| structured_content_rows | arr  | 待调查                                                       |                                                              |
| review_id               | num  | 待调查                                                       |                                                              |
| is_profit               | bool | 待调查                                                       |                                                              |
| is_in_profit            | bool | 待调查                                                       |                                                              |
| updated_at              | num  | 上次更新时间                                                 | 时间为unix时间戳                                             |
| deleted_at              | num  | 删除时间                                                     | 时间为unix时间戳                                             |
| pre_pub_status          | num  | 待调查                                                       |                                                              |
| cate_id                 | num  | 待调查                                                       |                                                              |
| profit_post_status      | num  | 待调查                                                       |                                                              |
| audit_status            | num  | 待调查                                                       |                                                              |
| meta_content            | str  | 待调查                                                       |                                                              |
| is_missing              | bool | 待调查                                                       |                                                              |
| block_reply_img         | num  | 待调查                                                       |                                                              |
| is_showing_missing      | bool | 待调查                                                       |                                                              |
| block_latest_reply_time | num  | 待调查                                                       |                                                              |
| selected_comment        | num  | 待调查                                                       |                                                              |

`data`对象→`post`对象→`forum`对象：

| 字段       | 类型 | 内容             | 备注 |
| ---------- | ---- | ---------------- | ---- |
| id         | num  | 板块id           |      |
| name       | str  | 板块名称         |      |
| icon       | str  | 板块图标         |      |
| game_id    | num  | 板块所属的游戏id |      |
| forum_cate | null | 待调查           |      |

`data`对象→`post`对象→`topics`列表→对象：

| 字段           | 类型 | 内容     | 备注 |
| -------------- | ---- | -------- | ---- |
| id             | num  | 标签id   |      |
| name           | str  | 标签名   |      |
| cover          | str  | 标签封面 |      |
| is_top         | bool | 待调查   |      |
| is_good        | bool | 待调查   |      |
| is_interactive | bool | 待调查   |      |
| game_id        | num  | 待调查   |      |
| content_type   | num  | 待调查   |      |

`data`对象→`post`对象→`user`对象：

| 字段          | 类型 | 内容             | 备注 |
| ------------- | ---- | ---------------- | ---- |
| uid           | str  | 用户uid          |      |
| nickname      | str  | 用户昵称         |      |
| introduce     | str  | 用户简介         |      |
| avatar        | str  | 用户头像id       |      |
| gender        | num  | 用户性别         |      |
| certification | obj  | 用户认证信息     |      |
| level_exp     | obj  | 用户社区经验     |      |
| is_following  | bool | 是否为正在关注   |      |
| is_followed   | bool | 是否为曾经关注的 |      |
| avatar_url    | str  | 用户头像链接     |      |
| pendant       | str  | 用户头像挂件     |      |

`data`对象→`post`对象→`user`对象→`certification`对象：

| 字段  | 类型 | 内容                                                         | 备注 |
| ----- | ---- | ------------------------------------------------------------ | ---- |
| type  | num  | 认证类别<br />1 社区或游戏官方<br />2 已认证的创作者<br />0 未认证的用户 |      |
| label | str  | 认证具体信息                                                 |      |

`data`对象→`post`对象→`user`对象→`level_exp`对象：

| 字段  | 类型 | 内容           | 备注 |
| ----- | ---- | -------------- | ---- |
| level | num  | 用户的社区等级 |      |
| exp   | num  | 用户的社区经验 |      |

`data`对象→`post`对象→`collection`对象：

| 字段                | 类型 | 内容                           | 备注 |
| ------------------- | ---- | ------------------------------ | ---- |
| prev_post_id        | str  | 该集合下的上一篇文章的文章id   |      |
| next_post_id        | str  | 该集合下的下一篇文章的文章id   |      |
| collection_id       | str  | 集合id                         |      |
| cur                 | num  | 当前文章在该集合下的指针       |      |
| total               | num  | 该集合下的所有文章数量         |      |
| collection_title    | str  | 集合标题                       |      |
| prev_post_game_id   | num  | 该集合下的上一篇文章的游戏id   |      |
| next_post_game_id   | num  | 该集合下的下一篇文章的游戏id   |      |
| prev_post_view_type | num  | 该集合下的上一篇文章的呈现类型 |      |
| next_post_view_type | num  | 该集合下的下一篇文章的呈现类型 |      |

`data`对象→`post`对象→`link_card_list`数组→对象：

| 字段                   | 类型 | 内容         | 备注 |
| ---------------------- | ---- | ------------ | ---- |
| link_type              | num  | 待调查       |      |
| origin_url             | str  | 卡片跳转链接 |      |
| landing_url            | str  | 卡片跳转链接 |      |
| cover                  | str  | 卡片封面链接 |      |
| title                  | str  | 卡片标题     |      |
| origin_user_avatar     | str  | 待调查       |      |
| origin_user_nickname   | str  | 待调查       |      |
| card_id                | str  | 卡片id       |      |
| card_status            | num  | 卡片状态     |      |
| market_price           | str  | 待调查       |      |
| price                  | str  | 待调查       |      |
| button_text            | str  | 待调查       |      |
| landing_url_type       | num  | 待调查       |      |
| card_meta              | null | 待调查       |      |
| origin_user_avatar_url | str  | 待调查       |      |


<details>
<summary>查看示例</summary>

```json
{
  "data": {
    "post": {
      "post": {
        "game_id": 2,
        "post_id": "41059886",
        "f_forum_id": 43,
        "uid": "8625030",
        "subject": "【V3.8攻略·七圣召唤】万叶、烟绯、坎蒂丝新卡一图流解读！",
        "content": "<p>UID：100068298</p><p>万叶：更顺滑的扩体系</p><p>烟绯：平稳输出的重击角色</p><p>坎蒂丝：攻守兼备的水系第三</p><div class=\"ql-image\"><div class=\"ql-image-box\"><img src=\"https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/db192e0f21f2719c13c69bc85175f282_5699736559184340260.jpg\"></div></div><div class=\"ql-image\"><div class=\"ql-image-box\"><img src=\"https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/f8db66f0beb54e3423d3d8e6cacfd7e4_2535685064569067888.jpg\"></div></div><div class=\"ql-image\"><div class=\"ql-image-box\"><img src=\"https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/40b282ea11d5b7ac5c037b3af6016dc2_7874735248209588968.jpg\"></div></div><p><br></p><p class=\"ql-align-center\">想查看更多七圣相关内容</p><p class=\"ql-align-center\">不妨点击下方链接！（原神观测枢里啥都有！贼好看！233333）</p><p class=\"ql-align-center\"><br></p><div class=\"ql-link-card\"><a href=\"https://bbs.mihoyo.com/ys/strategy/summon?bbs_presentation_style=no_header\" target=\"_blank\" class=\"mhy-link-card card-normal\"><div class=\"card-cover\" style=\"background-image: url(&#34;https://img-static.mihoyo.com/card/bbs_entity_normal.png&#34;);\"></div> <div class=\"card-info\"><div class=\"card-title\">旅行者创作平台-观测枢-原神wiki旅行者创作平台-观测枢-原神wiki</div> </div></a></div><p class=\"ql-align-center\"><br></p><div class=\"ql-image ql-align-center\"><div class=\"ql-image-box\"><img src=\"https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/925d88ae002ac40aca17affb5eae12b8_8695567098614745990.jpeg\"></div></div>",
        "cover": "",
        "view_type": 1,
        "created_at": 1688792222,
        "images": [
          "https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/db192e0f21f2719c13c69bc85175f282_5699736559184340260.jpg",
          "https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/f8db66f0beb54e3423d3d8e6cacfd7e4_2535685064569067888.jpg",
          "https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/40b282ea11d5b7ac5c037b3af6016dc2_7874735248209588968.jpg",
          "https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/925d88ae002ac40aca17affb5eae12b8_8695567098614745990.jpeg"
        ],
        "post_status": {
          "is_top": false,
          "is_good": false,
          "is_official": false
        },
        "topic_ids": [
          818,
          947,
          1264,
          1442
        ],
        "view_status": 1,
        "max_floor": 5,
        "is_original": 1,
        "republish_authorization": 2,
        "reply_time": "2023-07-13 16:04:27",
        "is_deleted": 0,
        "is_interactive": false,
        "structured_content": "[{\"insert\":\"UID：100068298\\n万叶：更顺滑的扩体系\\n烟绯：平稳输出的重击角色\\n坎蒂丝：攻守兼备的水系第三\\n\"},{\"insert\":{\"image\":\"https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/db192e0f21f2719c13c69bc85175f282_5699736559184340260.jpg\"},\"attributes\":{\"height\":10187,\"width\":3401,\"size\":8673621,\"ext\":\"jpg\"}},{\"insert\":{\"image\":\"https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/f8db66f0beb54e3423d3d8e6cacfd7e4_2535685064569067888.jpg\"},\"attributes\":{\"height\":10187,\"width\":3401,\"size\":7970675,\"ext\":\"jpg\"}},{\"insert\":{\"image\":\"https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/40b282ea11d5b7ac5c037b3af6016dc2_7874735248209588968.jpg\"},\"attributes\":{\"height\":10187,\"width\":3401,\"size\":8702329,\"ext\":\"jpg\"}},{\"insert\":\"\\n想查看更多七圣相关内容\"},{\"insert\":\"\\n\",\"attributes\":{\"align\":\"center\"}},{\"insert\":\"不妨点击下方链接！（原神观测枢里啥都有！贼好看！233333）\"},{\"insert\":\"\\n\\n\",\"attributes\":{\"align\":\"center\"}},{\"insert\":{\"link_card\":{\"link_type\":1,\"origin_url\":\"https://bbs.mihoyo.com/ys/strategy/summon?bbs_presentation_style=no_header\",\"landing_url\":\"https://bbs.mihoyo.com/ys/strategy/summon?bbs_presentation_style=no_header\",\"cover\":\"https://img-static.mihoyo.com/card/bbs_entity_normal.png\",\"title\":\"旅行者创作平台-观测枢-原神wiki旅行者创作平台-观测枢-原神wiki\",\"card_id\":\"1619262852990324736\",\"card_status\":1,\"landing_url_type\":1}}},{\"insert\":\"\\n\",\"attributes\":{\"align\":\"center\"}},{\"insert\":{\"image\":\"https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/925d88ae002ac40aca17affb5eae12b8_8695567098614745990.jpeg\"},\"attributes\":{\"align\":\"center\",\"height\":270,\"width\":1080,\"size\":41161,\"ext\":\"jpg\"}},{\"insert\":\"\\n\"}]",
        "structured_content_rows": [],
        "review_id": 0,
        "is_profit": false,
        "is_in_profit": true,
        "updated_at": 1689235467,
        "deleted_at": 0,
        "pre_pub_status": 0,
        "cate_id": 0,
        "profit_post_status": -2,
        "audit_status": 0,
        "meta_content": "",
        "is_missing": false,
        "block_reply_img": 1,
        "is_showing_missing": false,
        "block_latest_reply_time": 0,
        "selected_comment": 2
      },
      "forum": {
        "id": 43,
        "name": "攻略",
        "icon": "https://upload-bbs.mihoyo.com/upload/2020/09/14/ce666cea7c971b04e4b4a6fe0a9ebfd0.png",
        "game_id": 2,
        "forum_cate": null
      },
      "topics": [
        {
          "id": 818,
          "name": "萌新冒险手册",
          "cover": "https://upload-bbs.mihoyo.com/upload/2021/10/19/f71efba1fba54f7f0f9ecf97646007fb_4823359932407618155.png",
          "is_top": false,
          "is_good": false,
          "is_interactive": false,
          "game_id": 0,
          "content_type": 2
        },
        {
          "id": 947,
          "name": "原神观测枢",
          "cover": "https://upload-bbs.mihoyo.com/upload/2022/02/14/8efc5670a3dd0467bf7fb1866bd5d203_2630690909080422615.png",
          "is_top": false,
          "is_good": false,
          "is_interactive": false,
          "game_id": 0,
          "content_type": 2
        },
        {
          "id": 1264,
          "name": "七圣召唤",
          "cover": "https://upload-bbs.miyoushe.com/upload/2022/11/25/fbab7b47dce9d09cb1f06557531ac9a1_1617410903526086645.jpg",
          "is_top": false,
          "is_good": false,
          "is_interactive": false,
          "game_id": 0,
          "content_type": 2
        },
        {
          "id": 1442,
          "name": "原神3.8攻略征集",
          "cover": "https://bbs-static.miyoushe.com/static/2023/07/05/cd54aef8d8f13f8fe50e5969287afd23_1358935079530174555.jpg",
          "is_top": false,
          "is_good": false,
          "is_interactive": false,
          "game_id": 0,
          "content_type": 3
        }
      ],
      "user": {
        "uid": "8625030",
        "nickname": "疲惫不堪的嘤酱",
        "introduce": "观测枢不知名编辑，《萌新手册》群：641333155",
        "avatar": "100291",
        "gender": 0,
        "certification": {
          "type": 2,
          "label": "观测者、游戏领域作者、攻略作者"
        },
        "level_exp": {
          "level": 16,
          "exp": 75725
        },
        "is_following": false,
        "is_followed": false,
        "avatar_url": "https://img-static.mihoyo.com/communityweb/upload/15032157c9308b6caf01ad3df6ee8ea8.png",
        "pendant": "https://upload-bbs.mihoyo.com/upload/2020/08/14/e1c20ea595bf737350b54fc28ba8114f_7790722755343149315.png"
      },
      "self_operation": {
        "attitude": 0,
        "is_collected": false
      },
      "stat": {
        "view_num": 441,
        "reply_num": 7,
        "like_num": 97,
        "bookmark_num": 1,
        "forward_num": 1
      },
      "help_sys": null,
      "cover": null,
      "image_list": [
        {
          "url": "https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/db192e0f21f2719c13c69bc85175f282_5699736559184340260.jpg",
          "height": 10187,
          "width": 3401,
          "format": "jpg",
          "size": "8673621",
          "crop": null,
          "is_user_set_cover": false,
          "image_id": "141465208",
          "entity_type": "IMG_ENTITY_POST",
          "entity_id": "41059886",
          "is_deleted": false
        },
        {
          "url": "https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/f8db66f0beb54e3423d3d8e6cacfd7e4_2535685064569067888.jpg",
          "height": 10187,
          "width": 3401,
          "format": "jpg",
          "size": "7970675",
          "crop": null,
          "is_user_set_cover": false,
          "image_id": "141464931",
          "entity_type": "IMG_ENTITY_POST",
          "entity_id": "41059886",
          "is_deleted": false
        },
        {
          "url": "https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/40b282ea11d5b7ac5c037b3af6016dc2_7874735248209588968.jpg",
          "height": 10187,
          "width": 3401,
          "format": "jpg",
          "size": "8702329",
          "crop": null,
          "is_user_set_cover": false,
          "image_id": "141464962",
          "entity_type": "IMG_ENTITY_POST",
          "entity_id": "41059886",
          "is_deleted": false
        },
        {
          "url": "https://upload-bbs.miyoushe.com/upload/2023/07/08/8625030/925d88ae002ac40aca17affb5eae12b8_8695567098614745990.jpeg",
          "height": 270,
          "width": 1080,
          "format": "jpg",
          "size": "41161",
          "crop": null,
          "is_user_set_cover": false,
          "image_id": "141465005",
          "entity_type": "IMG_ENTITY_POST",
          "entity_id": "41059886",
          "is_deleted": false
        }
      ],
      "is_official_master": false,
      "is_user_master": false,
      "hot_reply_exist": false,
      "vote_count": 0,
      "last_modify_time": 1688792279,
      "recommend_type": "",
      "collection": {
        "prev_post_id": "39655694",
        "next_post_id": "0",
        "collection_id": "1609609",
        "cur": 9,
        "total": 9,
        "collection_title": "七圣召唤",
        "prev_post_game_id": 2,
        "next_post_game_id": 0,
        "prev_post_view_type": 1,
        "next_post_view_type": 0
      },
      "vod_list": [],
      "is_block_on": false,
      "forum_rank_info": null,
      "link_card_list": [
        {
          "link_type": 1,
          "origin_url": "https://bbs.mihoyo.com/ys/strategy/summon?bbs_presentation_style=no_header",
          "landing_url": "https://bbs.mihoyo.com/ys/strategy/summon?bbs_presentation_style=no_header",
          "cover": "https://img-static.mihoyo.com/card/bbs_entity_normal.png",
          "title": "旅行者创作平台-观测枢-原神wiki旅行者创作平台-观测枢-原神wiki",
          "origin_user_avatar": "",
          "origin_user_nickname": "",
          "card_id": "1619262852990324736",
          "card_status": 1,
          "market_price": "",
          "price": "",
          "button_text": "",
          "landing_url_type": 1,
          "card_meta": null,
          "origin_user_avatar_url": ""
        }
      ],
      "news_meta": null
    }
  },
  "message": "OK",
  "retcode": 0
}
```
</details>

## 获取文章评论信息

_请求方式：GET_

`https://bbs-api.miyoushe.com/post/wapi/getPostReplies`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| gids | num | 游戏id |  |
| is_hot | bool | 是否以热度排序 |  |
| post_id | num | 文章id |  |
| size | num | 请求的最大评论数量(0-20) |  |
| last_id | num | 从last_id处向下获取评论 | 若不传入该字段，则默认从评论第1条开始获取 |

根对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| retcode | num | 返回码<br>1101 参数`post_id`对应的文章不存在 | |
| message | str | 返回消息 | |
| data | obj | 评论信息 | |

`data`对象：

| 字段           | 类型 | 内容                                 | 备注 |
| -------------- | ---- | ------------------------------------ | ---- |
| list           | arr  | 用户评论列表                         |      |
| last_id        | num  | 当次请求下的最后一条的评论id         |      |
| is_last        | bool | 当次请求是否含有该文章中最后一条评论 |      |
| pin_reply_id   | num  | 置顶评论的id                         |      |
| post_owner_uid | num  | 文章作者uid                          |      |

`data`对象→`list`数组→对象   或   `data`对象→`list`数组→对象→`sub_replies`对象：

| 字段            | 类型        | 内容               | 备注                              |
| --------------- | ----------- | ------------------ | --------------------------------- |
| images          | arr         | 评论中的图片对象   |                                   |
| is_lz           | bool        | 是否为楼主         |                                   |
| master_status   | obj         | 待调查             |                                   |
| r_post          | null        | 待调查             |                                   |
| r_reply         | null        | 待调查             |                                   |
| r_user          | null \| obj | 被回复的用户信息   | 当评论为子评论时为obj，否则为null |
| reply           | obj         | 回复信息           |                                   |
| self_operation  | obj         | 待调查             |                                   |
| stat            | obj         | 评论统计信息       |                                   |
| sub_replies     | arr         | 该评论下的评论信息 |                                   |
| sub_reply_count | num         | 该评论下有多少评论 |                                   |
| user            | obj         | 发表评论的用户信息 |                                   |

`data`对象→`list`数组→对象→`images`数组→对象   或   `data`对象→`list`数组→对象→`sub_replies`对象→`images`数组→对象：

| 字段        | 类型 | 内容        | 备注 |
| ----------- | ---- | ----------- | ---- |
| entity_id   | str  | 实体id      |      |
| entity_type | str  | 实体类型    |      |
| format      | str  | 图片格式    |      |
| height      | num  | 图片高度    |      |
| image_id    | str  | 图片id      |      |
| is_deleted  | bool | 是否被删除  |      |
| url         | str  | 图片url链接 |      |
| width       | num  | 图片宽度    |      |

`data`对象→`list`数组→对象→`reply`对象   或   `data`对象→`list`数组→对象→`sub_replies`对象→`reply`对象：

| 字段                    | 类型 | 内容                | 备注                         |
| ----------------------- | ---- | ------------------- | ---------------------------- |
| content                 | str  | 评论内容            |                              |
| created_at              | num  | 发布日期            |                              |
| delete_src              | num  | 待调查              |                              |
| deleted_at              | num  | 待调查              |                              |
| f_forum_id              | num  | 文章板块id          |                              |
| f_reply_id              | str  | 待调查              |                              |
| floor_id                | num  | 评论所在的楼层数    |                              |
| game_id                 | num  | 游戏id              |                              |
| has_block_word          | bool | 是否存在敏感词      |                              |
| is_deleted              | num  | 是否被删除          |                              |
| is_showing_missing      | bool | 是否显示已丢失      |                              |
| is_top                  | bool | 是否置顶            |                              |
| overt_status            | num  | 待调查              |                              |
| post_id                 | str  | 文章id              |                              |
| r_uid                   | str  | 待调查              |                              |
| reply_id                | str  | 评论id              |                              |
| selected_comment_time   | num  | 待调查              |                              |
| struct_content          | str  | 结构化的评论内容    | 可使用json解析器对其进行解析 |
| structured_content_rows | arr  | 待调查              |                              |
| uid                     | str  | 发表评论的用户的uid |                              |
| updated_at              | num  | 上次更新时间        |                              |

`data`对象→`list`数组→对象→`stat`对象   或   `data`对象→`list`数组→对象→`sub_replies`对象→`stat`对象：

| 字段        | 类型 | 内容       | 备注        |
| ----------- | ---- | ---------- | ----------- |
| dislike_num | num  | 点踩数量   |             |
| like_num    | num  | 点赞数量   |             |
| reply_num   | num  | 评论数量   | 此处一般为0 |
| sub_num     | num  | 子评论数量 |             |

`data`对象→`list`数组→`user`对象   或   `data`对象→`list`数组→对象→`sub_replies`对象→`user`对象：

| 字段          | 类型 | 内容         | 备注 |
| ------------- | ---- | ------------ | ---- |
| uid           | str  | 用户uid      |      |
| nickname      | str  | 用户昵称     |      |
| introduce     | str  | 用户简介     |      |
| avatar        | str  | 用户头像id   |      |
| gender        | num  | 用户性别     |      |
| certification | obj  | 用户认证信息 |      |
| level_exp     | obj  | 用户社区经验 |      |
| ip_region     | str  | ip属地       |      |
| avatar_url    | str  | 用户头像链接 |      |
| pendant       | str  | 用户头像挂件 |      |

`data`对象→`list`数组→`user`对象→`certification`对象   或   `data`对象→`list`数组→对象→`sub_replies`对象→`user`对象→`certification`对象：

| 字段  | 类型 | 内容                                                         | 备注 |
| ----- | ---- | ------------------------------------------------------------ | ---- |
| type  | num  | 认证类别<br />1 社区或游戏官方<br />2 已认证的创作者<br />0 未认证的用户 |      |
| label | str  | 认证具体信息                                                 |      |

`data`对象→`list`数组→`user`对象→`level_exp`对象   或   `data`对象→`list`数组→对象→`sub_replies`对象→`user`对象→`level_exp`对象：

| 字段  | 类型 | 内容           | 备注 |
| ----- | ---- | -------------- | ---- |
| level | num  | 用户的社区等级 |      |
| exp   | num  | 用户的社区经验 |      |





<details>
<summary>查看示例</summary>

```json
{
    "retcode": 0,
    "message": "OK",
    "data": {
        "list": [
            {
                "reply": {
                    "game_id": 2,
                    "post_id": "41200597",
                    "reply_id": "1679067950588375040",
                    "uid": "296742597",
                    "r_uid": "0",
                    "content": "差3个月才满18<img src=\"https://upload-bbs.miyoushe.com/upload/2023/07/12/296742597/74dc09c514c0dbca30db01d93cd607af_1723221593250820730.jpg\">",
                    "f_forum_id": 28,
                    "f_reply_id": "0",
                    "floor_id": 38,
                    "is_deleted": 0,
                    "delete_src": 0,
                    "created_at": 1689155969,
                    "updated_at": 1689156176,
                    "deleted_at": 2288912640,
                    "struct_content": "[{\"insert\":\"差3个月才满18\\r\\n\"},{\"insert\":{\"image\":\"https://upload-bbs.miyoushe.com/upload/2023/07/12/296742597/74dc09c514c0dbca30db01d93cd607af_1723221593250820730.jpg\"},\"attributes\":{\"height\":117,\"width\":177}},{\"insert\":\"\\r\\n\"}]",
                    "structured_content_rows": [],
                    "is_top": false,
                    "has_block_word": false,
                    "overt_status": 0,
                    "is_showing_missing": false,
                    "selected_comment_time": 0
                },
                "user": {
                    "uid": "296742597",
                    "nickname": "神也佑我海林",
                    "introduce": "",
                    "avatar": "100067",
                    "gender": 0,
                    "certification": {
                        "type": 0,
                        "label": ""
                    },
                    "level_exp": {
                        "level": 8,
                        "exp": 7595
                    },
                    "avatar_url": "https://img-static.mihoyo.com/communityweb/upload/044c17a8bd344093a3582f375eb7b004.png",
                    "pendant": "https://bbs-static.miyoushe.com/static/2023/04/14/6d6898ebadd83bf82437daef6ac6dbf2_3802189920345130211.png",
                    "ip_region": "广东"
                },
                "stat": {
                    "reply_num": 0,
                    "like_num": 276,
                    "sub_num": 16,
                    "dislike_num": 2
                },
                "self_operation": {
                    "attitude": 0,
                    "reply_vote_attitude": 0
                },
                "master_status": {
                    "is_official_master": false,
                    "is_user_master": false
                },
                "images": [
                    {
                        "url": "https://upload-bbs.miyoushe.com/upload/2023/07/12/296742597/74dc09c514c0dbca30db01d93cd607af_1723221593250820730.jpg",
                        "height": 117,
                        "width": 177,
                        "format": "jpg",
                        "size": "19078",
                        "image_id": "141984157",
                        "entity_type": "IMG_ENTITY_REPLY",
                        "entity_id": "1679067950588375040",
                        "is_deleted": false
                    }
                ],
                "sub_replies": [
                    {
                        "reply": {
                            "game_id": 2,
                            "post_id": "41200597",
                            "reply_id": "1679073695420944384",
                            "uid": "313554431",
                            "r_uid": "296742597",
                            "content": "同_(偶像姬-沮丧)",
                            "f_forum_id": 28,
                            "f_reply_id": "1679067950588375040",
                            "floor_id": 38,
                            "is_deleted": 0,
                            "delete_src": 0,
                            "created_at": 1689157339,
                            "updated_at": 1689157339,
                            "deleted_at": 2288912640,
                            "struct_content": "[{\"insert\":\"同_(偶像姬-沮丧)\"}]",
                            "structured_content_rows": [],
                            "is_top": false,
                            "has_block_word": false,
                            "overt_status": 0,
                            "is_showing_missing": false,
                            "selected_comment_time": 0
                        },
                        "user": {
                            "uid": "313554431",
                            "nickname": "illiyan",
                            "introduce": "",
                            "avatar": "100430",
                            "gender": 0,
                            "certification": {
                                "type": 0,
                                "label": ""
                            },
                            "level_exp": {
                                "level": 5,
                                "exp": 1261
                            },
                            "avatar_url": "https://img-static.mihoyo.com/communityweb/upload/c9d11674eac7631d2210a1ba20799958.png",
                            "pendant": "https://upload-bbs.mihoyo.com/upload/2022/09/28/876e62fb1fdfba3267c90fe364a5ae4e_1594369066719402876.png",
                            "ip_region": "河北"
                        },
                        "stat": {
                            "reply_num": 0,
                            "like_num": 9,
                            "sub_num": 0,
                            "dislike_num": 0
                        },
                        "self_operation": {
                            "attitude": 0,
                            "reply_vote_attitude": 0
                        },
                        "master_status": {
                            "is_official_master": false,
                            "is_user_master": false
                        },
                        "images": [],
                        "sub_replies": [],
                        "is_lz": false,
                        "sub_reply_count": 0,
                        "r_user": {
                            "uid": "296742597",
                            "nickname": "神也佑我海林",
                            "introduce": "",
                            "avatar": "100067",
                            "gender": 0,
                            "certification": {
                                "type": 0,
                                "label": ""
                            },
                            "level_exp": {
                                "level": 8,
                                "exp": 7595
                            },
                            "avatar_url": "https://img-static.mihoyo.com/communityweb/upload/044c17a8bd344093a3582f375eb7b004.png",
                            "pendant": "https://bbs-static.miyoushe.com/static/2023/04/14/6d6898ebadd83bf82437daef6ac6dbf2_3802189920345130211.png",
                            "ip_region": ""
                        },
                        "r_reply": null,
                        "r_post": null
                    },
                    {
                        "reply": {
                            "game_id": 2,
                            "post_id": "41200597",
                            "reply_id": "1679133739880165376",
                            "uid": "319980026",
                            "r_uid": "296742597",
                            "content": "hhh我到啦，超，胜冠之试从没打过（默默上号）",
                            "f_forum_id": 28,
                            "f_reply_id": "1679067950588375040",
                            "floor_id": 38,
                            "is_deleted": 0,
                            "delete_src": 0,
                            "created_at": 1689171655,
                            "updated_at": 1689171655,
                            "deleted_at": 2288912640,
                            "struct_content": "[{\"insert\":\"hhh我到啦，超，胜冠之试从没打过（默默上号）\"}]",
                            "structured_content_rows": [],
                            "is_top": false,
                            "has_block_word": false,
                            "overt_status": 0,
                            "is_showing_missing": false,
                            "selected_comment_time": 0
                        },
                        "user": {
                            "uid": "319980026",
                            "nickname": "夏小雪哦",
                            "introduce": "",
                            "avatar": "40025",
                            "gender": 0,
                            "certification": {
                                "type": 0,
                                "label": ""
                            },
                            "level_exp": {
                                "level": 6,
                                "exp": 2758
                            },
                            "avatar_url": "https://img-static.mihoyo.com/communityweb/avatar/avatar40025.png",
                            "pendant": "",
                            "ip_region": "山东"
                        },
                        "stat": {
                            "reply_num": 0,
                            "like_num": 15,
                            "sub_num": 0,
                            "dislike_num": 0
                        },
                        "self_operation": {
                            "attitude": 0,
                            "reply_vote_attitude": 0
                        },
                        "master_status": {
                            "is_official_master": false,
                            "is_user_master": false
                        },
                        "images": [],
                        "sub_replies": [],
                        "is_lz": false,
                        "sub_reply_count": 0,
                        "r_user": {
                            "uid": "296742597",
                            "nickname": "神也佑我海林",
                            "introduce": "",
                            "avatar": "100067",
                            "gender": 0,
                            "certification": {
                                "type": 0,
                                "label": ""
                            },
                            "level_exp": {
                                "level": 8,
                                "exp": 7595
                            },
                            "avatar_url": "https://img-static.mihoyo.com/communityweb/upload/044c17a8bd344093a3582f375eb7b004.png",
                            "pendant": "https://bbs-static.miyoushe.com/static/2023/04/14/6d6898ebadd83bf82437daef6ac6dbf2_3802189920345130211.png",
                            "ip_region": ""
                        },
                        "r_reply": null,
                        "r_post": null
                    },
                    {
                        "reply": {
                            "game_id": 2,
                            "post_id": "41200597",
                            "reply_id": "1679296093050736640",
                            "uid": "331730845",
                            "r_uid": "296742597",
                            "content": "我就差40多天",
                            "f_forum_id": 28,
                            "f_reply_id": "1679067950588375040",
                            "floor_id": 38,
                            "is_deleted": 0,
                            "delete_src": 0,
                            "created_at": 1689210363,
                            "updated_at": 1689210363,
                            "deleted_at": 2288912640,
                            "struct_content": "[{\"insert\":\"我就差40多天\"}]",
                            "structured_content_rows": [],
                            "is_top": false,
                            "has_block_word": false,
                            "overt_status": 0,
                            "is_showing_missing": false,
                            "selected_comment_time": 0
                        },
                        "user": {
                            "uid": "331730845",
                            "nickname": "203890721",
                            "introduce": "",
                            "avatar": "100858",
                            "gender": 0,
                            "certification": {
                                "type": 0,
                                "label": ""
                            },
                            "level_exp": {
                                "level": 4,
                                "exp": 538
                            },
                            "avatar_url": "https://upload-bbs.miyoushe.com/upload/2022/12/07/e84c8493bf9cd6b102eece6ec5ebd82e_2931682514717279175.png",
                            "pendant": "",
                            "ip_region": "吉林"
                        },
                        "stat": {
                            "reply_num": 0,
                            "like_num": 8,
                            "sub_num": 0,
                            "dislike_num": 0
                        },
                        "self_operation": {
                            "attitude": 0,
                            "reply_vote_attitude": 0
                        },
                        "master_status": {
                            "is_official_master": false,
                            "is_user_master": false
                        },
                        "images": [],
                        "sub_replies": [],
                        "is_lz": false,
                        "sub_reply_count": 0,
                        "r_user": {
                            "uid": "296742597",
                            "nickname": "神也佑我海林",
                            "introduce": "",
                            "avatar": "100067",
                            "gender": 0,
                            "certification": {
                                "type": 0,
                                "label": ""
                            },
                            "level_exp": {
                                "level": 8,
                                "exp": 7595
                            },
                            "avatar_url": "https://img-static.mihoyo.com/communityweb/upload/044c17a8bd344093a3582f375eb7b004.png",
                            "pendant": "https://bbs-static.miyoushe.com/static/2023/04/14/6d6898ebadd83bf82437daef6ac6dbf2_3802189920345130211.png",
                            "ip_region": ""
                        },
                        "r_reply": null,
                        "r_post": null
                    }
                ],
                "is_lz": false,
                "sub_reply_count": 16,
                "r_user": null,
                "r_reply": null,
                "r_post": null
            }
        ],
        "last_id": "1",
        "is_last": false,
        "post_owner_uid": "384454482",
        "pin_reply_id": "0"
    }
}
```

</details>
