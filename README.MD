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

认证密钥介绍
------
`[AUTHKEY]`字段为接口加密数据定位符,使用`OpenSSL RSA4096`加密生成的下载用户唯一权限标识符<br>
无`AUTHKEY`将导致无法请求接口返回`400`错误,`AUTHKEY`包含唯一信息,请求过多将导致`AUTHKEY`加入黑名单<br>
由于加入`AUTHKEY`保护,用户下载的规则文件除自己外其他人将无法使用,极大程度抑制再分发和盗取接口行为<br>
`AUTHKEY`与`IP`等信息绑定,使用`AutoGroup`将导致无法使用,网络请求`Header`可以看到`IP`及`TimeStamp`信息<br>
请将`async.be`认证服务器加入代理列表,所以请务必保证IP一致!

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
|默认规则列表|https://raw.githubusercontent.com/CloudGateRules/RuleList/master/Default.json|
|开发规则列表|https://raw.githubusercontent.com/CloudGateRules/RuleList/master/Developers.json|

规则列表语法
------
规则列表支持更多参数,也就是在`SUFFIX`后面追加其他参数,如有需要可以在`SUFFIX`后面添加`\|[参数]`
比如说`KEYWORD`条目`[^example]\|[DIRECT]\|[force-remote-dns]`,后面可以增加`force-remote-dns`
`Rewrite`及`Header Rewrite`规则条目需要进行转义否则会出现错误!
|规则列表语法|功能描述|
|----|-----|
|`[SUFFIX]\|[Example.com]\|[DIRECT]`|SUFFIX规则条目|
|`[DOMAIN]\|[Example.com]\|[DIRECT]`|DOMAIN规则条目|
|`[^Example]\|[DIRECT]\|[force-remote-dns]`|KEYWORD规则条目|
|`[PROCESS]\|[Example]\|[Proxy]`|PROCESS-NAME规则条目|
|`[URLREGEX]\|[\\Example]\|[DIRECT]`|URL-REGEX规则条目|
|`[USERAGENT]\|[Example\*]\|[DIRECT]`|USER-AGENT规则条目|
|`[IPCIDR6]\|[2006::/16]\|[DIRECT]`|IP-CIDR6规则条目|
|`[10.0.0.0/8]\|[DIRECT]`|IPCIDR规则条目|
|`[\$FINAL]\|[Proxy]`|Other规则条目|
|`syria.sy = 127.0.0.1`|Host规则条目|
|`r1---sn-i3b7kn7d.googlevideo.com`|YouTube规则条目|
|`^(http|https):\/\/E\\d{2}.xample.com - reject`|Rewrite规则条目|
|`^(http|https):\/\/example.com header-del DNT`|HeaderRewrite规则条目|
|`example.com$$`|MITM规则条目|
|`<<SKIP`|跳过规则条目|
|`[AUTHKEY]`|AUTHKEY定位符|
|`<<Example`|注释内容条目|
|`[!Example]`|规则块行首|

规则列表字段
------
|规则列表块|功能描述|
|----|-----|
|`Info`|规则列表描述条目|
|`General`|General规则条目|
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
