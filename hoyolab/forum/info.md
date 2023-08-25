# 论坛基本信息

- [论坛](#论坛)
  - [获取论坛分区信息](#获取论坛分区信息)

---

## 论坛

### 获取论坛分区信息

_请求方式：GET_

`https://bbs-api-static.miyoushe.com/apihub/wapi/getAllGamesForums`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| gids | num | 游戏ID | 可选 |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| message | str | 返回消息 | |
| data | obj | 论坛分区数据 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| list | arr | 论坛分区数据 | |

`data`对象→`list`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| game_id | num | 游戏ID | |
| forums | arr | 论坛分区数据 | |

`data`对象→`list`数组→对象→`forums`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| id | num | 论坛分区ID | |
| game_id | num | 所属游戏ID | |
| name | str | 分区名称 | |
| order | num | 排序顺序 | 升序 |
| f_id | num | 待调查 | |
| visible | num | 可见性<br>1 可见 | |
| create_type | num | 待调查 | |
| view_type | num | 待调查 | |
| post_limit | num | 待调查 | |
| max_top | num | 待调查 | |
| post_order | str | 默认排序类型<br/>reply 最新回复 | |
| src_type | num | 待调查 | |
| icon | str | 分区图标 | |
| header_image | str | 分区头图URL | APP端头部部分 |
| hot_score | num | 待调查 | |
| icon_pure | str | 分区图标 | |
| des | str | 描述 | |
| post_num | num | 待调查 | |
| today_post | num | 待调查 | |
| reply_type | num | 待调查 | |
| edit_post | num | 待调查 | |
| created_at | str | 该论坛分区的创建时间 | |
| updated_at | str | 待调查 | |
| show_type | num | 待调查 | |
| default_tab | num | 待调查 | |
| read_me | str | 该论坛分区简介 | |
| forum_cate_list | arr | 待调查 | |
| video_cate_list | arr | 视频分区数据 | |

`data`对象→`list`数组→对象→`forums`数组→对象→`video_cate_list`→对象：

| 字段 | 类型 | 内容 | 备注 |
| --- | ---- | ---- | ---- |
| id | num | 子分区ID | |
| name | str | 子分区名称 | |
| forum_id | num | 父分区ID | |
| desc | str | 子分区描述 | |
| remark | str | 子分区备注 | |

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "list": [
      {
        "game_id": 4,
        "forums": [
          {
            "id": 37,
            "game_id": 4,
            "name": "律所",
            "order": 1,
            "f_id": 0,
            "visible": 1,
            "create_type": 0,
            "view_type": 1,
            "post_limit": 3,
            "max_top": 3,
            "post_order": "reply",
            "src_type": 0,
            "icon": "https://upload-bbs.mihoyo.com/upload/2020/04/05/220478baa5f0fbbfd6452219ff6a9e5c.png",
            "header_image": "https://upload-bbs.mihoyo.com/upload/2019/08/27/df0439e4970738b8f9faebba31bac089.png",
            "hot_score": 1278957,
            "icon_pure": "https://upload-bbs.mihoyo.com/upload/2020/04/05/220478baa5f0fbbfd6452219ff6a9e5c.png",
            "des": "又到了第一喜欢的摸鱼鱼时间！",
            "post_num": 0,
            "today_post": 0,
            "reply_type": 1,
            "edit_post": 1,
            "created_at": "2019-08-27 19:04:19",
            "updated_at": "2023-01-12 17:00:25",
            "show_type": 1,
            "default_tab": 1,
            "read_me": "欢迎来到未定事件簿·律所！\n请律师在发帖前阅读【社区版规】，了解正确的发帖方式，更好地和其他律师进行交流哦~\n律师可在律所置顶中找到晒卡集中帖以及召回码分享集中帖。\n为了各位律师在浏览版区时能够保持愉快的心情，请遵守版规，不要在晒卡集中帖外发布晒卡内容！\n律所中抽卡分享的帖子将被版务团队直接删除，多次违反版规的律师将按照版规进行处理，感谢各位律师的理解。",
            "forum_cate_list": [],
            "video_cate_list": [
              {
                "id": 9,
                "name": "考据杂谈",
                "forum_id": 37,
                "desc": "以科普、考据、杂谈等为展示题材的视频内容",
                "remark": "单视频"
              },
              ...
            ]
          },
          ...
        ]
      },
      ...
    ]
  }
}
```
</details>