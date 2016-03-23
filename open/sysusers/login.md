## 用户登录

### 请求：
* POST 测试服地址：http://sso.360bao.com/api/sysusers/login
- phone	必须	手机号
- password	必须	密码（需要md5加密）
- access_token 必须

### 返回：

如果成功返回用户信息JSON

如果失败返回错误说明

- errcode	错误码
- errmsg	错误说明
