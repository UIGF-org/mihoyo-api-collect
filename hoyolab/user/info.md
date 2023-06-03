# 用户基本信息

- [用户信息](#用户信息)
  - [获取用户完整信息](#获取用户完整信息)
  - [获取用户发布的文章](#获取用户发布的文章)
  - [通过Cookie获取用户`authkey`A](#通过cookie获取账号authkeya)
  - [通过Cookie获取用户`authkey`B](#通过cookie获取账号authkeyb)

---

## 获取用户完整信息

**国服：**

_请求方式：GET_

`https://bbs-api.miyoushe.com/user/api/getUserFullInfo`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| uid | num | 米游社账号ID | |
| gids | num | 论坛分区ID | 可选，决定`data`对象→`user_info`对象→`level_exp`对象的内容 |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码<br>-20001 用户不存在 | |
| message | str | 返回消息 | |
| data | obj | 用户信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| user_info | obj | 该用户的详细信息 | |
| follow_relation | obj | 请求Cookie对应用户与该用户的关系 | |
| auth_relations | obj | 待调查 | 似乎总为空对象 |
| is_in_blacklist | bool | 是否被封禁 | |
| is_has_collection | bool | 是否拥有文章合集 | |
| is_creator | bool | false | |
| customer_service | obj | 客服工作人员信息 | |
| audit_info | obj | 昵称与简介的审核状态信息 | |

`data`对象→`user_info`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| uid | str | 该米游社用户的ID | |
| nickname | str | 昵称 | |
| introduce | str | 该用户的简介内容 | |
| avatar | str | 该用户的头像的ID | |
| gender | num | 该用户设置的性别<br>0 保密<br>1 男<br>2 女 | |
| certification | obj | 该用户获得的认证的信息 | |
| level_exps | arr | 该用户在每个论坛分区的等级信息 | |
| achieve | obj | 该用户的粉丝、关注、话题等信息 | |
| community_info | obj | 该用户在社区中的信息 | |
| avatar_url | str | 该用户头像的图片URL | |
| certifications | arr | 该用户得到的认证信息 | |
| level_exp | null | 该用户在参数`gids`对应论坛分区的等级信息 | 若没有传递`gids`参数，则为空对象 |
| pendant | str | 该用户的头像框图片URL | |
| is_logoff | bool | 是否已注销 | |
| ip_region | str | 该用户的IP属地 | |

`data`对象→`user_info`对象→`certification`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| type | num | 认证类型<br>0 没有认证<br>1 官方认证<br>2 个人认证 | |
| label | str | 认证标签 | |

`data`对象→`user_info`对象→`level_exp`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| level | num | 在该分区的等级 | |
| exp | num | 在该分区的经验 | |
| game_id | num | 该论坛分区的ID | |

`data`对象→`user_info`对象→`level_exps`数组→对象：

与`data`对象→`user_info`对象→`level_exp`对象的结构相同

`data`对象→`user_info`对象→`achieve`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| like_num | str | 该用户获得的点赞数 | |
| post_num | str | 该用户发布的文章数 | |
| replypost_num | str | 该用户的转发文章数 | |
| follow_cnt | str | 关注的用户数 | |
| followed_cnt | str | 该用户的粉丝数 | |
| topic_cnt | str | 该用户的建立的话题数 | |
| new_follower_num | str | 待调查 | |
| good_post_num | str | 该用户的精选文章数 | |
| follow_collection_cnt | str | 该用户关注的文章合集数 | |

`data`对象→`user_info`对象→`community_info`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| is_realname | bool | true | |
| agree_status | bool | true | |
| silent_end_time | num | 禁言结束时间的Unix时间戳 | |
| forbid_end_time | num | 封禁结束时间的Unix时间戳 | |
| info_upd_time | num | 个人信息更新时间的时间戳，有时为年份 | |
| privacy_invisible | obj | 该用户的隐私可见性设置 | |
| notify_disable | obj | 该用户的通知屏蔽设置 | |
| has_initialized | bool | true | |
| user_func_status | obj | 该用户开启的功能 | |
| forum_silent_info | arr | 待调查 | |
| last_login_ip | str | 上次登录的IP | 总是为空字符串 |
| last_login_time | num | 上次登录时间的Unix时间戳 | 总是为0 |
| created_at | num | 用户注册时间的Unix时间戳 | |

`data`对象→`user_info`对象→`community_info`对象→`privacy_invisible`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| post | bool | 是否隐藏发布的文章 | |
| collect | bool | 是否隐藏收藏的文章 | |
| watermark | bool | 在评论和文章中的图片是否添加水印 | |
| reply | bool | 是否隐藏回复 | |
| post_and_instant | bool | 是否隐藏发布的文章 | |

`data`对象→`user_info`对象→`community_info`对象→`notify_disable`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| reply | bool | 是否屏蔽回复提醒 | |
| upvote | bool | 是否屏蔽点赞提醒 | |
| follow | bool | 是否屏蔽关注提醒 | |
| system | bool | 是否屏蔽系统信息 | |
| chat | bool | 是否屏蔽评论提醒 | |

`data`对象→`user_info`对象→`community_info`对象→`user_func_status`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| enable_history_view | bool | 是否开启历史记录 | |
| enable_recommend | bool | 是否开启推荐 | |
| enable_mention | bool | 是否开启@ | |
| user_center_view | num | 是否开启用户中心 | |

`data`对象→`user_info`对象→`certifications`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| id | str | 该认证的ID | |
| certification_id | str | 0 | |
| type | num | 认证类型<br>1 官方认证<br>2 个人认证 | |
| label | str | 认证标签 | |

`data`对象→`follow_relation`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| is_following | bool | 是否已关注该用户 | 若未设置Cookie，则始终为false |
| is_followed | bool | 是否被该用户关注 | 若未设置Cookie，则始终为false |

`data`对象→`customer_service`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| is_customer_service_staff | bool | 是否是客服工作人员 | |
| game_id | num | 未知 | |

`data`对象→`audit_info`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| is_nickname_in_audit | bool | 昵称是否正在审核 | |
| nickname | str | 正在审核的昵称 | 若没有正在审核的昵称，则为空字符串 |
| is_introduce_in_audit | bool | 简介是否正在审核 | |
| introduce | str | 正在审核的简介 | 若没有正在审核的简介，则为空字符串 |
| nickname_status | num | 昵称状态<br>0 未知<br>1 正常<br>2 昵称审核中 | |


<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "user_info": {
      "uid": "75379477",
      "nickname": "提瓦特徒步团",
      "introduce": "人类的本质是搬运工",
      "avatar": "10013",
      "gender": 0,
      "certification": {
        "type": 1,
        "label": "官方认证：梦想是环游世界"
      },
      "level_exps": [
        {
          "level": 16,
          "exp": 101229,
          "game_id": 2
        },
        {
          "level": 1,
          "exp": 0,
          "game_id": 8
        },
        {
          "level": 1,
          "exp": 0,
          "game_id": 5
        },
        {
          "level": 2,
          "exp": 60,
          "game_id": 1
        },
        {
          "level": 1,
          "exp": 0,
          "game_id": 4
        },
        {
          "level": 1,
          "exp": 0,
          "game_id": 3
        },
        {
          "level": 1,
          "exp": 0,
          "game_id": 6
        }
      ],
      "achieve": {
        "like_num": "38092256",
        "post_num": "266",
        "replypost_num": "1438",
        "follow_cnt": "2",
        "followed_cnt": "1000036",
        "topic_cnt": "0",
        "new_follower_num": "625674",
        "good_post_num": "0",
        "follow_collection_cnt": "0"
      },
      "community_info": {
        "is_realname": true,
        "agree_status": true,
        "silent_end_time": 0,
        "forbid_end_time": 0,
        "info_upd_time": 2022,
        "privacy_invisible": {
          "post": false,
          "collect": false,
          "watermark": true,
          "reply": false,
          "post_and_instant": false
        },
        "notify_disable": {
          "reply": false,
          "upvote": false,
          "follow": false,
          "system": false,
          "chat": false
        },
        "has_initialized": true,
        "user_func_status": {
          "enable_history_view": true,
          "enable_recommend": true,
          "enable_mention": true,
          "user_center_view": 1
        },
        "forum_silent_info": [],
        "last_login_ip": "",
        "last_login_time": 0,
        "created_at": 0
      },
      "avatar_url": "https://img-static.mihoyo.com/communityweb/avatar/avatar10013.png",
      "certifications": [
        {
          "id": "120",
          "certification_id": "0",
          "type": 1,
          "label": "梦想是环游世界"
        }
      ],
      "level_exp": null,
      "pendant": "",
      "is_logoff": false,
      "ip_region": "上海"
    },
    "follow_relation": {
      "is_following": true,
      "is_followed": false
    },
    "auth_relations": [],
    "is_in_blacklist": false,
    "is_has_collection": false,
    "is_creator": false,
    "customer_service": {
      "is_customer_service_staff": false,
      "game_id": 0
    },
    "audit_info": {
      "is_nickname_in_audit": false,
      "nickname": "",
      "is_introduce_in_audit": false,
      "introduce": "",
      "nickname_status": 0
    }
  }
}
```

</details>

## 获取用户发布的文章

**国服：**

_请求方式：GET_

网页：`https://bbs-api.miyoushe.com/post/wapi/userPost`
应用：`https://bbs-api.miyoushe.com/painter/api/user_instant/list`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| size | num | 获取的文章数量 | |
| uid | num | 米游社用户ID | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |

## 通过Cookie获取账号`authkey`A

<!-- `authkey`A。 -->

**国服：**

_请求方式：POST_

> _需要验证Cookie_
>
> SToken

`https://api-takumi.miyoushe.com/account/auth/api/genAuthKey`

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| game_biz | str | 米游社区域<br>bbs_cn 国服 | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码<br>1002 请求体的`game_biz`字段不正确 | |
| message | str | 返回消息 | |
| data | obj | `authkey`信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| sign_type | num | 2 | |
| authkey_ver | num | 1 | |
| authkey | str | `authkey`A | |

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "sign_type": 2,
    "authkey_ver": 1,
    "authkey": "..."
  }
}
```

</details>

**国际服：**

`未知`

## 通过Cookie获取账号`authkey`B

在请求例如获取用户的游戏抽卡记录等API时需要使用到`authkey`B。

**国服：**

_请求方式：POST_

> _需要验证请求头_
>
> `x-rpc-client_type`：`2`
> LK`salt`
> `DS1`
>
> _需要验证Cookie_
>
> SToken

`https://api-takumi.miyoushe.com/binding/api/genAuthKey`
<!--`https://hk4e-sdk.mihoyo.com/hk4e_cn/combo/granter/login/genAuthKey`-->

**JSON请求：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| game_biz | str | 获取的`authkey`B的游戏<br>hk4e_cn 《原神》<br>hkrpg_cn 《崩坏：星穹铁道》<br> | |
| game_uid | num | 游戏

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码<br>1002 请求体的`game_biz`字段不正确 | |
| message | str | 返回消息 | |
| data | obj | `authkey`信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| sign_type | num | 2 | |
| authkey_ver | num | 1 | |
| authkey | str | `authkey`B | |

<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "sign_type": 2,
    "authkey_ver": 1,
    "authkey": "..."
  }
}
```

</details>

**国际服：**

`未知`