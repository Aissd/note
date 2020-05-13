1、Webpack Bundle Analyzer

​	https://www.npmjs.com/package/webpack-bundle-analyzer

​	该插件的默认配置：https://www.cnblogs.com/hss-blog/p/10244315.html

​	1）安装

```
npm install --save-dev webpack-bundle-analyzer
```

​	2）vue.config.js:

```
const BundleAnalyzerPlugin = require('webpack-bundle-analyzer').BundleAnalyzerPlugin;
module.exports = {
	configureWebpack: {
   		plugins: [
      		new BundleAnalyzerPlugin()
    	]
  	}
}
```
