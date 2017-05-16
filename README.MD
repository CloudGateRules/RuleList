规则列表
===========================
该项目是通过规则列表实时生成生成多种规则配置文件,规则列表使用`JSON`格式编写,并需要使用规则列表语法

规则列表介绍
------
规则列表通过方括号包裹字段通过竖号分隔字段,YouTube和Host列表块无需使用方括号包裹!<br>
规则列表处理时会自动按照不同的规则格式生成相应的规则,规则列表处理时自动忽略掉不需要的部分!<br>
通过规则列表生成`Surge/A.BIG.T/Shadowrocket/Potatso/Potatso2/Cross/Hosts`等规则配置文件<br>
更新规则时也只需要更新规则列表即可,不需要关心不同规则格式的编写的困扰!<br>
由于一些原因,目前只支持`Basic/Advanced`规则<br>

鉴权令牌介绍
------
`<TOKEN>`字段为接口加密随机值替换定位符,使用OpenSSL RSA4096加密生成的下载用户唯一鉴权标识符<br>
无TOKEN将导致无法请求接口返回400错误,TOKEN包含唯一信息,请求过多将导致TOKEN与IP加入黑名单<br>
由于加入`TOKEN`保护,用户下载的分享规则文件除自己外其他人将无法使用,极大程度抑制再分发和盗取接口行为<br>
由于TOKEN与IP等信息绑定,所以使用`AutoGroup`将导致无法使用,在网络请求`Debugging Cookie`里可以看到IP及时间戳<br>
或者可以尝试将`async.be`和`burpsuite.applinzi.com`鉴权服务器加入代理列表<br>
`TOKEN`由下载服务器`async.be`生成,`TOKEN`由接口服务器`burpsuite.applinzi.com`检测,所以请务必保证IP一致!

用户使用方法
------
在`Advanced`规则末尾找到`List`键名对应键值,填入规则列表URL地址即可!<br>
`"Other":{"List":"https://raw.githubusercontent.com/BurpSuite/RuleList/master/Default.json"}`<br>
<br>
在`Basic`规则是在网址后面加上`List={规则列表地址}`即可!<br>
`https://async.be/Rule/Basic/Surge?List=https://raw.githubusercontent.com/BurpSuite/RuleList/master/Default.json`

规则列表信息
------
|规则列表名称|规则列表地址|
|----|-----|
|默认规则列表|https://raw.githubusercontent.com/BurpSuite/RuleList/master/Default.json|
|开发规则列表|https://raw.githubusercontent.com/BurpSuite/RuleList/master/Developers.json|

规则列表语法
------
|规则列表语法|功能描述|
|----|-----|
|`<TOKEN>`|TOKEN字段,防止接口被拷贝盗用|
|`<<Example`|注释字段|
|`[!Example]`|规则块字段|
|`[$Example]`|其他字段|
|`[^Example]`|关键词字段|
|`[SUFFIX]\|[apple.com]\|[DIRECT]`|每个规则字段使用方括号包裹|
|`example.com\\/example`|正则表达式需要转义|
|`[IPCIDR6]`|等价IP-CIDR6参数|
|`[URLREGEX]`|等价URL-REGEX参数|
|`[USERAGENT]`|等价USER-AGENT参数|
|`[DOMAIN]\|[apple.com]\|[DIRECT]\|[]`|DOMAIN第四个字段为预留字段适配新参数,可以为空,可以为多个参数|
|`[SUFFIX]\|[apple.com]\|[DIRECT]\|[]`|SUFFIX第四个字段为预留字段适配新参数,可以为空,可以为多个参数|
|`[^example]\|[DIRECT]\|[force-remote-dns]`|KEYWORD第三个字段为预留字段适配新参数,可以为空,可以为多个参数|
|`[10.0.0.0/8]\|[DIRECT]\|[no-resolve]`|IP-CIDR第三个字段为预留字段,可以为空,可以为多个参数|
|`[URLREGEX]\|[\\Example]\|[DIRECT]\|[]`|URL-REGEX第四个字段为预留字段适配新参数,可以为空,可以为多个参数|
|`[USERAGENT]\|[Example*]\|[DIRECT]\|[]`|USER-AGENT第四个字段为预留字段适配新参数,可以为空,可以为多个参数|
|`[IPCIDR6]\|[2007::/16]\|[REJECT]\|[]`|IP-CIDR6第四个字段为预留字段适配新参数,可以为空,可以为多个参数|

规则列表字段
------
|规则列表块|功能描述|
|----|-----|
|`Info`|规则列表描述信息字段|
|`General`|General规则块|
|`Apple`|用户选择SUFFIX规则块\|Proxy将替换为用户选择的规则组|
|`Advanced`|用户选择SUFFIX规则块\|Proxy将替换为用户选择的规则组|
|`Basic`|用户选择SUFFIX规则块\|Proxy将替换为用户选择的规则组|
|`DIRECT`|DIRECT规则块|
|`REJECT`|REJECT规则块|
|`KEYWORD`|用户选择SUFFIX规则块\|Proxy将替换为用户选择的规则组|
|`URLREGEX`|用户选择SUFFIX规则块\|Proxy将替换为用户选择的规则组|
|`USERAGENT`|用户选择SUFFIX规则块\|Proxy将替换为用户选择的规则组|
|`IPCIDR6`|用户选择SUFFIX规则块\|Proxy将替换为用户选择的规则组|
|`IPCIDR`|用户选择SUFFIX规则块\|Proxy将替换为用户选择的规则组|
|`Other`|用户选择SUFFIX规则块\|Proxy将替换为用户选择的规则组|
|`Host`|Host规则块|
|`YouTube`|YouTube规则块|
|`Rewrite`|Rewrite规则块|
|`MITM`|MITMHostName规则块|
|`SKIP`|跳过不开启选项规则块|
