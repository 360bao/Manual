#1.	平台简介
##1.1	使命和目标

360Bao平台是华谊保险销售公司的互联网战略平台。公司通过360Bao平台为保险公司显著增加业绩，为互联网公司提供重要的用户流量和业务数据变现，为公司自身积累海量用户资源和数据，从而为电销和精英代理人平台提供数据基础。360Bao是华谊打造场景化保险生态的核心平台，起到连接其他各方资源的作用。
##1.2	整体架构
![整体架构](https://github.com/360bao/Manual/blob/master/1.png)
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
##3.2报文格式
##3.3接口详细
##3.4获取发动机和车架号
##3.5基础信息接口
##3.6车型选择接口
##3.7获取报价接口
##3.8修改报价接口
##3.9保存保费接口
##3.10申请核保接口
##3.11配送信息修改接口
##3.12支付检查接口
##3.13获取验证码接口(126)
##3.14保存验证码（127）
##3.15承保接口
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
