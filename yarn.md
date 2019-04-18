##
1. 安装yarn
```
npm i yarn -g --verbose
```
2. 更换安装源地址
```
yarn config set registry https://registry.npm.taobao.org
```
## 常用指令
* yarn / yarn install 等同于npm install 批量安装依赖
* yarn add xxx 等同于 npm install xxx —save 安装指定包到指定位置
* yarn remove xxx 等同于 npm uninstall xxx —save 卸载指定包
* yarn add xxx —dev 等同于 npm install xxx —save-dev
* yarn upgrade 等同于 npm update 升级全部包
* yarn global add xxx 等同于 npm install xxx -g 全局安装指定包
