## 用户注册

### 请求：
* POST 测试服地址：http://sso.360bao.com/api/sysusers/modify
```javascript
{
  "access_token": "ACCESS_TOKEN",
  "user":{
      "phone":"12111",
      "full_name":"12111",
      "sex":1, //0:female, 1:male, 2:other
      "birthday":1444333, //epoch time
      "idcard":"511000...",
      "address":"北京...",
      "avatar":"http://xxx",
      "employee_number":"123",
      "extra": {
          "项目名称":"",
          "分公司":"",
          "销售机构":"",
          "区部"":"",
          "组别":""
          //"...":"..."
      }
  }
}
```

### 返回：
