# AddDcdnIpaDomain {#doc_api_dcdn_AddDcdnIpaDomain .reference}

调用AddDcdnIpaDomain添加IP4层应用加速域名，一次只能提交一个加速域名。

 **调用该接口前，请您注意：** 

-   创建加速域名之前，必须先开通全站加速IPA服务。
-   加速域名必须已备案完成。
-   源站内容，如果不在阿里云平台上，需要审核，审核工作会在下一工作日前完成。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=dcdn&api=AddDcdnIpaDomain&type=RPC&version=2018-01-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AddDcdnIpaDomain|系统规定参数。取值：AddDcdnIpaDomain。

 |
|DomainName|String|是|example.com|需要接入全站加速IPA的域名。支持泛域名，以点号（.）开头，例如：.example.com。

 |
|Sources|String|是|\[\{"content":"1.1.1.1","type":"ipaddr","priority":"20","port":80,"weight":"15"\}\]|回源地址列表。

 |
|CheckUrl|String|否|yourCheckUrl|检测URL。

 |
|ResourceGroupId|String|否|123|资源组ID，不传时，自动补全默认资源组ID。

 |
|Scope|String|否|domestic|取值范围：**domestic**、**overseas**、**global**，默认为**domestic**。

 国际用户、国内L3及以上用户设置有效。

 |
|TopLevelDomain|String|否|yourTopLevelDomain|顶级接入域。

 |

Sources各字段含义

|参数

|类型

|是否必选

|描述

|
|----|----|------|----|
|type

|String

|是

|源站类型。\*\*ipaddr\*\*：IP源站；\*\*domain\*\*：域名源站；\*\*oss\*\*：不支持oss。

|
|content

|String

|是

|回源地址，可以是\*\*IP\*\*或\*\*域名\*\*。

|
|port

|Integer

|是

|自定义端口，范围：\*\*0\*\*~\*\*65535\*\*。

|
|priority

|String

|否

|源站地址对应的优先级，支持\*\*20\*\*和\*\*30\*\*，默认\*\*20\*\*。\*\*20\*\*是主，\*\*30\*\*是备。

|
|weight

|String

|否

|回源权重，\*\*100\*\*以内，默认\*\*10\*\*。

|

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|0AEDAF20-4DDF-4165-8750-47FF9C1929C9|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}
http://dcdn.aliyuncs.com?Action=AddDcdnIpaDomain
&DomainName=example.com
&Sources=[{"content":"1.1.1.1","type":"ipaddr","priority":"20","port":80}]
&<公共请求参数>
```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<AddDcdnIpaDomainResponse>
	  <RequestId>0AEDAF20-4DDF-4165-8750-47FF9C1929C9</RequestId>
</AddDcdnIpaDomainResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"RequestId":"0AEDAF20-4DDF-4165-8750-47FF9C1929C9"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidDomainName.Malformed|The specified DomainName is invalid.|域名格式错误。|
|400|InvalidSource.Content.Malformed|The specified Source Content is invalid.|源站信息错误，请重新填写。|
|400|MissingSource.Content|The Source Content must be specified.|Source Content必填，请填写后重试。|
|400|MissingSource.Type|The Source Type must be specified.|Source Type必填，请填写后重试。|
|400|InvalidSource.Type.Malformed|The specified Source Type is invalid.|Source Type格式错误，请重新填写。|
|400|InvalidSource.Priority.Malformed|The specified Source Priority is invalid.|Source Priority格式错误，请填写正确的格式。|
|400|InvalidScope.Malformed|The specified Scope is invalid.|Scope错误，请填写正确的Scope后重新请求。|
|400|SourceIp.Exceed|The maximum number of back-to-origin IP addresses is exceeded.|回源ip个数超过限额。|
|400|InvalidCertificate|The specified certificate format is invalid.|Certificate格式错误，请填写正确的Certificate后重试。|
|400|InvalidCertificate.TooLong|The maximum length of the certificate is exceeded.|Certificate长度超过限制。|
|400|CheckSourceHealthFailed|Error checking the security. Provide the valid origin site information.|安全检查失败，请提供正确的源站信息。|
|400|ExtensiveAndAllBothExist|A wildcard domain name and a domain name with an all. prefix cannot be both specified.|泛域名与all.开头域名不能同时存在。|
|400|CdnTypeNotSupportExtensiveDomain|Wildcard domain names are not supported.|不支持泛域名。|
|400|ExtensiveAndSpecificDomainConflict|The wildcard domain name overlaps a domain name at the same level.|泛域名和同级精确域名互斥，请重新添加。|
|400|InvalidResourceGroupId.Malformed|The specified ResourceGroupId is invalid.|ResourceGroupId错误，请填写正确的ResourceGroupId。|
|400|DomainReserved|The root domain of your domain is reserved by another account. Submit a ticket to contact customer support.|该域名的根域已经被其他账号占用，若需要新增提交工单处理。|
|400|InvalidDomainNameLevel|The alicdn.com domain supports a maximum of three levels of domain.|alicdn.com最多支持三级域名。|
|400|TopLevelDomain.NotFound|The specified TopLevelDomain does not exist.|顶级接入域不存在。|
|400|EntityNotExists.ResourceGroup|The resource group does not exist.|该资源组不存在。|
|400|InvalidStatus.ResourceGroup|The current status of the resource group does not support this operation.|资源组当前状态不允许进行此操作。|
|400|NotInternationRealIdentity|Real-name registration is required for services offered in Mainland China.|根据中华人民共和国法律规定，在中国境内购买使用信息服务的用户需要进行实名登记。|
|400|InvalidSource.Port.Malformed|The source port is empty, or it is outside the range 0-65535.|源站端口号为空，或者不在0-65535范围内。|
|403|DcdnIpaServiceNotFound|The DCDN IPA service has not been activated.|没有开通Dcdn Ipa服务。|

访问[错误中心](https://error-center.aliyun.com/status/product/dcdn)查看更多错误码。

