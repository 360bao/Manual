![huayi](http://www.360bao.com/Content/Image/logo.png)


##正式服务器地址
http://service.360bao.com
##测试服务器地址1
http://service.360bao.com:50023
测试服务器1返回固定数据，用于测试访问者的解析方法

##第一步：从服务器请求SessionId
使用注册得到的partnerId，向服务器请求SessionId

* url:http://service.360bao.com/fast/beigin_session
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
该步骤也可以不调用，不影响整体报价和购买流程，第三方如果有自己的用户数据库，则可以使用自己的数据。
行驶区域码见 [附1](#附1)

* url:http://service.360bao.com/fast/get_customer_info
* 上行数据：
```javascript
{
  "sessionId": "51ac21fc4efc4f8ca16b7b816fd175f7",
  "cityCode": "510100",
  "noLicense": false,//新车还未上牌
  "licenseNo": "川AP9u81",//车牌号
  "ownerPhone": "13271822680"//车主电话号码
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

注：premium都以分为单位。

* url:http://service.360bao.com/fast/get_price
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
  "damageCoverage": true,//车辆损失险 [投保:true,不投保:false]
  "thirdPartyLiabilityCoverage": 300000.0,//三责险 见 [附3]
  "robberyTheftCoverage": true,//全车盗抢险 [投保:true,不投保:false]
  "driverLiabilityCoverage": 10000.0,//司机座位责任险 见 [附4]
  "passengerLiabilityCoverage": 10000.0,//乘客座位责任险 见 [附5]
  "damageNoneDeductible": true,//不计免赔险(车损险) [投保:true,不投保:false]
  "thirdPartyLiabilityNoneDeductible": true,//不计免赔险(三者险) [投保:true,不投保:false]
  "robberyTheftNoneDeductible": true,//不计免赔险(机动车盗抢险) [投保:true,不投保:false]
  "driverLiabilityNoneDeductible": true,//不计免赔险(司机险) [投保:true,不投保:false]
  "passengerLiabilityNoneDeductible": true,//不计免赔险(乘客险) [投保:true,不投保:false]
  "glassBrokenCoverage": 0,//玻璃单独破碎险 见 [附6]
  "spontaneousCombustionCoverage": false,//自燃损失险 [投保:true,不投保:false]
  "scratchCoverage": 0,//车身划痕损险  见 [附7]
  "withAverageCoverage": false,//发动机涉水损失险 [投保:true,不投保:false]
  "forceCoverage": true,//交强险 [投保:true,不投保:false]
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
      "premium": 371450,
      "value": 0
    },
    "damage": {
      "label": "机动车损失保险",
      "premium": 122574,
      "value": 52352.00
    },
    "damageNoneDeductible": {
      "label": "不计免赔险(机动车损失保险)",
      "premium": 18386,
      "value": 1
    },
    "driverLiability": {
      "label": "车上人员责任保险(驾驶员)",
      "premium": 2962,
      "value": 10000.00
    },
    "driverLiabilityNoneDeductible": {
      "label": "不计免赔险(车上人员责任保险(驾驶员))",
      "premium": 444,
      "value": true
    },
    "forceCoverage": {
      "label": "交强险",
      "premium": 0,
      "value": true
    },
    "glassBroken": {
      "label": "玻璃单独破碎险",
      "premium": 11229,
      "value": 1
    },
    "lastClaimText": {
      "label": "上年出险信息",
      "premium": "",
      "value": "经行协平台查询，您的爱车上年出险次数为1次，合计赔付款金额为1350.00元"
    },
    "passengerLiability": {
      "label": "车上人员责任保险(乘客)",
      "premium": 7514,
      "value": 10000.00
    },
    "passengerLiabilityNoneDeductible": {
      "label": "不计免赔险(车上人员责任保险(乘客))",
      "premium": 1127,
      "value": true
    },
    "robberyTheft": {
      "label": "全车盗抢保险",
      "premium": 27204,
      "value": 52352.00
    },
    "robberyTheftNoneDeductible": {
      "label": "不计免赔险(全车盗抢保险)",
      "premium": 5441,
      "value": true
    },
    "scratch": {
      "label": "车身划痕损失险",
      "premium": 44073,
      "value": 2000.00
    },
    "scratchNoneDeductible": {
      "label": "不计免赔险(车身划痕损失险)",
      "premium": 0,
      "value": false
    },
    "spontaneousCombustion": {
      "label": "自燃损失险",
      "premium": 11348,
      "value": 52352.00
    },
    "thirdPartyLiability": {
      "label": "商业第三者责任险",
      "premium": 103607,
      "value": 300000.00
    },
    "thirdPartyLiabilityNoneDeductible": {
      "label": "不计免赔险(商业第三者责任险)",
      "premium": 15541,
      "value": true
    },
    "withAverage": {
      "label": "发动机涉水损失险",
      "premium": 0,
      "value": true
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
      "premium": 66500
    },
    "forceTotal": {
      "label": "交强险总保费",
      "premium": 96500
    },
    "vehicleTax": {
      "label": "车船税",
      "premium": 30000
    }
  },
  "sessionId": "51ac21fc4efc4f8ca16b7b816fd175f7",
  "success": true,
  "total": {
    "label": "网购价",
    "premium": 467950
  }
}
```
##第四步：提交配送信息并获取支付链接
地区码的取得，详见 [附2](#附2)
* url:http://service.360bao.com/fast/pre_pay
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
  "bizTotalPremium": 439880,//商业总保费
  "forceBeginDate": "2016-03-17",//交强险起保日期
  "forcePremium": 95000,//交强险保费
  "forceTotalPremium": 96500,//交强险保费（交强险+车船税）
  "payUrl": "http://chexian.sinosig.com/netCarPcPayVerifyAction.action?proposalno=556be090ddc65d0f6714ca28033cc5696ae99318245422ac\u0026insrancename=8a74f2394ce3c9ba",//支付链接
  "sessionId": "51ac21fc4efc4f8ca16b7b816fd175f7",
  "standardPremium": 701341,//市场价
  "success": true,
  "totalPremium": 540880,//网购价
  "vehicleTaxPremium": 6000//车船税
}
```

# 附1
Simple是简称

```javascript
[{"Id":110000,"Name":"北京","Simple":"京","CityList":[{"Id":110100,"Name":"北京"}]},{"Id":120000,"Name":"天津","Simple":"津","CityList":[{"Id":120100,"Name":"天津"}]},{"Id":130000,"Name":"河北","Simple":"冀","CityList":[{"Id":130100,"Name":"石家庄"},{"Id":130200,"Name":"唐山"},{"Id":130300,"Name":"秦皇岛"},{"Id":130400,"Name":"邯郸"},{"Id":130500,"Name":"邢台"},{"Id":130600,"Name":"保定"},{"Id":130700,"Name":"张家口"},{"Id":130800,"Name":"承德"},{"Id":130900,"Name":"沧州"},{"Id":131000,"Name":"廊坊"},{"Id":131100,"Name":"衡水"}]},{"Id":140000,"Name":"山西","Simple":"晋","CityList":[{"Id":140100,"Name":"太原"},{"Id":140200,"Name":"大同"},{"Id":140300,"Name":"阳泉"},{"Id":140400,"Name":"长治"},{"Id":140500,"Name":"晋城"},{"Id":140600,"Name":"朔州"},{"Id":140700,"Name":"晋中"},{"Id":140800,"Name":"运城"},{"Id":140900,"Name":"忻州"},{"Id":141000,"Name":"临汾"},{"Id":141100,"Name":"吕梁"}]},{"Id":150000,"Name":"内蒙古","Simple":"蒙","CityList":[{"Id":150100,"Name":"呼和浩特"},{"Id":150200,"Name":"包头"},{"Id":150300,"Name":"乌海"},{"Id":150400,"Name":"赤峰"},{"Id":150500,"Name":"通辽"},{"Id":150600,"Name":"鄂尔多斯"},{"Id":150700,"Name":"呼伦贝尔"},{"Id":150800,"Name":"巴彦淖尔"},{"Id":150900,"Name":"乌兰察布"},{"Id":152200,"Name":"兴安盟"},{"Id":152500,"Name":"锡林郭勒盟"},{"Id":152900,"Name":"阿拉善盟"}]},{"Id":210000,"Name":"辽宁","Simple":"辽","CityList":[{"Id":210100,"Name":"沈阳"},{"Id":210200,"Name":"大连"},{"Id":210300,"Name":"鞍山"},{"Id":210400,"Name":"抚顺"},{"Id":210500,"Name":"本溪"},{"Id":210600,"Name":"丹东"},{"Id":210700,"Name":"锦州"},{"Id":210800,"Name":"营口"},{"Id":210900,"Name":"阜新"},{"Id":211000,"Name":"辽阳"},{"Id":211100,"Name":"盘锦"},{"Id":211200,"Name":"铁岭"},{"Id":211300,"Name":"朝阳"},{"Id":211400,"Name":"葫芦岛"}]},{"Id":220000,"Name":"吉林","Simple":"吉","CityList":[{"Id":220100,"Name":"长春"},{"Id":220200,"Name":"吉林"},{"Id":220300,"Name":"四平"},{"Id":220400,"Name":"辽源"},{"Id":220500,"Name":"通化"},{"Id":220600,"Name":"白山"},{"Id":220700,"Name":"松原"},{"Id":220800,"Name":"白城"},{"Id":222400,"Name":"延边"}]},{"Id":230000,"Name":"黑龙江","Simple":"黑","CityList":[{"Id":230100,"Name":"哈尔滨"},{"Id":230200,"Name":"齐齐哈尔"},{"Id":230300,"Name":"鸡西"},{"Id":230400,"Name":"鹤岗"},{"Id":230500,"Name":"双鸭山"},{"Id":230600,"Name":"大庆"},{"Id":230700,"Name":"伊春"},{"Id":230800,"Name":"佳木斯"},{"Id":230900,"Name":"七台河"},{"Id":231000,"Name":"牡丹江"},{"Id":231100,"Name":"黑河"},{"Id":231200,"Name":"绥化"},{"Id":232700,"Name":"大兴安岭"}]},{"Id":310000,"Name":"上海","Simple":"沪","CityList":[{"Id":310100,"Name":"上海"}]},{"Id":320000,"Name":"江苏","Simple":"苏","CityList":[{"Id":320100,"Name":"南京"},{"Id":320200,"Name":"无锡"},{"Id":320300,"Name":"徐州"},{"Id":320400,"Name":"常州"},{"Id":320500,"Name":"苏州"},{"Id":320600,"Name":"南通"},{"Id":320700,"Name":"连云港"},{"Id":320800,"Name":"淮安"},{"Id":320900,"Name":"盐城"},{"Id":321000,"Name":"扬州"},{"Id":321100,"Name":"镇江"},{"Id":321200,"Name":"泰州"},{"Id":321300,"Name":"宿迁"}]},{"Id":330000,"Name":"浙江","Simple":"浙","CityList":[{"Id":330100,"Name":"杭州"},{"Id":330200,"Name":"宁波"},{"Id":330300,"Name":"温州"},{"Id":330400,"Name":"嘉兴"},{"Id":330500,"Name":"湖州"},{"Id":330600,"Name":"绍兴"},{"Id":330700,"Name":"金华"},{"Id":330800,"Name":"衢州"},{"Id":330900,"Name":"舟山"},{"Id":331000,"Name":"台州"},{"Id":331100,"Name":"丽水"}]},{"Id":340000,"Name":"安徽","Simple":"皖","CityList":[{"Id":340100,"Name":"合肥"},{"Id":340200,"Name":"芜湖"},{"Id":340300,"Name":"蚌埠"},{"Id":340400,"Name":"淮南"},{"Id":340500,"Name":"马鞍山"},{"Id":340600,"Name":"淮北"},{"Id":340700,"Name":"铜陵"},{"Id":340800,"Name":"安庆"},{"Id":341000,"Name":"黄山"},{"Id":341100,"Name":"滁州"},{"Id":341200,"Name":"阜阳"},{"Id":341300,"Name":"宿州"},{"Id":341400,"Name":"巢湖"},{"Id":341500,"Name":"六安"},{"Id":341600,"Name":"亳州"},{"Id":341700,"Name":"池州"},{"Id":341800,"Name":"宣城"}]},{"Id":350000,"Name":"福建","Simple":"闽","CityList":[{"Id":350100,"Name":"福州"},{"Id":350200,"Name":"厦门"},{"Id":350300,"Name":"莆田"},{"Id":350400,"Name":"三明"},{"Id":350500,"Name":"泉州"},{"Id":350600,"Name":"漳州"},{"Id":350700,"Name":"南平"},{"Id":350800,"Name":"龙岩"},{"Id":350900,"Name":"宁德"}]},{"Id":360000,"Name":"江西","Simple":"赣","CityList":[{"Id":360100,"Name":"南昌"},{"Id":360200,"Name":"景德镇"},{"Id":360300,"Name":"萍乡"},{"Id":360400,"Name":"九江"},{"Id":360500,"Name":"新余"},{"Id":360600,"Name":"鹰潭"},{"Id":360700,"Name":"赣州"},{"Id":360800,"Name":"吉安"},{"Id":360900,"Name":"宜春"},{"Id":361000,"Name":"抚州"},{"Id":361100,"Name":"上饶"}]},{"Id":370000,"Name":"山东","Simple":"鲁","CityList":[{"Id":370100,"Name":"济南"},{"Id":370200,"Name":"青岛"},{"Id":370300,"Name":"淄博"},{"Id":370400,"Name":"枣庄"},{"Id":370500,"Name":"东营"},{"Id":370600,"Name":"烟台"},{"Id":370700,"Name":"潍坊"},{"Id":370800,"Name":"济宁"},{"Id":370900,"Name":"泰安"},{"Id":371000,"Name":"威海"},{"Id":371100,"Name":"日照"},{"Id":371200,"Name":"莱芜"},{"Id":371300,"Name":"临沂"},{"Id":371400,"Name":"德州"},{"Id":371500,"Name":"聊城"},{"Id":371600,"Name":"滨州"},{"Id":371700,"Name":"菏泽"}]},{"Id":410000,"Name":"河南","Simple":"豫","CityList":[{"Id":410100,"Name":"郑州"},{"Id":410200,"Name":"开封"},{"Id":410300,"Name":"洛阳"},{"Id":410400,"Name":"平顶山"},{"Id":410500,"Name":"安阳"},{"Id":410600,"Name":"鹤壁"},{"Id":410700,"Name":"新乡"},{"Id":410800,"Name":"焦作"},{"Id":410900,"Name":"濮阳"},{"Id":411000,"Name":"许昌"},{"Id":411100,"Name":"漯河"},{"Id":411200,"Name":"三门峡"},{"Id":411300,"Name":"南阳"},{"Id":411400,"Name":"商丘"},{"Id":411500,"Name":"信阳"},{"Id":411600,"Name":"周口"},{"Id":411700,"Name":"驻马店"},{"Id":419000,"Name":"济源"}]},{"Id":420000,"Name":"湖北","Simple":"鄂","CityList":[{"Id":420100,"Name":"武汉"},{"Id":420200,"Name":"黄石"},{"Id":420300,"Name":"十堰"},{"Id":420500,"Name":"宜昌"},{"Id":420600,"Name":"襄阳"},{"Id":420700,"Name":"鄂州"},{"Id":420800,"Name":"荆门"},{"Id":420900,"Name":"孝感"},{"Id":421000,"Name":"荆州"},{"Id":421100,"Name":"黄冈"},{"Id":421200,"Name":"咸宁"},{"Id":421300,"Name":"随州"},{"Id":422800,"Name":"恩施"},{"Id":423100,"Name":"仙桃"},{"Id":423200,"Name":"潜江"},{"Id":423300,"Name":"天门"},{"Id":423400,"Name":"神农架"}]},{"Id":430000,"Name":"湖南","Simple":"湘","CityList":[{"Id":430100,"Name":"长沙"},{"Id":430200,"Name":"株洲"},{"Id":430300,"Name":"湘潭"},{"Id":430400,"Name":"衡阳"},{"Id":430500,"Name":"邵阳"},{"Id":430600,"Name":"岳阳"},{"Id":430700,"Name":"常德"},{"Id":430800,"Name":"张家界"},{"Id":430900,"Name":"益阳"},{"Id":431000,"Name":"郴州"},{"Id":431100,"Name":"永州"},{"Id":431200,"Name":"怀化"},{"Id":431300,"Name":"娄底"},{"Id":433100,"Name":"湘西"}]},{"Id":440000,"Name":"广东","Simple":"粤","CityList":[{"Id":440100,"Name":"广州"},{"Id":440200,"Name":"韶关"},{"Id":440300,"Name":"深圳"},{"Id":440400,"Name":"珠海"},{"Id":440500,"Name":"汕头"},{"Id":440600,"Name":"佛山"},{"Id":440700,"Name":"江门"},{"Id":440800,"Name":"湛江"},{"Id":440900,"Name":"茂名"},{"Id":441200,"Name":"肇庆"},{"Id":441300,"Name":"惠州"},{"Id":441400,"Name":"梅州"},{"Id":441500,"Name":"汕尾"},{"Id":441600,"Name":"河源"},{"Id":441700,"Name":"阳江"},{"Id":441800,"Name":"清远"},{"Id":441900,"Name":"东莞"},{"Id":442000,"Name":"中山"},{"Id":445100,"Name":"潮州"},{"Id":445200,"Name":"揭阳"},{"Id":445300,"Name":"云浮"}]},{"Id":450000,"Name":"广西","Simple":"桂","CityList":[{"Id":450100,"Name":"南宁"},{"Id":450200,"Name":"柳州"},{"Id":450300,"Name":"桂林"},{"Id":450400,"Name":"梧州"},{"Id":450500,"Name":"北海"},{"Id":450600,"Name":"防城港"},{"Id":450700,"Name":"钦州"},{"Id":450800,"Name":"贵港"},{"Id":450900,"Name":"玉林"},{"Id":451000,"Name":"百色"},{"Id":451100,"Name":"贺州"},{"Id":451200,"Name":"河池"},{"Id":451300,"Name":"来宾"},{"Id":451400,"Name":"崇左"}]},{"Id":460000,"Name":"海南","Simple":"琼","CityList":[{"Id":460100,"Name":"海口"},{"Id":460200,"Name":"三亚"},{"Id":461100,"Name":"五指山"},{"Id":461200,"Name":"琼海"},{"Id":461300,"Name":"儋州"},{"Id":461400,"Name":"文昌"},{"Id":461500,"Name":"万宁"},{"Id":461600,"Name":"东方"},{"Id":461700,"Name":"定安"},{"Id":461800,"Name":"屯昌"},{"Id":461900,"Name":"澄迈"},{"Id":462000,"Name":"临高"},{"Id":462100,"Name":"白沙"},{"Id":462200,"Name":"昌江"},{"Id":462300,"Name":"乐东"},{"Id":462400,"Name":"陵水"},{"Id":462500,"Name":"保亭"},{"Id":462600,"Name":"琼中"}]},{"Id":500000,"Name":"重庆","Simple":"渝","CityList":[{"Id":500100,"Name":"重庆"}]},{"Id":510000,"Name":"四川","Simple":"川","CityList":[{"Id":510100,"Name":"成都"},{"Id":510300,"Name":"自贡"},{"Id":510400,"Name":"攀枝花"},{"Id":510500,"Name":"泸州"},{"Id":510600,"Name":"德阳"},{"Id":510700,"Name":"绵阳"},{"Id":510800,"Name":"广元"},{"Id":510900,"Name":"遂宁"},{"Id":511000,"Name":"内江"},{"Id":511100,"Name":"乐山"},{"Id":511300,"Name":"南充"},{"Id":511400,"Name":"眉山"},{"Id":511500,"Name":"宜宾"},{"Id":511600,"Name":"广安"},{"Id":511700,"Name":"达州"},{"Id":511800,"Name":"雅安"},{"Id":511900,"Name":"巴中"},{"Id":512000,"Name":"资阳"},{"Id":513200,"Name":"阿坝"},{"Id":513300,"Name":"甘孜"},{"Id":513400,"Name":"凉山"}]},{"Id":520000,"Name":"贵州","Simple":"贵","CityList":[{"Id":520100,"Name":"贵阳"},{"Id":520200,"Name":"六盘水"},{"Id":520300,"Name":"遵义"},{"Id":520400,"Name":"安顺"},{"Id":522200,"Name":"铜仁"},{"Id":522300,"Name":"黔西南"},{"Id":522400,"Name":"毕节"},{"Id":522600,"Name":"黔东南"},{"Id":522700,"Name":"黔南"}]},{"Id":530000,"Name":"云南","Simple":"云","CityList":[{"Id":530100,"Name":"昆明"},{"Id":530300,"Name":"曲靖"},{"Id":530400,"Name":"玉溪"},{"Id":530500,"Name":"保山"},{"Id":530600,"Name":"昭通"},{"Id":530700,"Name":"丽江"},{"Id":530800,"Name":"普洱"},{"Id":530900,"Name":"临沧"},{"Id":532300,"Name":"楚雄"},{"Id":532500,"Name":"红河"},{"Id":532600,"Name":"文山"},{"Id":532800,"Name":"西双版纳"},{"Id":532900,"Name":"大理"},{"Id":533100,"Name":"德宏"},{"Id":533300,"Name":"怒江"},{"Id":533400,"Name":"迪庆"}]},{"Id":610000,"Name":"陕西","Simple":"陕","CityList":[{"Id":610100,"Name":"西安"},{"Id":610200,"Name":"铜川"},{"Id":610300,"Name":"宝鸡"},{"Id":610400,"Name":"咸阳"},{"Id":610500,"Name":"渭南"},{"Id":610600,"Name":"延安"},{"Id":610700,"Name":"汉中"},{"Id":610800,"Name":"榆林"},{"Id":610900,"Name":"安康"},{"Id":611000,"Name":"商洛"}]},{"Id":620000,"Name":"甘肃","Simple":"甘","CityList":[{"Id":620100,"Name":"兰州"},{"Id":620200,"Name":"嘉峪关"},{"Id":620300,"Name":"金昌"},{"Id":620400,"Name":"白银"},{"Id":620500,"Name":"天水"},{"Id":620600,"Name":"武威"},{"Id":620700,"Name":"张掖"},{"Id":620800,"Name":"平凉"},{"Id":620900,"Name":"酒泉"},{"Id":621000,"Name":"庆阳"},{"Id":621100,"Name":"定西"},{"Id":621200,"Name":"陇南"},{"Id":622900,"Name":"临夏"},{"Id":623000,"Name":"甘南"}]},{"Id":630000,"Name":"青海","Simple":"青","CityList":[{"Id":630100,"Name":"西宁"},{"Id":632100,"Name":"海东"},{"Id":632200,"Name":"海北"},{"Id":632300,"Name":"黄南"},{"Id":632500,"Name":"海南"},{"Id":632600,"Name":"果洛"},{"Id":632700,"Name":"玉树"},{"Id":632800,"Name":"海西"}]},{"Id":640000,"Name":"宁夏","Simple":"宁","CityList":[{"Id":640100,"Name":"银川"},{"Id":640200,"Name":"石嘴山"},{"Id":640300,"Name":"吴忠"},{"Id":640400,"Name":"固原"},{"Id":640500,"Name":"中卫"}]},{"Id":650000,"Name":"新疆","Simple":"新","CityList":[{"Id":650100,"Name":"乌鲁木齐"},{"Id":650200,"Name":"克拉玛依"},{"Id":652100,"Name":"吐鲁番"},{"Id":652200,"Name":"哈密"},{"Id":652300,"Name":"昌吉"},{"Id":652700,"Name":"博尔塔拉"},{"Id":652800,"Name":"巴音郭楞"},{"Id":652900,"Name":"阿克苏"},{"Id":653000,"Name":"克孜勒苏"},{"Id":653100,"Name":"喀什"},{"Id":653200,"Name":"和田"},{"Id":654000,"Name":"伊犁"},{"Id":654200,"Name":"塔城"},{"Id":654300,"Name":"阿勒泰"},{"Id":654500,"Name":"奎屯"},{"Id":655100,"Name":"石河子"}]}]
```

# 附2

使用jsonp调用：http://services.360bao.com:50011/region?parent={parent}来获取地理位置：
http://services.360bao.com:50011/region?parent=0，取得的数据如下：

```javascript
[{"TITLE":"北京","CODE":"11"},{"TITLE":"天津","CODE":"12"},{"TITLE":"河北省","CODE":"13"},{"TITLE":"山西省","CODE":"14"},{"TITLE":"内蒙古自治区","CODE":"15"},{"TITLE":"辽宁省","CODE":"21"},{"TITLE":"吉林省","CODE":"22"},{"TITLE":"黑龙江省","CODE":"23"},{"TITLE":"上海市","CODE":"31"},{"TITLE":"江苏省","CODE":"32"},{"TITLE":"浙江省","CODE":"33"},{"TITLE":"安徽省","CODE":"34"},{"TITLE":"福建省","CODE":"35"},{"TITLE":"江西省","CODE":"36"},{"TITLE":"山东省","CODE":"37"},{"TITLE":"河南省","CODE":"41"},{"TITLE":"湖北省","CODE":"42"},{"TITLE":"湖南省","CODE":"43"},{"TITLE":"广东省","CODE":"44"},{"TITLE":"广西壮族自治区","CODE":"45"},{"TITLE":"海南省","CODE":"46"},{"TITLE":"重庆市","CODE":"50"},{"TITLE":"四川省","CODE":"51"},{"TITLE":"贵州省","CODE":"52"},{"TITLE":"云南省","CODE":"53"},{"TITLE":"西藏自治区","CODE":"54"},{"TITLE":"陕西省","CODE":"61"},{"TITLE":"甘肃省","CODE":"62"},{"TITLE":"青海省","CODE":"63"},{"TITLE":"宁夏回族自治区","CODE":"64"},{"TITLE":"新疆维吾尔自治区","CODE":"65"}]
```

# 附3
三责险待选项：
- 0:不投保
- 50000 :5万
- 100000:10万
- 200000:20万
- 300000:30万
- 500000:50万
- 1000000:100万

# 附4
司机座位责任险待选项
- 0:不投保
- 10000:1万
- 20000:2万
- 30000:3万
- 40000:4万
- 50000:5万
- 100000:10万
- 200000:20万

# 附5
乘客座位责任险待选项
- 0:不投保
- 10000:1万
- 20000:2万
- 30000:3万
- 40000:4万
- 50000:5万
- 100000:10万
- 200000:20万

# 附6
玻璃单独破碎险待选项
- 0:不投保
- 1:国产
- 2:进口

# 附7
车身划痕损险待选项
- 0:不投保
- 2000:2000元
- 5000:5000元