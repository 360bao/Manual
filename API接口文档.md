##1.	平台简介
###1.1	使命和目标

360Bao平台是华谊保险销售公司的互联网战略平台。公司通过360Bao平台为保险公司显著增加业绩，为互联网公司提供重要的用户流量和业务数据变现，为公司自身积累海量用户资源和数据，从而为电销和精英代理人平台提供数据基础。360Bao是华谊打造场景化保险生态的核心平台，起到连接其他各方资源的作用。
###1.2	整体架构
![平台整体架构 ](https://github.com/360bao/Manual/blob/master/1.png)
###1.3协议规则
合作伙伴接入360Bao平台，调用JS API遵循以下基本规则：

- 采用POST方法提交
- 提交和返回数据都为JSON
- 统一采用UTF-8字符编码

<table>
   <tr>
      <td>属性</td>
      <td>规则</td>
   </tr>
   <tr>
      <td>使用协议</td>
      <td>HTTP/HTTPS</td>
   </tr>
   <tr>
      <td>数据格式</td>
      <td>XML、JSON</td>
   </tr>
   <tr>
      <td>传参方式</td>
      <td>POST</td>
   </tr>
   <tr>
      <td>POST参数</td>
      <td>原始XML数据、JSON数据</td>
   </tr>
   <tr>
      <td>XML格式</td>
      <td>报文格式统一</td>
   </tr>
   <tr>
      <td>JSON格式</td>
      <td>请求响应格式模板统一</td>
   </tr>
   <tr>
      <td>幂等性</td>
      <td>服务方可以重复接收内容相同的请求，并返回相同的处理结果</td>
   </tr>
</table>

##2.	JS SDK

``` javascript
{
	“API_Category”: “Connect”,
	“Method”:”Register”,
	“Parameter”:[{
		“Parameter1”:”P1”,
		“Parameter2”:”P2”,
		……
	}]
	“Return”:[{
		“Return1”:”R1”,
		“Return2”:”R2”,	
		……
	}]
}
```
###2.1接入API (CATEGORY: CONNECT)
接入API提供合作伙伴接入验证功能，共有三个方法：
- 注册：提供手机号、密码，注册成为合作伙伴，获取专属URL和Error
Register(PhoneNum string, Password string) (URL string, Error error)
- 登录：提供手机号、密码登录，获得SessionID或Error
Login(PhoneNum string, Password string) (SessionId string, Error error)
- 修改密码：提供手机号、旧密码和新密码，获得Error
UpdateLogin(PhoneNum string, OldPassword string,  NewPassword string)  (Error error)

###2.2交易查询API (CATEGORY: QUERY)
交易查询API提供保单、佣金的信息查询，以及提交保单数据异常的申请。
- 查询保单：获取部分或全部保单数据
- 查询佣金：获取佣金明细
- 异常申请：
 
##3.车险接口
###3.1交互模式
<table>
   <tr>
      <td>属性</td>
      <td>规则</td>
   </tr>
   <tr>
      <td>使用协议</td>
      <td>HTTP/HTTPS</td>
   </tr>
   <tr>
      <td>数据格式</td>
      <td>XML</td>
   </tr>
   <tr>
      <td>传参方式</td>
      <td>POST</td>
   </tr>
   <tr>
      <td>POST参数</td>
      <td>原始XML数据</td>
   </tr>
   <tr>
      <td>XML格式</td>
      <td>报文格式统一</td>
   </tr>
   <tr>
      <td>幂等性</td>
      <td>服务方可以重复接收内容相同的请求，并返回相同的处理结果</td>
   </tr>
</table>
###3.1.1业务流程图
![业务流程图](https://github.com/360bao/Manual/blob/master/2.png)

###3.1.2接口列表 
<table>
   <tr>
      <td>接口名称</td>
      <td>交易类型</td>
      <td>是否必要</td>
      <td>发起方</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>初始化颜色</td>
      <td>050</td>
      <td>否</td>
      <td>H5页面专用</td>
      <td>此为使用h5页面接口专用初始化背景 按钮颜色的</td>
   </tr>
   <tr>
      <td>获取发动机和车架号</td>
      <td>095</td>
      <td>是</td>
      <td>第三方</td>
      <td>用户选择机构和输入车牌后立即请求此接口获取需要补录的两号（新车除外）</td>
   </tr>
   <tr>
      <td>基础信息接口</td>
      <td>100</td>
      <td>是</td>
      <td>第三方</td>
      <td>合作公司（第三方）将保险公司要求的数据提交给阳光车险接口平台，接口平台返回用户需要录入信息的表单控件，控件类型请详见《车险接口说明1.0》。</td>
   </tr>
   <tr>
      <td>获取报价</td>
      <td>105</td>
      <td>是</td>
      <td>第三方</td>
      <td>合作公司（第三方）将用户填写的表单数据提交给保险公司，保险公司返回报价信息。</td>
   </tr>
   <tr>
      <td>修改报价</td>
      <td>110</td>
      <td>否</td>
      <td>第三方</td>
      <td>第三方将用户选择投保的险种或套餐，险别信息提交给接口平台，平台返回报价信息UN积分，加投信息。</td>
   </tr>
   <tr>
      <td>保存保费获取投保礼</td>
      <td>115</td>
      <td>否</td>
      <td>第三方</td>
      <td>第三方将用户选择投保的套餐请求接口平台，接口保存计算返回投保礼 加投信息。</td>
   </tr>
   <tr>
      <td>核保请求</td>
      <td>120</td>
      <td>是</td>
      <td>第三方</td>
      <td>第三方将用户信息、第三方订单信息、投保礼、加投等提交给保险公司核保</td>
   </tr>
   <tr>
      <td>支付校验</td>
      <td>125</td>
      <td>是</td>
      <td>第三方</td>
      <td>用户在支付之前，第三方需请求车险接口平台检查用户是否可在网上支付。</td>
   </tr>
   <tr>
      <td>出单请求</td>
      <td>130</td>
      <td>是</td>
      <td>第三方</td>
      <td>用户在对已核投保单进行支付后，第三方将订单信息、支付信息发送给阳光车险接口平台，接口平台进行出单操作，并将出单结果反馈第三方。</td>
   </tr>
   <tr>
      <td>配送信息修改</td>
   </tr>
   <tr>
      <td></td>
      <td>135</td>
      <td>否</td>
      <td>第三方</td>
      <td>用户在核保后和支付前如果要修改配送地址。第三方将数据发送给阳光车间接口平台。</td>
   </tr>
   <tr>
      <td>获取验证码</td>
      <td>126</td>
      <td>否</td>
      <td>第三方</td>
      <td>北京机构，阳光车险平台在核保请求时（120接口）返回用户未获取到验证码信息。第三方可通过此接口向阳光车险平台获取验证码。</td>
   </tr>
   <tr>
      <td>保存验证码</td>
      <td>127</td>
      <td>否</td>
      <td></td>
      <td>北京机构，第三方可调用此接口通知阳光车险平台保存验证码。</td>
   </tr>
</table>

##3.2报文格式
系统和第三方之间数据通过xml进行交互，交互报文的规则如下

示例报文汇总： 

数据文件采用标准的XML格式，字符编码为GBK；报文的根是PackageList，第二层节点由<Package>构成(可以有多个<Package>)，<Package>由报文头（Header）、签名信息（Sign）和报文体（Request淘宝请求、Response响应）三部分组成，如下：

<table>
   <tr>
      <td>报文块</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>声明部分</td>
      <td>以<?xml version="1.0" encoding="GBK"?>为格式声明</td>
   </tr>
   <tr>
      <td>根节点</td>
      <td>以<PackageList>为起始标记，以</PackageList>为结束标记。可以包含多个<Package>节点。</td>
   </tr>
   <tr>
      <td>报文根</td>
      <td>以<Package>为起始标记，以</Package>为结束标记。</td>
   </tr>
   <tr>
      <td>报文头</td>
      <td>以< Header>为起始标记，以</ Header>为结束标记。</td>
   </tr>
   <tr>
      <td>签名信息</td>
      <td>以<Sign>为起始标记，以< /Sign >为结束标记。</td>
   </tr>
   <tr>
      <td>报文体</td>
      <td>以<Request>或<Response>为起始标记，以</Request>或</Response>为结束标记。(第三方请求用<Request>)</td>
   </tr>
</table>

注1：双方的接口需要支持多个<Package>节点的情况。
注2：无论报头还是报体，都会经常扩展新字段，因此第三方公司在实现时务必让其可以自动兼容。新扩展字段都是非必选字段。

###3.2.1报文头

请求报文的报文头是固定的，第三方请求与保险公司请求头信息略有不同，第三方请求报文From为第三方的标识，To为保险公司URL；保险公司返回报文From为保险公司ComId，To为三方的标识。
报文头格式：

<table>
   <tr>
      <td>No.</td>
      <td>字段</td>
      <td>字段名</td>
      <td>类型</td>
      <td>必传</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>1</td>
      <td>Version</td>
      <td>报文版本</td>
      <td>字符</td>
      <td>Y</td>
      <td>报文版本号，本稳定版本号都是2</td>
   </tr>
   <tr>
      <td>2</td>
      <td>RequestType</td>
      <td>交易类型</td>
      <td>枚举</td>
      <td>Y</td>
      <td>见3.3交易类型</td>
   </tr>
   <tr>
      <td>3</td>
      <td>InsureType</td>
      <td>投保类型</td>
      <td>字符</td>
      <td>N</td>
      <td>见附录默认100</td>
   </tr>
   <tr>
      <td>3</td>
      <td>SessionId</td>
      <td>唯一标识</td>
      <td>数字</td>
      <td>Y</td>
      <td>能够唯一标识一次业务会话，在用户整个投保流程中唯一，注意RequestType=100时必须重新生成，返回不可复用</td>
   </tr>
   <tr>
      <td>6</td>
      <td>SendTime</td>
      <td>发送时间</td>
      <td>时间</td>
      <td>Y</td>
      <td>报文发送时间</td>
   </tr>
   <tr>
      <td>7</td>
      <td>Status</td>
      <td>状态</td>
      <td>字符</td>
      <td>Y</td>
      <td>参考数据字典</td>
   </tr>
   <tr>
      <td>100-正常</td>
   </tr>
   <tr>
      <td>200-需要补录</td>
   </tr>
   <tr>
      <td>其他异常（300、400）</td>
   </tr>
   <tr>
      <td>8</td>
      <td>ErrorMessage</td>
      <td>错误信息</td>
      <td>字符</td>
      <td>N</td>
      <td></td>
   </tr>
   <tr>
      <td>9</td>
      <td>SellerId</td>
      <td>第三平台的卖家ID</td>
      <td>字符</td>
      <td>Y</td>
      <td>例如：在淘宝平台上开店，这个是淘宝中对应商店的ID。由第三方生成，并且唯一。</td>
   </tr>
   <tr>
      <td>10</td>
      <td>AgentCode</td>
      <td>服务区域代码</td>
      <td>字符</td>
      <td>  Y</td>
      <td>如：W03210001</td>
   </tr>
</table>

报文头示范

``` xml
<Header>
  <Version>2</Version>
  <RequestType>105</RequestType>
  <InsureType>100</InsureType>
  <SessionId>33763110891482088102118850914</SessionId>
  <AgentCode>W03210001</AgentCode>
  <SendTime>2013-04-24 18:28:42</SendTime>
  <Status></Status>
  <SellerId></SellerId>
  <ErrorMessage></ErrorMessage> 
</Header>

```
###3.2.2报文签名
为了保证数据传输的安全性，我们会对报文体进行加签，收到报文后，必须对报文经行验签，保证报文的没有被伪造

<table>
   <tr>
      <td>No.</td>
      <td>字段</td>
      <td>字段名</td>
      <td>类型</td>
      <td>大小</td>
      <td>必传</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>1</td>
      <td>Sign</td>
      <td>签名内容</td>
      <td>字符</td>
      <td></td>
      <td>Y</td>
      <td>只对报文体加签</td>
   </tr>
</table>

