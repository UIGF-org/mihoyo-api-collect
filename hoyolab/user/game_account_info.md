# 游戏账号信息

- [原神](#原神)
  - [获取玩家首页信息](#获取玩家首页信息)
  - [获取玩家角色信息](#获取玩家角色信息)
  - [获取玩家深境螺旋信息](#获取玩家深境螺旋信息)

---

## 原神

### 获取玩家首页信息

**国服：**

_请求方式：GET_

> _需要验证请求头_
> `x-rpc-client_type`：`5`
> _需要验证网页Cookie_

`https://api-takumi-record.mihoyo.com/game_record/app/genshin/api/index`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| role_id | num | 原神UID | |
| server | str | 服务器名称 | |

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
| role | obj | 玩家基础信息 | |
| avatars | arr | 玩家拥有的角色的信息 | 若Cookie对应的账号不是自己的，则只返回好感度最高的8个角色。 |
| stats | obj | 玩家世界信息 | |
| city_explorations | arr | 待调查 | 似乎没有用 |
| world_explorations | arr | 玩家的世界探索信息 | |
| homes | arr | 玩家的尘歌壶信息 | |

`data`对象→`role`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| AvatarUrl | str | 玩家头像 | 总是为空字符串 |
| nickname | str | 玩家昵称 | |
| region | str | 玩家账号的服务器名称 | |
| level | num | 玩家的冒险等级 | |

`data`对象→`avatars`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| id | num | 该角色的ID | |
| image | str | 该角色的头像 | |
| element | str | 该角色的元素 | 英文 |
| fetter | num | 该角色的好感度 | |
| level | num | 该角色的等级 | |
| rarity | num | 该角色的稀有度 | |
| actived_constellation_num | num | 该角色的已激活命之座数量 | |
| card_image | str | 该角色的角色卡 | |
| is_chosen | bool | 是否收藏了该角色 | |

`data`对象→`stats`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| active_day_number | num | 该玩家的游玩天数 | |
| achievement_number | num | 该玩家已达成的成就数量 | |
| anemoculus_number | num | 该玩家已供奉的风神瞳数量 | |
| geoculus_number | num | 该玩家已供奉的岩神瞳数量 | |
| avatar_number | num | 该玩家拥有的角色数量 | |
| way_point_number | num | 该玩家已激活的传送锚点数量 | |
| domain_number | num | 该玩家已激活的秘境入口数量 | |
| spiral_abyss | num | 该玩家当前的深境螺旋层级 | |
| precious_chest_number | num | 该玩家已开启的珍贵的宝箱数量 | |
| luxurious_chest_number | num | 该玩家已开启的华丽的宝箱数量 | |
| exquisite_chest_number | num | 该玩家已开启的精致的宝箱数量 | |
| common_chest_number | num | 该玩家已开启的普通的宝箱数量 | |
| electroculus_number | num | 该玩家已供奉的雷神瞳数量 | |
| magic_chest_number | num | 该玩家已开启的奇馈宝箱数量 | |
| dendroculus_number | num | 该玩家已供奉的草神瞳数量 | |

`data`对象→`world_explorations`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| level | num | 地区声望等级 | |
| exploration_percentage | num | 地区探索度 | 百分比×10，例如10%探索度则该字段为100 |
| icon | str | 地区图标 | |
| name | str | 地区名称 | |
| type | str | Reputation 声望<br/> | |
| offerings | arr | 该地区除神像以外的等级信息，例如须弥的梦之树、稻妻的神樱树等 | |
| id | num | 该地区的ID | |
| parent_id | num | 父地区的ID | |
| map_url | str | 该地区在米游社观测枢原神大地图的链接 | |
| strategy_url | str | 该地区在米游社攻略的链接 | |
| background_image | str | 该地区的背景图 | |
| inner_icon | str | 该地区的图标 | |
| cover | str | 该地区的覆盖图 | |

`data`对象→`world_explorations`数组→对象→`offerings`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| name | str | 名称 | |
| level | num | 等级 | |
| icon | str | 图标 | |

`data`对象→`homes`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| level | num | 该玩家的尘歌壶等级 | |
| visit_num | num | 该玩家的尘歌壶总造访人数 | |
| comfort_num | num | 尘歌壶该岛的洞天仙力 | |
| item_num | num | 该玩家的摆设图纸数量 | |
| name | str | 尘歌壶该岛的名称 | |
| icon | str | 尘歌壶该岛的图标 | |
| comfort_level_name | str | 尘歌壶该岛的洞天仙力的称号 | |
| comfort_level_icon | str | 尘歌壶该岛的洞天仙力的图标 | |


<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "role": {
      "AvatarUrl": "",
      "nickname": "※青衫入雨※",
      "region": "cn_gf01",
      "level": 57
    },
    "avatars": [
      {
        "id": 10000002,
        "image": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Ayaka.png",
        "name": "神里绫华",
        "element": "Cryo",
        "fetter": 10,
        "level": 90,
        "rarity": 5,
        "actived_constellation_num": 0,
        "card_image": "https://upload-bbs.mihoyo.com/game_record/genshin/character_card_icon/UI_AvatarIcon_Ayaka_Card.png",
        "is_chosen": false
      },
      ...
    ],
    "stats": {
      "active_day_number": 340,
      "achievement_number": 631,
      "anemoculus_number": 66,
      "geoculus_number": 130,
      "avatar_number": 46,
      "way_point_number": 285,
      "domain_number": 46,
      "spiral_abyss": "12-3",
      "precious_chest_number": 290,
      "luxurious_chest_number": 113,
      "exquisite_chest_number": 965,
      "common_chest_number": 1455,
      "electroculus_number": 128,
      "magic_chest_number": 80,
      "dendroculus_number": 182
    },
    "city_explorations": [],
    "world_explorations": [
      {
        "level": 5,
        "exploration_percentage": 560,
        "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/city_icon/UI_ChapterIcon_Xumi.png",
        "name": "须弥",
        "type": "Reputation",
        "offerings": [
          {
            "name": "梦之树",
            "level": 29,
            "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/city_icon/UI_ChapterOffering_DreamTree.png"
          }
        ],
        "id": 8,
        "parent_id": 0,
        "map_url": "https://webstatic.mihoyo.com/ys/app/interactive-map/index.html?bbs_presentation_style=no_header&utm_source=mys&utm_medium=ys&utm_campaign=gamerecord&lang=zh-cn&_markerFps=24#/map/2?center=3116.00,-3823.00&zoom=-2.00&shown_types=",
        "strategy_url": "https://bbs.mihoyo.com/ys/strategy/channel/map/45/251?bbs_presentation_style=no_header",
        "background_image": "https://upload-bbs.mihoyo.com/game_record/genshin/city_icon/UI_ChapterBackground_Xumi.png",
        "inner_icon": "https://upload-bbs.mihoyo.com/game_record/genshin/city_icon/UI_ChapterInnerIcon_Xumi.png",
        "cover": "https://upload-bbs.mihoyo.com/game_record/genshin/city_icon/UI_ChapterCover_Xumi.png"
      },
      ...
    ],
    "homes": [
      {
        "level": 8,
        "visit_num": 3,
        "comfort_num": 6500,
        "item_num": 466,
        "name": "罗浮洞",
        "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/home/UI_HomeworldModule_2_Pic.png",
        "comfort_level_name": "初显锦绣",
        "comfort_level_icon": "https://upload-bbs.mihoyo.com/game_record/genshin/home/UI_Homeworld_Comfort_5.png"
      },
      ...
    ]
  }
}
```
</details>


**国际服：**

_请求方式：GET_

> _需要验证请求头_
> `x-rpc-client_type`：`5`
> _需要验证网页Cookie_

`https://bbs-api-os.hoyolab.com/game_record/genshin/api/index`

参数：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| role_id | num | 原神UID | |
| server | str | 服务器名称 | |


### 获取玩家角色信息

**国服：**

_请求方式：POST_

> _需要验证请求头_
> `x-rpc-client_type`：`5`
> _需要验证网页Cookie_


`https://api-takumi-record.mihoyo.com/game_record/app/genshin/api/character`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| server | str | 服务器名称 | |
| role_id | num | 原神UID | |

**JSON返回**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| message | str | 返回消息 | |
| data | obj | 该游戏账号的角色信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| avatars | arr | 该账号拥有的角色的信息 | 若Cookie对应的账号不是自己的，则只返回好感度最高的8个角色。 |
| role | obj | 该账号的基本信息 | |

`data`对象→`avatars`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| id | num | 角色ID | |
| image | str | 角色的图像 | |
| icon | str | 角色的图标 | |
| name | str | 角色姓名 | |
| element | str | 角色的元素 | 英文 |
| fetter | num | 角色好感度 | |
| level | num | 角色等级 | |
| rarity | num | 角色稀有度 | |
| weapon | obj | 角色持有武器的信息 | |
| reliquaries | arr | 角色佩戴的圣遗物的信息 | |
| constellations | arr | 角色的命之座信息 | |
| actived_constellation_num | num | 该角色已点亮的命之座数量 | |
| costumes | arr | 该账号拥有的该角色衣装信息 | |
| external | | 待调查 | |

`data`对象→`avatars`数组→对象→`weapon`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| id | num | 该武器ID | |
| name | str | 该武器的名称 | |
| icon | str | 该武器的图标 | |
| type | num | 该武器的类型 | |
| rarity | num | 该武器的稀有度 | |
| level | num | 该武器的等级 | |
| promote_level | num | 该武器的精炼等级 | |
| type_name | str | 该武器所属类型的名称 | |
| desc | str | 该武器的描述 | |
| affix_level | num | 待调查 | |

`data`对象→`avatars`数组→对象→`reliquaries`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| id | num | 该圣遗物的ID | |
| name | str | 该圣遗物的名称 | |
| icon | str | 该圣遗物的图标 | |
| pos | num | 该圣遗物的位置<br/>1 生之花<br/>2 死之羽<br/>3 空之杯<br/>4 时之沙<br/>5 理之冠 | |
| rarity | num | 该圣遗物的稀有度 | |
| level | num | 该圣遗物的等级 | |
| set | obj | 该圣遗物所属的圣遗物套装的信息 | |
| pos_name | str | 该圣遗物的位置的名称 | |

`data`对象→`avatars`数组→对象→`reliquaries`数组→对象→`set`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| id | num | 该圣遗物套装的ID | |
| name | str | 该圣遗物套装的名称 | |
| affixes | arr | 该圣遗物套装的套装效果信息 | |

`data`对象→`avatars`数组→对象→`reliquaries`数组→对象→`set`对象→`affixes`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| activation_number | num | 需要装备多少该套装内的圣遗物才能激活该效果 | |
| effect | str | 该圣遗物套装效果的描述 | |


`data`对象→`avatars`数组→对象→`constellations`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| id | num | 该命之座的ID | |
| name | str | 该命之座的名称 | |
| icon | str | 该命之座的图标 | |
| effect | str | 该命之座的描述 | |
| is_actived | bool | 该账号是否已激活该命之座 | |
| pos | num | 该命之座的位置 | |

`data`对象→`avatars`数组→对象→`costumes`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| id | num | 该衣装的ID | |
| name | str | 该衣装的名称 | |
| icon | str | 该衣装的图标 | |

`data`对象→`role`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| AvatarUrl | str | 该账号的头像 | 似乎没有用 |
| nickname | str | 该账号的昵称 | |
| region | str | 该账号在的服务器的名称 | |
| level | num | 该账号的冒险等级 | |


<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "avatars": [
      {
        "id": 10000002,
        "image": "https://upload-bbs.mihoyo.com/game_record/genshin/character_image/UI_AvatarIcon_Ayaka@2x.png",
        "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Ayaka.png",
        "name": "神里绫华",
        "element": "Cryo",
        "fetter": 10,
        "level": 90,
        "rarity": 5,
        "weapon": {
          "id": 11505,
          "name": "磐岩结绿",
          "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/equip/UI_EquipIcon_Sword_Morax.png",
          "type": 1,
          "rarity": 5,
          "level": 90,
          "promote_level": 6,
          "type_name": "单手剑",
          "desc": "由纯净的翠玉精琢细雕而成的仪礼宝剑，挥舞时剑风中似有叹息之声。",
          "affix_level": 1
        },
        "reliquaries": [
          {
            "id": 71544,
            "name": "历经风雪的思念",
            "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/equip/UI_RelicIcon_14001_4.png",
            "pos": 1,
            "rarity": 5,
            "level": 20,
            "set": {
              "id": 2140011,
              "name": "冰风迷途的勇士",
              "affixes": [
                {
                  "activation_number": 2,
                  "effect": "获得15%冰元素伤害加成。"
                },
                ...
              ]
            },
            "pos_name": "生之花"
          },
          ...
        ],
        "constellations": [
          {
            "id": 21,
            "name": "霜杀墨染樱",
            "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/constellation_icon/UI_Talent_S_Ayaka_01.png",
            "effect": "神里绫华的普通攻击或重击对敌人造成<color=#99FFFFFF>冰元素伤害</color>时，有50%的几率使<color=#FFD780FF>神里流·冰华</color>的冷却时间缩减0.3秒。该效果每0.1秒只能触发一次。",
            "is_actived": false,
            "pos": 1
          },
          ...
        ],
        "actived_constellation_num": 0,
        "costumes": [],
        "external": null
      },
      ...
    ],
    "role": {
      "AvatarUrl": "",
      "nickname": "玄天",
      "region": "cn_gf01",
      "level": 56
    }
  }
}
```
</details>

**国际服：**

_请求方式：POST_

> _需要验证请求头_
> `x-rpc-client_type`：`5`
> _需要验证网页Cookie_


`未知`


**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| server | str | 服务器名称 | |
| role_id | num | 原神UID | |

**JSON返回**

根对象：

<!-- | 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| message | str | 返回消息 | |
| data | obj | 该游戏账号的角色信息 | | -->


### 获取玩家深境螺旋信息


**国服：**


_请求方式：GET_

> _需要验证请求头_
> `x-rpc-client_type`：`5`
> _需要验证网页Cookie_

`https://api-takumi-record.mihoyo.com/game_record/app/genshin/api/spiralAbyss`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| server | str | 服务器名称 | |
| role_id | num | 原神UID | |
| schedule_type | num | 要查询的是哪期深渊信息<br/>1 当期<br/>2 上期 | |


根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码<br/>10102 目标用户未公开数据 | |
| message | str | 返回消息 | |
| data | obj | 该游戏账号的深境螺旋信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| schedule_id | num | 这期深境螺旋的ID | |
| start_time | str | 这期深境螺旋开始时的Unix时间戳 | |
| end_time | str | 这期深境螺旋结束时间的Unix时间戳 | |
| total_battle_times | num | 该玩家在这期深境螺旋总共战斗的间数量 | |
| total_win_times | num | 该玩家在这期深境螺旋总共胜利的间数量 | |
| max_floor | str | 该玩家在这期最深抵达的间 | |
| reveal_rank | arr | 该玩家在这期深境螺旋使用次数最多的角色的信息 | |
| defeat_rank | arr | 该玩家在这期深境螺旋击破数量最多的角色的信息 | |
| damage_rank | arr | 该玩家在这期深境螺旋中伤害最大的角色的信息 | |
| take_damage_rank | arr | 该玩家在这期深境螺旋中承受伤害最多的角色的信息 | |
| normal_skill_rank | arr | 该玩家在这期深境螺旋中释放最多元素战技的角色的信息 | |
| energy_skill_rank | arr | 该玩家在这期深境螺旋中释放最多元素爆发的角色的信息 | |
| floors | arr | 该玩家在这期深境螺旋第8层及以上层的信息 | |
| total_star | num | 该玩家在这期深境螺旋得到的星的数量 | |
| is_unlock | bool | 该玩家是否已解锁渊月螺旋 | |

`data`对象→`reveal_rank`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| avatar_id | num | 该角色的ID | |
| avatar_icon | str | 该角色的图标 | |
| value | num | 该玩家在这期深境螺旋的使用该角色的次数 | |
| rarity | num | 该角色的稀有度 | |

`data`对象→`defeat_rank`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| avatar_id | num | 该角色的ID | |
| avatar_icon | str | 该角色的图标 | |
| value | num | 该玩家在这期深境螺旋中该角色击破的次数 | |
| rarity | num | 该角色的稀有度 | |

`data`对象→`damage_rank`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| avatar_id | num | 该角色的ID | |
| avatar_icon | str | 该角色的图标 | |
| value | num | 该玩家在这期深境螺旋中该角色输出的最大伤害 | |
| rarity | num | 该角色的稀有度 | |

`data`对象→`take_damage_rank`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| avatar_id | num | 该角色的ID | |
| avatar_icon | str | 该角色的图标 | |
| value | num | 该玩家在这期深境螺旋中该角色承受的伤害 | |
| rarity | num | 该角色的稀有度 | |

`data`对象→`take_damage_rank`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| avatar_id | num | 该角色的ID | |
| avatar_icon | str | 该角色的图标 | |
| value | num | 该玩家在这期深境螺旋中该角色承受的伤害 | |
| rarity | num | 该角色的稀有度 | |

`data`对象→`normal_skill_rank`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| avatar_id | num | 该角色的ID | |
| avatar_icon | str | 该角色的图标 | |
| value | num | 该玩家在这期深境螺旋中该角色释放的元素战技数量 | |
| rarity | num | 该角色的稀有度 | |

`data`对象→`energy_skill_rank`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| avatar_id | num | 该角色的ID | |
| avatar_icon | str | 该角色的图标 | |
| value | num | 该玩家在这期深境螺旋中该角色释放的元素爆发数量 | |
| rarity | num | 该角色的稀有度 | |

`data`对象→`floors`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| index | num | 该层的位置 | |
| icon | | 该层的图标，似乎没有用 | |
| is_unlock | bool | 该玩家是否已通过这层 | |
| settle_time | num | 该玩家通过这层的时间 | 总是为`0` |
| star | num | 该玩家在这层获得的星的数量 | |
| max_star | num | 该层最多可获得的星的数量 | |
| levels | arr | 该层的间的信息 | |

`data`对象→`floors`数组→对象→`levels`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| index | num | 该间的位置 | |
| star | num | 该玩家在这间获得的星的数量 | |
| max_star | num | 这间最多可获得的星的数量 | |
| battles | arr | 该玩家在这间的上半、下半的战斗信息 | |

`data`对象→`floors`数组→对象→`levels`数组→对象→`battles`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| index | num | 1 上半<br/>2 下半 | |
| timestamp | str | 该玩家开始战斗时的Unix时间戳 | |
| avatars | arr | 该玩家在该间的上半或下半战斗使用的角色的信息 | |

`data`对象→`floors`数组→对象→`levels`数组→对象→`battles`数组→对象→`avatars`数组→对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| id | num | 该角色的ID | |
| icon | str | 该角色的图标 | |
| level | num | 该角色的等级 | |
| rarity | num | 该角色的稀有度 | |


<details>
<summary>查看示例</summary>

```json
{
  "retcode": 0,
  "message": "OK",
  "data": {
    "schedule_id": 63,
    "start_time": "1675195200",
    "end_time": "1676491199",
    "total_battle_times": 32,
    "total_win_times": 20,
    "max_floor": "12-3",
    "reveal_rank": [
      {
        "avatar_id": 10000052,
        "avatar_icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Shougun.png",
        "value": 16,
        "rarity": 5
      },
      {
        "avatar_id": 10000030,
        "avatar_icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
        "value": 14,
        "rarity": 5
      },
      {
        "avatar_id": 10000025,
        "avatar_icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
        "value": 14,
        "rarity": 4
      },
      {
        "avatar_id": 10000073,
        "avatar_icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
        "value": 13,
        "rarity": 5
      }
    ],
    "defeat_rank": [
      {
        "avatar_id": 10000052,
        "avatar_icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_side_icon/UI_AvatarIcon_Side_Shougun.png",
        "value": 63,
        "rarity": 5
      }
    ],
    "damage_rank": [
      {
        "avatar_id": 10000052,
        "avatar_icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_side_icon/UI_AvatarIcon_Side_Shougun.png",
        "value": 127921,
        "rarity": 5
      }
    ],
    "take_damage_rank": [
      {
        "avatar_id": 10000052,
        "avatar_icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_side_icon/UI_AvatarIcon_Side_Shougun.png",
        "value": 175343,
        "rarity": 5
      }
    ],
    "normal_skill_rank": [
      {
        "avatar_id": 10000032,
        "avatar_icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_side_icon/UI_AvatarIcon_Side_Bennett.png",
        "value": 112,
        "rarity": 4
      }
    ],
    "energy_skill_rank": [
      {
        "avatar_id": 10000047,
        "avatar_icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_side_icon/UI_AvatarIcon_Side_Kazuha.png",
        "value": 62,
        "rarity": 5
      }
    ],
    "floors": [
      {
        "index": 8,
        "icon": "",
        "is_unlock": true,
        "settle_time": "0",
        "star": 9,
        "max_star": 9,
        "levels": [
          {
            "index": 1,
            "star": 3,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675518215",
                "avatars": [
                  {
                    "id": 10000032,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Bennett.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000023,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xiangling.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000025,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
                    "level": 90,
                    "rarity": 4
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675518263",
                "avatars": [
                  {
                    "id": 10000078,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Alhatham.png",
                    "level": 80,
                    "rarity": 5
                  },
                  {
                    "id": 10000031,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Fischl.png",
                    "level": 80,
                    "rarity": 4
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000073,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              }
            ]
          },
          {
            "index": 2,
            "star": 3,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675518335",
                "avatars": [
                  {
                    "id": 10000032,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Bennett.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000023,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xiangling.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000025,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
                    "level": 90,
                    "rarity": 4
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675518383",
                "avatars": [
                  {
                    "id": 10000078,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Alhatham.png",
                    "level": 80,
                    "rarity": 5
                  },
                  {
                    "id": 10000031,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Fischl.png",
                    "level": 80,
                    "rarity": 4
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000073,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              }
            ]
          },
          {
            "index": 3,
            "star": 3,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675518455",
                "avatars": [
                  {
                    "id": 10000032,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Bennett.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000023,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xiangling.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000025,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
                    "level": 90,
                    "rarity": 4
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675518507",
                "avatars": [
                  {
                    "id": 10000078,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Alhatham.png",
                    "level": 80,
                    "rarity": 5
                  },
                  {
                    "id": 10000031,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Fischl.png",
                    "level": 80,
                    "rarity": 4
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000073,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              }
            ]
          }
        ]
      },
      {
        "index": 9,
        "icon": "",
        "is_unlock": true,
        "settle_time": "0",
        "star": 9,
        "max_star": 9,
        "levels": [
          {
            "index": 1,
            "star": 3,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675195660",
                "avatars": [
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000032,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Bennett.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000039,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Diona.png",
                    "level": 73,
                    "rarity": 4
                  },
                  {
                    "id": 10000052,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Shougun.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675195715",
                "avatars": [
                  {
                    "id": 10000022,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Venti.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000075,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Wanderer.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000002,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Ayaka.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              }
            ]
          },
          {
            "index": 2,
            "star": 3,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675195765",
                "avatars": [
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000032,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Bennett.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000039,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Diona.png",
                    "level": 73,
                    "rarity": 4
                  },
                  {
                    "id": 10000052,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Shougun.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675195832",
                "avatars": [
                  {
                    "id": 10000022,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Venti.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000075,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Wanderer.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000002,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Ayaka.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              }
            ]
          },
          {
            "index": 3,
            "star": 3,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675195880",
                "avatars": [
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000032,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Bennett.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000039,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Diona.png",
                    "level": 73,
                    "rarity": 4
                  },
                  {
                    "id": 10000052,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Shougun.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675195929",
                "avatars": [
                  {
                    "id": 10000022,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Venti.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000075,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Wanderer.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000002,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Ayaka.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              }
            ]
          }
        ]
      },
      {
        "index": 10,
        "icon": "",
        "is_unlock": true,
        "settle_time": "0",
        "star": 9,
        "max_star": 9,
        "levels": [
          {
            "index": 1,
            "star": 3,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675196184",
                "avatars": [
                  {
                    "id": 10000052,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Shougun.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000073,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000025,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000031,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Fischl.png",
                    "level": 80,
                    "rarity": 4
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675196243",
                "avatars": [
                  {
                    "id": 10000002,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Ayaka.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000022,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Venti.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              }
            ]
          },
          {
            "index": 2,
            "star": 3,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675196304",
                "avatars": [
                  {
                    "id": 10000052,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Shougun.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000073,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000025,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000031,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Fischl.png",
                    "level": 80,
                    "rarity": 4
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675196338",
                "avatars": [
                  {
                    "id": 10000002,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Ayaka.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000022,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Venti.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              }
            ]
          },
          {
            "index": 3,
            "star": 3,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675196375",
                "avatars": [
                  {
                    "id": 10000052,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Shougun.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000073,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000025,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000031,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Fischl.png",
                    "level": 80,
                    "rarity": 4
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675196405",
                "avatars": [
                  {
                    "id": 10000002,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Ayaka.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000022,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Venti.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              }
            ]
          }
        ]
      },
      {
        "index": 11,
        "icon": "",
        "is_unlock": true,
        "settle_time": "0",
        "star": 9,
        "max_star": 9,
        "levels": [
          {
            "index": 1,
            "star": 3,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675421955",
                "avatars": [
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000022,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Venti.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000059,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Heizo.png",
                    "level": 70,
                    "rarity": 4
                  },
                  {
                    "id": 10000076,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Faruzan.png",
                    "level": 80,
                    "rarity": 4
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675422299",
                "avatars": [
                  {
                    "id": 10000002,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Ayaka.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000073,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000025,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
                    "level": 90,
                    "rarity": 4
                  }
                ]
              }
            ]
          },
          {
            "index": 2,
            "star": 3,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675196645",
                "avatars": [
                  {
                    "id": 10000052,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Shougun.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000025,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000073,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000031,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Fischl.png",
                    "level": 80,
                    "rarity": 4
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675196706",
                "avatars": [
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000032,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Bennett.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000023,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xiangling.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000002,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Ayaka.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              }
            ]
          },
          {
            "index": 3,
            "star": 3,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675196815",
                "avatars": [
                  {
                    "id": 10000052,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Shougun.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000025,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000073,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000031,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Fischl.png",
                    "level": 80,
                    "rarity": 4
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675196863",
                "avatars": [
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000032,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Bennett.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000023,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xiangling.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000002,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Ayaka.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              }
            ]
          }
        ]
      },
      {
        "index": 12,
        "icon": "",
        "is_unlock": true,
        "settle_time": "0",
        "star": 6,
        "max_star": 9,
        "levels": [
          {
            "index": 1,
            "star": 2,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675560429",
                "avatars": [
                  {
                    "id": 10000078,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Alhatham.png",
                    "level": 80,
                    "rarity": 5
                  },
                  {
                    "id": 10000031,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Fischl.png",
                    "level": 80,
                    "rarity": 4
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000073,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675560593",
                "avatars": [
                  {
                    "id": 10000052,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Shougun.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000025,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000032,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Bennett.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000023,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xiangling.png",
                    "level": 90,
                    "rarity": 4
                  }
                ]
              }
            ]
          },
          {
            "index": 2,
            "star": 2,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675561066",
                "avatars": [
                  {
                    "id": 10000078,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Alhatham.png",
                    "level": 80,
                    "rarity": 5
                  },
                  {
                    "id": 10000031,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Fischl.png",
                    "level": 80,
                    "rarity": 4
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000073,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
                    "level": 90,
                    "rarity": 5
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675561261",
                "avatars": [
                  {
                    "id": 10000052,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Shougun.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000025,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000032,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Bennett.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000023,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xiangling.png",
                    "level": 90,
                    "rarity": 4
                  }
                ]
              }
            ]
          },
          {
            "index": 3,
            "star": 2,
            "max_star": 3,
            "battles": [
              {
                "index": 1,
                "timestamp": "1675197621",
                "avatars": [
                  {
                    "id": 10000073,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Nahida.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000052,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Shougun.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000025,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Xingqiu.png",
                    "level": 90,
                    "rarity": 4
                  },
                  {
                    "id": 10000032,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Bennett.png",
                    "level": 90,
                    "rarity": 4
                  }
                ]
              },
              {
                "index": 2,
                "timestamp": "1675197742",
                "avatars": [
                  {
                    "id": 10000002,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Ayaka.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000047,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Kazuha.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000030,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Zhongli.png",
                    "level": 90,
                    "rarity": 5
                  },
                  {
                    "id": 10000014,
                    "icon": "https://upload-bbs.mihoyo.com/game_record/genshin/character_icon/UI_AvatarIcon_Barbara.png",
                    "level": 52,
                    "rarity": 4
                  }
                ]
              }
            ]
          }
        ]
      }
    ],
    "total_star": 42,
    "is_unlock": true
  }
}
```
</details>