# create order:
```javascript
{
    "insurance": {
        "pid": "xxtx",
        "name": "孝行天下",
        "insurancePeriod": "10年",
        "paymentPeriod": "10年",
        "premium": 5000000,
        "copies": 1,
        "subInsurances": [
            {
                "name": "孝行天下子保险1",
                "premium": 2000000,
                "copies": 1
            },
            {
                "name": "孝行天下子保险2",
                "premium": 1,
                "copies": 1
            }
        ]
    },
    "applicant": {
        "fullName": "投保人",
        "idType": "身份证",
        "idNo": "37172219841024847X",
        "relationship2Insured": "父母",
        "address": "云南省 大理白族自治州 云龙县",
        "zipCode": "100223",
        "phone": "13588888888",
        "email": "test@360bao.com"
    },
    "insured": {
        "fullName": "被保人",
        "idType": "身份证",
        "idNo": "532929200305074400",
        "address": "云南省 大理白族自治州 云龙县",
        "zipCode": "100223",
        "phone": "13588888888",
        "email": "test@360bao.com"
    },
    "beneficiaries": [
        {
            "fullName": "受益人1",
            "idType": "身份证",
            "idNo": "37172219841024847X",
            "relationship2Insured": "父母",
            "allocatedShare": 36,
            "phone": "13588888888",
            "email": "test@360bao.com"
        },
        {
            "fullName": "受益人2",
            "idType": "身份证",
            "idNo": "511028198604304384",
            "relationship2Insured": "父母",
            "allocatedShare": 64,
            "phone": "13588888888",
            "email": "test@360bao.com"
        }
    ],
    "addressee": {
        "fullName": "联系人",
        "phone": "13588888888",
        "zipCode": "123456",
        "detail": "四川省 内江市 隆昌县",
        "email": "test@360bao.com"
    },
    "cardHolder": {
        "fullName": "持卡人",
        "idType": "身份证",
        "idNo": "511028198604304384",
        "phone": "13588888888",
        "bankName": "招商银行",
        "account": "62226287654488"
    },
    "payment": {
        "paymentType": "alipay"
    },
    "extraData": {
        "附加信息1": "hahah"
    }
}
```

```javascript
/* 证件类型
"护照"     
"其它"     
"身份证"    
"军人证"    
"出生证明"	
"异常身份证"
"回乡证"	
"户口簿"	
"警官证"	
*/

/* 支付类型
"wxpay"     
"alipay"     
*/

/*银行类型
"中国银行"
"中国工商银行"
"中国农业银行"
"中国建设银行"
"中国交通银行"
"中国光大银行"
"邮储银行"
"深圳发展银行"
"招商银行"
"宁波银行"
"中国平安银行"
*/
```
