###### 需要调用确认付款接口的返回码
|ret_code|ret_msg|备注说明 |
|:---|:---|:---|
|4002|疑似重复提交订单|调用付款申请接口返回 4002 时，请商户先人工审核该订单，确认无误后调用确认付款接口 |
|4003|收款银行卡和姓名不一致|调用付款申请接口返回 4003 时，请商户先人工审核该订单，确认无误后调用确认付款接口 |
|4004 |疑似重复提交订单且收款银行卡和姓名不一致 |调用付款申请接口返回 4004 时，请商户先人工审核该订单，确认无误后调用确认付款接口 |


## 确认付款 

###### 请求地址

```html
https://instantpay.lianlianpay.com/paymentapi/confirmPayment.htm 
```
###### 请求参数列表 

|字段说明|字段名|是否必须|类型|描述|
|:---|:---|:---|:---|:---|
|商户编号|oid_partner|是|String(18)|商户编号是商户在连连支付平台上开设的商户 号码，为 18 位数字，如： 201304121000001004 |
|平台来源|platform|否|String|平台来源能有效区分该交易是从此平台发起，并能有效定义用户来源。|
|版本号|api_version|是|String(3)|输入当前版本号1.0|
|签名|sign|是|String|RSA加密签名，见安全签名机制|
|签名方式|sign_type|是|String(3)|RSA|
|商户付款流水号|no_order|是|String(32)|商户系统唯一标识该付款的流水号|
|确认付款验证码|confirm_code|是|String(6)|确认付款验证码，来自付款申请接口返回|
|服务器异步通知地址|notify_url|是|String(64)|连连支付将付款结果通知商户服务端的地址，建议使用https协议。|

###### 请求参数采用post json 报文进行，样例如下： 
```html
{
 "api_version":"1.0",
 "confirm_code":"137007",
 "no_order":"20170208165924",
 "notify_url":"http://192.168.110.13:8080/test/tradepayapi/receiveNotify.htm",
 "oid_partner":"201606221000921503",
 "sign":"CLVVqaS39aW9EurgJbljVR3gmti5emt4GJdi0f0edJjvr8k52HBB60cEu7UmiMxtqgm/gVA40OG42ANY96ZiEoiJnAPdBANTK3pJyYq/anw56wrGLLW/HIFiTslnvIpwqtQoSjBaz8h+J2aSXzFPywG6WXFsLyAb/NUJSCSb6dU=",
 "sign_type":"RSA"}
```
###### 请求参数 json 报文加密传输（pay_load 是以上参数 json 加密结果）： 
```html
{
 "oid_partner":"201606221000921503",
 "pay_load":"lianpay1_0_1$WJlWl6plHu1NJppMZJl0UhBo8xzwBA/0SlbrHwNbnejDLfr8SMqzv+tXRwX+9eGMX6nzsyO8kDR2\r\nReZ/w22hJhQauaJiKrDcaoAdw1++SX1H25rg+sX1D0oh+eYXzLBXCnTXAG61xHBAIDbOJK3bmjrp\r\nM2/VjEkY8+/zHnHO3t0=$icV1y+ZLWywLksIWy725MTrfAPasC7BNpdqyHzGUTWWYY2/YaeP9qVDOJ7xR4wPbWa27WjRCMANa\r\nH+7R2UcM7pD4z3Ns3LWAx7SGVMTC53ojJkEHWlES3vZH9iitCNuczsSx81gf+FazQSO9d3RJr5Ez\r\nK+MJrbDCMLw8b2VpGGs=$RUIyMkM0NEs=$tfXbWbTWnzseVnnu/9Rl0Pz0EzAHUs7teGYC25c8ZZ05V7EkCXVOwmhGSQRzDmlwVNl/drQxseVa\r\nHhyi1XKbfK8b94Gaq/bbQvsoKZ5XEczqNNVljJD+gwjTFaDn23Ac5YoPyXnKucAWpm8kFWOGe2/O\r\nWPtypAl5RuDmVM6q3Hn60QppwJMB5ajpUo1+udG7UofRdz9BGp/zso5AMUkgtEWwL8ilHTH7lxZa\r\n87eRYXCo/1cVoavsj8aVKPjbH7xcl7+sklx9nQSVZWxIoor78JlNQpjoGPaugEbUo3lW69/OixoI\r\npddgMjdzdmbxJWNryW7Y6RJPmbyEemvfRb3dgq9deecgO12wkH/lgbueRWMqpGN4hkSoJS9bYPhP\r\nGL01zbYxrQxWgaJR/y7Ue0TtNSX2sF+UfuYY3guutvUlqM4PWAFzSrIt/B64pX2HNWsEwRA07WuO\r\nmFZPuzb6YG4cWOqUmzwK/hcb8+OcA1L5zJTEA/WRmKDs1fM9heP/c4tiHQ==$7btIQ57N4wnhOoCEDPwZdp+sfHRx/LSFdrmiJVFbd+4="
}
```

###### 返回参数列表 

|参数名称|参数编码|是否必须|字段长度|描述和样例|
|:---|:---|:---|:---|:---|
|交易结果代码|ret_code|是|String(4)|0000 （付款申请确认成功）.|
|交易结果描述|ret_msg|是|String(100)|交易成功|
|签名方式|sign_type|是|String(3)|RSA |
|签名|sign|是|String|RSA加密签名，见安全签名机制|
|商户编号|oid_partner|是|String(18)|商户编号是商户在连连支付平台上开设的商户号码为18位数字，如 ：201304121000001004 |
|商户付款流水号|no_order|是|String(32)|商户系统唯一标识该付款的流水号|
|连连支付支付单号|oid_paybill|否|String(18)|支付订单创建成功的时候返回|

```html
{ 
"no_order": "2016072814226",   
"oid_paybill":"2016080446983389",   
"oid_partner": "201606020000150062",   
"ret_code": "0000",   
"ret_msg": "交易成功", 
"sign":"ZPZULntRpJwFmGNIVKwjLEF2Tze7bqs60rxQ22CqT5J1UlvGo575QK9z/+p+7E9cOoRoWzqR6xHZ6WVv3dloyGKDR0btvrdqPgUAoeaX/YOWzTh00vwcQ+HBtXE+vPTfAqjCTxiiSJEOY7ATCF1q7iP3sfQxhS0nDUug1LP3OLk=",  
"sign_type": "RSA"
} 
```
```html
{
 "no_order":"20170208165924",
 "oid_partner":"201606221000921503",
 "ret_code":"4005",
 "ret_msg":"商户未开通权限",
 "sign":"evMZvWLfHNhOh98VRMho6DQYFHIXQU8k7RsJUgK6DRiMODuCPs505HXraDakb5Ye+ba2M4W16pkh5qq3Z/9Z9qOrICkx2KoTSo02S6hoyMvwJ6Pqlfqnsq3I3thHbJC8YcehHHOz+9aoeb8mYSB1RkCTKqXkRuh0OYHS1DyPDrI=",
 "sign_type":"RSA"}
```
