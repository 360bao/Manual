##1.	平台简介
###1.1	使命和目标

360Bao平台是华谊保险销售公司的互联网战略平台。公司通过360Bao平台为保险公司显著增加业绩，为互联网公司提供重要的用户流量和业务数据变现，为公司自身积累海量用户资源和数据，从而为电销和精英代理人平台提供数据基础。360Bao是华谊打造场景化保险生态的核心平台，起到连接其他各方资源的作用。
###1.2	整体架构
![平台整体架构 ](https://github.com/360bao/Manual/blob/master/1.png)
###1.3协议规则
合作伙伴接入360Bao平台，调用JS API遵循以下基本规则：

- •	采用POST方法提交
- •	提交和返回数据都为JSON
- •	统一采用UTF-8字符编码

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
   <tr>
      <td></td>
   </tr>
</table>

##2.	JS SDK

```json
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
