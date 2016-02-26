![huayi](http://www.360bao.com/Content/Image/logo.png)


##测试服务器地址
http://service.360bao.com:50022

##第一步：从服务器请求SessionId
使用注册得到的partnerId，向服务器请求SessionId

* url:http://service.360bao.com:50022/fast/beigin_session
* 上行数据：
```javascript
{
  "partnerId": "beijinghuayi"
}
```
* 下行数据：
```javascript
{
  "success": true,
  "sessionId": "51ac21fc4efc4f8ca16b7b816fd175f7"//SessionId,以后每一次请求都需要将SessionId带入
}
```
##第二步：从服务器获取用户信息
输入车辆行驶区域，车牌号，手机号获取用户信息，如果用户以前在平台上购买过车险，则返回相关数据。

* url:http://service.360bao.com:50022/fast/get_customer_info
* 上行数据：
```javascript
{
  "sessionId": "51ac21fc4efc4f8ca16b7b816fd175f7",
  "cityCode": "510100",
  "noLicense": false,
  "licenseNo": "川AP9u81",
  "ownerMobile": "13271822680"
}
```
* 下行数据：
```javascript
{
  "engineNo": "8514691",//发动机号
  "isTransfered": false,//是否过户车
  "ownerIdNo": "510101198312185685",//车主身份证号
  "ownerName": "陈金龙",//车主姓名
  "registerDate": "2011-03-17",//车辆注册日期
  "sessionId": "51ac21fc4efc4f8ca16b7b816fd175f7",
  "success": true,
  "transferedDate": "1970-01-01",//过户日期
  "vehicleFrameNo": "ldc933l27a51489181",//车架号
  "vehicleId": "BZAAED0108",//车辆配置型号ID
  "vehicleModelName": ""//车辆配置型号名称
}
```
##第三步：提交用户信息和车险信息
提交用户信息和车险信息以获取报价

* url:http://service.360bao.com:50022/fast/get_price
* 上行数据：
```javascript
{
  "sessionId": "51ac21fc4efc4f8ca16b7b816fd175f7",
  "engineNo": "8514691",//发动机号
  "registerDate": "2011-03-17",//车辆注册日期
  "vehicleFrameNo": "ldc933l27a51489181",//车架号
  "vehicleId": "BZAAED0108",//车辆配置型号ID
  "isTransfered": false,//是否过户车
  "transferedDate": "",//过户日期
  "ownerName": "陈金龙",//车主姓名
  "ownerIdNo": "510101198312185685",//车主身份证号
  "damageCoverage": true,//车辆损失险
  "thirdPartyLiabilityCoverage": 300000.0,//三责险
  "robberyTheftCoverage": true,//全车盗抢险
  "driverLiabilityCoverage": 10000.0,//司机座位责任险
  "passengerLiabilityCoverage": 10000.0,//乘客座位责任险
  "damageNoneDeductible": true,//不计免赔险(车损险)
  "thirdPartyLiabilityNoneDeductible": true,//不计免赔险(三者险)
  "robberyTheftNoneDeductible": true,//不计免赔险(机动车盗抢险)
  "driverLiabilityNoneDeductible": true,//不计免赔险(司机险)
  "passengerLiabilityNoneDeductible": true,//不计免赔险(乘客险)
  "glassBrokenCoverage": 0,//玻璃单独破碎险
  "spontaneousCombustionCoverage": 0.0,//自燃损失险
  "scratchCoverage": 0.0,//车身划痕损险
  "withAverageCoverage": 0,//发动机涉水损失险
  "forceCoverage": true,//交强险
  "bizBeginDate": "2016-02-26",//商业险生效日期
  "forceBeginDate": "2016-02-26"//交强险生效日期
}
```
* 下行数据：
```javascript
{
  "biz": {
    "bizTotal": {
      "label": "商业总保费",
      "premium": "371450",
      "value": ""
    },
    "damage": {
      "label": "机动车损失保险",
      "premium": "122574",
      "value": "52352.00"
    },
    "damageNoneDeductible": {
      "label": "不计免赔险(机动车损失保险)",
      "premium": "18386",
      "value": "1"
    },
    "driverLiability": {
      "label": "车上人员责任保险(驾驶员)",
      "premium": "2962",
      "value": "10000.00"
    },
    "driverLiabilityNoneDeductible": {
      "label": "不计免赔险(车上人员责任保险(驾驶员))",
      "premium": "444",
      "value": "1"
    },
    "forceCoverage": {
      "label": "交强险",
      "premium": "0",
      "value": "1"
    },
    "glassBroken": {
      "label": "玻璃单独破碎险",
      "premium": "11229",
      "value": "1"
    },
    "lastClaimText": {
      "label": "上年出险信息",
      "premium": "",
      "value": "经行协平台查询，您的爱车上年出险次数为1次，合计赔付款金额为1350.00元"
    },
    "passengerLiability": {
      "label": "车上人员责任保险(乘客)",
      "premium": "7514",
      "value": "10000.00"
    },
    "passengerLiabilityNoneDeductible": {
      "label": "不计免赔险(车上人员责任保险(乘客))",
      "premium": "1127",
      "value": "1"
    },
    "robberyTheft": {
      "label": "全车盗抢保险",
      "premium": "27204",
      "value": "52352.00"
    },
    "robberyTheftNoneDeductible": {
      "label": "不计免赔险(全车盗抢保险)",
      "premium": "5441",
      "value": "1"
    },
    "scratch": {
      "label": "车身划痕损失险",
      "premium": "44073",
      "value": "2000.00"
    },
    "scratchNoneDeductible": {
      "label": "不计免赔险(车身划痕损失险)",
      "premium": "0",
      "value": "0"
    },
    "spontaneousCombustion": {
      "label": "自燃损失险",
      "premium": "11348",
      "value": "52352.00"
    },
    "thirdPartyLiability": {
      "label": "商业第三者责任险",
      "premium": "103607",
      "value": "300000.00"
    },
    "thirdPartyLiabilityNoneDeductible": {
      "label": "不计免赔险(商业第三者责任险)",
      "premium": "15541",
      "value": "1"
    },
    "withAverage": {
      "label": "发动机涉水损失险",
      "premium": "0",
      "value": "0"
    }
  },
  "deadline": {
    "bizBeginDate": {
      "label": "商业险起保日期",
      "value": "2016-03-17"
    },
    "forceBeginDate": {
      "label": "交强险起保日期",
      "value": "2016-03-17"
    }
  },
  "force": {
    "force": {
      "label": "交强险",
      "premium": "66500"
    },
    "forceTotal": {
      "label": "交强险总保费",
      "premium": "96500"
    },
    "vehicleTax": {
      "label": "车船税",
      "premium": "30000"
    }
  },
  "sessionId": "51ac21fc4efc4f8ca16b7b816fd175f7",
  "success": true,
  "total": {
    "label": "网购价",
    "premium": "467950",
    "value": ""
  }
}
```
##第四步：提交配送信息并获取支付链接

* url:http://service.360bao.com:50022/fast/pre_pay
* 上行数据：
```javascript
{
  "sessionId": "51ac21fc4efc4f8ca16b7b816fd175f7",
  "applicantName": "陈金龙",//投保人姓名
  "applicantId": "510101198312185685",//投保人身份证号码
  "applicantPhone": "13271822680",//投保人电话
  "insuredName": "陈金龙",//被保人姓名
  "insuredId": "510101198312185685",//被保人身份证号码
  "insuredIdAddress": "南湖公园旁",//被保人身份证地址
  "insuredPhone": "13271822680",//被保人电话
  "addresseeName": "陈金龙",//收件人姓名
  "addresseePhone": "13271822680",//收件人电话
  "addresseeCityCode": "110100",//收件人地区码
  "addresseeDetails": "南湖公园旁",//收件人地址
  "deliveryDate": "2016-02-27T00:00:00"//配送日期
}
```
* 下行数据：
```javascript
{
  "NeedVerifySMS": "",//是否需要短信验证（文档待完善，请稍候）
  "ProposalNo": "T211105092015097566",//保险公司投保单号
  "TBOrderId": "1746b46825e3488085f8c7b9bda54985",//华谊总订单号
  "bizBeginDate": "2016-03-17",//商业险起保日期
  "bizTotalPremium": "439880",//商业总保费
  "forceBeginDate": "2016-03-17",//交强险起保日期
  "forcePremium": "95000",//交强险保费
  "forceTotalPremium": "96500",//交强险保费（交强险+车船税）
  "payUrl": "http://chexian.sinosig.com/netCarPcPayVerifyAction.action?proposalno=556be090ddc65d0f6714ca28033cc5696ae99318245422ac\u0026insrancename=8a74f2394ce3c9ba",//支付链接
  "sessionId": "51ac21fc4efc4f8ca16b7b816fd175f7",
  "standardPremium": "701341",//市场价
  "success": true,
  "totalPremium": "540880",//网购价
  "vehicleTaxPremium": "6000"//车船税
}
```