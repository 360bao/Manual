##获取 access token

###请求：
* 测试服地址：http://platform.360bao.com/auth/token?grant_type=client_credentials&client_id=CLIENT_ID&client_secret=CLIENT_SECRET
- grant_type	必须	获取access_token填写client_credentials
- client_id	必须	第三方用户唯一凭证
- client_secret	必须	第三方用户唯一凭证密钥

###返回：
- access_token	获取到的凭证
- expires_in	凭证有效时间，单位：秒
