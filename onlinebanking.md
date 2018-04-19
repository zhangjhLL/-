# 付款 API 功能接口 

## 付款申请

###### 请求地址

```html
https://instantpay.lianlianpay.com/paymentapi/payment.htm
```

###### 请求参数列表 

|字段说明|字段名|是否必须|类型|描述|
|:---|:---|:---|:---|:---|
|商户编号|oid_partner|是|String(18)|商户编号是商户在连连支付平台上开设的商户 号码，为 18 位数字，如： 201304121000001004 |
|平台来源|platform|否|String(32)|平台来源能有效区分该交易是从此平台 发起，并能有效定义用户来源。|
|版本号|api_version|是|String(3)|输入当前版本号1.0|
|签名|sign|是|String|RSA加密签名，见安全签名机制|
|签名方式|sign_type|是| String(3)|RSA|
|商户付款流水号|no_order|是|String(32)|商户系统唯一标识该付款的流水号|
|商户付款时间|dt_order|是|String(14)|格式：YYYYMMDDH24MISS  14 位数字， 精确到秒|
|付款金额|money_order|是|Number(10 ,2)|付款金额，单位为元，精确到小数点后两位。 如：49.65元 |
|收款银行账号|card_no|是|String(32)||
|收款人姓名|acct_name|是|String|收款人姓名|
|收款银行名称|bank_name|否|String||
|订单描述|info_order|是|String(255)|付款用途 |
|对公对私标志|flag_card|是|String(1)|0-对私 1-对公 |
|服务器异步通知地址|notify_url|是|String(255)|连连支付平台在付款后通知商户服务端的地址|
|收款备注|memo|是|String(24)|传递至银行，特殊字符会过滤掉不传递至银行，单个字符过滤规则正则表达式：[^a-zA-Z0-9\\u4e00-\\u9fa5-_] |
|大额行号|prcptcd|否|String(12)|对公字段，若传，则省市支行可不传，且大额 行号以此为准。14家银行可不传,详情请看银行列表银|
|银行编码|bank_code|否|String|对公字段，见银行编码对公```bank_code```必传 |
|开户行所在市编码|city_code|否|String|对公字段，标准地市编码 14家银行可不传 详情请看银行列表|
|开户支行名称|brabank_name|否|String|对公字段 14家银行可不传 详情请看银行列表 |


###### 请求参数采用 post json 报文进行，样例如下： 

```html
curl https://instantpay.lianlianpay.com/paymentapi/payment.htm \
-H "Content-type:application/json;charset=utf-8" \
-d '：{
       "acct_name":"全渠道",
       "api_version":"1.0",
       "card_no":"621626*********0018",
       "dt_order":"20170317165929",
       "flag_card":"0",
       "info_order":"test测试10.00?",
       "memo":"代付",
       "money_order":"0.02",
       "no_order":"2017041316593411",
       "notify_url":"http://10.20.41.35:8080/tradepayapi/receiveNotify.htm",
       "oid_partner":"201606221000921503",
       "sign":"j6ZQkNVs/cq9d/+E0WnhhmySDWSfhQQ04i6Pt2ReVx4m6yTgxdsLBcY266pOmIJ3+/F4JPdVxEw782OT06KBFN/v9w17GALNV25FJqRRjx0q/+kePwlK3LMwxSXxuaNGG/uZzc/gZje5R2UXjZZf51gRL3kGWWcBUCN7uLMbdYQ=",
       "sign_type":"RSA"
}'
```
###### 请求参数 json 报文加密传输（pay_load 是以上参数 json 加密结果，加密用连连公钥）： 
```html
{
 "oid_partner":"201606221000921503",
 "pay_load":"lianpay1_0_1$il92rP0cRvcOt4AgKK/RVONOifeJcO2aQH567OKUuG4g2zk3Lje5pmogRD2Ab4MHMRLYwgB/4LpP\r\nEXgEJSfBoDy9ioINEDeDZ1oySMhVN2QIgJ77IGe8cL0LwbY5mZAI2Vccs80IY0Ls6SYmL6ULrr1m\r\nZm64L4tPe6A2RbExJVU=$TB1KKpxEIq+G36/UotINHpPB2mJwoD+rbZ5OSmA2E6WBXoqykoz3CqGESDLirQORMEqXSqYmyIdj\r\nxJeXtnLxWJ2484kt48xwcDuSwZ9tuIDdOzTmPioFL72UPpPr7EgODVq6zQ+fLtRKw95kBgLSxTge\r\nBt3sJb/Gtf738E1yuG8=$T0FIVFRCN0w=$uMFHDkWzqhGS/LDec4M4GGd/WqJ2WInKhQbtDDYwHLzfOq9cpibpHAFiyg6lMdKgk/T09RQnVt9/\r\n97buGOO1+D/uMRHxVXaQc0niYO4gXgkiqht+N25HXqUT1WQMzkRvG3AGAthfTuqRwl6396FFSGcv\r\nlo/ASpMKZZtwTl246762fasxytp21tfqBw/lB+o+BWyQSEstCa4NKBkuq4NAJPHpnDzDj1ba+PGQ\r\n3c72Rc+glu30pPCT8Xgik8zX1dGvEjB9viiEDspFDyEy7Gjur5RP9V6DdBn/9+o09DV57ooRCBks\r\n9FrYoB4/4OET/JA8pklmmGxD9Rb29iz5jnRVBxYQ87rXqOWpQOn3ZVxDGfFcdAYfJ/TuBfgJkAtW\r\noh1g1SkMFAMa791OGgaLZgpKdTAm5mcB/dpyhuaiPEZPqsW6Lj9+Jst29PgpQOWBOdKVvVXPeiXz\r\nd4XqbqHVq4k+GtEklUxo3J2/KeYE0YD7phEuNZFm5PxvJfL7b1urlIIGekuyEzIdgv+LAtEJrhrP\r\nniSkbKVo8ZbSdUNjeJDwviq+7PSLsZDSY2SFrFUe9s3p4vrB92pFJfOdKs7PXugWlOCi22fTRtPP\r\nocHJYWl5eAOKmymf08QsyaE7m9brmLT1A+JdyqHytoWjyC+wnskyjXNsjds+maf1UICVtybNHEla\r\noAyS3XU1LMqGoRM=$yd+pv1Omkce/Tji+P1pvcnNo7fsTzYe1FsohELb6+2o="
}
```
***


###### 返回参数列表 

|参数名称|参数编码|是否必须|字段长度|描述和样例|
|:---|:---|:---|:---|:---|
|交易结果代码|ret_code|是|String(4)|0000 （申请成功）.|
|交易结果描述|ret_msg|是|String(100)|交易成功|
|签名方式|sign_type|是|String|RSA |
|签名|sign|是|String|RSA加密签名，见安全签名机制|
|商户编号|oid_partner|是|String(18)|商户编号是商户在连连支付平台上开设的商户号码为18位数字，如 ：201304121000001004 |
|商户付款流水号|no_order|是|String(32)|商户系统唯一标识该付款的流水号|
|连连支付支付单号|oid_paybill|否|String(18)|支付订单创建成功的时候返回|
|验证码|confirm_code|否|String(6)|当校验疑似重复或卡号姓名不一致时返回，用于确认付款接口|

###### 付款接口返回响应报文，样例如下： 
```html
{   
    "no_order": "2016081814228",   
    "oid_partner": "201606020000150062",   
    "oid_paybill": "2016081847411984",   
    "ret_code": "0000",   
    "ret_msg": "交易成功",   
    "sign":"gMMBfHBkD6gFDfV0DgA9yGYubY1nejBnVpEh0UTAgYPIYVb5F7TPdoh8R3WnYPFn3RFG4M4oRJT26wdbXtJj84z5N1mzqIOxBzQ6IZ5gXz2tFq1dWy9ro0GDG9DmxPpTj5BidOzE4 85/caI81EEtQnvrva4z14NHFL3vEC2QJoo=",   
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
}'
```
