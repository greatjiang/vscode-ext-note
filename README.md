# 初步了解VSCode 插件
> 点滴积累

**插件存放位置**
macOS: ~/.vscode/extensions


## 快速开发一个代码片段
**准备**
1. 注册微软开发账号 生成一个key https://www.cnblogs.com/liuxianan/p/vscode-plugin-publish.html
2. vsce create-publisher your-publisher-name
3. npm i vsce -g

**开发**
1. npm i -g yo
2. npm i -g generator-code
3. yo code
4. api https://code.visualstudio.com/docs/editor/userdefinedsnippets
5. 上传github
6. npm version x.x.x
7. vsce publish