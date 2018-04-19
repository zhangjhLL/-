## 付款结果查询

###### 请求地址

```html
https://instantpay.lianlianpay.com/paymentapi/queryPayment.htm 
```
###### 请求参数列表 

|字段说明|字段名|是否必须|类型|描述|
|:---|:---|:---|:---|:---|
|商户编号|oid_partner|是|String(18)|商户编号是商户在连连支付平台上开设的商户 号码，为 18 位数字，如： 201304121000001004 |
|平台来源|platform|否|String(32)|平台来源能有效区分该交易是从此平台发起，并能有效定义用户来源。|
|版本号|api_version|是|String(3)|输入当前版本号1.0|
|签名|sign|是|String|RSA加密签名，见安全签名机制|
|签名方式|sign_type|是|String|RSA|
|商户付款流水号|no_order|是|String(32)|商户系统唯一标识该付款的流水号|
|连连支付支付单号|oid_paybill|否|String(16)||

###### 请求参数采用post json 报文进行，样例如下：

```html
{ 
 "oid_partner":"201103171000000000", 
 "api_version":"1.0", 
 "no_order":"2013051500005", 
 "oid_paybill":"2013051613121201", 
 "sign_type ":"RSA",        
 "sign":"ZPZULntRpJwFmGNIVKwjLEF2Tze7bqs60rxQ22CqT5J1UlvGo575QK9z/ +p+7E9cOoRoWzqR6xHZ6WVv3dloyGKDR0btvrdqPgUAoeaX/YOWzTh00vwcQ+HBtXE+vP TfAqjCTxiiSJEOY7ATCF1q7iP3sfQxhS0nDUug1LP3OLk=" 
 }
```
###### 返回参数列表 

|参数名称|参数编码|是否必须|字段长度|描述和样例|
|:---|:---|:---|:---|:---|
|交易结果代码|ret_code|是|String(4)|0000 （查询成功）.|
|交易结果描述|ret_msg|是|String(100)|交易成功|
|签名方式|sign_type|是|String|RSA |
|签名|sign|是|String|RSA加密签名，见安全签名机制|
|商户编号|oid_partner|是|String(18)|商户编号是商户在连连支付平台上开设的商户号码为18位数字，如 ：201304121000001004 |
|商户付款流水号|no_order|是|String(32)|商户系统唯一标识该付款的流水号|
|商户下单时间|dt_order|是|String(14)|格式：YYYYMMDDH24MISS  14位数字，精确到秒 |
|付款金额|money_order|是|Number(8,2)|付款金额，单位为元，精确到小数点后两位。如：49.65 |
|连连支付支付单号|oid_paybill|否|String(18)||
|付款结果|result_pay|是|String|<br/>APPLY 付款申请</br><br/>CHECK 复核申请</br> <br/>SUCCESS 付款成功</br><br/>PROCESSING 付款处理中 </br><br/>CANCEL 付款退款(付款成功后，有可能发生退款)</br> <br/>FAILURE  付款失败</br> <br/>CLOSED  付款关闭 结果以此为准</br>|
|账务日期|settle_date|否|String(8)|YYYYMMDD|
|订单描述|info_order|否|String(255)||

###### 返回样例如下：
```html
{   
  "dt_order": "20160728144057",
  "info_order": "测试",
  "money_order": "46.78",
  "no_order": "2016072814226",
  "oid_partner": "201606020000150062",
  "oid_paybill": "2016072846609676",
  "result_pay": "PROCESSING",
  "ret_code": "0000",
  "ret_msg": "交易成功",
  "sign":"ZPZULntRpJwFmGNIVKwjLEF2Tze7bqs60rxQ22CqT5J1UlvGo575QK9z/+p+7E9cOoRoWzqR6xHZ6WVv3dloyGKDR0btvrdqPgUAoeaX/YOWzTh00vwcQ+HBtXE+vPTfAqjCTxiiSJEOY7ATCF1q7iP3sfQxhS0nDUug1LP3OLk=",
  "sign_type": "RSA" 
} 
```
```html
{
   "oid_partner":"201606221000921503",
   "ret_code":"4005",
   "ret_msg":"商户未开通权限",
   "sign":"AtkijrjIozoGkA7u7m19mAoWyddXZnTs28t/NSrM80hBD2W6g+uJYTso8yMgA+XApj61YZ93q2NlQ8dyoiLMbwOrsqbx5cODCiFDv8t57c7CMZbzjiFXWqwXY3+Y11AHQtNK0EKAELn8pV58hJURg2JgbjtFPwQ+PT5MOCLzXbE=",
   "sign_type":"RSA"
}
```
