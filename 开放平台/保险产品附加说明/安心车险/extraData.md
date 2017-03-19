##extraData

```javascript
{
  "vehicle": {
    "cityCode": "440100",//车辆运行城市,目前仅支持广东和北京,见地区编码文档<areaCode.md>
    "plateNo": "粤A33381",//车牌号(如果无牌则空白)
    "vehicleCode": "BZAAED0110",//车辆配置型号编码(附1)
    "vehicleModel": "东风标致307 2010款 豪华版 手动档 1.6L 参考价：95800",
    "vin": "LDC933L24A5148401",//车架号
    "engineNo": "8544401",//发动机号
    "registrationDate": "20140301",//车辆注册日期
    "seats": 5,//座位数
    "transferredDate": "20170301",//过户日期(如果不是过户车则空白)
    "owner": {
      "fullName": "陈多大",//车主姓名
      "phone": "13271822680",//车主电话号码
      "idType": "身份证",//车主身份证号
      "idNo": "37172219841024847X",
      "email": "chenjinlong@360bao.com",
      "address": "南湖水乡"
    }
  },
  "insurances": {
    "compulsory": {
      "startDate": "20170320", //交强险生效日期
      "coverage": true //交强险 [true:投保 false:不投保]
    },
    "commerce": {
      "startDate": "20170320", //商业险生效日期
      "insurances": {
        "damage": {
          "noDeductible": {
            "coverage": true //不计免赔 [true:投保 false:不投保]
          },
          "coverage": true //车辆损失险 [true:投保 false:不投保]
        },
        "thirdPartyLiability": {
          "noDeductible": {
            "coverage": true //不计免赔 [true:投保 false:不投保]
          },
          "coverage": 50000 //三责险 [0:不投保 50000 :5万 100000:10万 200000:20万 300000:30万 500000:50万 1000000:100万 2000000:200万 3000000:300万]
        },
        "robberyTheft": {
          "noDeductible": {
            "coverage": true //不计免赔 [true:投保 false:不投保]
          },
          "coverage": true //全车盗抢险 [true:投保 false:不投保]
        },
        "driverLiability": {
          "noDeductible": {
            "coverage": true //不计免赔 [true:投保 false:不投保]
          },
          "coverage": 10000 //司机座位责任险 [0:不投保 10000:1万 20000:2万 30000:3万 40000:4万 50000:5万 100000:10万 200000:20万 300000:30万 500000:50万 1000000:100万]
        },
        "passengerLiability": {
          "noDeductible": {
            "coverage": true //不计免赔 [true:投保 false:不投保]
          },
          "coverage": 10000 //乘客座位责任险 [0:不投保 10000:1万 20000:2万 30000:3万 40000:4万 50000:5万 100000:10万 200000:20万 300000:30万 500000:50万 1000000:100万]
        },
        "glassBreakage": {
          "coverage": "domestic" //玻璃单独破碎险 [空着不填:不投保 domestic:国产 imported:进口]
        },
        "scratch": {
          "noDeductible": {
            "coverage": true //不计免赔 [true:投保 false:不投保]
          },
          "coverage": 2000 //车身划痕损险  [0:不投保 2000:2000元 5000:5000元 10000:10000元]
        },
        "spontaneousCombustion": {
          "noDeductible": {
            "coverage": true //不计免赔 [true:投保 false:不投保]
          },
          "coverage": true //自燃损失险 [true:投保 false:不投保]
        },
        "withAverage": {
          "noDeductible": {
            "coverage": true //不计免赔 [true:投保 false:不投保]
          },
          "coverage": true //发动机涉水损失险 [true:投保 false:不投保]
        },
        "unknown3rdParty": {
          "coverage": true //机动车损失保险无法找到第三方特约险 [true:投保 false:不投保]
        },
        "moralDamageLiability": {
          "noDeductible": {
            "coverage": true //不计免赔 [true:投保 false:不投保]
          },
          "coverage": 10000 //精神损害抚慰金责任险,只能是10000
        },
        "anyGarage": {
          "coverage": true //指定修理厂险
        }
      }
    }
  }
}
```
#  需特别注意

* 购买北京地区车险必须对投保人和被保人进行身份信息采集，也就是需要上传身份证上正背面所有信息，包括姓名，性别，民族，出生日期，住址，身份证号，签发机关，有效期限
* 采集信息时，可以让用户手动输入，也可以调用我们的身份证OCR服务，参见 [身份证OCR服务](<../../公共服务/身份证OCR服务.md>)
* 广东地区仅需要姓名，身份证号


# 附1

使用jsonp调用：http://platform.360bao.com/foundation/auto/query_model?model={model}来获取车辆配置型号编码，其中model是用户行驶证的车型信息
