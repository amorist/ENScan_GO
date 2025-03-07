
# ENScan_GO

ENScanGo 是现有开源项目 [ENScan](https://github.com/wgpsec/ENScan) 的GO升级版本

**仅用于学习参考，请勿遵守相关法律规定**

![](https://shields.io/badge/Go-1.17-green?logo=go)



<p align="center">
  <a href="https://github.com/wgpsec/ENScan_GO">
    <img src="README/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">ENScan的Go版本实现</h3>
  <p align="center">
    解决遇到的各种针对国内企业信息收集难题
    <br />
    <a href="https://github.com/wgpsec/ENScan_GO"><strong>探索更多Tricks »</strong></a>
    <br />
    <br />
    <a href="https://github.com/wgpsec/ENScan_GO/releases">下载可执行文件</a>
    ·
    <a href="https://github.com/wgpsec/ENScan_GO/issues">反馈Bug</a>
    ·
    <a href="https://github.com/wgpsec/ENScan_GO/issues">提交需求</a>
  </p>

**使用本程序可能导致账号被封，请谨慎操作**




### 功能列表

 - 使用支持以下API，并支持合并数据导出
    - 爱企查
    - 天眼查
    - 阿拉丁
    - 酷安
    - 七麦数据

 - 查询信息
    - ICP备案
    - APP
    - 微博
    - 微信公众号
    - 控股公司
    - 供应商
    - 客户信息
    - 小程序
    - 控股X的公司的以上所有信息
    - ...
 - 通过APK市场收集使用信息

### 使用指南

命令行参数如下
```
  -branch 查询分支机构（分公司）信息
  -delay int 每个请求延迟（S）-1为随机延迟1-5S (default 1)
  -f string 包含公司关键词的文件一行一个
  -field string 获取字段信息 eg website
  -i string 公司ID（根据你查询的type不同ID不同）
  -invest int 投资比例 eg 100
  -invest-rd 投资比例不明确（可能不是完全控股）
  -is-branch 查询分支机构（分公司）详细信息ICP备案APP等
  -is-debug 是否显示debug详细信息
  -is-group 查询集团信息
  -is-merge 是否合并导出
  -is-pid 批量查询文件是否为PID
  -n string 公司名称关键词 eg 小米
  -o string 结果输出的文件夹位置(可选)
  -type string 收集渠道信息（默认爱企查）eg qcc (default "aqc") all为收集全部
  -v    版本信息
```

字段支持:

```
"icp", "weibo", "wechat", "app", "weibo", "job", "wp", "copyright"
v0.0.4 开始 website已改为icp！！！
```

#### 快速使用

首先需要生成配置文件，在目录下会生成 `config.yaml` 的配置文件

```shell
./ENScanPublic_amd64_linux -v
```

配置信息如下

```yaml
version: 0.1 			# 请勿修改版本号！
common:
  output: ""            # 导出文件位置
  field: [ ]			# 查询字段 如["website"]
cookies:
  aiqicha: ''           # 爱企查   Cookie
  tianyancha: ''        # 天眼查   Cookie
  qcc: ''               # 企查查   Cookie
  aldzs: ''             # 阿拉神灯 Token
  xlb: ''               # 小蓝本   Token

```

生成配置文件之后即可开始信息收集

Eg：快速收集小米相关信息 默认收集：企业基本信息、微博、ICP备案、APP、微信公众号

```shell
./ENScanPublic_amd64_linux -n 小米
```

![image-20220106220045213](README/image-20220106220045213.png)

你可能会遇到如下情况，需要填写Cookie 以爱企查（默认收集源）为例

打开 aiqicha.baidu.com

![image-20220106220211277](README/image-20220106220211277.png)

通过滑动验证后可以正常打开网站，在console（控制台）输入 `console.log(document.cookie)` 或其他方式获取全部Cookie并粘贴至配置文件 `''`中

![image-20220106220402445](README/image-20220106220402445.png)

这时候再重复命令即可查看到结果，注意如果信息中含有 `*`，你需要登陆后获取Cookie才能去除`*`信息

![image-20220106220603809](README/image-20220106220603809.png)

[![asciicast](https://asciinema.org/a/460250.svg)](https://asciinema.org/a/460250)

![image-20220106224656577](README/image-20220106224656577.png)

### 场景使用

#### 只想获取备案信息

```shell
./ENScanPublic_amd64_linux -n 小米  -field icp
```

[![asciicast](https://asciinema.org/a/460252.svg)](https://asciinema.org/a/460252)

#### 获取占股100的子公司下所有ICP备案网站

```
./ENScanPublic_amd64_linux -n 小米通讯 -invest-num 100 -field icp
```

![image-20220106224603776](README/image-20220106224603776.png)

[![asciicast](https://asciinema.org/a/460255.svg)](https://asciinema.org/a/460255)

#### 使用天眼查数据源

```
 ./ENScanPublic_amd64_linux -n 小米 -type tyc
```



###  交流

关注公众号 `WgpSec狼组安全团队` 回复`加群`一起交流~

![](https://assets.wgpsec.org/www/images/wechat.png)

[![Stargazers over time](https://starchart.cc/wgpsec/ENScan_GO.svg)](https://starchart.cc/wgpsec/ENScan_GO)
