#1.	平台简介
##1.1	使命和目标

360Bao平台是华谊保险销售公司的互联网战略平台。公司通过360Bao平台为保险公司显著增加业绩，为互联网公司提供重要的用户流量和业务数据变现，为公司自身积累海量用户资源和数据，从而为电销和精英代理人平台提供数据基础。360Bao是华谊打造场景化保险生态的核心平台，起到连接其他各方资源的作用。
##1.2	整体架构
![平台整体架构 ](https://github.com/360bao/Manual/blob/master/1.png)
##1.3协议规则
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

#2.	JS SDK

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
##2.1接入API (CATEGORY: CONNECT)
接入API提供合作伙伴接入验证功能，共有三个方法：
- 注册：提供手机号、密码，注册成为合作伙伴，获取专属URL和Error
Register(PhoneNum string, Password string) (URL string, Error error)
- 登录：提供手机号、密码登录，获得SessionID或Error
Login(PhoneNum string, Password string) (SessionId string, Error error)
- 修改密码：提供手机号、旧密码和新密码，获得Error
UpdateLogin(PhoneNum string, OldPassword string,  NewPassword string)  (Error error)

##2.2交易查询API (CATEGORY: QUERY)
交易查询API提供保单、佣金的信息查询，以及提交保单数据异常的申请。
- 查询保单：获取部分或全部保单数据
- 查询佣金：获取佣金明细
- 异常申请：
 
#3.车险接口
##3.1交互模式
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

####3.2.1报文头

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
      <td>参考数据字典<br>100-正常<br>200-需要补录<br>其他异常（300、400）</td>
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

注：接口平台生成签名，用java非对称加密方式。详情参考附件加密说明。

###3.2.3报文体

报文体是报文的主要数据承载体，报文体很多控件组成，一组控件代表不同的含义。报文体体分请求报文体和返回报文体，请求报文体包含在<Request></Request>里，返回报文包含在<Response></Response>里
请求报文体（Request）：

<table>
   <tr>
      <td>No.</td>
      <td>字段</td>
      <td>含义</td>
      <td>类型</td>
      <td>属性</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>1</td>
      <td>InputsList</td>
      <td>用户录入信息集</td>
      <td>控件</td>
      <td></td>
      <td>InputsList由多个Inputs构成。多个Inputs会根据出现在报文里面的先后顺序展现到页面</td>
   </tr>
   <tr>
      <td>2</td>
      <td>Inputs</td>
      <td>用户录入信息</td>
      <td>控件</td>
      <td>type：自定义模块名</td>
      <td>用户输入的信息，都会以Input方式传给保险公司，Input的name为保险公司指定的值，Input的value为用户填写的值</td>
   </tr>
   <tr>
      <td>3</td>
      <td>Order</td>
      <td>第三方的订单信息</td>
      <td>控件</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>4</td>
      <td>Payment</td>
      <td>第三方支付单信息</td>
      <td>控件</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td></td>
   </tr>
</table>

返回报文体（Response）

<table>
   <tr>
      <td>No.</td>
      <td>字段</td>
      <td>含义</td>
      <td>类型</td>
      <td>属性</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>1</td>
      <td>TagsList</td>
      <td>控件定义信息集合</td>
      <td>控件</td>
      <td></td>
      <td>由多个Tags组成，如果有多个Tags，将会根据报文的信息展示，不同的Tags类型，会分块，与InputsList成对，一个TagsList会变成InputsList</td>
   </tr>
   <tr>
      <td>2</td>
      <td>Tags</td>
      <td>提供给用户录入信息的控件</td>
      <td>控件</td>
      <td>type：自定义模块名</td>
      <td>由多个Tag组成，如果有多个Tag，将会按照报文的顺序展示，一个Tags会变成个Inputs回传给保险公司</td>
   </tr>
   <tr>
      <td>3</td>
      <td>Tag</td>
      <td>控件</td>
      <td>控件</td>
      <td>readonly：是否允许用户修改，取值true或者false</td>
      <td>由多个Definition组成，一个Tag最中会变成一个Input回传给保险公司</td>
   </tr>
   <tr>
      <td>4</td>
      <td>Definition</td>
      <td>控件描述信息</td>
      <td>控件</td>
      <td>type：控件类型<br>key：控件的key<br>lable：显示文字<br>value：默认值<br>data：初始数据<br>dataUrl：初始数据连接<br>checkUrl：数据验证地址<br>premium: 险别保费<br>range ：范围<br>type、key、lable是必选项，对于类似select这样的控件，data或者dataUrl应该是必须的<br>range:输入的值必须在这个知道范围内</td>
   </tr>
   <tr>
      <td>5</td>
      <td>Order</td>
      <td>第三方订单信息</td>
      <td>控件</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>6</td>
      <td>Payment</td>
      <td>第三方支付单信息</td>
      <td>控件</td>
      <td></td>
      <td></td>
   </tr>
</table>

###3.2.4Tag特别说明
1. 套餐tag中，value保存金额时单位为元，Premium单位为分；
2. Disable设置为不可操作后（即设置为1），值不会回传给保险公司；
3. Premium只有套餐tag中使用，单位默认为分；
4. label 元素名称；
5. key 对应元素的数据字典；
6. data 提供给用户选择的数据。
7. dataUrl 初始数据远程数据地址。
8. 一个Tag控件是一个元素。

##3.3接口详细
###3.3.1初始化背景色
     此接口只为第三方使用H5页面接口时，需要配置页面背景色和按钮颜色的。
未使用H5页面接口不需要阅读，跳过。
###3.3.2请求报文
``` xml
<?xml version='1.0' encoding='GBK' standalone='yes'?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>050</RequestType>
			<InsureType>100</InsureType>
			<SessionId>SMG0000000</SessionId>
			<From>MobileCar</From>
			<To>Server</To>
			<AgentCode>W02400654</AgentCode>
			<SendTime>2015-01-21 20:15:24</SendTime>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Request>
			<InputsList></InputsList>
		</Request>
	<Sign>Dw5eRgbkwsIXBNbJk6ttGFlBmv6GmX19iLeGU--ijygwqeQ4G12-BPOJh1HecnrjrxjND2OWGcLPGR2IcOqRx90DAXFtGnntOISCRPa0zWsSaD6m_KuvYBA4l9W6c5WykS34Cajt-7sdRtxB2ifyFFv8zPWGy3K9h0ToDyjmyQU</Sign>
	</Package>
</PackageList>
```
###3.3.3返回报文
``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<version>2</version>
			<RequestType>050</RequestType>
			<InsureType>100</InsureType>
			<SessionId>SMG0000000</SessionId>
			<SellerId>3597746367</SellerId>
			<SendTime>2015-01-21 20:15:24</SendTime>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
	<Sign>DQKjke82VWGZgi7Atf8j6LNIRK1u9PILdWkBS5cY7wbgPDYcx_FKIRn8BUVjnruUdjzPo3W2HVbLPmHjqA-iZBbIjL8JUCVeIuvatKsbcln64d28x6FFWPvl2EklGKECA8C8LZEG65rH49PJDM7TvEGVO81h42uPPEPAb2vKLvk</Sign>
		<Response>
			<TagsList>
				<Tags type="cssArray">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">background</Definition>
						<Definition name="label">css</Definition>
						<Definition name="value">#ff8700</Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">radio</Definition>
						<Definition name="label">css</Definition>
						<Definition name="value">#53c35d</Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
				</Tags>
			</TagsList>
		</Response>
	</Package>
</PackageList>
```
##3.4获取发动机和车架号
用户选择机构和输入车牌后触发此接口，返回是否需要用户补录信息。
 需要录入信息：
<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>可为空</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>cityCode</td>
      <td>城市代码</td>
      <td>String</td>
      <td>否</td>
      <td>城市国标码</td>
   </tr>
   <tr>
      <td>licenseNo</td>
      <td>车牌号</td>
      <td>String</td>
      <td>是</td>
      <td>新车为空</td>
   </tr>
   <tr>
      <td>noLicenseFlag</td>
      <td>新车未上牌</td>
      <td>String</td>
      <td>否</td>
      <td>1：新车，0：非新车</td>
   </tr>
</table>
###3.4.1请求报文
``` xml
<?xml version='1.0' encoding='GBK' standalone='yes'?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>095</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501212131161338</SessionId>
			<From>MobileCar</From>
			<To>Server</To>
			<AgentCode>W00110002</AgentCode>
			<SendTime>2015-01-21 21:31:37</SendTime>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Request>
			<InputsList>
				<Inputs type='vehicleInfo'>
					<input name='licenseNo'>冀A00021</input>
					<input name='cityCode'>07518800</input>
					<input name='noLicenseFlag'>0</input>
				</Inputs>
			</InputsList>
		</Request>
		<Sign>bOSUg6k2XvfetURrXxb7sn7n2mDV8MfbuDWu4bVihL1cFtCkhdG_P2S8EIebaspNU_lmFQ63-SP_wjL6_et_VHpvGIrckT8LIq5WQVbVok9n2hioTlsmNRFC_cZoXR-VQczTN_3t6-JraY-7xB1YSul2sZCPTUwDxz0qzRs-mXk</Sign>
	</Package>
</PackageList>
```
###3.4.2返回报文
通过机构和车牌返回是否需要补录信息：
如果需要补录（status节点为200）返回补录的节点，如果不需要（status节点为100）返回的数据：
``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<version>2</version>
			<RequestType>095</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501212131161338</SessionId>
			<SellerId>3597746367</SellerId>
			<SendTime>2015-01-21 21:31:38</SendTime>
			<Status>200</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Sign>dl-G_33FZ25tmZCQU2WQb9kgBvn7yDCfMsrT_d5H1ehWOnmtTeRsAD6bkIsEP0jhxnsQYpe0H2drAE31EJLjG0-X1VVJNNVbix6Bq1R5-XFpU9xHzwIdpO8AeKuiIBjL9zB6-2UkM6QSByVFAECUSDt14ufJEiGDhvj_2KclXiw</Sign>
		<Response>
			<TagsList>
				<Tags type="vehicleInfo">
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">vehicleFrameNo</Definition>
						<Definition name="label">车架号</Definition>
						<Definition name="value"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">engineNo</Definition>
						<Definition name="label">发动机号</Definition>
						<Definition name="value"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
				</Tags>
			</TagsList>
		</Response>
	</Package>
</PackageList>
```
##3.5基础信息接口
该接口初步设计在根据车牌和身份证查询客户信息后直接调用输入项接口，返回客户需要补充的信息。
<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>是否可为空</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>cityCode</td>
      <td>城市代码</td>
      <td>String</td>
      <td>否</td>
      <td>阳光提供见下说明</td>
   </tr>
   <tr>
      <td>licenseNo</td>
      <td>车牌号</td>
      <td>String</td>
      <td>是</td>
      <td>新车为空</td>
   </tr>
   <tr>
      <td>noLicenseFlag</td>
      <td>新车未上牌</td>
      <td>String</td>
      <td>否</td>
      <td>1：新车，0：非新车</td>
   </tr>
   <tr>
      <td>ownerName</td>
      <td>车主姓名</td>
      <td>String</td>
      <td>否</td>
      <td>姓名</td>
   </tr>
   <tr>
      <td>ownerMobile</td>
      <td>手机号码</td>
      <td>String</td>
      <td>否</td>
      <td>月份，如：13800138000</td>
   </tr>
   <tr>
      <td>agentCode</td>
      <td>服务区域代码</td>
      <td>String</td>
      <td>否</td>
      <td>如：W03210001</td>
   </tr>
   <tr>
      <td>spsource</td>
      <td>广告来源代码</td>
      <td>String</td>
      <td>否</td>
      <td>P05代码</td>
   </tr>
   <tr>
      <td>netcampaignno</td>
      <td>网销营销活动代码 </td>
      <td>String</td>
      <td>否</td>
      <td>H代码</td>
   </tr>
   <tr>
      <td>accountType</td>
      <td>账号类型</td>
      <td>String</td>
      <td>是</td>
      <td>QQ、微信</td>
   </tr>
   <tr>
      <td>accountNo</td>
      <td>账号</td>
      <td>String</td>
      <td>是</td>
      <td></td>
   </tr>
   <tr>
      <td>terminalType</td>
      <td>终端类型</td>
      <td>String</td>
      <td>是</td>
      <td>例如：1：IPAD；</td>
   </tr>

</table>
城市编码请求阳光提供的地址返回josn字符用jsonp解决ajax跨域请求（注：如果是ajax请求，最好使用post方式提交，避免乱码）

根据参数返回对应城市地址

http://chexian.sinosig.com/travelCity!getTravelCityForInterface.action?hotSign=4&limit=0&queryCon=邯郸&contName=大名&encoding=GBK&callback=jsonp1045

hotSign 为查询类型标识 说明一下。机构就是投保地区

hotSign 为0:根据关键字查询机构。queryCon为用户输入的关键字，可是城市拼音缩写、拼音全拼、汉字

hotSign 为1:查询热门城市，查询热门城市queryCon、contName为空或不传即可。

hotSign 为2:查询二级机构（也就是省份）。queryCon、contName为空或不传即可。

hotSign 为3:根据选择的省份或者城市查询三级或四级级机构。queryCon为省份或者城市的机构代码。如：选择北京的下级机构，queryCon为北京的机构代码。contName为空或不传即可。

hotSign 为4:根据城市名称查询机构。queryCon为城市名称（不带市）。如：选择北京的下级机构，queryCon为北京的机构代码。contName为县或区名称（不带县或区）

 limit分页输入0即可
 
 返回示例：
 ``` javascript
 jsonp1045(
 
[
    {
        "id": "01562800", 
        "ContName": "北京 通州", 
        "rank": "3", 
        "spelling": "tongzhou", 
        "spellingAcronym": "tz", 
        "cityPlate": "京", 
        "proPlate": "京"
    }, 
    {
        "id": "03546710", 
        "ContName": "南通市 通州", 
        "rank": "4", 
        "spelling": "tongzhou", 
        "spellingAcronym": "tz", 
        "cityPlate": "苏F", 
        "proPlate": "苏F"
    }, 
    {
        "id": "06526202", 
        "ContName": "南阳市 桐柏县", 
        "rank": "4", 
        "spelling": "tongbaixian", 
        "spellingAcronym": "tbx", 
        "cityPlate": "豫R", 
        "proPlate": "豫R"
    }, 
    {
        "id": "06665104", 
        "ContName": "开封市 通许县", 
        "rank": "4", 
        "spelling": "tongxuxian", 
        "spellingAcronym": "txx", 
        "cityPlate": "豫B", 
        "proPlate": "豫B"
    }, 
    {
        "id": "19501702", 
        "ContName": "杭州市 桐庐市", 
        "rank": "4", 
        "spelling": "tonglushi", 
        "spellingAcronym": "tls", 
        "cityPlate": "浙A", 
        "proPlate": "浙A"
    }, 
    {
        "id": "19533020", 
        "ContName": "嘉兴市 桐乡县", 
        "rank": "4", 
        "spelling": "tongxiangxian", 
        "spellingAcronym": "txx", 
        "cityPlate": "浙F", 
        "proPlate": "浙F"
    }, 
    {
        "id": "25573000", 
        "ContName": "铜川市", 
        "rank": "3", 
        "spelling": "TongChuanShi", 
        "spellingAcronym": "tcs", 
        "cityPlate": "陕B", 
        "proPlate": "陕B"
    }, 
    {
        "id": "27511400", 
        "ContName": "通化市", 
        "rank": "3", 
        "spelling": "TongHuaShi", 
        "spellingAcronym": "ths", 
        "cityPlate": "吉E", 
        "proPlate": "吉E"
    }, 
    {
        "id": "33581002", 
        "ContName": "安庆市 桐城市", 
        "rank": "4", 
        "spelling": "tongcheng", 
        "spellingAcronym": "tc", 
        "cityPlate": "皖H", 
        "proPlate": "皖H"
    }, 
    {
        "id": "36582200", 
        "ContName": "通辽市", 
        "rank": "3", 
        "spelling": "TongLiaoShi", 
        "spellingAcronym": "tls", 
        "cityPlate": "蒙G", 
        "proPlate": "蒙G"
    }, 
    {
        "id": "37520600", 
        "ContName": "厦门 同安区", 
        "rank": "3", 
        "spelling": "tonganqu", 
        "spellingAcronym": "taq", 
        "cityPlate": "闽D", 
        "proPlate": "闽D"
    }
]

)
 ```
Id:城市code 对应请求报文cityCode  

ContName：城市名称

rank：机构等级（从2开始）

Spelling：城市拼音全拼

spellingAcronym：城市拼音缩写

cityPlate:城市车牌号前缀
###3.5.1请求报文
``` xml
<?xml version='1.0' encoding='GBK' standalone='yes'?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>100</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501212139114572</SessionId>
			<From>MobileCar</From>
			<To>Server</To>
			<AgentCode>W02400654</AgentCode>
			<SendTime>2015-01-21 21:40:13</SendTime>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Request>
			<InputsList>
				<Inputs type='vehicleInfo'>
					<input name='ownerName'>儿童</input>
					<input name='ownerMobile'>18511565612</input>
					<input name='terminalType'>1</input>
					<input name='cityCode'>08512200</input>
					<input name='eSalesNo'></input>
					<input name='accountNo'>PZ101913</input>
					<input name='bizModel'></input>
					<input name='agentCode'>W02400654</input>
					<input name='licenseNo'></input>
					<input name='netcampaignno'>Net</input>
					<input name='accountType'>2</input>
					<input name='noLicenseFlag'>1</input>
					<input name='ownerEmail'>5675677576@qq.com</input>
					<input name='spsource'>P05-ADWBPZYL-M-xs165</input>
				</Inputs>
			</InputsList>
		</Request>
		<Sign>WG65RuD0IS0EtzlIXRBLfjE3LKWtNrITseGxwZSmv9leaASCXB1uhXOVCySCApG0cgSyewuwTSJqPHTVgJ8swgL_fEqVDP4Y-i-_HUOdQIxzs2Is09X8nOyOdVOl6nYqZsp6t7Ij4Vj00qH8O4-7gHUmyqRfUJJA5FJQ1akia4s</Sign>
	</Package>
</PackageList>
```
###3.5.2返回报文
1.通过车牌和身份证信息查询客户，根据查询结果情况返回：
如果可直接报价则报价套餐和车辆、车主信息返回（status节点为100），否则新保返回需要采集信息的节点（status节点为200），第三方根据返回报文向用户展示采集项。
新保返回的数据：
<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>是否为空</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>ownerIdNo</td>
      <td>身份证</td>
      <td>text</td>
      <td>否</td>
      <td>完整身份证号</td>
   </tr>
   <tr>
      <td>ownerName</td>
      <td>车主姓名</td>
      <td>text</td>
      <td>否</td>
      <td>车主姓名</td>
   </tr>
   <tr>
      <td>vehicleId</td>
      <td>车辆Id</td>
      <td>hidden</td>
      <td>否</td>
      <td>客户车型Id</td>
   </tr>
   <tr>
      <td>vehicleModelName</td>
      <td>品牌型号</td>
      <td>text</td>
      <td>否</td>
      <td>车辆品牌：车型选择接口。</td>
   </tr>
   <tr>
      <td>vehicleFrameNo</td>
      <td>车架号</td>
      <td>text</td>
      <td>否</td>
      <td>小于17位以行驶证为准</td>
   </tr>
   <tr>
      <td>engineNo</td>
      <td>发动机号</td>
      <td>text</td>
      <td>否</td>
      <td>小于20位以行驶证为准</td>
   </tr>
   <tr>
      <td>registerDate</td>
      <td>注册日期</td>
      <td>cascade</td>
      <td>否</td>
      <td>级联显示</td>
   </tr>
   <tr>
      <td>specialCarFlag</td>
      <td>是否过户车</td>
      <td>radio</td>
      <td>否</td>
      <td>是：1；否：0</td>
   </tr>
   <tr>
      <td>specialCarDate</td>
      <td>过户日期</td>
      <td>Date</td>
      <td>是</td>
      <td>例如：2013-02-01</td>
   </tr>
   <tr>
      <td>vehicleInvoiceNo</td>
      <td>新车购置发票号</td>
      <td>text</td>
      <td>否</td>
      <td>北京新车时采集</td>
   </tr>
   <tr>
      <td>vehicleInvoiceDate</td>
      <td>发票开具日期</td>
      <td>Date</td>
      <td>否</td>
      <td>北京新车时采集</td>
   </tr>
   <tr>
      <td>isOcr</td>
      <td>是否使用OCR</td>
      <td>hidden</td>
      <td>否</td>
      <td>是否使用OCR采集信息 0不使用 1使用</td>
   </tr>
</table>

新车或需要补充信息列表请参考附录表1.
```xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<version>2</version>
			<RequestType>100</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501212139114572</SessionId>
			<SellerId>3597746367</SellerId>
			<SendTime>2015-01-21 21:40:14</SendTime>
			<Status>200</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Sign>KpdzqOvh6jveNMtq2Sv2fowKoq5t6iB-wNOCbxZWF4ki4WjX-cCIaeP73ZMI6ovOyuny12SaW6fQ7pmdyRiZX7B56c4vcwNf4i2QhU2u9KUv26fEIN5Kd6oo7d6dZ_kzjy3JaFr7ot8kCryPosk62kX5JXGgaZxOIqlJbL8X5pI</Sign>
		<Response>
			<TagsList>
				<Tags type="vehicleInfo">
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">isOcr</Definition>
						<Definition name="label">是否使用OCR
                        </Definition>
						<Definition name="value">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">vehicleFrameNo</Definition>
						<Definition name="label">车架号</Definition>
						<Definition name="value"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">vehicleModelName</Definition>
						<Definition name="label">品牌型号</Definition>
						<Definition name="value"></Definition>
						<Definition name="dataUrl"><![CDATA[http://1.202.156.227:7002/Partner/netVehicleModel.action]]></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">vehicleId</Definition>
						<Definition name="label">车辆代码</Definition>
						<Definition name="value"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">engineNo</Definition>
						<Definition name="label">发动机号</Definition>
						<Definition name="value"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">seats</Definition>
						<Definition name="label">座位数</Definition>
						<Definition name="value">5</Definition>
						<Definition name="data"><![CDATA[2:2;3:3;4:4;5:5;6:6;7:7;8:8;9:9;10:10;11:11]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">date</Definition>
						<Definition name="key">firstRegisterDate</Definition>
						<Definition name="label">注册登记日期
                        </Definition>
						<Definition name="value"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">radio</Definition>
						<Definition name="key">specialCarFlag</Definition>
						<Definition name="label">是否过户车：
                         </Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[是:1;否:0]]>
                        </Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">date</Definition>
						<Definition name="label">过户日期</Definition>
						<Definition name="key">specialCarDate</Definition>
						<Definition name="value"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">ownerName</Definition>
						<Definition name="label">车主</Definition>
						<Definition name="value">儿童</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">ownerIdNo</Definition>
						<Definition name="label">身份证号码</Definition>
						<Definition name="value"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
				</Tags>
			</TagsList>
		</Response>
	</Package>
</PackageList>
```
报文注释：
>
Tags表示一类型的输入项，把输入信息分类，方便准确填写信息，目前输入项分为车辆信息、车主信息、被保险人信息、配送信息和其他信息，其他信息主要指没有归类的输入项，比如车船税补充信息等。

Tag标签是具体的输入项，每个需要填写的信息要一个tag标签。

Definition是输入项属性的配置信息，有六种类型标示输入项的属性。

type:标示输入项类型，有text，select，checkbox，radio，label,hidden或第三方定义的标签，其中label标示该标签为显示标签，只展示给用户看就可以了，不需要客户输入，但是不允许客户修改。

key：指标签的名称，根据这个字段取value。

lable：输入项的标题，

disable: 1客户无法选择或输入，

value: 输入项的默认值，如果没有默认值该项为空。

premium: 保费,显示商业险责任的保费

check: 字段的校验规则，主要使用在text输入框

dataUrl：输入项中输入的值需要到服务器上查询具体的信息，目前主要使用的地方是车型查询，客户输入车辆品牌，根据输入信息到车型库中查询车辆明细。

checkUrl:输入项的验证功能，在输入项有复杂的验证时，没有办法在第三方那边配置，可以通过该值，客户输入完后焦点离开时会请求该地址，验证输入项是否合法，返回的是json格式数据，如果成功返回true，如果验证失败返回false和错误提示信息。


定义套餐：全面套餐，热门套餐和自由组合套餐。
保险公司可以根据自己定义的套餐返回，自由组合套餐是必返回，保险全部的责任和输入项，如果责任之间有关系在返回的套餐中定义。
如果报价异常或者需要中断流程，或者等待状态，返回相对应的报文，返回报文中Stauts节点设置为相对的值（300：拒保、400：中断流程），展示信息提示（ErrorMessages节点数据）。
     

```xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Package>
    <Header>
      <version>2</version>
      <RequestType>100</RequestType>
      <InsureType>100</InsureType>
      <SessionId>33763110891482088102118850914</SessionId>
      <From>2051078519</From>
      <To>taobao</To>
      <SendTime>2013-04-24 18:28:42</SendTime>
      <Status>400</Status>
      <ErrorMessages>亲！您投保不成功，稍后坐席会与您联系！</ErrorMessages>
    </Header>    
<Response>
</Response>
<Sign>ddfhsdgdghdfgdhdsgdgdfdfgdfgfdfgdgdf</Sign>
  </Package>
</PackageList>
```
##3.6车型选择接口
获取表单接口返回数据不是续保报价数据，需要采集车辆、车主信息。品牌型号是通过接口方式和车险接口平台交互获取，以供用户选择车型。
###3.6.1请求数据
采用ajax异步方式交互，用jsonp解决ajax跨域请求。

生产地址：http://chexian.sinosig.com/Partner/netVehicleModel.action?page=1&pageSize=6&searchCode=bh7&searchType=0&encoding=GBK&isSeats=1&callback=jsonp1045

测试地址：
http://1.202.156.227:7002/Partner/netVehicleModel.action?page=1&pageSize=6&searchCode=bh7&searchType=0&encoding=GBK&isSeats=1&callback=jsonp1045

为了避免一次交互，数据量过大，车型选择采用分页方式。

page和pageSize是页面数据和每页显示条数。

searchCode是用户输入的关键字或者vin码。

searchType 标识用户的查询类型。0：关键字查询；1：vin码查询（车架号）。

isSeats 是否查询座位数 1：查询。其他可不传此参数
###3.6.2返回数据
例如：
jsonp1045(
``` json
{"rows":[{"key":"XDABBD0017","value":"北京现代 1.4L 北京现代雅绅特 自动档 尊贵型 参考价：98800","seats":5},{"key":"XDAAMD0045","value":"北京现代 1.6L 北京现代伊兰特 自动档 2007款 舒适型 参考价：98800","seats":5},{"key":"XDAAMD0068","value":"北京现代 1.6L 北京现代伊兰特 自动档 2008款 舒适型 参考价：107200","seats":5},{"key":"XDABBD0008","value":"北京现代 1.6L 北京现代雅绅特 自动档 豪华型 参考价：108300","seats":5},{"key":"XDAAMD0017","value":"北京现代 1.6L 北京现代伊兰特 自动档 豪华型 参考价：142000","seats":5},{"key":"XDABFD0011","value":"北京现代 1.4L 北京现代瑞纳 自动档 2011款 豪华型 参考价：108400","seats":5}],"counter":225}
```

