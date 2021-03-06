# vue-mobile2

## 教程
这个vue项目使用 [lib-flexible](https://github.com/amfe/lib-flexible) + [px2rem-loader](https://github.com/Jinjiang/px2rem-loader) 实现移动端适配

### lib-flexible
首先我们使用**lib-flexble**达到适配效果

#### 安装
```shell
yarn add lib-flexble
```
或者
```shell
npm install lib-flexible --save
```
#### 引入
在**main.js**文件中引入**lib-flexble**
```javascript
import 'lib-flexble'
```
通过上面这两步，就实现了vue项目使用lib-flexible来将移动端适配;
#### 原理
lib-flexible自动在html的head中添加一个**meta name="viewport"**的标签，同时自动设置html的font-size为屏幕宽度除以10，也就1rem等于html根节点的font-size。

例如：假如设计稿的宽度是750px，此时1rem应该等于75px。假如量的某个元素的宽度是300px，那么在css里面定义这个元素的宽度就是width: 4rem。

### px2rem-loader
如果每次从设计稿量出来的尺寸都手动去计算一下rem，就会导致我们效率比较慢，还有可能会计算错误，所以我们可以使用**px2rem-loader**自动将css中的**px**转成**rem**。
#### 安装
```shell
yarn add px2rem-loader
```
或者
```shell
npm install px2rem-loader --save-dev
```
#### 配置
在根目录的**vue.config.js**文件（没有就新建）进行配置
```javascript
module.exports = {
  chainWebpack: config => {
    config.module
      .rule('css')
        .test(/\.css$/)
        .oneOf('vue')
        .resourceQuery(/\?vue/)
        .use('px2rem')
          .loader('px2rem-loader')
          .options({
            remUnit: 75
          })
  }
}
```
#### 最后重启项目即可
