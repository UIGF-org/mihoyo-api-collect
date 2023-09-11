# 游戏充值

- [游戏充值](#游戏充值)
  - [操作步骤](#pay-step)
  - [请求商店内容](#请求商店内容)
  - [创建订单信息](#创建订单信息)
  - [获取订单支付状态](#获取订单支付状态)

---

## 游戏充值

*注：这是网页api，并非游戏内api，因此游戏部分内容（例如原神纪行类内容）无法通过该api进行购买*

<h3 id="pay-step">操作步骤</h3>

1. 请求商店内容
2. 创建订单信息
3. 获取订单支付状态

### 请求商店内容

_请求方式：POST_

`https://{游戏id}-sdk.mihoyo.com/{游戏区服id}/mdk/shopwindow/shopwindow/fetchGoods`
例如：`https://hk4e-sdk.mihoyo.com/hk4e_cn/mdk/shopwindow/shopwindow/fetchGoods`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| released_flag | bool | 未知         |                               |
| game | str | 游戏区服id | 必须与url中的游戏id一致 |
| region | str | 服务器id   | 必须与url中的游戏区服id一致 |
| uid | str | 游戏uid      | |
| account | str | 米游社uid | |

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| data | obj | 返回数据 | |
| message | str  | 返回信息 |  |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| goods_list | list | 商店物品列表 | |

`data`对象→列表→`goods_list`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| goods_id | str | 商品id |                                                              |
| goods_name | str | 商品名称 |  |
| goods_name_i18n_key | str | 未知 |                                                              |
| goods_desc | str | 商品介绍         | |
| goods_desc_i18n_key | str | 未知 | |
| goods_type | str | 商品类型 | MonthlyCard  月卡类商品<br />Normal  普通商品                |
| goods_unit | str | 商品个数 |  |
| goods_icon | str | 商品图标 |  |
| currency | str | 货币计算单位缩写 | CNY 人民币                                                   |
| price | str | 价格 | 按使用货币的最小单位计算（例如货币计算单位为人民币时，此处单位为分；原神中空月祝福的价格为30元人民币，则此处的值为3000） |
| symbol | str | 货币单位符号 |  |
| tier_id | str | 商品层级id |  |
| bonus_desc | obj | 附赠内容介绍 | 非首充状态时展示的内容 |
| once_bonus_desc | obj | 附赠内容介绍 | 首充状态时展示的内容，不存在首充、用户已使用首充或商品为月卡类物品时值为null |
| available | bool | 是否可用 |  |
| tips_desc | str | 未知 |  |
| tips_i18n_key | str | 未知 |  |
| battle_pass_limit | str | 未知 |  |

`data`对象→列表→`goods_list`对象→`bonus_desc`对象：

| 字段                | 类型 | 内容         | 备注 |
| ------------------- | ---- | ------------ | ---- |
| bonus_desc          | str  | 附赠内容名称 |      |
| bonus_desc_i18n_key | str  | 未知         |      |
| bonus_unit          | num  | 附赠内容个数 |      |
| bonus_goods_id      | str  | 附赠内容id   |      |
| bonus_icon          | str  | 附赠内容图标 |      |

<details>
<summary>查看示例</summary>

 ```json
 {
   "retcode": 0,
   "message": "OK",
   "data": {
     "goods_list": [
       {
         "goods_id": "ys_chn_primogem1ststall_tier1",
         "goods_name": "创世结晶",
         "goods_name_i18n_key": "",
         "goods_desc": "",
         "goods_desc_i18n_key": "",
         "goods_type": "Normal",
         "goods_unit": "60",
         "goods_icon": "https://sdk-webstatic.mihoyo.com/sdk-payment-upload/2022/09/07/0f362595da2e37a7a8fde1bb120656d2_594155779359709441.png",
         "currency": "CNY",
         "price": "600",
         "symbol": "￥",
         "tier_id": "Tier_1",
         "bonus_desc": {
           "bonus_desc": "",
           "bonus_desc_i18n_key": "",
           "bonus_unit": 0,
           "bonus_goods_id": "",
           "bonus_icon": ""
         },
         "once_bonus_desc": null,
         "available": true,
         "tips_desc": "",
         "tips_i18n_key": "",
         "battle_pass_limit": "0"
       },
       {
         "goods_id": "ys_chn_primogem2ndstall_tier5",
         "goods_name": "创世结晶",
         "goods_name_i18n_key": "",
         "goods_desc": "",
         "goods_desc_i18n_key": "",
         "goods_type": "Normal",
         "goods_unit": "300",
         "goods_icon": "https://sdk-webstatic.mihoyo.com/sdk-payment-upload/2022/09/07/830e247bb0cfffa5c74a04e79c0040f5_1814106121630644354.png",
         "currency": "CNY",
         "price": "3000",
         "symbol": "￥",
         "tier_id": "Tier_5",
         "bonus_desc": {
           "bonus_desc": "原石",
           "bonus_desc_i18n_key": "",
           "bonus_unit": 30,
           "bonus_goods_id": "",
           "bonus_icon": "https://sdk-webstatic.mihoyo.com/sdk-payment-upload/2022/09/07/bd9f0229dd9b07a6a4f355560634e26e_9134197201842315357.png"
         },
         "once_bonus_desc": null,
         "available": true,
         "tips_desc": "",
         "tips_i18n_key": "",
         "battle_pass_limit": "0"
       },
       {
         "goods_id": "ys_chn_primogem3rdstall_tier15",
         "goods_name": "创世结晶",
         "goods_name_i18n_key": "",
         "goods_desc": "",
         "goods_desc_i18n_key": "",
         "goods_type": "Normal",
         "goods_unit": "980",
         "goods_icon": "https://sdk-webstatic.mihoyo.com/sdk-payment-upload/2022/09/07/dfefc92ce56e3b5615ef28d6b1119b8b_5835214000384994274.png",
         "currency": "CNY",
         "price": "9800",
         "symbol": "￥",
         "tier_id": "Tier_15",
         "bonus_desc": {
           "bonus_desc": "原石",
           "bonus_desc_i18n_key": "",
           "bonus_unit": 110,
           "bonus_goods_id": "",
           "bonus_icon": "https://sdk-webstatic.mihoyo.com/sdk-payment-upload/2022/09/07/bd9f0229dd9b07a6a4f355560634e26e_6996232761265057834.png"
         },
         "once_bonus_desc": null,
         "available": true,
         "tips_desc": "",
         "tips_i18n_key": "",
         "battle_pass_limit": "0"
       },
       {
         "goods_id": "ys_chn_primogem4thstall_tier30",
         "goods_name": "创世结晶",
         "goods_name_i18n_key": "",
         "goods_desc": "",
         "goods_desc_i18n_key": "",
         "goods_type": "Normal",
         "goods_unit": "1980",
         "goods_icon": "https://sdk-webstatic.mihoyo.com/sdk-payment-upload/2022/09/07/e918ecfedcb13113eb627fd944199272_3460055016813877022.png",
         "currency": "CNY",
         "price": "19800",
         "symbol": "￥",
         "tier_id": "Tier_30",
         "bonus_desc": {
           "bonus_desc": "原石",
           "bonus_desc_i18n_key": "",
           "bonus_unit": 260,
           "bonus_goods_id": "",
           "bonus_icon": "https://sdk-webstatic.mihoyo.com/sdk-payment-upload/2022/09/07/bd9f0229dd9b07a6a4f355560634e26e_2358463156075320275.png"
         },
         "once_bonus_desc": null,
         "available": true,
         "tips_desc": "",
         "tips_i18n_key": "",
         "battle_pass_limit": "0"
       },
       {
         "goods_id": "ys_chn_primogem5thstall_tier50",
         "goods_name": "创世结晶",
         "goods_name_i18n_key": "",
         "goods_desc": "",
         "goods_desc_i18n_key": "",
         "goods_type": "Normal",
         "goods_unit": "3280",
         "goods_icon": "https://sdk-webstatic.mihoyo.com/sdk-payment-upload/2022/09/07/70e703a64e8786390ab8b7cdc35dbeeb_6358952826545947027.png",
         "currency": "CNY",
         "price": "32800",
         "symbol": "￥",
         "tier_id": "Tier_50",
         "bonus_desc": {
           "bonus_desc": "原石",
           "bonus_desc_i18n_key": "",
           "bonus_unit": 600,
           "bonus_goods_id": "",
           "bonus_icon": "https://sdk-webstatic.mihoyo.com/sdk-payment-upload/2022/09/07/bd9f0229dd9b07a6a4f355560634e26e_1730792081423418950.png"
         },
         "once_bonus_desc": null,
         "available": true,
         "tips_desc": "",
         "tips_i18n_key": "",
         "battle_pass_limit": "0"
       },
       {
         "goods_id": "ys_chn_primogem6thstall_tier60",
         "goods_name": "创世结晶",
         "goods_name_i18n_key": "",
         "goods_desc": "",
         "goods_desc_i18n_key": "",
         "goods_type": "Normal",
         "goods_unit": "6480",
         "goods_icon": "https://sdk-webstatic.mihoyo.com/sdk-payment-upload/2022/09/07/24fa6b6190ce5da6928e431a832d85c3_5932007685099741224.png",
         "currency": "CNY",
         "price": "64800",
         "symbol": "￥",
         "tier_id": "Tier_60",
         "bonus_desc": {
           "bonus_desc": "原石",
           "bonus_desc_i18n_key": "",
           "bonus_unit": 1600,
           "bonus_goods_id": "",
           "bonus_icon": "https://sdk-webstatic.mihoyo.com/sdk-payment-upload/2022/09/07/bd9f0229dd9b07a6a4f355560634e26e_8010514725467837459.png"
         },
         "once_bonus_desc": null,
         "available": true,
         "tips_desc": "",
         "tips_i18n_key": "",
         "battle_pass_limit": "0"
       },
       {
         "goods_id": "ys_chn_blessofmoon_tier5",
         "goods_name": "空月祝福",
         "goods_name_i18n_key": "",
         "goods_desc": "<p>【空月祝福介绍】<br />\n每次购买空月祝福，可立即获得300创世结晶与为期30天的空月祝福生效时间。</p>\n\n<p>空月祝福生效时间内，每日可登录领取90原石。（每日凌晨4点更新【GMT+8】）</p>\n\n<p>【注意事项】<br />\n1. 空月祝福剩余生效时间&le;180天时续购，总生效时间才会延长。</p>\n\n<p>2. 当空月祝福剩余生效时间&gt;180天时不可再进行购买。但如因特殊情况导致重复购买，总生效时间将无法累加，并将直接返还330创世结晶。</p>\n\n<p>3. 玩家在空月祝福生效期间如因未登录而未领取的原石，将不会返还。</p>\n",
         "goods_desc_i18n_key": "",
         "goods_type": "MonthlyCard",
         "goods_unit": "0",
         "goods_icon": "https://sdk-webstatic.mihoyo.com/sdk-payment-upload/2020/06/08/2da77803b9b2ffc2a2b763a59e9c125f_5219067706372136934.png",
         "currency": "CNY",
         "price": "3000",
         "symbol": "￥",
         "tier_id": "Tier_5",
         "bonus_desc": {
           "bonus_desc": "",
           "bonus_desc_i18n_key": "",
           "bonus_unit": 0,
           "bonus_goods_id": "",
           "bonus_icon": ""
         },
         "once_bonus_desc": null,
         "available": true,
         "tips_desc": "",
         "tips_i18n_key": "",
         "battle_pass_limit": "0"
       }
     ]
   }
 }
 ```

</details>


### 创建订单信息

_请求方式：POST_

> _需要验证请求头_
>
> _`x-rpc-client_type`:`4`_
>
> _`x-rpc-device_id`_
>
> _需要验证cookie_
>
> _`stoken_v1`_
>
> *`stuid`*
>
> *`ltoken_v1`*
>
> *`ltuid`*
>
> *`cookie_token`*
>
> *`account_id`*

`https://{游戏id}-sdk.mihoyo.com/{游戏区服id}/mdk/atropos/api/createOrder`
例如：`https://hk4e-sdk.mihoyo.com/hk4e_cn/mdk/atropos/api/createOrder`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| open_id | str | 未知 | |
| special_info | str | 未知     | 通过网页方式充值的值为topup_center |
| order | obj | 订单信息 |  |
| sign | str | 订单签名 | 生成方式见下 |

`order`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| account | str | 米游社uid | |
| region | str | 游戏区服id | |
| uid | str | 游戏id | |
| delivery_url | str | 未知 | |
| device | str | 设备id | |
| channel_id | int | 未知           | |
| client_ip | str | 未知 | |
| client_type | int | 订单请求平台id | |
| game | str | 游戏标识符id | |
| amount | str | 商品价格 | |
| goods_num | int | 商品个数 | |
| goods_id | str | 商品id | |
| goods_title | str | 商品名称 | |
| price_tier | str | 价格层级 | |
| currency | str | 货币单位 | |
| pay_plat | str | 支付平台 | alipay 支付宝 |
| pay_type | str | 支付方式 | alipay 支付宝 |
| pay_vendor | str | 支付供应商 | alipay 支付宝 |

注：

订单签名生成方式：

所需的key为`6bdc3982c25f3f3c38668a32d287d16b`

1. 根据字典的键进行排序

2. 根据排序后的键依次获取他们的值并拼接成字符串

3. 使用上述的key和HmacSHA256算法对得到的字符串进行加密，得到的字符串结果为16进制

示例代码如下（Python）：

   

```python
import json
import pprint
import time
from hashlib import sha256
import hmac

import requests

h = """Cookie: stoken=***; stuid=311526738; ltoken=***; ltuid=311526738; cookie_token=***; account_id=311526738
x-rpc-client_type: 4
x-rpc-device_id: ***"""

header = dict(list(map(lambda l: l.split(": "), h.split("\n"))))

def get_sign(data, key):
    key = key.encode('utf-8')
    message = data.encode('utf-8')
    sign = hmac.new(key, message, digestmod=sha256).hexdigest()
    print(sign)
    return sign

key = '6bdc3982c25f3f3c38668a32d287d16b'

post_data = {"open_id": "", "special_info": "topup_center",
       "order": {"account": "311526738",
                 "region": "cn_gf01",
                 "uid": "216973385",
                 "delivery_url": "",
                 "device": "***",
                 "channel_id": 1,
                 "client_ip": "",
                 "client_type": 4,
                 "game": "hk4e_cn",
                 "amount": "3000",
                 "goods_num": 1,
                 "goods_id": "ys_chn_blessofmoon_tier5",
                 "goods_title": "空月祝福",
                 "price_tier": "Tier_5",
                 "currency": "CNY",
                 "pay_plat": "alipay",
                 "pay_type": "alipay",
                 "pay_vendor": "alipay"},
       "sign": ""}

sort_key = sorted(post_data['order'].keys())
values_str = ''.join([str(post_data['order'][key]) for key in sort_key])
print(values_str)

post_data['sign'] = get_sign(values_str, key)
b = requests.post('https://hk4e-sdk.mihoyo.com/hk4e_cn/mdk/atropos/api/createOrder', json=post_data, headers=header)
pprint.pprint(b.json())
```

**JSON返回：**

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| data | obj | 返回数据 | |
| message | str | 返回信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| account | str | 米游社uid | |
| action | str | 未知 | |
| amount | str | 待支付金额 | |
| balance | str | 未知 | |
| cluster | str | 未知 | |
| create_time | str | 订单创建时间戳 | |
| currency | str | 货币单位简称 | |
| encode_order | str | 支付链接 | 生成的二维码所指向的链接 |
| ext_info | str | 未知 | |
| foreign_serial | str | 未知 | |
| goods_id | str | 商品id | |
| method | str | 未知 | |
| order_no | str | 支付平台订单编号 | |
| redirect_url | str | 支付网关url | |
| session_cookie | str | 未知 | |

**备注：**

<details>
<summary>查看示例</summary>
```json
{
    'data': 
    	{
            'account': '311526738',
          	'action': '',
          	'amount': '3000',
          	'balance': '0',
          	'cluster': '',
          	'create_time': '1694413535',
          	'currency': 'CNY',
          	'encode_order': 'https://qr.alipay.com/bax05682icnzhnjqivkf00c3',
          	'ext_info': '',
          	'foreign_serial': '',
          	'goods_id': 'ys_chn_blessofmoon_tier5',
          	'method': '',
          	'order_no': '1701119779159945792',
          	'redirect_url': 'https://openapi.alipay.com/gateway.do',
          	'session_cookie': ''
        },
 	'message': 'OK',
 	'retcode': 0
}
```

</details>

### 获取订单支付状态

_请求方式：GET_

> _需要验证请求头_
>
> _`x-rpc-client_type`:`4`_
>
> _`x-rpc-device_id`_
>
> _需要验证cookie_
>
> _`stoken_v1`_
>
> *`stuid`*
>
> *`ltoken_v1`*
>
> *`ltuid`*
>
> *`cookie_token`*
>
> *`account_id`*

`https://{游戏标识符id}-sdk.mihoyo.com/{游戏区服id}/mdk/atropos/api/checkOrder`
例如：`https://hk4e-sdk.mihoyo.com/hk4e_cn/mdk/atropos/api/checkOrder`

**参数：**

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| order_no | str | 支付平台订单编号 | |
| game | str | 游戏区服id | |
| region | str | 服务器id         |  |
| uid | str  | 游戏uid | |

根对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| retcode | num | 返回码 | |
| data | obj | 返回数据 | |
| message | str | 返回信息 | |

`data`对象：

| 字段 | 类型 | 内容 | 备注 |
| ---- | ---- | ---- | ---- |
| amount | str  | 价格 | |
| goods_num | str | 商品数量 | |
| goods_title | str | 商品名称 | |
| order_no | str | 支付平台订单编号 | |
| pay_plat | str | 支付平台 | |
| status | str | 支付状态 | 1 未支付<br />900 已支付 |

<details>
<summary>查看示例</summary>

- 请求：`https://hk4e-sdk.mihoyo.com/hk4e_cn/mdk/atropos/api/checkOrder?order_no=1701125802130158976&game=hk4e_cn&region=cn_gf01&uid=216973385`
- 返回：
  ```json
  //未支付
  {
      "retcode": 0,
      "message": "OK",
      "data": {
          "status": 1,
          "amount": "600",
          "goods_title": "创世结晶×60",
          "goods_num": "1",
          "order_no": "1701125802130158976",
          "pay_plat": "alipay"
      }
  }
  //已支付
  {
      "retcode": 0,
      "message": "OK",
      "data": {
          "status": 900,
          "amount": "600",
          "goods_title": "创世结晶×60",
          "goods_num": "1",
          "order_no": "1701125802130158976",
          "pay_plat": "alipay"
      }
  }
  ```

</details>
