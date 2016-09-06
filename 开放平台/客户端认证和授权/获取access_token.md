##获取 access token

------------

###说明：
> access token访问令牌包含此次访问api会话的安全信息。该令牌是代理人授权的安全标识，并控制代理人相关操作的能力。

###请求方式：
> GET

###请求地址：
    > http://platform.360bao.com/auth/token

###请求参数：
> 
  * grant_type：必须，获取access_token填写client_credentials
  * client_id：必须，第三方用户唯一凭证
  * client_secret：必须，第三方用户唯一凭证密钥
 
###请求示例：
> http://platform.360bao.com/auth/token?client_id=test&client_secret=为您分配的secret&grant_type=client_credentials

###下行数据：
```
{
    "access_token": "W8B0p5sAQeKFcUwf_BVdQQ",//获取到的凭证
    "expires_in": 7200,//获取到的凭证
    "token_type": "Bearer"//令牌类型
}
```




