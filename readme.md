# vscode 插件开发极简教程
首先，vscode 的插件开发很简单。如果读完这篇需要 5 分钟，那么至少有 4 分钟是花在看我写的废话上，实际上只用 1 分钟就能入门。好想把标题改成“1 分钟入门 vscode 插件开发”！

写个网页现在还得用 vue 或 react，免不了搭建个环境，还得构建项目、打包……而开发 vscode 插件，你只需要[安装一个 vscode](https://code.visualstudio.com/)，其他什么都不要（不要用太老版本的 vscode）。

下面是一个极简的 vscode 插件，代码只有四行。功能是：在 vscode 启动后，弹出一个通知：
![mini-vsc-plugin](https://files20220620.oss-cn-shanghai.aliyuncs.com/mini_vsc_plugin.png)

（从现在开始计时，不过分吧……）

你只需要新建一个文件夹，然后用 vscode 打开这个文件夹，再创建以下两个文件：
## 一、package.json
package.json 是描述项目的文件，存放基本信息（项目名、版本、环境等）
``` json
{
  "name": "vsc-plugin-demo",
	"version": "0.0.1",
	"engines": {
		"vscode": "^1.47.3"
	},
	"activationEvents": [
		"onStartupFinished"
	],
	"main": "./ext.js"
}
```
这种文件，一般不称之为“代码”。需要说明的是：
+ activationEvents: 声明插件启动的时机，此处是在 onStartupFinished，即（vscode）启动完成时（启动插件）
+ main: 主程序文件的路径

## 二、ext.js
主程序只有这四行代码：
``` js
const vscode = require('vscode')

exports.activate = function() {
  vscode.window.showInformationMessage('hello, ppz')
}
```
第 1 行代码，引入 vscode 核心库，不需要手动安装，它提供了开发插件所需的大部分 api。

第 2 到 4 行代码，定义了“启动插件的函数”，即通过这个函数，让插件跑起来。函数体部分只有一行，通过调用 vscode 提供的 api，展示一个通知：```hello, ppz```。

## 运行
至此，插件已经完成，运行一下试试：
+ 用鼠标点一下 ```ext.js``` 文件
+ 按键盘上的 f5
+ 点击弹出窗口中的 ```VS Code Extension Development```

（你已经入门 vscode 插件开发，计时结束）

## 最后
上面的代码可以从 github 上下载：[仓库地址](https://github.com/ppz-pro/vsc-plugin-startup)
``` bash
git clone https://github.com/ppz-pro/vsc-plugin-startup.git
```

如果说 vscode 插件开发比某一种程序开发难，那是因为你在它上面才花了 1 分钟。相比于动辄几个月的技术培训，这 1 分钟实在是太微乎其微了。如果你也感兴趣，可以直接看 [vscode 的官方教程](https://code.visualstudio.com/api/get-started/your-first-extension)，很全面，也很细。

当然，在这忙忙碌碌、繁繁乱乱的生活中，能静下心来学习，已实属不易，共勉吧！

最后的最后，自荐我在 2022 年上海疫情封控期间写的插件 —— [PPZ](https://marketplace.visualstudio.com/items?itemName=ppz.ppz)，它提供了操作数据库的图形界面，目前功能还很简单，后续功能会慢慢丰富起来。  
[PPZ 的 github 链接](https://github.com/ppz-pro/ppz.vscode)、[PPZ 的 gitee 链接](https://gitee.com/ppz-pro/ppz.vscode)
