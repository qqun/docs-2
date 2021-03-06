# 订单

## 统一下单

注：
参数 appid, mch_id, nonce_str, sign, sign_type 可不用传入

```php
$result = $app->order->unify([
    'body' => '腾讯充值中心-QQ会员充值',
    'out_trade_no' => '20150806125346',
    'total_fee' => 88,
    'spbill_create_ip' => '123.12.12.123', // 可选，如不传该参数，SDK 将会自动获取相应 IP 地址
    'notify_url' => 'https://pay.weixin.qq.com/wxpay/pay.action', // 支付结果通知网址，如果不设置则会使用配置里的默认地址
    'trade_type' => 'JSAPI',
    'openid' => 'oUpF8uMuAJO_M2pxb1Q9zNjWeS6o',
]);

// $result:
//{
//  "xml": {
//    "return_code": "SUCCESS",
//    "return_msg": "OK",
//    "appid": "wx2421b1c4390ec4sb",
//    "mch_id": "10000100",
//    "nonce_str": "IITRi8Iabbblz1J",
//    "openid": "oUpF8uMuAJO_M2pxb1Q9zNjWeSs6o",
//    "sign": "7921E432F65EB8ED0CE9755F0E86D72F2",
//    "result_code": "SUCCESS",
//    "prepay_id": "wx201411102639507cbf6ffd8b0779950874",
//    "trade_type": "JSAPI"
//  }
//}
```

## 查询订单

该接口提供所有微信支付订单的查询，商户可以通过该接口主动查询订单状态，完成下一步的业务逻辑。

需要调用查询接口的情况：

  - 当商户后台、网络、服务器等出现异常，商户系统最终未接收到支付通知；
  - 调用支付接口后，返回系统错误或未知交易状态情况；
  - 调用被扫支付API，返回USERPAYING的状态；
  - 调用关单或撤销接口API之前，需确认支付状态；

### 根据商户订单号查询

```php
$app->order->queryByOutTradeNumber("商户系统内部的订单号（out_trade_no）");
```

### 根据微信订单号查询

```php
$app->order->queryByTransactionId("微信订单号（transaction_id）");
```

## 关闭订单

> 注意：订单生成后不能马上调用关单接口，最短调用时间间隔为5分钟。

```php
$app->order->close(商户系统内部的订单号（out_trade_no）);
```
