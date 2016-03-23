##获取 access token

###请求：
*测试服地址：http://sso.360bao.com/api/token?grant_type=client_credential&appid=APPID&secret=SECRET
- grant_type	必须	获取access_token填写client_credential
- appid	必须	第三方用户唯一凭证
- secret	必须	第三方用户唯一凭证密钥，即appsecret

###返回：
-access_token	获取到的凭证
-expires_in	凭证有效时间，单位：秒
