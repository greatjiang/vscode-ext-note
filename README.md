# vscode-ext-note
vscode插件学习

## 基本
> vscode基于Electron
1. 自定义命令、快捷键、菜单
>1. 自定义命令，会出现在 Ctrl+Shift+P命令列表中，同时可以给命令配置快捷键、配置资源管理器菜单、编辑器菜单、标题菜单、下拉菜单、右上角图标等

2. 自定义跳转、自动补全、悬浮提示

3. 自定义设置、自定义欢迎页

4. 自定义WebView

5. 自定义左侧功能面板

6. 自定义颜色、图标主题

7. 新增语言支持
> 代码高亮、语法解析、折叠、跳转、补全等；

8. Markdown增强
> 自定义markdown预览的样式、添加一些新语法、新功能的支持

9. 其它
> 比如状态栏修改、通知提示、编辑器控制、git源代码控制、任务定义、Language Server、Debug Adapter等等。

## 搭建开发环境
**准备**
1. nodejs
2. npm
3. yeoman
  ```
  npm i -g yo
  ```
4. generator-code
  ```
  npm i -g generator-code
  ```
**插件存放位置**
macOS: ~/.vscode/extensions

**启动**
yo code

## 常用
**package.json**
1. activationEvents 扩展的激活事件 ？啥玩意
2. contributes 大部分功能配置

**修改之后最好在调试的状态下点击“重新连接”**

查找时 输入contributes-> commands -> title 的值

onCommand 指令调用调用
onLanguage 当使用当前配置语言时调用

**快捷键绑定**
```
contributes.keybindings
```
**设置菜单**
> 菜单应该是有很多种
```
contributes.menus
```

**推荐TS开发**


## 环境
1. 安装 npm i -g yo generator-code
2. 执行 yo code

**package.json**
字段含义 一眼看出来的就不写了
name 插件名字 全部小写不能有空格
displayName 应用市场名称 中英文随意
keywords 应用市场关键字
categories 应用市场分类
activationEvents: []  扩展的激活事件数组，可以被哪些事件激活扩展  !!!
contributes 直译贡献点 具体干啥的后续看看
  configuration 插件设置项
  commands  命令
  keybindings 快捷键绑定
  menus   菜单
    editor/context 编辑器右键菜单
    editor/title 编辑器右上角图标 没图片就显示文字
    editor/title/context 编辑器标题右键菜单
    explorer/context 资源管理器右键菜单
  snippets 代码片段 干啥的？
  viewsContainers activitybar图标 左侧侧边栏大的图标
  views 自定义侧边栏内的view
  iconThemes 图标主题

**activationEvents**
八种激活方式
onLanguage:${language}  语言
onCommand:${command} 指令
onDebug 
workspaceContains:${toplevelfilename} 工作目录？
onFileSystem:${scheme} ？
onView:${viewId} ？
onUri ？
* 所有不推荐

**命令**
vscode.commands.registerCommand 注册命令
context.subscriptions 把命令放到这里
```
vscode.commands.registerCommand(name, cb(uri))
context.subscriptions.push(name)
```
**编辑器命令**
仅在有被编辑器被激活时调用才生效
可以访问到当前活动编辑器textEditor
```
vscode.commands.registerTextEditorCommand('extension.testEditorCommand', (textEditor, edit) => {
	console.log('您正在执行编辑器命令！');
	console.log(textEditor, edit);
})
```

**执行命令**
很多命令都是返回一个类似于Promise的Thenable对象
啥？

**复杂命令**
[复杂命令](https://code.visualstudio.com/api/references/commands)

**菜单**
```
"menus": {
		"editor/title": [{
			"when": "resourceLangId == markdown",
			"command": "markdown.showPreview",
			"alt": "markdown.showPreviewToSide",
			"group": "navigation"
		}]
	}
```
editor/title 定义菜单出现在哪里
when 控制菜单何时出现
command 菜单被点击后要执行什么操作
alt   alt时的操作
group 定义菜单分组

**出现位置**
到时候再查
explorer/context、editor/context 常用

**group**
其它分组都是按照0-9、a-z的顺序排列的
每个类型的组都可以调整位置 ！！！
editor/context 编辑器上下文菜单
explorer/context 资源管理器上下文菜单
editor/title/context 编辑器标题上下文菜单（编辑器选项卡？）
editor/title 编辑标题菜单栏

组内排序
@<number>

快捷键
key: xxx
mac: xxx

## 参考资料
http://blog.haoji.me/vscode-plugin-overview.html