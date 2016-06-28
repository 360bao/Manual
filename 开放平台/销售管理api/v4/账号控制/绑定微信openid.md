##绑定微信

------------
###说明：
>  代理人绑定微信的接口

###请求方式：
> POST

###请求地址：
> http://platform.360bao.com/api/account/bind/wx

###授权：
> 需要授权，在request的Header中加入"Authorization":"Bearer "+jwt.
  例如：req.Header.Add("Authorization", "Bearer " + jwt)
  jwt通过[登录接口获取](https://github.com/360bao/Manual/blob/master/%E5%BC%80%E6%94%BE%E5%B9%B3%E5%8F%B0/%E9%94%80%E5%94%AE%E7%AE%A1%E7%90%86api/v4/%E8%B4%A6%E5%8F%B7%E6%8E%A7%E5%88%B6/%E7%99%BB%E5%BD%95.md)

###上行数据：
```
无
```
###下行数据：
```
{
    "message":"",
    "result":true
}
```
