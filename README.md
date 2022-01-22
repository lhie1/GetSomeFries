# 🍟 GetSomeFries
整点薯条  
又不是不能用  
Telegram讨论组:[🍟 整点薯条](https://t.me/GetSomeFries)

---

> 目录
- [🍟 GetSomeFries](#-getsomefries)
- [🍟 Cloudflare DNS](#-cloudflare-dns)
  - [简介](#简介)
  - [功能列表](#功能列表)
  - [todo](#todo)
  - [使用方式](#使用方式)
  - [图片说明](#图片说明)
  - [安装链接](#安装链接)
    - [正式版](#正式版)
    - [🧪测试版](#测试版)
- [🍟 Cloudflare WARP](#-cloudflare-warp)
  - [简介](#简介-1)
  - [功能列表](#功能列表-1)
  - [todo](#todo-1)
  - [使用方式](#使用方式-1)
  - [安装链接](#安装链接-1)
    - [🧪测试版](#测试版-1)
- [🍟 Disney Plus](#-disney-plus)
  - [简介](#简介-2)
  - [功能列表](#功能列表-2)
  - [todo](#todo-2)
  - [安装链接](#安装链接-2)
    - [🧪测试版](#测试版-2)
- [🍟 Netflix](#-netflix)
  - [简介](#简介-3)
  - [功能列表](#功能列表-3)
  - [todo](#todo-3)
  - [使用方式](#使用方式-2)
  - [安装链接](#安装链接-3)
    - [🧪试验版，随时可能修改/删除](#试验版随时可能修改删除)
- [鸣谢](#鸣谢)


---

# 🍟 Cloudflare DNS
## 简介
  * Cloudflare DNS记录管理及自动更新DDNS

  * 注:
    * 本插件使用[my-ip.io](https://www.my-ip.io/api)的api进行外部IP探测，请注意相关域名`api4.my-ip.io`和`api6.my-ip.io`的分流，以免获取到的是节点出口IP

## 功能列表
  * 自定义更新特定类型和内容记录
  * 自动更新未指定IP的A记录和AAAA记录
  * 通知(有，但不是完全有，有来自Cloudflare的错误和信息通知)
  * BoxJs集成
  * 持久化储存(有，但不是完全有，没有做反写功能)

## todo
  * 并行处理优化(阶段性完工，除非有更好的方法)
  * web面板(暂不开工)

## 使用方式
* 配合`BoxJs`及订阅使用
  * 安装`BoxJs`插件:
    * Loon: [boxjs.rewrite.loon.plugin](https://github.com/chavyleung/scripts/raw/master/box/rewrite/boxjs.rewrite.loon.plugin "BoxJs")
    * Quantumult X: [boxjs.rewrite.quanx.conf](https://github.com/chavyleung/scripts/raw/master/box/rewrite/boxjs.rewrite.quanx.conf "BoxJs")
    * Surge: [boxjs.rewrite.surge.sgmodule](https://github.com/chavyleung/scripts/raw/master/box/rewrite/boxjs.rewrite.surge.sgmodule "BoxJs")
  * 导入本项目订阅: [fries.boxjs.json](./box/fries.boxjs.json?raw=true "整点薯条")
  * 在`应用`-`整点薯条`-`Cloudflare`中填写您的Cloudflare DNS信息
    * 验证方式: 
      * API 令牌: 在[我的个人资料的'API 令牌'页面](https://dash.cloudflare.com/profile/api-tokens "API 令牌 | Cloudflare")的`API 令牌`生成，注意生成的令牌要有需管理区域的`DNS编辑`权限(推荐使用预设的`编辑区域 DNS`模版)
      * API 密钥: 在[我的个人资料的'API 令牌'页面](https://dash.cloudflare.com/profile/api-tokens "API 令牌 | Cloudflare")的`API 密钥`的`Global API Key`获取，注意此密钥默认拥有全部权限，不建议使用此方式
    * 验证内容: 即`API令牌`内容或`API 密钥`内容，注意`API 密钥`需分两行填写，第一行密钥，第二行邮箱
    * 区域ID: 在`区域`页面右下角的`API`小节的`区域 ID`，单击复制
    * 区域名称: 即域名
    * DNS记录: 格式范例如下，一行一个记录，A记录和AAAA记录如果不带内容则自动获取外部IP，如果带内容则以内容为准
      ```
      id=记录ID&type=类型&name=名称&content=内容&ttl=TTL&priority=优先级&proxied=是否代理
      id=12345ABCDE&type=MX&name=mail&content=127.0.0.1&ttl=1&priority=10&proxied=true
      type=A&name=www&proxied=false
      type=AAAA&name=ipv6&proxied=false
      ```
* 配合Surge模块的`argument`字段使用:
  * 使用[@baranwang](https://github.com/baranwang)的[Surge模块Argument代理](https://sgmodule-argument-proxy.vercel.app/)直接生成带配置的专属模块[使用说明](https://github.com/baranwang/sgmodule-argument-proxy#readme)
  * 暂不支持多记录，推荐使用BoxJs设置
  * 格式如下:
      ```
      argument=Token=令牌&zone_id=区域ID&zone_name=区域名称&dns_records_id=记录ID&dns_records_name=记录名称&dns_records_type=记录类型&dns_records_ttl=TTL&dns_records_priority=记录优先级&dns_records_proxied=是否代理
      ```
      例如:
      ```
      argument=Token=1234567ABCDEFG&zone_id=1234567ABCDEFG&zone_name=exapmle.com&dns_records_id=1234567ABCDEFG&dns_records_name=www&dns_records_proxied=false
      ```
      或
      ```
      argument=Token=1234567ABCDEFG&zone_id=1234567ABCDEFG&dns_records_name=www&dns_records_type=A&dns_records_proxied=false
      ```

## 图片说明
|  获取令牌  | 获取区域 ID | DNS记录添加 |
| :---- | :---- | :---- |
| 验证内容  | 区域ID | DNS记录  |
| 即API令牌内容或API 密钥内容 <br> 注意API 密钥需分两行填写，第一行密钥，第二行邮箱，如**示例2**  | 在区域页面右下角的API小节的区域 ID，单击复制 | **格式：** id=记录ID&type=类型&name=名称&content=内容&ttl=TTL&priority=优先级&proxied=是否代理 <br> **解读：** type为记录类型，name为解析子域名名称，proxied为是否开启代理（小云朵） <br> 如果你想要解析的域名为test.luca.xyz，解析的ip为1.2.3.4，那么name就是test，content就是1.2.3.4 <br> 如果你不知道一些参数的信息，可以只填写记录类型和记录名称以及指定的内容，如**示例2** |
|**API 令牌示例(单行)：** <br> 8M7wS6hCpXVc-DoRnPPY_UCWPgy8aea4Wy6kCe5T <br> **API 密钥示例(两行)：** <br> 1234567893feefc5f0q5000bfo0c38d90bbeb <br> example@example.com <br> **用户服务密钥示例(单行)：** <br> v1.0-e24fd090c02efcfecb4de8f4ff246fd5c75b48946fdf0ce26c59f91d0d90797b-cfa33fe60e8e34073c149323454383fc9005d25c9b4c502c2f063457ef65322eade065975001a0b4b4c591c5e1bd36a6e8f7e2d4fa8a9ec01c64c041e99530c2-07b9efe0acd78c82c8d9c690aacb8656d81c369246d7f996a205fe3c18e9254a|**示例：**  <br> 372e67954025e0ba6aaa6d586b9e0b59|**示例1：** <br> id=12345ABCDE&type=MX&name=mail&content=127.0.0.1&ttl=1&priority=10&proxied=true <br> **示例2：** <br> type=A&name=test&content=1.2.3.4&proxied=false|
|![获取令牌](./img/Cloudflare%20-%201.How.to.get.API.token.PNG?raw=true "Cloudflare - 1.How to get API token")|![获取区域 ID](./img/Cloudflare%20-%202.How.to.get.zone.id.JPG?raw=true "Cloudflare - 2.How to get zone id")|![DNS记录添加](./img/Cloudflare%20-%203.How.to.fill.in.the.form.JPG?raw=true "Cloudflare - 3.How to fill in the form")|

## 安装链接
### 正式版
  * Loon:
    * [Cloudflare_DNS.plugin](./plugins/Cloudflare_DNS.plugin?raw=true "🍟 Cloudflare DNS")
  * Quantumult X:
    * 下载脚本[Cloudflare_DNS.js](./js/Cloudflare_DNS.js?raw=true "🍟 Cloudflare DNS")并保存至`Quantumult X`的`Scripts`文件夹下
      * 修改配置文件，在`[task_local]`段添加如下内容：
      ```
      event-network https://github.com/VirgilClyne/GetSomeFries/blob/main/js/Cloudflare_DNS.js?raw=true, tag=Cloudflare DNS, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Cloudflare.png, enabled=true
      */10 * * * * https://github.com/VirgilClyne/GetSomeFries/blob/main/js/Cloudflare_DNS.js?raw=true, tag=Cloudflare DNS, img-url=https://raw.githubusercontent.com/Koolson/Qure/master/IconSet/Color/Cloudflare.png, enabled=true
      ```
  * Surge:
    * [Cloudflare_DNS.sgmodule](./sgmodule/Cloudflare_DNS.sgmodule?raw=true "🍟 Cloudflare DNS")
### 🧪测试版
  * Surge:
    * [Cloudflare_DNS.beta.sgmodule](./sgmodule/Cloudflare_DNS.beta.sgmodule?raw=true "🍟 Cloudflare DNS")

---

# 🍟 Cloudflare WARP
## 简介
  * Cloudflare WARP 注册管理及转换WireGuard配置

  * 注:
    * 自动邀请新用户刷WARP+流量”功能还没写

## 功能列表
  * BoxJs集成
  * 持久化储存(有，但不是完全有，没有做反写功能)
  * 通知(有，但不是完全有，有来自Cloudflare的错误和信息通知)
  * 注册新账户
  * 注册新账户(用自定义密钥对)并生成WireGuard配置文件
  * 注册新设备(注册ID)
  * 重绑定许可证(许可证 & 注册ID)
  * 查询账户信息(创建日期/剩余流量/邀请人数等)
  * 查询设备配置(设备名称/设备类型/创建日期/活动状态等)
  * 自定义客户端设备类型


## todo
  * 自动邀请新用户刷WARP+流量”功能还没写

## 使用方式
* 配合`BoxJs`及订阅使用
  * 安装`BoxJs`插件:
    * Loon: [boxjs.rewrite.loon.plugin](https://github.com/chavyleung/scripts/raw/master/box/rewrite/boxjs.rewrite.loon.plugin "BoxJs")
    * Quantumult X: [boxjs.rewrite.quanx.conf](https://github.com/chavyleung/scripts/raw/master/box/rewrite/boxjs.rewrite.quanx.conf "BoxJs")
    * Surge: [boxjs.rewrite.surge.sgmodule](https://github.com/chavyleung/scripts/raw/master/box/rewrite/boxjs.rewrite.surge.sgmodule "BoxJs")
  * 导入本项目订阅: [fries.boxjs.json](./box/fries.boxjs.json?raw=true "整点薯条")
  * 在`应用`-`整点薯条`-`Cloudflare`中填写您的Cloudflare WARP信息
      1. BoxJs要先填写Loon\quanX\Surge的API地址 不然看不到日志输出
      2. 打开Cloudflare WARP模块
    * 注册新账户(用自定义密钥对)并生成WireGuard配置文件
      1. 运行方式选择`注册新账户(用自定义密钥对)并生成WireGuard配置文件`
      2. 在WireGuard客户端中`新建隧道`-`生成密钥对`
      3. 将WireGuard生成的私钥和公钥填写到BoxJs中的`WireGuard: 私钥`和`WireGuard: 公钥`
      4. 页面最下方点`保存`
      5. 点击Cloudflare WARP页面右上角的`圆箭头按钮`运行
      6. 记录下日志中提供的信息，导入或填入WireGuard
    * 重绑定许可证(许可证 & 注册ID)
      1. 运行方式选择`重绑定许可证(许可证 & 注册ID)`
      2. 填写你要换绑的`WARP: 许可证(账户)/License(Account)`
      3. 填写你要绑定到此许可证的`WARP: 注册ID(设备ID/客户端ID/配置文件ID)`
      4. 填写此注册ID对应的token到`WARP: 验证内容/Verify Content`
      5. 点击页面下方的`保存`
      6. 点击Cloudflare WARP页面右上角的`圆箭头按钮`运行
      7. 记录下日志中提供的信息

## 安装链接
### 🧪测试版
  * BoxJs:
    * [fries.boxjs.json](./box/fries.boxjs.json?raw=true "整点薯条")

  * Surge:
    * [Cloudflare_1.1.1.1_with_WARP.beta.sgmodule](./sgmodule/Cloudflare_1.1.1.1_with_WARP.beta.sgmodule?raw=true "🍟 Cloudflare 1.1.1.1 APP with WARP Client Info")
    * 此模块仅查询1.1.1.1 APP的配置信息,增删改请用上方BoxJs订阅或APP客户端
      * Surge安装后，重新打开一次1.1.1.1的APP，即可在通知中看到配置信息，在Surge的日志中也会输出完整配置文件内容

---

# 🍟 Disney Plus
## 简介
  * 无视地区线路限制，强制加载特定地区内容

  * 注:
    * 凑合用,翻车别找我
    * 至少相关线路属于任意可用地区，不会被直接拒绝连接

## 功能列表
  * 修改部分地区检测
  * 显示指定地区内容
  * 修改内容可用状态

## todo
  * 我咋知道

## 安装链接
### 🧪测试版
  * Surge:
    * [Disney_Plus.beta.sgmodule](./sgmodule/Disney_Plus.beta.sgmodule?raw=true "🍟 Redirect Disney Plus Region to 🇸🇬SG")
      * 此测试模块强制指定为新加坡区

---

# 🍟 Netflix
## 简介
  * 自定义部分Netflix功能

  * 注:
    * 试验性质
    * 翻车别找我
    * 部分设置可能改了也没效果

## 功能列表
  * 强制解除地区限制(可能改了也没用)
  * 启用VTT字幕(对于Web和Android等平台,还要指定VTT字幕服务器)
  * 启用AirPlay
    * 需要正经支持Airplay视频投屏的设备如`Apple TV`,`Sony`、`LG`、`三星`电视，国产破解Airplay的兼容方案就别想了
  * 允许Widevine DRM播放
  * 其他设置内容详见[iOS平台全部设置项列表](https://github.com/VirgilClyne/GetSomeFries/wiki/iOS平台全部设置项列表)
  * 修改当前CDN所属地区
  * 修改当前IP地址(可能改了也没用)
  * 修改当前IP地址是否已有用户(可能改了也没用，关系到多人共用IP封非自制内容的问题)

## todo
  * 我咋知道

## 使用方式
* 配合`BoxJs`及订阅使用
  * 安装`BoxJs`插件:
    * Loon: [boxjs.rewrite.loon.plugin](https://github.com/chavyleung/scripts/raw/master/box/rewrite/boxjs.rewrite.loon.plugin "BoxJs")
    * Quantumult X: [boxjs.rewrite.quanx.conf](https://github.com/chavyleung/scripts/raw/master/box/rewrite/boxjs.rewrite.quanx.conf "BoxJs")
    * Surge: [boxjs.rewrite.surge.sgmodule](https://github.com/chavyleung/scripts/raw/master/box/rewrite/boxjs.rewrite.surge.sgmodule "BoxJs")
  * 导入本项目订阅: [fries.boxjs.json](./box/fries.boxjs.json?raw=true "整点薯条")
  * 在`应用`-`整点薯条`-`Netflix`中填写需要修改Netflix的信息
  * `配置：功能内容`段落示例如下
    ```
    hideAccountPaymentEnabledOnBuild=50.0.0
    isAccountProfileLinkEnabled=true
    allowWidevinePlayback=true
    airPlayDisabledEnabledOnBuild=50.0.0
    preferRichWebVTTOverImageBasedSubtitle=true
    requestRichWebVTTAsExperimental=true
    previewsWebVttStyleUrl=https:\/\/webvtt-s.nflxext.com\/35\/PreviewsWebVTTStyle.plist
    iPhoneWebVttStyleUrl=https:\/\/webvtt-s.nflxext.com\/35\/iPhoneWebVTTStyle.plist
    iPadWebVttStyleUrl=https:\/\/webvtt-s.nflxext.com\/35\/iPadWebVTTStyle.plist
    ```
* 配合Surge模块的`argument`字段使用:
  * 使用[@baranwang](https://github.com/baranwang)的[Surge模块Argument代理](https://sgmodule-argument-proxy.vercel.app/)直接生成带配置的专属模块[使用说明](https://github.com/baranwang/sgmodule-argument-proxy#readme)
  * 暂不支持多记录，推荐使用BoxJs设置
  * 格式如下:
      ```
      argument=懒得写
      ```
      例如:
      ```
      argument=geolocation_policy=ALLOW&geolocation_country=SG&onfig_allowWidevinePlayback=true&config_airPlayDisabledEnabledOnBuild=50.0.0&config_preferRichWebVTTOverImageBasedSubtitle=true&config_reuseAVPlayerEnabledOnBuild=0&config_nfplayerReduxEnabledOnBuild=50.0.0
      ```

## 安装链接
### 🧪试验版，随时可能修改/删除
  * Loon:
    * [Netflix.beta.plugin](./plugins/Netflix.beta.plugin?raw=true "🍟 Netflix")
  * Quantumult X:
    * [Netflix.beta.qxrewrite](./qxrewrite/Netflix.beta.qxrewrite?raw=true "🍟 Netflix")
  * Surge:
    * [Netflix.beta.sgmodule](./sgmodule/Netflix.beta.sgmodule?raw=true "🍟 Netflix")

---

# 鸣谢
  * 排名不分先后  
[@chavyleung](https://github.com/chavyleung)  
[@NobyDa](https://github.com/NobyDa)  
[@zZPiglet](https://github.com/zZPiglet)  
[@yichahucha](https://github.com/yichahucha)  
[@Peng-YM](https://github.com/Peng-YM)  
[@app2smile](https://github.com/app2smile)  
[@Loon0x00](https://github.com/Loon0x00)  
[@Tartarus2014](https://github.com/Tartarus2014)  
[@Hackl0us](https://github.com/Hackl0us)  
