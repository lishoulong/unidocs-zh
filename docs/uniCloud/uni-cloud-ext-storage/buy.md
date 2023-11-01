## 开通@open

1. 登录[uniCloud web控制台](https://unicloud.dcloud.net.cn/)
2. 选择一个服务空间
3. 选择左侧扩展存储菜单，开通

![](https://qiniu-web-assets.dcloud.net.cn/unidoc/zh/3707/uni-cloud-ext-storage/431.png)

**注意**

- 一个空间只能开通一个扩展存储，实例会自动和当前服务空间绑定
- 开通前保证金账户余额需≥200元，扩展存储按量余额需>0元

## 费用说明@fee

### 计费项

|资源项								|单位	|售价（元）	|
|--										|--		|--					|
|ecdn-302流量（国内）		|GB		|0.18				|
|ecdn-302流量（海外）		|GB		|0.18				|
|ecdn-sdk流量（国内）		|GB		|0.18				|
|ecdn-sdk流量（海外）		|GB		|0.18				|
|cdn-普通流量（国内）	|GB		|0.18				|
|cdn-普通流量（海外）	|GB		|0.18				|
|oss存储容量					|GB/天|0.0043			|
|oss外网流量					|GB		|0.18				|
|cdn回源流量					|GB		|0.18				|
|get请求次数					|万次	|0.01				|
|put请求次数					|万次	|0.01				|

### 充值保证金

扩展存储是按量计费的，使用需要先充值200元保证金

在uniCloud web控制台前往【费用中心】-【按量余额充值】充值保证金（若保证金账户余额≥200元则无需充值）

![](https://qiniu-web-assets.dcloud.net.cn/unidoc/zh/3707/429.png)

### 充值余额

在uniCloud web控制台前往【费用中心】-【按量余额充值】充值扩展存储余额

![](https://qiniu-web-assets.dcloud.net.cn/unidoc/zh/3707/428.png)

## 如何使用？

如何使用扩展存储，请参考[扩展存储API](uniCloud/uni-cloud-ext-storage/api.md)