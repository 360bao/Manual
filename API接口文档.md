#1.	平台简介
##1.1	使命和目标

360Bao平台是华谊保险销售公司的互联网战略平台。公司通过360Bao平台为保险公司显著增加业绩，为互联网公司提供重要的用户流量和业务数据变现，为公司自身积累海量用户资源和数据，从而为电销和精英代理人平台提供数据基础。360Bao是华谊打造场景化保险生态的核心平台，起到连接其他各方资源的作用。
##1.2	整体架构
<img src="https://github.com/360bao/Manual/blob/master/1.png>
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
<img src="https://github.com/360bao/Manual/blob/master/2.png">

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
```      xml
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
 ```json
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
``` xml
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
     

``` xml
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
{
    "rows": [
        {
            "key": "XDABBD0017", 
            "value": "北京现代 1.4L 北京现代雅绅特 自动档 尊贵型 参考价：98800", 
            "seats": 5
        }, 
        {
            "key": "XDAAMD0045", 
            "value": "北京现代 1.6L 北京现代伊兰特 自动档 2007款 舒适型 参考价：98800", 
            "seats": 5
        }, 
        {
            "key": "XDAAMD0068", 
            "value": "北京现代 1.6L 北京现代伊兰特 自动档 2008款 舒适型 参考价：107200", 
            "seats": 5
        }, 
        {
            "key": "XDABBD0008", 
            "value": "北京现代 1.6L 北京现代雅绅特 自动档 豪华型 参考价：108300", 
            "seats": 5
        }, 
        {
            "key": "XDAAMD0017", 
            "value": "北京现代 1.6L 北京现代伊兰特 自动档 豪华型 参考价：142000", 
            "seats": 5
        }, 
        {
            "key": "XDABFD0011", 
            "value": "北京现代 1.4L 北京现代瑞纳 自动档 2011款 豪华型 参考价：108400", 
            "seats": 5
        }
    ], 
    "counter": 225
}
```
)
>
数据说明：

rows:当前页查询出的车辆信息数据；

Key：每个车辆信息对应的车型Id；

Value:每个车辆信息对应的车型说明；

Seats:每个车对应的座位数。

counter:车辆信息总量；

##3.7获取报价接口
保费计算中输入项的值参考附录1中的参数定义。
在保费计算过程中如果保险公司发现计算失败需要重新补充信息，直接返回需要补充信息tag标签，淘宝会根据标签展示信息给客户进行数据补录。
###3.7.1请求报文
<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>是否可为空</td>
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
      <td>车型Id</td>
      <td>hidden</td>
      <td>否</td>
      <td>客户车型Id</td>
   </tr>
   <tr>
      <td>vehicleFrameNo</td>
      <td>车架号</td>
      <td>text</td>
      <td>否</td>
      <td>小等于17位以行驶证为准</td>
   </tr>
   <tr>
      <td>seats</td>
      <td>车座数</td>
      <td>select</td>
      <td>是</td>
      <td>1-11。有显示项为必填</td>
   </tr>
   <tr>
      <td>engineNo</td>
      <td>发动机号</td>
      <td>text</td>
      <td>否</td>
      <td>小于20位以行驶证为准</td>
   </tr>
   <tr>
      <td>firstRegisterDate</td>
      <td>注册日期</td>
      <td>cascade</td>
      <td>否</td>
      <td>日期格式yyyy-MM-dd。小于等于当前日期。（如果是新车，选择的时间范围为一年以内。）</td>
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
      <td>packageType</td>
      <td>报价套餐类型</td>
      <td>text</td>
      <td>是</td>
      <td>报价页面显示报价套餐</td>
   </tr>
</table>

``` xml
<?xml version='1.0' encoding='GBK' standalone='yes'?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>105</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<From>MobileCar</From>
			<To>Server</To>
			<AgentCode>W02400654</AgentCode>
			<SendTime>2015-01-29 20:53:45</SendTime>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Request>
			<InputsList>
				<Inputs type='vehicleInfo'>
					<input name='engineNo'>567756747657567</input>
					<input name='ownerName'>日日通</input>
					<input name='packageType'>luxury</input>
					<input name='vehicleFrameNo'>45654568675685684</input>
					<input name='vehicleId'>XDAAMD0068</input>
					<input name='firstRegisterDate'>2015-01-29</input>
					<input name='vehicleModelName'></input>
					<input name='seats'>5</input>
					<input name='ownerIdNo'>130429198601173637</input>
					<input name='specialCarFlag'>0</input>
				</Inputs>
			</InputsList>
		</Request>
		<Sign>ZEEgD2tbi1mBoJMmnDw4DDc7gvpMjpqybs5pmQk_h28t3iYbhznokmKwCekubHU5WJJKRkT4i1e8ZCQT-9F3sCNnLcgzxnhJvPoJY1blTzPi7ZayoNNWtS76gYJ8UTQHWUZRcE_1eLWskLwOz7tAIQ6YAIPVG1W6xZYZVxRUSTE</Sign>
	</Package>
</PackageList>

```
其中packageType代表用户上一步前选择的套餐列表，续保数据时候此值无效。

###3.7.2返回报文(费改前)
如果请求报文中存在节点数据不正确，则获取报价接口（105）返回采集此节点数据的报文，返回报文中Status节点设置为200，返回报文如获取报价表单返回报文。
例如，请求报文中ownerIdNo和registerDate节点的数据不正确或者无，车险则会返回让用户补录这两个节点信息。其他节点如是。节点数据参考获取报价表单接口（100）

算价正确并返回相对应的套餐。
<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>备注</td>
   </tr>
   <tr>
      <td></td>
      <td></td>
      <td>全保、续保</td>
      <td>全保</td>
      <td></td>
   </tr>
   <tr>
      <td>cov_200</td>
      <td>车辆损失险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;足额投保:XXX</td>
   </tr>
   <tr>
      <td>cov_600</td>
      <td>商业第三者责任险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;5万:50000.00;…</td>
   </tr>
   <tr>
      <td>cov_500</td>
      <td>全车盗抢险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;投保:XXX</td>
   </tr>
   <tr>
      <td>cov_701</td>
      <td>司机座位责任险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_702</td>
      <td>乘客座位责任险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_321</td>
      <td>指定专修厂</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_310</td>
      <td>自燃损失险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;投保:XXX</td>
   </tr>
   <tr>
      <td>cov_231</td>
      <td>玻璃单独破碎险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;国产玻璃:1;进口玻璃:2</td>
   </tr>
   <tr>
      <td>cov_210</td>
      <td>车身划痕损险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;2千:2000.00</td>
   </tr>
   <tr>
      <td>cov_390</td>
      <td>高速高价救援险</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0;投保:1(费改后已删除)</td>
   </tr>
   <tr>
      <td>cov_291</td>
      <td>发动机特别损失险</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_640</td>
      <td>交通事故精神损害赔偿责任险</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_921</td>
      <td>不计免赔险（机动车盗抢险）</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_922</td>
      <td>不计免赔险（车身划痕损失险）</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_911</td>
      <td>不计免赔险(车损险)</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_912</td>
      <td>不计免赔险(三者险)</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_928</td>
      <td>不计免赔险(司机险)</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_929</td>
      <td>不计免赔险(乘客险)</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>forceFlag</td>
      <td>交强险</td>
      <td>radio</td>
      <td>radio</td>
      <td>投保:1;不投保:0</td>
   </tr>
   <tr>
      <td>forcePremium</td>
      <td>交强险</td>
      <td>label</td>
      <td>label</td>
      <td>交强险保费</td>
   </tr>
   <tr>
      <td>vehicleTaxPremium</td>
      <td>车船税</td>
      <td>label</td>
      <td>label</td>
      <td>车船税保费</td>
   </tr>
   <tr>
      <td>forceTotalPremium</td>
      <td>交强险总保费</td>
      <td>label</td>
      <td>label</td>
      <td>交强险总保费</td>
   </tr>
   <tr>
      <td>bizTotalPremium</td>
      <td>商业保费</td>
      <td>label</td>
      <td>label</td>
      <td>商业保费</td>
   </tr>
   <tr>
      <td>standardPremium</td>
      <td>市场价(应缴总保费)</td>
      <td>label</td>
      <td>label</td>
      <td>应缴总保费</td>
   </tr>
   <tr>
      <td>totalPremium</td>
      <td>网购价(实际保费)</td>
      <td>label</td>
      <td>label</td>
      <td>实际保费</td>
   </tr>
   <tr>
      <td>bizBeginDate</td>
      <td>商业险保险起期</td>
      <td>Date</td>
      <td>Date</td>
      <td>商业险保险起期</td>
   </tr>
   <tr>
      <td>forceBeginDate</td>
      <td>交强险保险起期</td>
      <td>Date</td>
      <td>Date</td>
      <td>交强险保险起期</td>
   </tr>
   <tr>
      <td>lastClaimText</td>
      <td>上年出险信息</td>
      <td>label</td>
      <td>label</td>
      <td>展示上年用户出险的信息</td>
   </tr>
   <tr>
      <td>presentVal</td>
      <td>积分值</td>
      <td>label</td>
      <td>label</td>
      <td>投保礼可用费用或者UN积分</td>
   </tr>
   <tr>
      <td>hasAddPresent</td>
      <td>是否有加投</td>
      <td>label</td>
      <td>label</td>
      <td>是否有加投信息</td>
   </tr>
   <tr>
      <td>presentType</td>
      <td>投保礼或UN积分标识</td>
      <td>label</td>
      <td>label</td>
      <td>投保礼或UN积分标识</td>
   </tr>
   <tr>
      <td>isRunAreaFlag</td>
      <td>是否可以使用指省</td>
      <td>label</td>
      <td>label</td>
      <td>是否可以使用指省0:否；1：是</td>
   </tr>
   <tr>
      <td>runArea</td>
      <td>行驶区域</td>
      <td>radio</td>
      <td>radio</td>
      <td>行驶区域04：全国；03指省</td>
   </tr>
   <tr>
      <td>isDriverFlag</td>
      <td>是否可以使用指驾</td>
      <td>label</td>
      <td>label</td>
      <td>是否可以使用指驾 0:否；1：是</td>
   </tr>
   <tr>
      <td>agreedDriver</td>
      <td>是否指定驾驶员</td>
      <td>radio</td>
      <td>radio</td>
      <td>是否指定驾驶员 0：否；1：是</td>
   </tr>
   <tr>
      <td>driverName</td>
      <td>驾驶员姓名</td>
      <td>text</td>
      <td>text</td>
      <td>驾驶员姓名</td>
   </tr>
   <tr>
      <td>driverNum</td>
      <td>驾驶证号</td>
      <td>text</td>
      <td>text</td>
      <td>驾驶证号</td>
   </tr>
   <tr>
      <td>drivateDate</td>
      <td>驾驶证领证日期</td>
      <td>date</td>
      <td>date</td>
      <td>驾驶证领证日期</td>
   </tr>
   <tr>
      <td>isImmevalid</td>
      <td>是否及时生效</td>
      <td>label</td>
      <td>label</td>
      <td>是否及时生效</td>
   </tr>
   <tr>
      <td>immeValidHoursStart</td>
      <td>生效时间(小时)</td>
      <td>select</td>
      <td>select</td>
      <td>生效时间(小时)</td>
   </tr>
</table>

``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<version>2</version>
			<RequestType>105</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<SellerId>3597746367</SellerId>
			<SendTime>2015-01-29 20:54:02</SendTime>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Sign>ZVj5_nu9dTX040TsihOxc9HT1KqAOFrpg2h7-yu8ip0E5rgaAltZNKUrDqtWr1KxSaECaMITo6XacH-cv7BxC1B7hBvsoj2adap_r0BgQY1xDUPsa96jxztjLVulSlhx_2l8R8cI9RgwjhhVjQpxqCAFaUTMSqF500FA-owQjbE</Sign>
		<Response>
			<packageType>luxury</packageType>
			<TagsList>
				<Tags type="vehicleInfo">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">cityCode</Definition>
						<Definition name="label">城市代码</Definition>
						<Definition name="value">08512200</Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">licenseNo</Definition>
						<Definition name="label">车牌号</Definition>
						<Definition name="value">粤A00005</Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">noLicenseFlag</Definition>
						<Definition name="label">新车未上牌</Definition>
						<Definition name="value">0</Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleModelName</Definition>
						<Definition name="label">品牌型号</Definition>
						<Definition name="value">北京现代BH7164AY轿车</Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleId</Definition>
						<Definition name="label">车辆代码</Definition>
						<Definition name="value">XDAAMD0068</Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">firstRegisterDate</Definition>
						<Definition name="label">注册登记日期</Definition>
						<Definition name="value">2015-01-29</Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">engineNo</Definition>
						<Definition name="label">发动机号</Definition>
						<Definition name="value">567756747657567</Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleFrameNo</Definition>
						<Definition name="label">车架号</Definition>
						<Definition name="value">45654568675685684</Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
				</Tags>
				<Tags type="ownerInfo">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">ownerName</Definition>
						<Definition name="label">车主</Definition>
						<Definition name="value">日日通</Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">ownerIdNo</Definition>
						<Definition name="label">身份证</Definition>
						<Definition name="value">130429198601173637</Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
				</Tags>
				<Tags type="luxury">
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_200</Definition>
						<Definition name="label">车辆损失险</Definition>
						<Definition name="value">98800.00</Definition>
						<Definition name="range">98800.00,107200</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;足额投保:98800.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">145736</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_600</Definition>
						<Definition name="label">商业第三者责任险</Definition>
						<Definition name="value">300000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;5万:50000.00;10万:100000.00;15万:150000.00;20万:200000.00;30万:300000.00;50万:500000.00;100万:1000000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">104033</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_701</Definition>
						<Definition name="label">司机座位责任险</Definition>
						<Definition name="value">10000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;1万/座:10000.00;2万/座:20000.00;3万/座:30000.00;4万/座:40000.00;5万/座:50000.00;10万/座:100000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">3392</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_702</Definition>
						<Definition name="label">乘客座位责任险</Definition>
						<Definition name="value">10000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;1万/座:10000.00;2万/座:20000.00;3万/座:30000.00;4万/座:40000.00;5万/座:50000.00;10万/座:100000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">8722</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_500</Definition>
						<Definition name="label">全车盗抢险</Definition>
						<Definition name="value">98800.00</Definition>
						<Definition name="range">0,98800.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;投保:98800.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">48786</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_231</Definition>
						<Definition name="label">玻璃单独破碎险</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;国产玻璃:1;进口玻璃:2]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">15957</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_310</Definition>
						<Definition name="label">自燃损失险</Definition>
						<Definition name="value">0.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;投保:98800.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_210</Definition>
						<Definition name="label">车身划痕损险</Definition>
						<Definition name="value">0.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;2000:2000.00;5000:5000.00;10000:10000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_321</Definition>
						<Definition name="label">指定专修厂</Definition>
						<Definition name="value">0.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;投保:10.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(车辆损失险)</Definition>
						<Definition name="key">cov_911</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">21860</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(商业第三者责任险)</Definition>
						<Definition name="key">cov_912</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">15605</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(司机座位责任险)</Definition>
						<Definition name="key">cov_928</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">509</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(乘客座位责任险)</Definition>
						<Definition name="key">cov_929</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">1308</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(全车盗抢险)</Definition>
						<Definition name="key">cov_921</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(划痕险)</Definition>
						<Definition name="key">cov_922</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[不可投保:0]]></Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_291</Definition>
						<Definition name="label">发动机特别损失险</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[不可投保:0]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_390</Definition>
						<Definition name="label">高速高价救援险</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_640</Definition>
						<Definition name="label">交通事故精神损害赔偿责任险</Definition>
						<Definition name="value">0.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;1万:10000.00;2万:20000.00;5万:50000.00;10万:100000.00;15万:150000.00;20万:200000.00;30万:300000.00;50万:500000.00;100万:1000000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">lastClaimText</Definition>
						<Definition name="label">上年出险信息</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">radio</Definition>
						<Definition name="label">交强险</Definition>
						<Definition name="key">forceFlag</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[投保:1;不投保:0]]></Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">bizTotalPremium</Definition>
						<Definition name="label">商业总保费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">365909</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">standardPremium</Definition>
						<Definition name="label">市场价</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">548102</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">totalPremium</Definition>
						<Definition name="label">网购价</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">460909</Definition>
					</Tag>
				</Tags>
				<Tags type="deadline">
					<Tag>
						<Definition name="type">date</Definition>
						<Definition name="label">商业险起保日期</Definition>
						<Definition name="key">bizBeginDate</Definition>
						<Definition name="value">2015-01-30</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">date</Definition>
						<Definition name="label">交强险起保日期</Definition>
						<Definition name="key">forceBeginDate</Definition>
						<Definition name="value">2015-01-30</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
				</Tags>
				<Tags type="force">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">forcePremium</Definition>
						<Definition name="label">交强险</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">95000</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleTaxPremium</Definition>
						<Definition name="label">车船税</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">forceTotalPremium</Definition>
						<Definition name="label">交强险总保费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">95000</Definition>
					</Tag>
				</Tags>
				<Tags type="lifeTableCpm">
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">presentType</Definition>
						<Definition name="label">投保礼或UN积分标识</Definition>
						<Definition name="value">1</Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">presentVal</Definition>
						<Definition name="label">投保礼或UN积分值</Definition>
						<Definition name="value">900.0</Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">hasAddPresent</Definition>
						<Definition name="label">是否有加投</Definition>
						<Definition name="value">0</Definition>
						<Definition name="premium"></Definition>
					</Tag>
				</Tags>
				<Tags type="runAreaType">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">isRunAreaFlag</Definition>
						<Definition name="label">是否可以使用指省</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">runArea</Definition>
						<Definition name="label">行驶区域</Definition>
						<Definition name="value">04</Definition>
						<Definition name="data"><![CDATA[全国:04;省内:03]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
				</Tags>
				<Tags type="driverInfoFlag">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">isDriverFlag</Definition>
						<Definition name="label">是否可以使用指架</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">radio</Definition>
						<Definition name="key">agreedDriver</Definition>
						<Definition name="label">是否指定驾驶员</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[是:1;否:0]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
				</Tags>
				<Tags type="driverInfo">
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">driverName</Definition>
						<Definition name="label">姓名</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">driverNum</Definition>
						<Definition name="label">驾驶证号</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">cdate</Definition>
						<Definition name="key">drivateDate</Definition>
						<Definition name="label">初次领证日期</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
				</Tags>
				<Tags type="immevalid">
					<Tag>
						<Definition name="type">radio</Definition>
						<Definition name="key">isImmevalid</Definition>
						<Definition name="label">是否及时生效</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[是:1;否:0]]></Definition>
						<Definition name="dataUrl"><![CDATA[]]>
						</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">生效时间(小时)</Definition>
						<Definition name="key">immeValidHoursStart</Definition>
						<Definition name="value">21</Definition>
						<Definition name="data"><![CDATA[21:21;22:22;23:23;24:24]]></Definition>
					</Tag>
				</Tags>
			</TagsList>
		</Response>
	</Package>
</PackageList>
```
###3.7.3返回报文(费改后)
<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>备注</td>
   </tr>
   <tr>
      <td></td>
      <td></td>
      <td>全保、续保</td>
      <td>全保</td>
      <td></td>
   </tr>
   <tr>
      <td>cov_200</td>
      <td>机动车损失保险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;足额投保:XXX</td>
   </tr>
   <tr>
      <td>cov_600</td>
      <td>商业第三者责任险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;5万:50000.00;…</td>
   </tr>
   <tr>
      <td>cov_500</td>
      <td>全车盗抢保险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;投保:XXX</td>
   </tr>
   <tr>
      <td>cov_701</td>
      <td>车上人员责任保险(驾驶员)</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_702</td>
      <td>车上人员责任保险(乘客)</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_321</td>
      <td>指定修理厂险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_310</td>
      <td>自燃损失险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;投保:XXX</td>
   </tr>
   <tr>
      <td>cov_231</td>
      <td>玻璃单独破碎险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;国产玻璃:1;进口玻璃:2</td>
   </tr>
   <tr>
      <td>cov_210</td>
      <td>车身划痕损失险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;2千:2000.00</td>
   </tr>
   <tr>
      <td>cov_291</td>
      <td>发动机涉水损失险</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_640</td>
      <td>精神损害抚慰金责任险</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_734</td>
      <td>修理期间费用补偿险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1（费改添加）</td>
   </tr>
   <tr>
      <td>cov_731</td>
      <td>修理期间费用补偿险</td>
      <td>label</td>
      <td>text</td>
      <td>保额（费改添加）</td>
   </tr>
   <tr>
      <td>cov_732</td>
      <td>修理期间费用补偿险</td>
      <td>label</td>
      <td>text</td>
      <td>天数（费改添加）</td>
   </tr>
   <tr>
      <td>cov_733</td>
      <td>机动车损失保险无法找到第三方特约险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1（费改添加）</td>
   </tr>
   <tr>
      <td>cov_921</td>
      <td>不计免赔险（全车盗抢保险）</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_922</td>
      <td>不计免赔险（车身划痕损失险）</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_911</td>
      <td>不计免赔险(机动车损失保险)</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_912</td>
      <td>不计免赔险(商业第三者责任险)</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_928</td>
      <td>不计免赔险(车上人员责任保险(驾驶员))</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_929</td>
      <td>不计免赔险(车上人员责任保险(乘客))</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>forceFlag</td>
      <td>交强险</td>
      <td>radio</td>
      <td>radio</td>
      <td>投保:1;不投保:0</td>
   </tr>
   <tr>
      <td>forcePremium</td>
      <td>交强险</td>
      <td>label</td>
      <td>label</td>
      <td>交强险保费</td>
   </tr>
   <tr>
      <td>vehicleTaxPremium</td>
      <td>车船税</td>
      <td>label</td>
      <td>label</td>
      <td>车船税保费</td>
   </tr>
   <tr>
      <td>forceTotalPremium</td>
      <td>交强险总保费</td>
      <td>label</td>
      <td>label</td>
      <td>交强险总保费</td>
   </tr>
   <tr>
      <td>bizTotalPremium</td>
      <td>商业总保费</td>
      <td>label</td>
      <td>label</td>
      <td>商业保费</td>
   </tr>
   <tr>
      <td>standardPremium</td>
      <td>市场价(应缴总保费)</td>
      <td>label</td>
      <td>label</td>
      <td>应缴总保费</td>
   </tr>
   <tr>
      <td>totalPremium</td>
      <td>网购价(实际保费)</td>
      <td>label</td>
      <td>label</td>
      <td>实际保费</td>
   </tr>
   <tr>
      <td>bizBeginDate</td>
      <td>商业险起保日期[保险起期]</td>
      <td>Date</td>
      <td>Date</td>
      <td>商业险保险起期</td>
   </tr>
   <tr>
      <td>forceBeginDate</td>
      <td>交强险起保日期[保险起期]</td>
      <td>Date</td>
      <td>Date</td>
      <td>交强险保险起期</td>
   </tr>
   <tr>
      <td>lastClaimText</td>
      <td>上年出险信息</td>
      <td>label</td>
      <td>label</td>
      <td>展示上年用户出险的信息</td>
   </tr>
   <tr>
      <td>presentVal</td>
      <td>投保礼或UN积分值[积分值]</td>
      <td>label</td>
      <td>label</td>
      <td>投保礼可用费用或者UN积分</td>
   </tr>
   <tr>
      <td>hasAddPresent</td>
      <td>是否有加投</td>
      <td>label</td>
      <td>label</td>
      <td>是否有加投信息</td>
   </tr>
   <tr>
      <td>presentType</td>
      <td>投保礼或UN积分标识</td>
      <td>label</td>
      <td>label</td>
      <td>投保礼或UN积分标识</td>
   </tr>
   <tr>
      <td>isRunAreaFlag</td>
      <td>是否可以使用指省</td>
      <td>label</td>
      <td>label</td>
      <td>是否可以使用指省0:否；1：是</td>
   </tr>
   <tr>
      <td>runArea</td>
      <td>行驶区域</td>
      <td>radio</td>
      <td>radio</td>
      <td>行驶区域04：全国；03指省</td>
   </tr>
   <tr>
      <td>isDriverFlag</td>
      <td>是否可以使用指驾</td>
      <td>label</td>
      <td>label</td>
      <td>是否可以使用指驾 0:否；1：是</td>
   </tr>
   <tr>
      <td>agreedDriver</td>
      <td>是否指定驾驶员</td>
      <td>radio</td>
      <td>radio</td>
      <td>是否指定驾驶员 0：否；1：是</td>
   </tr>
   <tr>
      <td>driverName</td>
      <td>驾驶员姓名</td>
      <td>text</td>
      <td>text</td>
      <td>驾驶员姓名</td>
   </tr>
   <tr>
      <td>driverNum</td>
      <td>驾驶证号</td>
      <td>text</td>
      <td>text</td>
      <td>驾驶证号</td>
   </tr>
   <tr>
      <td>drivateDate</td>
      <td>驾驶证领证日期</td>
      <td>date</td>
      <td>date</td>
      <td>驾驶证领证日期</td>
   </tr>
   <tr>
      <td>isImmevalid</td>
      <td>是否及时生效</td>
      <td>label</td>
      <td>label</td>
      <td>是否及时生效</td>
   </tr>
   <tr>
      <td>immeValidHoursStart</td>
      <td>生效时间(小时)</td>
      <td>select</td>
      <td>select</td>
      <td>生效时间(小时)</td>
   </tr>
</table>

``` xml

<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<version>2</version>
			<RequestType>105</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201505071529491721</SessionId>
			<SellerId>3597746367</SellerId>
			<SendTime>2015-05-07 15:36:51</SendTime>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Sign>fIlXQ6vYJKqor-XeUG4swZraT2WC78QZr3giIpMRjRUGcaYyF0IT58P9_O73yNbyqo_8z8ivN9pg9ng0e2RJJCJwpL4n3G9S4z0g4_EN2865n6xUAia4NZl3Ev9R3sXQ_8tuQzz9fErSjPMPh-Gs80_u8dmYF6BAPU7uVUxBxZQ</Sign>
		<Response>
			<packageType>luxury</packageType>
			<TagsList>
				<Tags type="vehicleInfo">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">cityCode</Definition>
						<Definition name="label">城市代码</Definition>
						<Definition name="value">17112200</Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">licenseNo</Definition>
						<Definition name="label">车牌号</Definition>
						<Definition name="value">桂AU1232</Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">noLicenseFlag</Definition>
						<Definition name="label">新车未上牌</Definition>
						<Definition name="value">0</Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleModelName</Definition>
						<Definition name="label">品牌型号</Definition>
						<Definition name="value">北京现代BH7140AW轿车</Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleId</Definition>
						<Definition name="label">车辆代码</Definition>
						<Definition name="value">XDABBD0017</Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">firstRegisterDate</Definition>
						<Definition name="label">注册登记日期</Definition>
						<Definition name="value">2015-05-07</Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">engineNo</Definition>
						<Definition name="label">发动机号</Definition>
						<Definition name="value">123123</Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleFrameNo</Definition>
						<Definition name="label">车架号</Definition>
						<Definition name="value">43532313565464564</Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">specialCarFlag</Definition>
						<Definition name="label">是否过户车</Definition>
						<Definition name="value">0</Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">specialCarDate</Definition>
						<Definition name="label">过户日期</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleInvoiceNo</Definition>
						<Definition name="label">新车购置发票号</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleInvoiceDate</Definition>
						<Definition name="label">发票开具日期</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
				</Tags>
				<Tags type="ownerInfo">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">ownerName</Definition>
						<Definition name="label">车主</Definition>
						<Definition name="value">观点</Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">ownerIdNo</Definition>
						<Definition name="label">身份证</Definition>
						<Definition name="value">710000199010262433</Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">ownerMobile</Definition>
						<Definition name="label">手机号码</Definition>
						<Definition name="value">13512312312</Definition>
						<Definition name="premium"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
				</Tags>
				<Tags type="luxury">
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_200</Definition>
						<Definition name="label">车辆损失险</Definition>
						<Definition name="value">96800.00</Definition>
						<Definition name="range">0,96800.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;足额投保:96800.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">136875</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_600</Definition>
						<Definition name="label">商业第三者责任险</Definition>
						<Definition name="value">200000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;5万:50000.00;10万:100000.00;15万:150000.00;20万:200000.00;30万:300000.00;50万:500000.00;100万:1000000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">85400</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_701</Definition>
						<Definition name="label">司机座位责任险</Definition>
						<Definition name="value">10000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;1万/座:10000.00;2万/座:20000.00;3万/座:30000.00;4万/座:40000.00;5万/座:50000.00;10万/座:100000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">2962</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_702</Definition>
						<Definition name="label">乘客座位责任险</Definition>
						<Definition name="value">10000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;1万/座:10000.00;2万/座:20000.00;3万/座:30000.00;4万/座:40000.00;5万/座:50000.00;10万/座:100000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">7514</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_500</Definition>
						<Definition name="label">全车盗抢险</Definition>
						<Definition name="value">96800.00</Definition>
						<Definition name="range">0,96800.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;投保:96800.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">38044</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_231</Definition>
						<Definition name="label">玻璃单独破碎险</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;国产玻璃:1;进口玻璃:2]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">13288</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_310</Definition>
						<Definition name="label">自燃损失险</Definition>
						<Definition name="value">0.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;投保:96800.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_210</Definition>
						<Definition name="label">车身划痕损险</Definition>
						<Definition name="value">0.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;2000:2000.00;5000:5000.00;10000:10000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_321</Definition>
						<Definition name="label">指定专修厂</Definition>
						<Definition name="value">0.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;投保:15.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(车辆损失险)</Definition>
						<Definition name="key">cov_911</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">20531</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(商业第三者责任险)</Definition>
						<Definition name="key">cov_912</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">12810</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(司机座位责任险)</Definition>
						<Definition name="key">cov_928</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">444</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(乘客座位责任险)</Definition>
						<Definition name="key">cov_929</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">1127</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(全车盗抢险)</Definition>
						<Definition name="key">cov_921</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">7609</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(划痕险)</Definition>
						<Definition name="key">cov_922</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[不可投保:0]]></Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_291</Definition>
						<Definition name="label">发动机特别损失险</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_640</Definition>
						<Definition name="label">交通事故精神损害赔偿责任险</Definition>
						<Definition name="value">0.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;1万:10000.00;2万:20000.00;5万:50000.00;10万:100000.00;15万:150000.00;20万:200000.00;30万:300000.00;50万:500000.00;100万:1000000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_734</Definition>
						<Definition name="label">修理期间费用补偿险</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">cov_731</Definition>
						<Definition name="label">修理期间费用补偿险</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">cov_732</Definition>
						<Definition name="label">修理期间费用补偿险</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_733</Definition>
						<Definition name="label">机动车损失保险无法找到第三方特约险</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">lastClaimText</Definition>
						<Definition name="label">上年出险信息</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">radio</Definition>
						<Definition name="label">交强险</Definition>
						<Definition name="key">forceFlag</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[投保:1;不投保:0]]></Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">bizTotalPremium</Definition>
						<Definition name="label">商业总保费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">326604</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">standardPremium</Definition>
						<Definition name="label">市场价</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">650820</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">totalPremium</Definition>
						<Definition name="label">网购价</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">445604</Definition>
					</Tag>
				</Tags>
				<Tags type="deadline">
					<Tag>
						<Definition name="type">date</Definition>
						<Definition name="label">商业险起保日期</Definition>
						<Definition name="key">bizBeginDate</Definition>
						<Definition name="value">2015-05-08</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">date</Definition>
						<Definition name="label">交强险起保日期</Definition>
						<Definition name="key">forceBeginDate</Definition>
						<Definition name="value">2015-05-08</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
				</Tags>
				<Tags type="force">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">forcePremium</Definition>
						<Definition name="label">交强险</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">95000</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleTaxPremium</Definition>
						<Definition name="label">车船税</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">24000</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">forceTotalPremium</Definition>
						<Definition name="label">交强险总保费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">119000</Definition>
					</Tag>
				</Tags>
				<Tags type="lifeTableCpm">
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">presentType</Definition>
						<Definition name="label">投保礼或UN积分标识</Definition>
						<Definition name="value">0</Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">presentVal</Definition>
						<Definition name="label">投保礼或UN积分值</Definition>
						<Definition name="value">0</Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">hasAddPresent</Definition>
						<Definition name="label">是否有加投</Definition>
						<Definition name="value">0</Definition>
						<Definition name="premium"></Definition>
					</Tag>
				</Tags>
				<Tags type="runAreaType">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">isRunAreaFlag</Definition>
						<Definition name="label">是否可以使用指省</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">runArea</Definition>
						<Definition name="label">行驶区域</Definition>
						<Definition name="value">04</Definition>
						<Definition name="data"><![CDATA[全国:04;省内:03]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
				</Tags>
				<Tags type="driverInfoFlag">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">isDriverFlag</Definition>
						<Definition name="label">是否可以使用指驾</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">radio</Definition>
						<Definition name="key">agreedDriver</Definition>
						<Definition name="label">是否指定驾驶员</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[是:1;否:0]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
				</Tags>
				<Tags type="driverInfo">
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">driverName</Definition>
						<Definition name="label">姓名</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">driverNum</Definition>
						<Definition name="label">驾驶证号</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">cdate</Definition>
						<Definition name="key">drivateDate</Definition>
						<Definition name="label">初次领证日期</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
				</Tags>
				<Tags type="driverInfo">
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">driverName</Definition>
						<Definition name="label">姓名</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">driverNum</Definition>
						<Definition name="label">驾驶证号</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">cdate</Definition>
						<Definition name="key">drivateDate</Definition>
						<Definition name="label">初次领证日期</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
				</Tags>
				<Tags type="campaignViewPlan">
					<Tag>
						<Definition name="campaignMarke"></Definition>
						<Definition name="isShow">1</Definition>
						<Definition name="realPremium"></Definition>
						<Definition name="campaignPremium"></Definition>
						<Definition name="tips">您可以获得63的U商星级奖励积分</Definition>
					</Tag>
				</Tags>
			</TagsList>
		</Response>
	</Package>
</PackageList>

```
##3.8修改报价接口
该接口只计算自由组合的商业险报价，请求的报文中应该只包含自由组合的信息。
###3.8.1请求报文(费改前)
请求入参：
<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>是否可为空</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>cov_200</td>
      <td>车辆损失险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;足额投保:XXX</td>
   </tr>
   <tr>
      <td>cov_600</td>
      <td>商业第三者责任险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;5万:50000.00;…</td>
   </tr>
   <tr>
      <td>cov_500</td>
      <td>全车盗抢险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;投保:XXX</td>
   </tr>
   <tr>
      <td>cov_701</td>
      <td>司机座位责任险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_702</td>
      <td>乘客座位责任险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_321</td>
      <td>指定专修厂</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_310</td>
      <td>自燃损失险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;投保:XXX</td>
   </tr>
   <tr>
      <td>cov_231</td>
      <td>玻璃单独破碎险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;国产玻璃:1;进口玻璃:2</td>
   </tr>
   <tr>
      <td>cov_210</td>
      <td>车身划痕损险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;2千:2000.00</td>
   </tr>
   <tr>
      <td>cov_390</td>
      <td>高速高价救援险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1（费改后删除）</td>
   </tr>
   <tr>
      <td>cov_291</td>
      <td>发动机特别损失险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_640</td>
      <td>交通事故精神损害赔偿责任险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_921</td>
      <td>不计免赔险（机动车盗抢险）</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_922</td>
      <td>不计免赔险（车身划痕损失险）</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_911</td>
      <td>不计免赔险(车损险)</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_912</td>
      <td>不计免赔险(三者险)</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_928</td>
      <td>不计免赔险(司机险)</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_929</td>
      <td>不计免赔险(乘客险)</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>forceFlag</td>
      <td>交强险</td>
      <td>String</td>
      <td>否</td>
      <td>投保:1;不投保:0</td>
   </tr>
   <tr>
      <td>bizBeginDate</td>
      <td>商业险保险起期</td>
      <td>String</td>
      <td>是</td>
      <td>商业险保险起期</td>
   </tr>
   <tr>
      <td>forceBeginDate</td>
      <td>交强险保险起期</td>
      <td>String</td>
      <td>是</td>
      <td>交强险保险起期</td>
   </tr>
   <tr>
      <td>packageType</td>
      <td>用户选择套餐</td>
      <td>String </td>
      <td>是</td>
      <td>用户选择的套餐</td>
   </tr>
   <tr>
      <td>isImmevalid</td>
      <td>是否及时生效</td>
      <td>String</td>
      <td>否</td>
      <td>是否及时生效</td>
   </tr>
   <tr>
      <td>immeValidHoursStart</td>
      <td>生效时间(小时)</td>
      <td>String</td>
      <td>是</td>
      <td>生效时间(小时)</td>
   </tr>
   <tr>
      <td>runArea</td>
      <td>行驶区域</td>
      <td>String</td>
      <td>否</td>
      <td>行驶区域</td>
   </tr>
   <tr>
      <td>agreedDriver</td>
      <td>是否指定驾驶员</td>
      <td>String</td>
      <td>否</td>
      <td>是否指定驾驶员</td>
   </tr>
   <tr>
      <td>driverDate</td>
      <td>驾驶证领证日期</td>
      <td>String</td>
      <td>是</td>
      <td>驾驶证领证日期</td>
   </tr>
   <tr>
      <td>driverNum</td>
      <td>驾驶证号</td>
      <td>String</td>
      <td>是</td>
      <td>驾驶证号</td>
   </tr>
   <tr>
      <td>driverName</td>
      <td>驾驶员姓名</td>
      <td>String</td>
      <td>是</td>
      <td>驾驶员姓名</td>
   </tr>
</table>
``` xml
<?xml version='1.0' encoding='GBK' standalone='yes'?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>110</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<From>MobileCar</From>
			<To>Server</To>
			<AgentCode>W02400654</AgentCode>
			<SendTime>2015-01-29 21:21:58</SendTime>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Request>
			<InputsList>
				<Inputs>
					<input name='cov_640'>0.00</input>
					<input name='cov_310'>0.00</input>
					<input name='packageType'>optional</input>
					<input name='cov_321'>0.00</input>
					<input name='cov_291'>0</input>
					<input name='cov_702'>20000.00</input>
					<input name='forceBeginDate'>2015-01-29</input>
					<input name='forceFlag'>1</input>
					<input name='cov_701'>10000.00</input>
					<input name='cov_928'>1</input>
					<input name='cov_929'>1</input>
					<input name='cov_231'>1</input>
					<input name='cov_500'>98800.00</input>
					<input name='cov_210'>0.00</input>
					<input name='cov_200'>98800.00</input>
					<input name='cov_921'>0</input>
					<input name='cov_600'>300000.00</input>
					<input name='cov_922'>0</input>
					<input name='cov_912'>1</input>
					<input name='cov_390'>0</input>
					<input name='cov_911'>1</input>
					<input name='bizBeginDate'>2015-01-30</input>
				</Inputs>
				<Inputs type='immevalid'>
					<input name='immeValidHoursStart'>22</input>
					<input name='isImmevalid'>1</input>
				</Inputs>
				<Inputs type='runAreaType'>
					<input name='runArea'>04</input>
				</Inputs>
				<Inputs type='driverInfoFlag'>
					<input name='agreedDriver'>1</input>
				</Inputs>
				<Inputs type='driverInfo'>
					<input name='driverDate'>2015-01-1</input>
					<input name='driverNum'>130429198601173637</input>
					<input name='driverName'>的方法</input>
				</Inputs>
			</InputsList>
		</Request>
		<Sign>X947HN2Vbudjyk8gGY6he15rAr37tZu5ylhxcCvkO_VCoSo60gXlPz3lniFUbzeboWG4-wfBpawtPKDY_CHNboJzLH7TiH4XSbqyxfPrVQAyMoDwi5mZR7wEd8nQhqUkxAzCi6Pw2wJ3JnKwNOe5QKnPQJDM7Ae7BGeIHY4mP9I</Sign>
	</Package>
</PackageList>
```
当用户选择套餐为自由定制时（packageType=optional），需要入参险种列表，其他套餐只需要传入套餐和起保日期即可，不必传险种列表（传入无效）。
要求页面在切换套餐时如果切换的当前套餐已经有算价过的信息不必要再请求算价，只有当前套餐未算价过才可请求后台算价，自由定制（packageType=optional）除外。
###3.8.2返回报文(费改前)
返回数据见获取报价表单返回数据
``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<version>2</version>
			<RequestType>110</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<SellerId>3597746367</SellerId>
			<SendTime>2015-01-29 21:22:10</SendTime>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Sign>hvhJ3z2ZMHaaz1e1vEmwQZIPh2NgsuEnr09Mv_z8rez8hQYr4IpwcOFR-SJxgW9azDTN83kpqlAfg8J6JvDZ1xlvDX5fU9OeN3SGabkjfPejwDg0JT5rACrxP6uPgH-63ZQzQRNggVndNbV8Ea8RffR9Z8mSLrwDQHSiwFug7SE</Sign>
		<Response>
			<packageType>optional</packageType>
			<TagsList>
				<Tags type="optional">
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_200</Definition>
						<Definition name="label">车辆损失险</Definition>
						<Definition name="value">98800.00</Definition>
						<Definition name="range">98800.00,107200</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;足额投保:98800.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">145731</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_600</Definition>
						<Definition name="label">商业第三者责任险</Definition>
						<Definition name="value">300000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;5万:50000.00;10万:100000.00;15万:150000.00;20万:200000.00;30万:300000.00;50万:500000.00;100万:1000000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">104030</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_701</Definition>
						<Definition name="label">司机座位责任险</Definition>
						<Definition name="value">10000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;1万/座:10000.00;2万/座:20000.00;3万/座:30000.00;4万/座:40000.00;5万/座:50000.00;10万/座:100000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">3392</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_702</Definition>
						<Definition name="label">乘客座位责任险</Definition>
						<Definition name="value">20000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;1万/座:10000.00;2万/座:20000.00;3万/座:30000.00;4万/座:40000.00;5万/座:50000.00;10万/座:100000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">17443</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_500</Definition>
						<Definition name="label">全车盗抢险</Definition>
						<Definition name="value">98800.00</Definition>
						<Definition name="range">0,98800.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;投保:98800.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">48785</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_231</Definition>
						<Definition name="label">玻璃单独破碎险</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;国产玻璃:1;进口玻璃:2]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">15957</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_310</Definition>
						<Definition name="label">自燃损失险</Definition>
						<Definition name="value">0.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;投保:98800.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_210</Definition>
						<Definition name="label">车身划痕损险</Definition>
						<Definition name="value">0.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;2000:2000.00;5000:5000.00;10000:10000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_321</Definition>
						<Definition name="label">指定专修厂</Definition>
						<Definition name="value">0.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;投保:10.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(车辆损失险)</Definition>
						<Definition name="key">cov_911</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">21860</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(商业第三者责任险)</Definition>
						<Definition name="key">cov_912</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">15605</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(司机座位责任险)</Definition>
						<Definition name="key">cov_928</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">509</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(乘客座位责任险)</Definition>
						<Definition name="key">cov_929</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">2616</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(全车盗抢险)</Definition>
						<Definition name="key">cov_921</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(划痕险)</Definition>
						<Definition name="key">cov_922</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[不可投保:0]]></Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_291</Definition>
						<Definition name="label">发动机特别损失险</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[不可投保:0]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_390</Definition>
						<Definition name="label">高速高价救援险</Definition>
						<Definition name="value">0</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_640</Definition>
						<Definition name="label">交通事故精神损害赔偿责任险</Definition>
						<Definition name="value">0.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;1万:10000.00;2万:20000.00;5万:50000.00;10万:100000.00;15万:150000.00;20万:200000.00;30万:300000.00;50万:500000.00;100万:1000000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">lastClaimText</Definition>
						<Definition name="label">上年出险信息</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">radio</Definition>
						<Definition name="label">交强险</Definition>
						<Definition name="key">forceFlag</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[投保:1;不投保:0]]></Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">bizTotalPremium</Definition>
						<Definition name="label">商业总保费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">375928</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">standardPremium</Definition>
						<Definition name="label">市场价</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">560522</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">totalPremium</Definition>
						<Definition name="label">网购价</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">470928</Definition>
					</Tag>
				</Tags>
				<Tags type="deadline">
					<Tag>
						<Definition name="type">date</Definition>
						<Definition name="label">商业险起保日期</Definition>
						<Definition name="key">bizBeginDate</Definition>
						<Definition name="value">2015-01-30</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">date</Definition>
						<Definition name="label">交强险起保日期</Definition>
						<Definition name="key">forceBeginDate</Definition>
						<Definition name="value">2015-01-29</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
				</Tags>
				<Tags type="force">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">forcePremium</Definition>
						<Definition name="label">交强险</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">95000</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleTaxPremium</Definition>
						<Definition name="label">车船税</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">forceTotalPremium</Definition>
						<Definition name="label">交强险总保费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">95000</Definition>
					</Tag>
				</Tags>
				<Tags type="lifeTableCpm">
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">presentType</Definition>
						<Definition name="label">投保礼或UN积分标识</Definition>
						<Definition name="value">1</Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">presentVal</Definition>
						<Definition name="label">投保礼或UN积分值</Definition>
						<Definition name="value">900.0</Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">hasAddPresent</Definition>
						<Definition name="label">是否有加投</Definition>
						<Definition name="value">0</Definition>
						<Definition name="premium"></Definition>
					</Tag>
				</Tags>
				<Tags type="immevalid">
					<Tag>
						<Definition name="type">radio</Definition>
						<Definition name="key">isImmevalid</Definition>
						<Definition name="label">是否及时生效</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[是:1;否:0]]></Definition>
						<Definition name="dataUrl"><![CDATA[您的保单将在 2015-01-29 22:00:00生效，超过此时间投保单将失效，不允许支付。]]></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">生效时间(小时)</Definition>
						<Definition name="key">immeValidHoursStart</Definition>
						<Definition name="value">22</Definition>
						<Definition name="data"><![CDATA[22:22;23:23;24:24]]></Definition>
					</Tag>
				</Tags>
			</TagsList>
		</Response>
	</Package>
</PackageList>
```
第三方要根据交强险和商业险标签判断是否显示保费。

用户选择日期算价后可能存
在重复投保，系统会提示重复投保的信息（ErrorMessages），此提示信息需要展示给用户，并且商业会正常算价结果，交强将会算价失败。
其他参考获取报价表单（100）接口
###3.8.3请求报文(费改后)
请求入参
<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>是否可为空</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>cov_200</td>
      <td>机动车损失保险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;足额投保:XXX</td>
   </tr>
   <tr>
      <td>cov_600</td>
      <td>商业第三者责任险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;5万:50000.00;…</td>
   </tr>
   <tr>
      <td>cov_500</td>
      <td>全车盗抢保险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;投保:XXX</td>
   </tr>
   <tr>
      <td>cov_701</td>
      <td>车上人员责任保险(驾驶员)</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_702</td>
      <td>车上人员责任保险(乘客)</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_321</td>
      <td>指定专修厂险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_310</td>
      <td>自燃损失险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;投保:XXX</td>
   </tr>
   <tr>
      <td>cov_231</td>
      <td>玻璃单独破碎险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;国产玻璃:1;进口玻璃:2</td>
   </tr>
   <tr>
      <td>cov_210</td>
      <td>车身划痕损失险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;2千:2000.00</td>
   </tr>
   <tr>
      <td>cov_291</td>
      <td>发动机涉水损失险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_640</td>
      <td>精神损害抚慰金责任险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_734</td>
      <td>修理期间费用补偿险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1（费改添加）</td>
   </tr>
   <tr>
      <td>cov_731</td>
      <td>修理期间费用补偿险</td>
      <td>String</td>
      <td>是</td>
      <td>保额：50-500元内正整数（费改添加）</td>
   </tr>
   <tr>
      <td>cov_732</td>
      <td>修理期间费用补偿险</td>
      <td>String</td>
      <td>是</td>
      <td>修理期间天数：1-90内正整数（费改添加）</td>
   </tr>
   <tr>
      <td>cov_733</td>
      <td>机动车损失保险无法找到第三方特约险</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1（费改添加）</td>
   </tr>
   <tr>
      <td>cov_921</td>
      <td>不计免赔险（全车盗抢保险）</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_922</td>
      <td>不计免赔险（车身划痕损失险）</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_911</td>
      <td>不计免赔险(机动车损失保险)</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_912</td>
      <td>不计免赔险(商业第三者责任险)</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_928</td>
      <td>不计免赔险(车上人员责任保险(驾驶员))</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_929</td>
      <td>不计免赔险(车上人员责任保险(乘客))</td>
      <td>String</td>
      <td>否</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>forceFlag</td>
      <td>交强险</td>
      <td>String</td>
      <td>否</td>
      <td>投保:1;不投保:0</td>
   </tr>
   <tr>
      <td>bizBeginDate</td>
      <td>商业险保险起期</td>
      <td>String</td>
      <td>是</td>
      <td>商业险保险起期</td>
   </tr>
   <tr>
      <td>forceBeginDate</td>
      <td>交强险保险起期</td>
      <td>String</td>
      <td>是</td>
      <td>交强险保险起期</td>
   </tr>
   <tr>
      <td>packageType</td>
      <td>用户选择套餐</td>
      <td>String </td>
      <td>是</td>
      <td>用户选择的套餐</td>
   </tr>
   <tr>
      <td>isImmevalid</td>
      <td>是否及时生效</td>
      <td>String</td>
      <td>否</td>
      <td>是否及时生效</td>
   </tr>
   <tr>
      <td>immeValidHoursStart</td>
      <td>生效时间(小时)</td>
      <td>String</td>
      <td>是</td>
      <td>生效时间(小时)</td>
   </tr>
   <tr>
      <td>runArea</td>
      <td>行驶区域</td>
      <td>String</td>
      <td>否</td>
      <td>行驶区域</td>
   </tr>
   <tr>
      <td>agreedDriver</td>
      <td>是否指定驾驶员</td>
      <td>String</td>
      <td>否</td>
      <td>是否指定驾驶员</td>
   </tr>
   <tr>
      <td>driverDate</td>
      <td>驾驶证领证日期</td>
      <td>String</td>
      <td>是</td>
      <td>驾驶证领证日期</td>
   </tr>
   <tr>
      <td>driverNum</td>
      <td>驾驶证号</td>
      <td>String</td>
      <td>是</td>
      <td>驾驶证号</td>
   </tr>
   <tr>
      <td>driverName</td>
      <td>驾驶员姓名</td>
      <td>String</td>
      <td>是</td>
      <td>驾驶员姓名</td>
   </tr>
</table>
``` xml
<?xml version='1.0' encoding='GBK' standalone='yes'?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
<Package>
<Header>
<Version>2</Version>
<RequestType>110</RequestType>
<InsureType>100</InsureType>
<SessionId>201505071529491721</SessionId>
<From>MobileCar</From>
<To>Server</To>
<AgentCode>W02400652</AgentCode>
<SendTime>2015-05-07 15:39:16</SendTime>
<SellerId>3597746367</SellerId>
<Status>100</Status>
<ErrorMessage></ErrorMessage>
<terminalTpye></terminalTpye>
</Header>
<Request>
<InputsList>
<Inputs>
<input name='cov_732'>90</input>
<input name='cov_310'>96800.00</input>
<input name='cov_731'>500</input>
<input name='cov_734'>1</input>
<input name='packageType'>optional</input>
<input name='cov_733'>1</input>
<input name='cov_291'>1</input>
<input name='forceFlag'>1</input>
<input name='cov_500'>96800.00</input>
<input name='cov_200'>96800.00</input>
<input name='cov_600'>200000.00</input>
<input name='bizBeginDate'>2015-05-08</input>
<input name='cov_640'>1000000.00</input>
<input name='cov_321'>15.00</input>
<input name='cov_702'>10000.00</input>
<input name='forceBeginDate'>2015-05-08</input>
<input name='cov_701'>10000.00</input>
<input name='cov_928'>1</input>
<input name='cov_929'>1</input>
<input name='cov_231'>1</input>
<input name='cov_210'>10000.00</input>
<input name='cov_921'>1</input>
<input name='cov_912'>1</input>
<input name='cov_922'>1</input>
<input name='cov_911'>1</input>
<input name='cov_390'></input>
</Inputs>
<Inputs type='immevalid'>
<input name='immeValidHoursStart'></input>
<input name='isImmevalid'>1</input>
</Inputs>
<Inputs type='runAreaType'>
<input name='runArea'>04</input>
</Inputs>
<Inputs type='driverInfoFlag'>
<input name='agreedDriver'></input>
</Inputs>
</InputsList>
</Request>
<Sign>IX1hYPiJsnMTQl0R_Sj_y__j3lvLcH3H15wv0Gk012LwBkUBKT0XPrtK_WUUf3ORokhJx3OXtXtJOog8H4S8jvvv3tkmodwPfdYzGs5wGvJaFvjXA_X13m6Kk7HHa2PVxMxTcNIbQO0BR0ZSOdIQTdSXeJDEWhdwDS-CuDJlYg0</Sign>
</Package>
</PackageList>
```
###3.8.4返回报文(费改后)
<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>备注</td>
   </tr>
   <tr>
      <td></td>
      <td></td>
      <td>全保、续保</td>
      <td>全保</td>
      <td></td>
   </tr>
   <tr>
      <td>cov_200</td>
      <td>机动车损失保险[车辆损失险]</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;足额投保:XXX</td>
   </tr>
   <tr>
      <td>cov_600</td>
      <td>商业第三者责任险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;5万:50000.00;…</td>
   </tr>
   <tr>
      <td>cov_500</td>
      <td>全车盗抢保险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;投保:XXX</td>
   </tr>
   <tr>
      <td>cov_701</td>
      <td>车上人员责任保险(驾驶员)</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_702</td>
      <td>车上人员责任保险(乘客)</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_321</td>
      <td>指定修理厂险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_310</td>
      <td>自燃损失险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;投保:XXX</td>
   </tr>
   <tr>
      <td>cov_231</td>
      <td>玻璃单独破碎险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;国产玻璃:1;进口玻璃:2</td>
   </tr>
   <tr>
      <td>cov_210</td>
      <td>车身划痕损失险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0.00;2千:2000.00</td>
   </tr>
   <tr>
      <td>cov_291</td>
      <td>发动机涉水损失险</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_640</td>
      <td>精神损害抚慰金责任险</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0.00;1万/座:10000.00;…</td>
   </tr>
   <tr>
      <td>cov_734</td>
      <td>修理期间费用补偿险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1（费改添加）</td>
   </tr>
   <tr>
      <td>cov_731</td>
      <td>修理期间费用补偿险</td>
      <td>label</td>
      <td></td>
      <td>text</td>
      <td>保额（费改添加）</td>
   </tr>
   <tr>
      <td>cov_732</td>
      <td>修理期间费用补偿险</td>
      <td>label</td>
      <td>text</td>
      <td>天数（费改添加）</td>
   </tr>
   <tr>
      <td>cov_733</td>
      <td>机动车损失保险无法找到第三方特约险</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1（费改添加）</td>
   </tr>
   <tr>
      <td>cov_921</td>
      <td>不计免赔险（全车盗抢保险）</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_922</td>
      <td>不计免赔险（车身划痕损失险）</td>
      <td>String</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_911</td>
      <td>不计免赔险(机动车损失保险)</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_912</td>
      <td>不计免赔险(商业第三者责任险)</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_928</td>
      <td>不计免赔险(车上人员责任保险(驾驶员))</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>cov_929</td>
      <td>不计免赔险(车上人员责任保险(乘客))</td>
      <td>label</td>
      <td>select</td>
      <td>不投保:0;投保:1</td>
   </tr>
   <tr>
      <td>forceFlag</td>
      <td>交强险</td>
      <td>radio</td>
      <td>radio</td>
      <td>投保:1;不投保:0</td>
   </tr>
   <tr>
      <td>forcePremium</td>
      <td>交强险</td>
      <td>label</td>
      <td>label</td>
      <td>交强险保费</td>
   </tr>
   <tr>
      <td>vehicleTaxPremium</td>
      <td>车船税</td>
      <td>label</td>
      <td>label</td>
      <td>车船税保费</td>
   </tr>
   <tr>
      <td>forceTotalPremium</td>
      <td>交强险总保费</td>
      <td>label</td>
      <td>label</td>
      <td>交强险总保费</td>
   </tr>
   <tr>
      <td>bizTotalPremium</td>
      <td>商业总保费</td>
      <td>label</td>
      <td>label</td>
      <td>商业保费</td>
   </tr>
   <tr>
      <td>standardPremium</td>
      <td>市场价(应缴总保费)</td>
      <td>label</td>
      <td>label</td>
      <td>应缴总保费</td>
   </tr>
   <tr>
      <td>totalPremium</td>
      <td>网购价(实际保费)</td>
      <td>label</td>
      <td>label</td>
      <td>实际保费</td>
   </tr>
   <tr>
      <td>bizBeginDate</td>
      <td>商业险起保日期[保险起期]</td>
      <td>Date</td>
      <td>Date</td>
      <td>商业险保险起期</td>
   </tr>
   <tr>
      <td>forceBeginDate</td>
      <td>交强险起保日期[保险起期]</td>
      <td>Date</td>
      <td>Date</td>
      <td>交强险保险起期</td>
   </tr>
   <tr>
      <td>lastClaimText</td>
      <td>上年出险信息</td>
      <td>label</td>
      <td>label</td>
      <td>展示上年用户出险的信息</td>
   </tr>
   <tr>
      <td>presentVal</td>
      <td>投保礼或UN积分值[积分值]</td>
      <td>label</td>
      <td>label</td>
      <td>投保礼可用费用或者UN积分</td>
   </tr>
   <tr>
      <td>hasAddPresent</td>
      <td>是否有加投</td>
      <td>label</td>
      <td>label</td>
      <td>是否有加投信息</td>
   </tr>
   <tr>
      <td>presentType</td>
      <td>投保礼或UN积分标识</td>
      <td>label</td>
      <td>label</td>
      <td>投保礼或UN积分标识</td>
   </tr>
   <tr>
      <td>isRunAreaFlag</td>
      <td>是否可以使用指省</td>
      <td>label</td>
      <td>label</td>
      <td>是否可以使用指省0:否；1：是</td>
   </tr>
   <tr>
      <td>runArea</td>
      <td>行驶区域</td>
      <td>radio</td>
      <td>radio</td>
      <td>行驶区域04：全国；03指省</td>
   </tr>
   <tr>
      <td>isDriverFlag</td>
      <td>是否可以使用指驾</td>
      <td>label</td>
      <td>label</td>
      <td>是否可以使用指驾 0:否；1：是</td>
   </tr>
   <tr>
      <td>agreedDriver</td>
      <td>是否指定驾驶员</td>
      <td>radio</td>
      <td>radio</td>
      <td>是否指定驾驶员 0：否；1：是</td>
   </tr>
   <tr>
      <td>driverName</td>
      <td>驾驶员姓名</td>
      <td>text</td>
      <td>text</td>
      <td>驾驶员姓名</td>
   </tr>
   <tr>
      <td>driverNum</td>
      <td>驾驶证号</td>
      <td>text</td>
      <td>text</td>
      <td>驾驶证号</td>
   </tr>
   <tr>
      <td>drivateDate</td>
      <td>驾驶证领证日期</td>
      <td>date</td>
      <td>date</td>
      <td>驾驶证领证日期</td>
   </tr>
   <tr>
      <td>isImmevalid</td>
      <td>是否及时生效</td>
      <td>label</td>
      <td>label</td>
      <td>是否及时生效</td>
   </tr>
   <tr>
      <td>immeValidHoursStart</td>
      <td>生效时间(小时)</td>
      <td>select</td>
      <td>select</td>
      <td>生效时间(小时)</td>
   </tr>
</table>
``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<version>2</version>
			<RequestType>110</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201505071529491721</SessionId>
			<SellerId>3597746367</SellerId>
			<SendTime>2015-05-07 15:39:36</SendTime>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Sign>ffXkTVbNMHwtPktUROjFxOk4nkhFSdo0lmNRUzkuBzsj7gJK-HCunGZiU70r9YLaj4nsvpUF2RZ08GMwFJmxe0bZ62kk2Bz_sMTg_dmrY6mMOYZKVehA9XUjj6J3nd50J6s9qyW0GUsc_OiU3GIMGAHXq9bt50dt0u1ijRWwduU</Sign>
		<Response>
			<packageType>optional</packageType>
			<TagsList>
				<Tags type="optional">
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_200</Definition>
						<Definition name="label">车辆损失险</Definition>
						<Definition name="value">96800.00</Definition>
						<Definition name="range">0,96800.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;足额投保:96800.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">150852</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_600</Definition>
						<Definition name="label">商业第三者责任险</Definition>
						<Definition name="value">200000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;5万:50000.00;10万:100000.00;15万:150000.00;20万:200000.00;30万:300000.00;50万:500000.00;100万:1000000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">94120</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_701</Definition>
						<Definition name="label">司机座位责任险</Definition>
						<Definition name="value">10000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;1万/座:10000.00;2万/座:20000.00;3万/座:30000.00;4万/座:40000.00;5万/座:50000.00;10万/座:100000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">3265</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_702</Definition>
						<Definition name="label">乘客座位责任险</Definition>
						<Definition name="value">10000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;1万/座:10000.00;2万/座:20000.00;3万/座:30000.00;4万/座:40000.00;5万/座:50000.00;10万/座:100000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">8281</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_500</Definition>
						<Definition name="label">全车盗抢险</Definition>
						<Definition name="value">96800.00</Definition>
						<Definition name="range">0,96800.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;投保:96800.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">41929</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_231</Definition>
						<Definition name="label">玻璃单独破碎险</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;国产玻璃:1;进口玻璃:2]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">14645</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_310</Definition>
						<Definition name="label">自燃损失险</Definition>
						<Definition name="value">96800.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;投保:96800.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">9250</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_210</Definition>
						<Definition name="label">车身划痕损险</Definition>
						<Definition name="value">10000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;2000:2000.00;5000:5000.00;10000:10000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">60517</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_321</Definition>
						<Definition name="label">指定专修厂</Definition>
						<Definition name="value">15.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;投保:15.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">22628</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(车辆损失险)</Definition>
						<Definition name="key">cov_911</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">22628</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(商业第三者责任险)</Definition>
						<Definition name="key">cov_912</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">14118</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(司机座位责任险)</Definition>
						<Definition name="key">cov_928</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">490</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(乘客座位责任险)</Definition>
						<Definition name="key">cov_929</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">1242</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(全车盗抢险)</Definition>
						<Definition name="key">cov_921</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">8386</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="label">不计免赔险(划痕险)</Definition>
						<Definition name="key">cov_922</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="premium">9078</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_291</Definition>
						<Definition name="label">发动机特别损失险</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">7542</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_640</Definition>
						<Definition name="label">交通事故精神损害赔偿责任险</Definition>
						<Definition name="value">1000000.00</Definition>
						<Definition name="data"><![CDATA[不投保:0.00;1万:10000.00;2万:20000.00;5万:50000.00;10万:100000.00;15万:150000.00;20万:200000.00;30万:300000.00;50万:500000.00;100万:1000000.00]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">637024</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_734</Definition>
						<Definition name="label">修理期间费用补偿险</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">358326</Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">cov_731</Definition>
						<Definition name="label">修理期间费用补偿险</Definition>
						<Definition name="value">500</Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">358326</Definition>
					</Tag>
					<Tag>
						<Definition name="type">text</Definition>
						<Definition name="key">cov_732</Definition>
						<Definition name="label">修理期间费用补偿险</Definition>
						<Definition name="value">90</Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">358326</Definition>
					</Tag>
					<Tag>
						<Definition name="type">select</Definition>
						<Definition name="key">cov_733</Definition>
						<Definition name="label">机动车损失保险无法找到第三方特约险</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[不投保:0;投保:1]]></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium">3771</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">lastClaimText</Definition>
						<Definition name="label">上年出险信息</Definition>
						<Definition name="value"></Definition>
						<Definition name="data"></Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">radio</Definition>
						<Definition name="label">交强险</Definition>
						<Definition name="key">forceFlag</Definition>
						<Definition name="value">1</Definition>
						<Definition name="data"><![CDATA[投保:1;不投保:0]]></Definition>
						<Definition name="premium">0</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">bizTotalPremium</Definition>
						<Definition name="label">商业总保费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">1468091</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">standardPremium</Definition>
						<Definition name="label">市场价</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">2288045</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">totalPremium</Definition>
						<Definition name="label">网购价</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">1587091</Definition>
					</Tag>
				</Tags>
				<Tags type="deadline">
					<Tag>
						<Definition name="type">date</Definition>
						<Definition name="label">商业险起保日期</Definition>
						<Definition name="key">bizBeginDate</Definition>
						<Definition name="value">2015-05-08</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">date</Definition>
						<Definition name="label">交强险起保日期</Definition>
						<Definition name="key">forceBeginDate</Definition>
						<Definition name="value">2015-05-08</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
				</Tags>
				<Tags type="force">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">forcePremium</Definition>
						<Definition name="label">交强险</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">95000</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleTaxPremium</Definition>
						<Definition name="label">车船税</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">24000</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">forceTotalPremium</Definition>
						<Definition name="label">交强险总保费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">119000</Definition>
					</Tag>
				</Tags>
				<Tags type="lifeTableCpm">
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">presentType</Definition>
						<Definition name="label">投保礼或UN积分标识</Definition>
						<Definition name="value">0</Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">presentVal</Definition>
						<Definition name="label">投保礼或UN积分值</Definition>
						<Definition name="value">0</Definition>
						<Definition name="premium"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="key">hasAddPresent</Definition>
						<Definition name="label">是否有加投</Definition>
						<Definition name="value">0</Definition>
						<Definition name="premium"></Definition>
					</Tag>
				</Tags>
				<Tags type="campaignViewPlan">
					<Tag>
						<Definition name="campaignMarke"></Definition>
						<Definition name="isShow">1</Definition>
						<Definition name="realPremium"></Definition>
						<Definition name="campaignPremium"></Definition>
						<Definition name="tips">您可以获得234的U商星级奖励积分</Definition>
					</Tag>
				</Tags>
			</TagsList>
		</Response>
	</Package>
</PackageList>
```
##3.9保存保费接口
接口说明：计算保费并且返回相关费用值（投保礼 和 加投信息）
请求入参：
<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>是否可为空</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>packageType</td>
      <td>用户选择套餐</td>
      <td>String</td>
      <td>是</td>
      <td>用户选择的套餐</td>
   </tr>
</table>
``` xml
<?xml version='1.0' encoding='GBK' standalone='yes'?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>115</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<From>MobileCar</From>
			<To>Server</To>
			<AgentCode>W02400654</AgentCode>
			<SendTime>2015-01-29 21:36:45</SendTime>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Request>
			<InputsList>
				<Inputs>
					<input name='packageType'>optional</input>
				</Inputs>
			</InputsList>
		</Request>
		<Sign>h3gvQtqn870LvZ80pybdRRlKZqZ4fHivHtBE75VQj7XRFqQHiK1Y-RSHbJTWFB2YrFSJ2ft-58MWZrT9JeUMKKCQPJGOCCXtQochbx0Li45ecDk6IKtIHQc99NHIZO6mul0WrK1D6suoSGOFkLSuXooBqJGZey3FJVQxBhynTnI</Sign>
	</Package>
</PackageList>
```
3.9.2返回报文
返回数据说明
<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>forcePremium</td>
      <td>交强险</td>
      <td>label</td>
      <td>交强险保费</td>
   </tr>
   <tr>
      <td>vehicleTaxPremium</td>
      <td>车船税</td>
      <td>label</td>
      <td>车船税保费</td>
   </tr>
   <tr>
      <td>forceTotalPremium</td>
      <td>交强险总保费</td>
      <td>label</td>
      <td>交强险总保费</td>
   </tr>
   <tr>
      <td>bizTotalPremium</td>
      <td>商业保费</td>
      <td>label</td>
      <td>商业保费</td>
   </tr>
   <tr>
      <td>standardPremium</td>
      <td>市场价(应缴总保费)</td>
      <td>label</td>
      <td>应缴总保费</td>
   </tr>
   <tr>
      <td>totalPremium</td>
      <td>网购价(实际保费)</td>
      <td>label</td>
      <td>实际保费</td>
   </tr>
   <tr>
      <td>bizBeginDate</td>
      <td>商业险保险起期</td>
      <td>Date</td>
      <td>商业险保险起期</td>
   </tr>
   <tr>
      <td>forceBeginDate</td>
      <td>交强险保险起期</td>
      <td>Date</td>
      <td>交强险保险起期</td>
   </tr>
   <tr>
      <td>特约</td>
   </tr>
   <tr>
      <td>engage_tra_1...</td>
      <td>交强特约</td>
      <td>label</td>
      <td>交强特约 都是以engage_tra_开头 存在多条</td>
   </tr>
   <tr>
      <td> engage_com_1...</td>
      <td>商业特约</td>
      <td>label</td>
      <td>商业特约 都是以engage_com_开头 存在多条</td>
   </tr>
   <tr>
      <td>投保礼（lifeTablePresents）和加投（addPresentPackages）</td>
   </tr>
   <tr>
      <td>AvailableCost</td>
      <td>投保礼可用总费用</td>
      <td>label</td>
      <td>投保礼可用总费用（最后说明）</td>
   </tr>
   <tr>
      <td>pkIdEncryption</td>
      <td>礼品id</td>
      <td>label</td>
      <td>礼品id加密选择后的需要回传</td>
   </tr>
   <tr>
      <td>presentName</td>
      <td>礼品名称</td>
      <td>label</td>
      <td>礼品名称</td>
   </tr>
   <tr>
      <td>showPrice</td>
      <td>礼品价格</td>
      <td>label</td>
      <td>礼品价格</td>
   </tr>
   <tr>
      <td>maxOptionalNum</td>
      <td>礼品最大可选数量</td>
      <td>label</td>
      <td>礼品最大可选数量</td>
   </tr>
   <tr>
      <td>presentType</td>
      <td>礼品类型 </td>
      <td>label</td>
      <td> 实物类/0、服务类/1、虚拟类/2、立减/3</td>
   </tr>
   <tr>
      <td>prePresentNum</td>
      <td>用户选择数量</td>
      <td>text</td>
      <td>投保礼用户选择数量回传</td>
   </tr>
   <tr>
      <td>phoneNoSign</td>
      <td>采集信息手机号标记</td>
      <td>label</td>
      <td>1--需采集；0--不用采集</td>
   </tr>
   <tr>
      <td>phoneNo</td>
      <td>手机号</td>
      <td>text</td>
      <td>手机号需要回传</td>
   </tr>
   <tr>
      <td>accountNumberSign</td>
      <td>采集信息账号号标记</td>
      <td>label</td>
      <td>1--需采集；0--不用采集</td>
   </tr>
   <tr>
      <td>accountNumber</td>
      <td>充值账号</td>
      <td>text</td>
      <td>游戏账号等 需要回传</td>
   </tr>
   <tr>
      <td>mustSelect</td>
      <td>加投中是否必须选择</td>
      <td>label</td>
      <td>1:必送 - 2：选送</td>
   </tr>
   <tr>
      <td>secondKillFlag</td>
      <td>加投是否限时</td>
      <td>label</td>
      <td>1：是，0：否</td>
   </tr>
   <tr>
      <td>secondKillEnd</td>
      <td>限时时间</td>
      <td>date</td>
      <td>限时礼品截止时间  年-月-日 时:分:秒</td>
   </tr>
   <tr>
      <td>sendNum</td>
      <td>加投此礼品送数量</td>
      <td>label</td>
      <td>加投此礼品送数量 补可以改变的 直接给用户展示</td>
   </tr>
   <tr>
      <td>remark</td>
      <td>礼品备注说明</td>
      <td>label</td>
      <td>礼品备注说明</td>
   </tr>
   <tr>
      <td>加投包说明（Presents）</td>
   </tr>
   <tr>
      <td>ruleCode</td>
      <td>包code</td>
      <td>label</td>
      <td>用户选择此包内容需要回传</td>
   </tr>
   <tr>
      <td>selectLimit</td>
      <td>包内可选数量</td>
      <td>label</td>
      <td>包内除去必选后剩下的可选择数量</td>
   </tr>
   <tr>
      <td>ruleName</td>
      <td>包名称</td>
      <td>label</td>
      <td>包名称</td>
   </tr>
   <tr>
      <td>ruleRemark</td>
      <td>包备注</td>
      <td>label</td>
      <td>需要展示给用户选择此礼品包的描述。如：只允许线上支付</td>
   </tr>
   <tr>
      <td>车籍地（isShowCarPlace）</td>
   </tr>
   
   <tr>
      <td>isShowCarPlace</td>
      <td>类型</td>
      <td>text</td>
      <td>车籍地</td>
   </tr>
</table>
>
 特约说明：
 
交强特约以engage_tra_开头，有几条特约就会产生几个。商业类似。

 投保礼规则说明：
 
1.用户选择投保礼数量(prePresentNum)<=礼品最大可选数量（maxOptionalNum）

2.用户选择的投保礼数量(prePresentNum)*展示价格（showPrice）<=投保礼可用总费用（AvailableCost）

3.用户选择礼品的礼品类型为立减 （presentType=3），则用户不可以再选择其他礼品

加投礼品规则说明：

1.用户只可以选择一个礼包，选择此包包要清除其他之前选择包的礼品

2.选择礼品不可以为超时礼品（secondKillEnd<当前时间） 

3.当前包用户选择选择礼品数量（不含必送礼品mustSelect=1）<=包内可选数量(selectLimit)

投保礼和加投共同规则：

1.采集信息手机号标记为需要（phoneNoSign=1），必须采集手机号（phoneNo）

2.采集信息账号号标记为需要（accountNumberSign=1），必须采集账号（accountNumber）

3.用户可以不投任何礼品
``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<version>2</version>
			<RequestType>115</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<SellerId>3597746367</SellerId>
			<SendTime>2015-01-29 21:36:51</SendTime>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Sign>FPYu3qzEI42tVASFQxfe8xEdxdC8MT-bNg1fPt2cDdgha2SL7sXUYwyxjZianIucZpcwQqN89nCmFvIJmzZUZoebEGQZmtCt-xaK4wbHxJiyFE1A0zzHD73EOEoZPjHuMMZM-598-281FvgDAwPhpB7FaM6Otov2PRkExigHfNw</Sign>
		<Response>
			<TagsList>
				<Tags type="deadline">
					<Tag>
						<Definition name="type">date</Definition>
						<Definition name="label">商业险起保日期</Definition>
						<Definition name="key">bizBeginDate</Definition>
						<Definition name="value">2015-01-30</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
					<Tag>
						<Definition name="type">date</Definition>
						<Definition name="label">交强险起保日期</Definition>
						<Definition name="key">forceBeginDate</Definition>
						<Definition name="value">2015-01-30</Definition>
						<Definition name="dataUrl"></Definition>
						<Definition name="checkUrl"></Definition>
					</Tag>
				</Tags>
				<Tags type="force">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">forcePremium</Definition>
						<Definition name="label">交强险费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">95000</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleTaxPremium</Definition>
						<Definition name="label">车船税费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">forceTotalPremium</Definition>
						<Definition name="label">交强险总保费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">95000</Definition>
					</Tag>
				</Tags>
				<Tags type="commercial">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">bizTotalPremium</Definition>
						<Definition name="label">商业总保费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">220024</Definition>
					</Tag>
				</Tags>
				<Tags type="subPremium">
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">standardPremium</Definition>
						<Definition name="label">市场总价</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">367464</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">totalPremium</Definition>
						<Definition name="label">网购总价</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">315024</Definition>
					</Tag>
				</Tags>
				<Tags type="engageList"></Tags>
				<Tags type="lifeTablePresents">
					<AvailableCost>600.0</AvailableCost>
					<PresentInfo>
						<Definition name="pkIdEncryption">1ebc155c4cbbd11a</Definition>
						<Definition name="presentName">oe团购礼品1</Definition>
						<Definition name="showPrice">50</Definition>
						<Definition name="maxOptionalNum">12</Definition>
						<Definition name="presentType">0</Definition>
						<Definition name="prePresentNum"></Definition>
						<Definition name="phoneNoSign">0</Definition>
						<Definition name="phoneNo"></Definition>
						<Definition name="accountNumberSign">0</Definition>
						<Definition name="accountNumber"></Definition>
						<Definition name="remark"></Definition>
					</PresentInfo>
				</Tags>
				<Tags type="addPresentPackages"></Tags>
<Tags type="isShowCarPlace">
					<Tag>
						<Definition name="type">hidden</Definition>
						<Definition name="label">车籍地</Definition>
						<Definition name="key">isShowCarPlace 
</Definition>
						<Definition name="value">1</Definition>
						<Definition name="premium"></Definition>
					</Tag>
</Tags>
			</TagsList>
		</Response>
	</Package>
</PackageList>
```
##3.10申请核保接口
申请核保中提交保费计算返回的报文信息，用户选择的商业险套餐和是否投保交强险信息。
###3.10.1请求报文

<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>是否可为空</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>车主信息（ownerInfo）</td>
   </tr>
   <tr>
      <td>ownerName</td>
      <td>车主姓名</td>
      <td>String</td>
      <td>否</td>
      <td>车主姓名（汉字）</td>
   </tr>
   <tr>
      <td>ownerIdNo</td>
      <td>车主证件号码</td>
      <td>String</td>
      <td>否</td>
      <td>身份证号</td>
   </tr>
   <tr>
      <td>ownerMobile</td>
      <td>车主手机</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>ownerEmail</td>
      <td>车主邮箱</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>投保人信息（applicantInfo）</td>
   </tr>
   <tr>
      <td>applicantName</td>
      <td>投保人姓名</td>
      <td>String</td>
      <td>否</td>
      <td>投保人姓名（汉字）</td>
   </tr>
   <tr>
      <td>applicantIdNo</td>
      <td>投保人证件号码</td>
      <td>String</td>
      <td>否</td>
      <td>身份证号</td>
   </tr>
   <tr>
      <td>applicantMobile</td>
      <td>车主手机</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>applicantEmail</td>
      <td>车主邮箱</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>被保险人（insuredInfo）</td>
   </tr>
   <tr>
      <td>insuredName</td>
      <td>被保险人姓名</td>
      <td>String</td>
      <td>否</td>
      <td>被保险人姓名（汉字）</td>
   </tr>
   <tr>
      <td>insuredIdNo</td>
      <td>被保险人证件号码</td>
      <td>String</td>
      <td>否</td>
      <td>身份证号</td>
   </tr>
   <tr>
      <td>insuredMobile</td>
      <td>被保险人手机</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>insuredEmail</td>
      <td>被保险人邮箱</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>配送信息（deliveryInfo）</td>
   </tr>
   <tr>
      <td>addresseeName</td>
      <td>收件人姓名</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>addresseeMobile</td>
      <td>收件人手机</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>sendDate</td>
      <td>配送时间</td>
      <td>String</td>
      <td>否</td>
      <td>配送时间格式YYYY-MM-DD</td>
   </tr>
   <tr>
      <td>addresseeProvince</td>
      <td>省份代码</td>
      <td>String</td>
      <td>否</td>
      <td>由阳光提供见下说明</td>
   </tr>
   <tr>
      <td>addresseeCity</td>
      <td>城市代码</td>
      <td>String</td>
      <td>否</td>
      <td>由阳光提供见下说明</td>
   </tr>
   <tr>
      <td>addresseeTown</td>
      <td>区县代码</td>
      <td>String</td>
      <td>否</td>
      <td>由阳光提供见下说明</td>
   </tr>
   <tr>
      <td>addresseeDetails</td>
      <td>收件地址</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>insuredaddresseeDetails</td>
      <td>被保人身份证地址</td>
      <td>String</td>
      <td>否</td>
      <td>需和身份证一致</td>
   </tr>
   <tr>
      <td>投保礼（lifeTablePresent）和加投（addPresentPackage）</td>
   </tr>
   <tr>
      <td>pkIdEncryptions</td>
      <td>礼品主键加密的集合</td>
      <td>String</td>
      <td>是</td>
      <td>礼品加密主键集合（,隔开）</td>
   </tr>
   <tr>
      <td>prepresentnums</td>
      <td>投保礼礼品数量集合</td>
      <td>String</td>
      <td>是</td>
      <td>（,隔开）和主键要一一对应数量一致</td>
   </tr>
   <tr>
      <td>prePhoneNos</td>
      <td>手机号集合</td>
      <td>String</td>
      <td>是</td>
      <td>（,隔开）和主键要一一对应数量一致，那怕是空也要拼装</td>
   </tr>
   <tr>
      <td>preAccountNumbers</td>
      <td>使用礼品账号集合</td>
      <td>String</td>
      <td>是</td>
      <td>（,隔开）和主键要一一对应数量一致，那怕是空也要拼装</td>
   </tr>
   <tr>
      <td>ruleCode</td>
      <td>加投code</td>
      <td>String</td>
      <td>是</td>
      <td>加投的包code</td>
   </tr>
   <tr>
      <td>第三方生成的订单信息</td>
   </tr>
   <tr>
      <td>TBOrderId</td>
      <td>第三方总订单号</td>
      <td>String</td>
      <td>否</td>
      <td>此订单号在请求中出现3次</td>
   </tr>
   <tr>
      <td>1.第三方总订单号</td>
   </tr>
   <tr>
      <td>2.第三方商业订单号</td>
   </tr>
   <tr>
      <td>3.第三方交强订单号</td>
   </tr>
   <tr>
      <td>车籍地采集（CarThroughCity)</td>
   </tr>
   <tr>
      <td>carPlace</td>
      <td>车籍地采集</td>
      <td>String</td>
      <td>否</td>
      <td>车籍地CODECODE</td>
   </tr>
</table>
配送信息说明：
收件地址为3级联动，具体省市区由阳光提供，用jsonp解决ajax跨域请求

http://chexian.sinosig.com/Net/nCityInfoAction!getRegionListByParentCodeForInterface.action?province=0&encoding=GBK&callback=jsonp1045
``` json
[
    {
        "TITLE": "北京", 
        "CODE": "11"
    }, 
    {
        "TITLE": "天津", 
        "CODE": "12"
    }, 
    {
        "TITLE": "河北省", 
        "CODE": "13"
    }, 
    {
        "TITLE": "山西省", 
        "CODE": "14"
    }, 
    {
        "TITLE": "内蒙古自治区", 
        "CODE": "15"
    }, 
    {
        "TITLE": "辽宁省", 
        "CODE": "21"
    }, 
    {
        "TITLE": "吉林省", 
        "CODE": "22"
    }, 
    {
        "TITLE": "黑龙江省", 
        "CODE": "23"
    }, 
    {
        "TITLE": "上海市", 
        "CODE": "31"
    }, 
    {
        "TITLE": "江苏省", 
        "CODE": "32"
    }, 
    {
        "TITLE": "浙江省", 
        "CODE": "33"
    }, 
    {
        "TITLE": "安徽省", 
        "CODE": "34"
    }, 
    {
        "TITLE": "福建省", 
        "CODE": "35"
    }, 
    {
        "TITLE": "江西省", 
        "CODE": "36"
    }, 
    {
        "TITLE": "山东省", 
        "CODE": "37"
    }, 
    {
        "TITLE": "河南省", 
        "CODE": "41"
    }, 
    {
        "TITLE": "湖北省", 
        "CODE": "42"
    }, 
    {
        "TITLE": "湖南省", 
        "CODE": "43"
    }, 
    {
        "TITLE": "广东省", 
        "CODE": "44"
    }, 
    {
        "TITLE": "广西壮族自治区", 
        "CODE": "45"
    }, 
    {
        "TITLE": "海南省", 
        "CODE": "46"
    }, 
    {
        "TITLE": "重庆市", 
        "CODE": "50"
    }, 
    {
        "TITLE": "四川省", 
        "CODE": "51"
    }, 
    {
        "TITLE": "贵州省", 
        "CODE": "52"
    }, 
    {
        "TITLE": "云南省", 
        "CODE": "53"
    }, 
    {
        "TITLE": "西藏自治区", 
        "CODE": "54"
    }, 
    {
        "TITLE": "陕西省", 
        "CODE": "61"
    }, 
    {
        "TITLE": "甘肃省", 
        "CODE": "62"
    }, 
    {
        "TITLE": "青海省", 
        "CODE": "63"
    }, 
    {
        "TITLE": "宁夏回族自治区", 
        "CODE": "64"
    }, 
    {
        "TITLE": "新疆维吾尔自治区", 
        "CODE": "65"
    }
]
```
其中province值为上级的代码，province=0时取全部省

其中
TITLE ：省市区的名字
CODE：省市区代码 需回传阳光

车籍地信息说明：
车籍地为2级联动，用ajax请求。

http://chexian.sinosig.com/carThroughCityAction/carThroughCityAction_getAllCarThroughCity.action?code=00&encoding=GBK&callback=jsonp1045
其中
CODECNAME：省市区的名字
CODECODE：省市区代码
``` json
[
    {
        "CODECNAME": "北京市", 
        "CODECODE": "11", 
        "id": 1
    }, 
    {
        "CODECNAME": "天津市", 
        "CODECODE": "12", 
        "id": 2
    }, 
    {
        "CODECNAME": "河北省", 
        "CODECODE": "13", 
        "id": 3
    }, 
    {
        "CODECNAME": "山西省", 
        "CODECODE": "14", 
        "id": 4
    }, 
    {
        "CODECNAME": "内蒙古自治区", 
        "CODECODE": "15", 
        "id": 5
    }, 
    {
        "CODECNAME": "辽宁省", 
        "CODECODE": "21", 
        "id": 6
    }, 
    {
        "CODECNAME": "吉林省", 
        "CODECODE": "22", 
        "id": 7
    }, 
    {
        "CODECNAME": "黑龙江省", 
        "CODECODE": "23", 
        "id": 8
    }, 
    {
        "CODECNAME": "上海市", 
        "CODECODE": "31", 
        "id": 9
    }, 
    {
        "CODECNAME": "江苏省", 
        "CODECODE": "32", 
        "id": 10
    }, 
    {
        "CODECNAME": "浙江省", 
        "CODECODE": "33", 
        "id": 11
    }, 
    {
        "CODECNAME": "安徽省", 
        "CODECODE": "34", 
        "id": 12
    }, 
    {
        "CODECNAME": "福建省", 
        "CODECODE": "35", 
        "id": 13
    }, 
    {
        "CODECNAME": "江西省", 
        "CODECODE": "36", 
        "id": 14
    }, 
    {
        "CODECNAME": "山东省", 
        "CODECODE": "37", 
        "id": 15
    }, 
    {
        "CODECNAME": "河南省", 
        "CODECODE": "41", 
        "id": 16
    }, 
    {
        "CODECNAME": "湖北省", 
        "CODECODE": "42", 
        "id": 17
    }, 
    {
        "CODECNAME": "湖南省", 
        "CODECODE": "43", 
        "id": 18
    }, 
    {
        "CODECNAME": "广东省", 
        "CODECODE": "44", 
        "id": 19
    }, 
    {
        "CODECNAME": "广西壮族自治区", 
        "CODECODE": "45", 
        "id": 20
    }, 
    {
        "CODECNAME": "海南省", 
        "CODECODE": "46", 
        "id": 21
    }, 
    {
        "CODECNAME": "重庆市", 
        "CODECODE": "50", 
        "id": 22
    }, 
    {
        "CODECNAME": "四川省", 
        "CODECODE": "51", 
        "id": 23
    }, 
    {
        "CODECNAME": "贵州省", 
        "CODECODE": "52", 
        "id": 24
    }, 
    {
        "CODECNAME": "云南省", 
        "CODECODE": "53", 
        "id": 25
    }, 
    {
        "CODECNAME": "西藏自治区", 
        "CODECODE": "54", 
        "id": 26
    }, 
    {
        "CODECNAME": "陕西省", 
        "CODECODE": "61", 
        "id": 27
    }, 
    {
        "CODECNAME": "甘肃省", 
        "CODECODE": "62", 
        "id": 28
    }, 
    {
        "CODECNAME": "青海省", 
        "CODECODE": "63", 
        "id": 29
    }, 
    {
        "CODECNAME": "宁夏回族自治区", 
        "CODECODE": "64", 
        "id": 30
    }, 
    {
        "CODECNAME": "新疆维吾尔自治区", 
        "CODECODE": "65", 
        "id": 31
    }, 
    {
        "CODECNAME": "台湾省", 
        "CODECODE": "71", 
        "id": 32
    }
]
```
其中
CODECNAME：省市区的名字
CODECODE：省市区代码
``` xml
<?xml version='1.0' encoding='GBK' standalone='yes'?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>120</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<From>MobileCar</From>
			<To>Server</To>
			<AgentCode>W02400654</AgentCode>
			<SendTime>2015-01-29 21:54:09</SendTime>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Request>
			<InputsList>
				<Inputs type='insuredInfo'>
					<input name='insuredIdNo'>130429198601173637</input>
					<input name='insuredEmail'></input>
					<input name='insuredName'>日日通</input>
					<input name='insuredMobile'>18511565612</input>
				</Inputs>
				<Inputs type='applicantInfo'>
					<input name='applicantEmail'></input>
					<input name='applicantIdNo'>130429198601173637</input>
					<input name='applicantMobile'>18511565612</input>
					<input name='applicantName'>日日通</input>
				</Inputs>
				<Inputs type='ownerInfo'>
					<input name='ownerName'>日日通</input>
					<input name='ownerMobile'></input>
					<input name='ownerIdNo'>130429198601173637</input>
					<input name='ownerEmail'>18511565612</input>
				</Inputs>
				<Inputs type='deliverInfo'>
					<input name='sendDate'></input>
					<input name='addresseeName'>日日通</input>
					<input name='addresseeMobile'>18511565612</input>
					<input name='addresseeProvince'>11</input>
					<input name='addresseeCity'>1101</input>
					<input name='addresseeTown'>110101</input>
					<input name='insuredaddresseeDetails'>北京 市辖区 东城区 为人为认为</input>
					<input name='addresseeDetails'>北京 市辖区 东城区 为人为认为</input>
				</Inputs>
				<Inputs type='lifeTablePresent'>
					<input name='preAccountNumbers'></input>
					<input name='pkIdEncryptions'>1ebc155c4cbbd11a</input>
					<input name='prePhoneNos'></input>
					<input name='prepresentnums'>1</input>
				</Inputs>
            
<Inputs type='CarThroughCity'>
	<input name='carPlace'>110000</input>
</Inputs>
			</InputsList>
			<Order>
				<TBOrderId>201501292002149038</TBOrderId>
				<SubOrderList>
					<SubOrder type='force'>
						<TBOrderId>201501292002149038</TBOrderId>
					</SubOrder>
					<SubOrder type='biz'>
						<TBOrderId>201501292002149038</TBOrderId>
					</SubOrder>
				</SubOrderList>
			</Order>
		</Request>
		<Sign>N12O766is77ZIcFPRS_OmTVOFgJ9I7P8rqN2Tu77kfhbhLfAuDrBP3abv4PMKBpuPpT-CayjUXlRkveJVuV14ml5ZZHDW6rY0TrG7RGTh7y9kvTtroM4LuGtFN7LctbXSxyL_rp9lo8J3cO5NyAknSL3_jjDl_iyZMpBozItzLU</Sign>
	</Package>
</PackageList>

```
###3.10.2返回报文
申请核保接口返回三个状态：
1.核保成功，返回投保单号。
2.核保中，在核保流程中
3.核保失败，返回核保失败原因

返回参数
<table>
   <tr>
      <td>TBOrderId</td>
      <td>第三方总订单号</td>
      <td>此订单号在请求中出现3次</td>
   </tr>
   <tr>
      <td>1.第三方总订单号</td>
   </tr>
   <tr>
      <td>2.第三方商业订单号</td>
   </tr>
   <tr>
      <td>3.第三方交强订单号</td>
   </tr>
   <tr>
      <td>ProposalNo</td>
      <td>保险公司投保单号</td>
      <td>1. 商业投保单号 2.交强投保单号</td>
   </tr>
   <tr>
      <td>ItemId</td>
      <td>第三方商品ID</td>
      <td>第三方商品ID</td>
   </tr>
   <tr>
      <td>forcePremium</td>
      <td>交强保费</td>
      <td></td>
   </tr>
   <tr>
      <td>vehicleTaxPremium</td>
      <td>车船税</td>
      <td></td>
   </tr>
   <tr>
      <td>bizTotalPremium</td>
      <td>商业总保费</td>
      <td></td>
   </tr>
   <tr>
      <td>standardPremium</td>
      <td>市场价</td>
      <td></td>
   </tr>
   <tr>
      <td>totalPremium</td>
      <td>网购价</td>
      <td></td>
   </tr>
   <tr>
      <td>IsIdVerifi</td>
      <td>是否需要身份证验证</td>
      <td>1:需要,0:不需要</td>
   </tr>
</table>
``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<version>2</version>
			<RequestType>120</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<SellerId>3597746367</SellerId>
			<SendTime>2015-01-29 21:54:16</SendTime>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Sign>Ii_nCYzOxSznAxpGR-YuJXjyi3fg1pLW4FfUvUkQdF67i3p6ohjCETEevYApxGNYjw3X9bPeG-nu1QUK6mNO3pWaJGuSD0ekXGyOVuMQI8BGoS8C-wXr6b1E5qgloi_VuavuAvZUd_is67IOhYmgVAvZfoHGsEqZiEcWkAcLoXs</Sign>
		<Response>
			<TagsList>
				<Tags>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">forcePremium</Definition>
						<Definition name="label">交强险费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">95000</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleTaxPremium</Definition>
						<Definition name="label">车船税费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">bizTotalPremium</Definition>
						<Definition name="label">商业总保费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">220024</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">totalPremium</Definition>
						<Definition name="label">网购总价</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">315024</Definition>
					</Tag>
				</Tags>
			</TagsList>
			<Order>
				<TBOrderId>201501292002149038</TBOrderId>
				<SubOrderList>
					<SubOrder type="biz">
						<TBOrderId>201501292002149038</TBOrderId>
						<ProposalNo>T085105092015000115</ProposalNo>
					</SubOrder>
					<SubOrder type="force">
						<TBOrderId>201501292002149038</TBOrderId>
						<ProposalNo>T085105072015000113</ProposalNo>
					</SubOrder>
				</SubOrderList>
			</Order>
            <IsIdVerifi>1</IsIdVerifi>
		</Response>
	</Package>
</PackageList>
```
其他参考获取报价表单（100）接口。

##3.11配送信息修改接口
申请核保中提交修改配送信息接口返回的报文信息。
###3.11.1请求报文

<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>是否可为空</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>配送信息（deliveryInfo）</td>
   </tr>
   <tr>
      <td>addresseeName</td>
      <td>收件人姓名</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>addresseeMobile</td>
      <td>收件人手机</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>sendDate</td>
      <td>配送时间</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>addresseeProvince</td>
      <td>省份代码</td>
      <td>String</td>
      <td>否</td>
      <td>由阳光提供见下说明</td>
   </tr>
   <tr>
      <td>addresseeCity</td>
      <td>城市代码</td>
      <td>String</td>
      <td>否</td>
      <td>由阳光提供见下说明</td>
   </tr>
   <tr>
      <td>addresseeTown</td>
      <td>区县代码</td>
      <td>String</td>
      <td>否</td>
      <td>由阳光提供见下说明</td>
   </tr>
   <tr>
      <td>addresseeDetails</td>
      <td>收件地址</td>
      <td>String</td>
      <td>否</td>
      <td></td>
   </tr>
   <tr>
      <td>insuredaddresseeDetails</td>
      <td>被保人身份证地址</td>
      <td>String</td>
      <td>否</td>
      <td>需和身份证一致</td>
   </tr>
</table>

配送信息说明：
收件地址为3级联动，具体省市区由阳光提供，用jsonp解决ajax跨域请求.

http://chexian.sinosig.com/Net/nCityInfoAction!getRegionListByParentCodeForInterface.action?province=0&encoding=GBK&callback=jsonp1045

其中province值为上级的代码，province=0时取全部省
```json
[
    {
        "TITLE": "北京", 
        "CODE": "11"
    }, 
    {
        "TITLE": "天津", 
        "CODE": "12"
    }, 
    {
        "TITLE": "河北省", 
        "CODE": "13"
    }, 
    {
        "TITLE": "山西省", 
        "CODE": "14"
    }, 
    {
        "TITLE": "内蒙古自治区", 
        "CODE": "15"
    }, 
    {
        "TITLE": "辽宁省", 
        "CODE": "21"
    }, 
    {
        "TITLE": "吉林省", 
        "CODE": "22"
    }, 
    {
        "TITLE": "黑龙江省", 
        "CODE": "23"
    }, 
    {
        "TITLE": "上海市", 
        "CODE": "31"
    }, 
    {
        "TITLE": "江苏省", 
        "CODE": "32"
    }, 
    {
        "TITLE": "浙江省", 
        "CODE": "33"
    }, 
    {
        "TITLE": "安徽省", 
        "CODE": "34"
    }, 
    {
        "TITLE": "福建省", 
        "CODE": "35"
    }, 
    {
        "TITLE": "江西省", 
        "CODE": "36"
    }, 
    {
        "TITLE": "山东省", 
        "CODE": "37"
    }, 
    {
        "TITLE": "河南省", 
        "CODE": "41"
    }, 
    {
        "TITLE": "湖北省", 
        "CODE": "42"
    }, 
    {
        "TITLE": "湖南省", 
        "CODE": "43"
    }, 
    {
        "TITLE": "广东省", 
        "CODE": "44"
    }, 
    {
        "TITLE": "广西壮族自治区", 
        "CODE": "45"
    }, 
    {
        "TITLE": "海南省", 
        "CODE": "46"
    }, 
    {
        "TITLE": "重庆市", 
        "CODE": "50"
    }, 
    {
        "TITLE": "四川省", 
        "CODE": "51"
    }, 
    {
        "TITLE": "贵州省", 
        "CODE": "52"
    }, 
    {
        "TITLE": "云南省", 
        "CODE": "53"
    }, 
    {
        "TITLE": "西藏自治区", 
        "CODE": "54"
    }, 
    {
        "TITLE": "陕西省", 
        "CODE": "61"
    }, 
    {
        "TITLE": "甘肃省", 
        "CODE": "62"
    }, 
    {
        "TITLE": "青海省", 
        "CODE": "63"
    }, 
    {
        "TITLE": "宁夏回族自治区", 
        "CODE": "64"
    }, 
    {
        "TITLE": "新疆维吾尔自治区", 
        "CODE": "65"
    }
]
```
其中
TITLE ：省市区的名字
CODE：省市区代码 需回传阳光
``` xml
<?xml version='1.0' encoding='GBK' standalone='yes'?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>135</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<From>MobileCar</From>
			<To>Server</To>
			<AgentCode>W02400654</AgentCode>
			<SendTime>2015-01-29 21:54:09</SendTime>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Request>
			<InputsList>
				<Inputs type='deliverInfo'>
					<input name='sendDate'></input>
					<input name='addresseeName'>日日通</input>
					<input name='addresseeMobile'>18511565612</input>
					<input name='addresseeProvince'>11</input>
					<input name='addresseeCity'>1101</input>
					<input name='addresseeTown'>110101</input>
					<input name='insuredaddresseeDetails'>北京 市辖区 东城区 为人为认为</input>
					<input name='addresseeDetails'>北京 市辖区 东城区 为人为认为</input>
				</Inputs>
		</Request>
		<Sign>N12O766is77ZIcFPRS_OmTVOFgJ9I7P8rqN2Tu77kfhbhLfAuDrBP3abv4PMKBpuPpT-CayjUXlRkveJVuV14ml5ZZHDW6rY0TrG7RGTh7y9kvTtroM4LuGtFN7LctbXSxyL_rp9lo8J3cO5NyAknSL3_jjDl_iyZMpBozItzLU</Sign>
	</Package>
</PackageList>

```
###3.11.2返回报文
修改配送信息接口返回两个状态：
1、	修改成功，返回status为100。
2、	修改失败，返回失败信息
修改成功报文;
``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<version>2</version>
			<RequestType>135</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<SellerId>3597746367</SellerId>
			<SendTime>2015-01-29 21:54:16</SendTime>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Sign>Ii_nCYzOxSznAxpGR-YuJXjyi3fg1pLW4FfUvUkQdF67i3p6ohjCETEevYApxGNYjw3X9bPeG-nu1QUK6mNO3pWaJGuSD0ekXGyOVuMQI8BGoS8C-wXr6b1E5qgloi_VuavuAvZUd_is67IOhYmgVAvZfoHGsEqZiEcWkAcLoXs</Sign>
		<Response>
		</Response>
	</Package>
</PackageList>

修改失败报文：
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<version>2</version>
			<RequestType>135</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<SellerId>3597746367</SellerId>
			<SendTime>2015-01-29 21:54:16</SendTime>
			<Status>400</Status>
			<ErrorMessage>亲，您选择的配送信息修改失败了!!!</ErrorMessage>
		</Header>
		<Sign>Ii_nCYzOxSznAxpGR-YuJXjyi3fg1pLW4FfUvUkQdF67i3p6ohjCETEevYApxGNYjw3X9bPeG-nu1QUK6mNO3pWaJGuSD0ekXGyOVuMQI8BGoS8C-wXr6b1E5qgloi_VuavuAvZUd_is67IOhYmgVAvZfoHGsEqZiEcWkAcLoXs</Sign>
		<Response>
		</Response>
	</Package>
</PackageList>
```
##3.12支付检查接口
在支付前第三方调用保险公司支付检查接口，验证投保单是否可以支付，验证参数通过第三方订单号，商业险投保单号和交强险投保单号，如果是单保一个产品，只有一个投保单号。

###3.12.1请求报文
<table>
   <tr>
      <td>TBOrderId</td>
      <td>第三方总订单号</td>
      <td>此订单号在请求中出现3次</td>
   </tr>
   <tr>
      <td>1.第三方总订单号</td>
   </tr>
   <tr>
      <td>2.第三方商业订单号</td>
   </tr>
   <tr>
      <td>3.第三方交强订单号</td>
   </tr>
   <tr>
      <td>ProposalNo</td>
      <td>保险公司投保单号</td>
      <td>1. 商业投保单号 2.交强投保单号</td>
   </tr>
   <tr>
      <td>ItemId</td>
      <td>第三方商品ID</td>
      <td>第三方商品ID</td>
   </tr>
</table>
``` xml
<?xml version='1.0' encoding='GBK' standalone='yes'?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>125</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<From>MobileCar</From>
			<To>Server</To>
			<AgentCode>W02400654</AgentCode>
			<SendTime>2015-01-29 21:54:17</SendTime>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Request>
			<Order>
				<TBOrderId>201501292002149038</TBOrderId>
				<SubOrderList>
					<SubOrder type='force'>
						<TBOrderId>201501292002149038</TBOrderId>
					</SubOrder>
					<SubOrder type='biz'>
						<TBOrderId>201501292002149038</TBOrderId>
					</SubOrder>
				</SubOrderList>
			</Order>
		</Request>
		<Sign>YCW8U_0QebBdwd_2KrZ7yDB1q8E-Z72Ps52J-az4-08OywCJoNdLlKoWoHXpiC3OJ_CmUzIW_pBIZosYIluWIJPHiTbn8qs2CLzcEiiqWJCAw41VD9GLPA-F1KVMTbTqi7qe9FjZXoYWggR5uVZo5KHPG47ITjKYNIR0ltrKtXE</Sign>
	</Package>
</PackageList>
```
###3.12.2返回报文
在支付检查接口中，保险公司检查是否可以支付时，如果发现已经不能支付，比如超过支付时间，脱保等，可以重新核保，返回给客户支付，也可以返回无法支付状态
1.成功，可以支付
2.确认中，保险公司可能在重新核保，需要核保通过后会
3.失败，无法支付

``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
	<Package>
		<Header>
			<version>2</version>
			<RequestType>125</RequestType>
			<InsureType>100</InsureType>
			<SessionId>201501292002149038</SessionId>
			<SellerId>3597746367</SellerId>
			<SendTime>2015-01-29 21:54:18</SendTime>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
		</Header>
		<Sign>PVF-R6JE-DqYF4olA0oButP2nhukhFDrYYKSZaCocfRE4VB7gepEWdjJuIjLttIeef4bX_lhDHSVIMIe532NgEzAsHCPk1fdcSWNOITzYFCMF2rttD9Q_V78aRqRDcybTAfOieBUoEwQoVOgzQWwVoGvvAC5OSH6fY37RyiG14k</Sign>
		<Response>
			<TagsList>
				<Tags>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">forcePremium</Definition>
						<Definition name="label">交强险费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">95000</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">vehicleTaxPremium</Definition>
						<Definition name="label">车船税费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">0</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">bizTotalPremium</Definition>
						<Definition name="label">商业总保费</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">220024</Definition>
					</Tag>
					<Tag>
						<Definition name="type">label</Definition>
						<Definition name="key">totalPremium</Definition>
						<Definition name="label">网购总价</Definition>
						<Definition name="value"></Definition>
						<Definition name="premium">315024</Definition>
					</Tag>
				</Tags>
			</TagsList>
			<Order>
				<TBOrderId>201501292002149038</TBOrderId>
				<Premium>315024</Premium>
				<PayNo></PayNo>
				<SubOrderList>
					<SubOrder type="biz">
						<TBOrderId>201501292002149038</TBOrderId>
						<ProposalNo>T085105092015000115</ProposalNo>
						<Premium>220024</Premium>
					</SubOrder>
					<SubOrder type="force">
						<TBOrderId>201501292002149038</TBOrderId>
						<ProposalNo>T085105072015000113</ProposalNo>
						<Premium>95000</Premium>
					</SubOrder>
				</SubOrderList>
			</Order>
		</Response>
	</Package>
</PackageList>
```
其他参考获取报价表单（100）接口。
##3.13获取验证码接口(126)
在120中新增加节点IsIdVerifi,如果120返回报文中,IsIdVerifi为1则直接调用127接口进行验证即可,无需调用此接口,只有在短信未发送到用户手机或用户多次输入验证码错误,需要重新获取验证码的时候才调用此接口.
###3.13.1请求报文
Request节点中 无参数
``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList>
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>126</RequestType>
			<InsureType>100</InsureType>
			<SessionId>SMG2014911334938732400740</SessionId>
			<AgentCode>W02400652</AgentCode>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
			<SendTime>2014-09-11 13:49:05</SendTime>
		</Header>
		<Request>
		</Request>	<Sign>KVZnM_TQMvDUcGQDI9Zs7kEnQZvoZiapyeoxm9gDS6MdQwPghuvI3LvjM7Gp42mY9pssmG-ounM-_Y2VfdH0u8z-b6QVJxO5b7npv5GSRxvvkRKxhWxxbxg1glcVAnnb-zum_JFqz-PCclLX4E6t-g2Q_6rDlGG-UoeoSfQ0Mr8
		</Sign>
	</Package>
</PackageList>

```
###3.13.2返回报文
<table>
   <tr>
      <td>字段</td>
      <td>名称</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>ResponseCode</td>
      <td>获取验证码结果</td>
      <td>success获取成功,其它为失败</td>
   </tr>
   <tr>
      <td>ResponseMessage</td>
      <td>获取验证码信息</td>
      <td>失败原因</td>
   </tr>
</table>
``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList>
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>126</RequestType>
			<InsureType>100</InsureType>
			<SessionId>SMG2014911334938732400740</SessionId>
			<AgentCode>W02400652</AgentCode>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
			<SendTime>2014-09-11 13:49:05</SendTime>
		</Header>
	<Sign>euPBGXG9-1MNLQ3jw62rFuY4_GPc-M86_TnqO5u8fD2MJ9tpZdUXEW2AdEKsoYNw5myFrw4boNOJsdZH43Lh2E3IKEQAa5QAJ8kJouKhgDoMFtN_JWEN3Xj0C_WjqTqX3Eu-lygHbphMgBVFPpcY-54WskjbMCx3lJJFgIwl2Ug</Sign>
	<Response>
		<ResponseCode>success</ResponseCode>
        <ResponseMessage>失败原因</ResponseMessage>
	</Response>
	</Package>
</PackageList>

```
##3.14保存验证码（127）
<table>
   <tr>
      <td>字段</td>
      <td>名称</td>
      <td>类型</td>
      <td>大小</td>
      <td>必传</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>IssueCode</td>
      <td>验证码</td>
      <td>字符</td>
      <td></td>
      <td>Y</td>
      <td>用户输入的验证码</td>
   </tr>
</table>
###3.14.1请求报文
``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList>
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>127</RequestType>
			<InsureType>100</InsureType>
			<SessionId>SMG2014911334938732400740</SessionId>
			<AgentCode>W02400652</AgentCode>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
			<SendTime>2014-09-11 13:49:05</SendTime>
		</Header>
		<Request>
			<IssueCode>14658</IssueCode> 
		</Request>	<Sign>KVZnM_TQMvDUcGQDI9Zs7kEnQZvoZiapyeoxm9gDS6MdQwPghuvI3LvjM7Gp42mY9pssmG-ounM-_Y2VfdH0u8z-b6QVJxO5b7npv5GSRxvvkRKxhWxxbxg1glcVAnnb-zum_JFqz-PCclLX4E6t-g2Q_6rDlGG-UoeoSfQ0Mr8
		</Sign>
	</Package>
</PackageList>
```
###3.14.2返回报文(与126返回报文相同)
<table>
   <tr>
      <td>字段</td>
      <td>名称</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>ResponseCode</td>
      <td>获取验证码结果</td>
      <td>success获取成功,其它为失败</td>
   </tr>
   <tr>
      <td>ResponseMessage</td>
      <td>获取验证码信息</td>
      <td>失败原因</td>
   </tr>
</table>
``` xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList>
	<Package>
		<Header>
			<Version>2</Version>
			<RequestType>126</RequestType>
			<InsureType>100</InsureType>
			<SessionId>SMG2014911334938732400740</SessionId>
			<AgentCode>W02400652</AgentCode>
			<SellerId>3597746367</SellerId>
			<Status>100</Status>
			<ErrorMessage></ErrorMessage>
			<SendTime>2014-09-11 13:49:05</SendTime>
		</Header>
		<Sign>euPBGXG9-1MNLQ3jw62rFuY4_GPc-M86_TnqO5u8fD2MJ9tpZdUXEW2AdEKsoYNw5myFrw4boNOJsdZH43Lh2E3IKEQAa5QAJ8kJouKhgDoMFtN_JWEN3Xj0C_WjqTqX3Eu-lygHbphMgBVFPpcY-54WskjbMCx3lJJFgIwl2Ug</Sign>
	<Response>
		<ResponseCode>success</ResponseCode>
        <ResponseMessage>失败原因</ResponseMessage>
	</Response>
	</Package>
</PackageList>

```
##3.15承保接口
支付信息(Payment)：
<table>
   <tr>
      <td>字段</td>
      <td>名称</td>
      <td>类型</td>
      <td>大小</td>
      <td>必传</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>TBOrderId</td>
      <td>第三方订单号</td>
      <td>字符</td>
      <td></td>
      <td>Y</td>
      <td></td>
   </tr>
   <tr>
      <td>PayOrderId</td>
      <td>支付平台订单号</td>
      <td>字符</td>
      <td></td>
      <td>Y</td>
      <td></td>
   </tr>
   <tr>
      <td>CheckPayNo</td>
      <td>支付流水号</td>
      <td>字符</td>
      <td></td>
      <td>Y</td>
      <td>形如</td>
   </tr>
   <tr>
      <td>B5000M386466139260786</td>
   </tr>
   <tr>
      <td>T1100P205700608474850</td>
   </tr>
   <tr>
      <td>PayType</td>
      <td>支付商类型</td>
      <td>字符</td>
      <td></td>
      <td>Y</td>
      <td>如：01。注：支付宝是01，快钱02等。其他支付类型待确定。</td>
   </tr>
   <tr>
      <td>PartnerId</td>
      <td>支付时所用的支付商的对应的合作者ID</td>
      <td>字符</td>
      <td></td>
      <td>Y</td>
      <td>如：2088601078742391，和PayType相对应。如果PayType为01。PartnerId则是阳光在支付宝平台账户的Id。</td>
   </tr>
   <tr>
      <td>PayTime</td>
      <td>支付时间</td>
      <td>时间</td>
      <td></td>
      <td>Y</td>
      <td>yyyy-MM-dd HH:mm:ss</td>
   </tr>
   <tr>
      <td>PayMoney</td>
      <td>支付金额</td>
      <td>数值</td>
      <td></td>
      <td>Y</td>
      <td>以分为单位</td>
   </tr>
   <tr>
      <td>AccountDate</td>
      <td>账务日期</td>
      <td>时间</td>
      <td></td>
      <td>Y</td>
      <td>同支付日期 yyyy-MM-dd</td>
   </tr>
   <tr>
      <td>AlipayBuyerAccount</td>
      <td>支付帐号</td>
      <td>字符</td>
      <td></td>
      <td>N</td>
      <td>如：zyhuai@wo.com.cn</td>
   </tr>
   <tr>
      <td>AlipayBuyerId</td>
      <td>支付帐号ID</td>
      <td>字符</td>
      <td></td>
      <td>N</td>
      <td>如：2088002566423974</td>
   </tr>
   <tr>
      <td>TBOrderId</td>
      <td>第三方总订单号</td>
      <td>字符</td>
      <td></td>
      <td>Y</td>
      <td>如：415468917875548</td>
   </tr>
   <tr>
      <td>ProposalNo</td>
      <td>保险公司保单号</td>
      <td>字符</td>
      <td></td>
      <td>Y</td>
      <td>如：T341005072013000023</td>
   </tr>
   <tr>
      <td>Premium</td>
      <td>保费</td>
      <td>字符</td>
      <td></td>
      <td>Y</td>
      <td>如：339059</td>
   </tr>
   <tr>
      <td>ItemId</td>
      <td>第三方商品ID</td>
      <td>字符</td>
      <td></td>
      <td>Y</td>
      <td>如：2000036117417</td>
   </tr>
</table>

###3.15.1请求报文
```  xml
<?xml version="1.0" encoding="GBK" standalone="yes"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Package>
    <Header>
      <Version>2</Version>
      <InsureType></InsureType>
      <RequestType>130/RequestType>
      <SessionId>33763110891482088102118850914</SessionId>
      <From>taobao</From>
      <To>2051078519</To>
      <AgentCode>W03210001</AgentCode>
      <SendTime>2013-04-24 18:28:42</SendTime>
      <Status></Status>
      <ErrorMessage></ErrorMessage>
    </Header>
    <Request>
      <Payment>
        <TBOrderId>3376311089148</TBOrderId>
        <PayOrderId>2013022600001000910000069408</PayOrderId>
        <CheckPayNo>B5000M386466139260786</CheckPayNo>
        <PayType>01</PayType>
        <PartnerId>2088601078742391</PartnerId>
        <PayTime>2013-02-26 10:43:19</PayTime>
        <PayMoney>1000000</PayMoney>
        <AccountDate>2013-02-26 10:43:19</AccountDate>
        <AlipayBuyerAccount>13524726578</AlipayBuyerAccount>
        <AlipayBuyerId>2088102118850914</AlipayBuyerId>
      </Payment>
      <Order>
        <TBOrderId>3376311089148</TBOrderId>
        <Premium>339059</Premium> 
        <SubOrderList>
		  <SubOrder type="biz">
            <TBOrderId>3376311089149</TBOrderId>
            <ItemId>26790524332</ItemId>
            <Premium>139059</Premium>
            <ProposalNo>8828900000144888</ProposalNo>
          </SubOrder>
		  <SubOrder type="force">
            <TBOrderId>3376311089139</TBOrderId>
            <ItemId>26790524332</ItemId>
            <Premium>200000</Premium>
            <ProposalNo>8828900000144889</ProposalNo>
          </SubOrder>
        </SubOrderList>
      </Order>
</Request>
    <Sign></Sign>
  </Package>
</PackageList>
```
###3.15.2返回报文
返回参数
<table>
   <tr>
      <td>TBOrderId</td>
      <td>第三方总订单号</td>
      <td>此订单号在请求中出现3次</td>
   </tr>
   <tr>
      <td>1.第三方总订单号</td>
   </tr>
   <tr>
      <td>2.第三方商业订单号</td>
   </tr>
   <tr>
      <td>3.第三方交强订单号</td>
   </tr>
   <tr>
      <td>ProposalNo</td>
      <td>保险公司投保单号</td>
      <td>1. 商业投保单号 2.交强投保单号</td>
   </tr>
   <tr>
      <td>PolicyNo</td>
      <td>保险公司保单号</td>
      <td>保险公司保单号</td>
   </tr>
</table>
``` xml
<?xml version="1.0" encoding="GBK"?>
<PackageList xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Package>
    <Header>
      <Version>2</Version>
      <InsureType>100</InsureType>
      <RequestType>130</RequestType>
      <SessionId>33763110891482088102118850914</SessionId>
      <From>taobao</From>
      <To>2051078519</To>
      <SendTime>2013-04-24 18:28:42</SendTime>
      <Status>2</Status>
      <ErrorMessage>2</ErrorMessage>
    </Header>
    <Sign></Sign>
    <Response>
      <Order>
        <TBOrderId>3376311089148</TBOrderId>
        <SubOrderList>
          <SubOrder type="biz">
          <TBOrderId>3376311089149</TBOrderId>
          <ProposalNo>8828900000144888</ProposalNo>
          <PolicyNo>8828900000144888</PolicyNo>
        </SubOrder>
        <SubOrder type="force">
          <TBOrderId>3376311089139</TBOrderId>
          <ProposalNo>8828900000144888</ProposalNo>
          <PolicyNo>8828900000144889</PolicyNo>
        </SubOrder>
      </SubOrderList>
     </Order>
   </Response>
  </Package>
</PackageList>
```
其他参考获取报价表单（100）接口。
#4.附录表

##4.1附录表1 投保输入项
<table>
   <tr>
      <td>字段</td>
      <td>描述</td>
      <td>类型</td>
      <td>是否为空</td>
      <td>备注</td>
   </tr>
   <tr>
      <td>cityCode</td>
      <td>城市代码</td>
      <td>Label</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>车辆信息（vehicleInfo）</td>
   </tr>
   <tr>
      <td>licenseNo</td>
      <td>车牌号</td>
      <td>Text</td>
      <td></td>
      <td>新车为空</td>
   </tr>
   <tr>
      <td>noLicenseFlag</td>
      <td>新车未上牌</td>
      <td>Checkbox</td>
      <td></td>
      <td>1：新车，0：非新车</td>
   </tr>
   <tr>
      <td>firstRegisterDate</td>
      <td>车辆初等日期</td>
      <td>Date</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>vehicleId</td>
      <td>车辆Id</td>
      <td>Hidden</td>
      <td></td>
      <td>客户车型Id，</td>
   </tr>
   <tr>
      <td>vehicleModelName</td>
      <td>车辆品牌型号</td>
      <td>Text</td>
      <td></td>
      <td>根据客户输入的信息到保险公司查询车辆信息</td>
   </tr>
   <tr>
      <td>vehicleFrameNo</td>
      <td>车架号</td>
      <td>text</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>engineNo</td>
      <td>发动机号</td>
      <td>text</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>transferFlag</td>
      <td>是否过户车</td>
      <td>Radio</td>
      <td></td>
      <td>1：是，0：否</td>
   </tr>
   <tr>
      <td>transferDate</td>
      <td>过户日期</td>
      <td>Date</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>vehicleInvoiceDate</td>
      <td>购车发票日期</td>
      <td>Date</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>runCardCertificateDate</td>
      <td>行驶证发证日期</td>
      <td>Date</td>
      <td></td>
      <td>行驶证发证时间</td>
   </tr>
   <tr>
      <td>bizBeginDate</td>
      <td>商业险保险起期</td>
      <td>Date</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>forceBeginDate</td>
      <td>交强险保险起期</td>
      <td>Date</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>车主信息（ownerInfo）</td>
   </tr>
   <tr>
      <td>ownerName</td>
      <td>车主姓名</td>
      <td>Label</td>
      <td></td>
      <td>车主姓名</td>
   </tr>
   <tr>
      <td>ownerIdType</td>
      <td>车主证件类型</td>
      <td>Select</td>
      <td></td>
      <td>车主证件类型</td>
   </tr>
   <tr>
      <td>ownerIdNo</td>
      <td>车主证件号码</td>
      <td>Text</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>ownerGender</td>
      <td>车主性别</td>
      <td>Radio</td>
      <td></td>
      <td>证件类型非身份证时需要</td>
   </tr>
   <tr>
      <td>ownerBirthday</td>
      <td>车主生日</td>
      <td>Date</td>
      <td></td>
      <td>证件类型非身份证时需要</td>
   </tr>
   <tr>
      <td>ownerAge</td>
      <td>车主年龄</td>
      <td>Text</td>
      <td></td>
      <td>备用字段</td>
   </tr>
   <tr>
      <td>ownerMobile</td>
      <td>车主手机</td>
      <td>Text</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>ownerEmail</td>
      <td>车主邮箱</td>
      <td>Text</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>投保人信息（applicantInfo）</td>
   </tr>
   <tr>
      <td>applicantName</td>
      <td>投保人姓名</td>
      <td>Label</td>
      <td></td>
      <td>投保人姓名</td>
   </tr>
   <tr>
      <td>applicantIdType</td>
      <td>投保人证件类型</td>
      <td>Select</td>
      <td></td>
      <td>投保人证件类型</td>
   </tr>
   <tr>
      <td>applicantIdNo</td>
      <td>投保人证件号码</td>
      <td>Text</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>applicantGender</td>
      <td>投保人性别</td>
      <td>Radio</td>
      <td></td>
      <td>证件类型非身份证时需要</td>
   </tr>
   <tr>
      <td>applicantBirthday</td>
      <td>投保人生日</td>
      <td>Date</td>
      <td></td>
      <td>证件类型非身份证时需要</td>
   </tr>
   <tr>
      <td>applicantMobile</td>
      <td>车主手机</td>
      <td>Text</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>applicantEmail</td>
      <td>车主邮箱</td>
      <td>Text</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>被保险人（insuredInfo）</td>
   </tr>
   <tr>
      <td>insuredName</td>
      <td>被保险人姓名</td>
      <td>Label</td>
      <td></td>
      <td>被保险人姓名</td>
   </tr>
   <tr>
      <td>insuredIdType</td>
      <td>被保险人证件类型</td>
      <td>Select</td>
      <td></td>
      <td>被保险人证件类型</td>
   </tr>
   <tr>
      <td>insuredIdNo</td>
      <td>被保险人证件号码</td>
      <td>Text</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>insuredGender</td>
      <td>被保险人性别</td>
      <td>Radio</td>
      <td></td>
      <td>证件类型非身份证时需要</td>
   </tr>
   <tr>
      <td>insuredBirthday</td>
      <td>被保险人生日</td>
      <td>Date</td>
      <td></td>
      <td>证件类型非身份证时需要</td>
   </tr>
   <tr>
      <td>insuredMobile</td>
      <td>被保险人手机</td>
      <td>Text</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>insuredEmail</td>
      <td>被保险人邮箱</td>
      <td>Text</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>配送信息（deliveryInfo）</td>
   </tr>
   <tr>
      <td>addresseeName</td>
      <td>收件人姓名</td>
      <td></td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>addresseeMobile</td>
      <td>收件人手机</td>
      <td></td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>sendDate</td>
      <td>配送时间</td>
      <td></td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>invoice</td>
      <td>发票抬头</td>
      <td>text</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>addresseeProvince</td>
      <td>省份代码</td>
      <td>Select</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>addresseeCity</td>
      <td>城市代码</td>
      <td>Select</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>addresseeTown</td>
      <td>区县代码</td>
      <td>select</td>
      <td></td>
      <td></td>
   </tr>
   <tr>
      <td>addresseeDetails</td>
      <td>收件地址</td>
      <td>Text</td>
      <td></td>
      <td></td>
   </tr>
</table>
#5.特别说明
注意事项
1：所有报文交互中涉及保费和支付金额等节点都是以分为单位，
如保费是100元，报文的节点是10000
``` xml
<Tag>
            <Definition name="type">label</Definition>
            <Definition name="key">covOd</Definition>
            <Definition name="lable">车险损失综合险</Definition>
            <Definition name="value">50万</Definition>
<Definition name="premium">10000</Definition>
<Definition name="disable">0</Definition>
<Definition name="check"></Definition>
            <Definition name="dataUrl"><![CDATA[]]></Definition>
            <Definition name="checkUrl"><![CDATA[]]></Definition>
          </Tag>
      <Tag>
                  <Definition name="type">label</Definition>
                  <Definition name="label">商业总保费</Definition>
                  <Definition name="key">bizTotalPremium</Definition>
                  <Definition name="value">139059</Definition>
                  <Definition name="premium">139059</Definition>
               </Tag>
               <Tag>
                  <Definition name="type">label</Definition>
                  <Definition name="label">市场总价</Definition>
                  <Definition name="key">standardPremium</Definition>
                  <Definition name="value">428210</Definition>
                  <Definition name="premium">428210</Definition>
               </Tag>
               <Tag>
                  <Definition name="type">label</Definition>
                  <Definition name="label">网购总价</Definition>
                  <Definition name="key">totalPremium</Definition>
                  <Definition name="value">230644</Definition>
                  <Definition name="premium">230644</Definition>
               </Tag>
```
如下节点，都是以分为单位。
``` xml
<Definition name="premium">10000</Definition>

<Premium>230643</Premium>

<payMoney>1000000<payMoney>
```
