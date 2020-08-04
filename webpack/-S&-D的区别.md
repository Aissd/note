1、

```
--save 可简写为-S
--save-dev可以简写为-D
```

2、npm install moduleName

```
npm install moduleName
1）安装模块到项目node_modules目录下
2）不会将依赖写入devDependencies或dependencies节点
3）运行npm install初始化项目时不会下载模块
```

3、npm install -g moduleName

```
1）安装模块到全局，不会在项目node_modules目录目录中保存模块包
2）不会将模块依赖写入devDependencies或dependencies节点
3）运行npm install初始化项目时不会下载模块
```

4、npm install --save moduleName

```
1）安装模块到项目node_modules目录下
2）会将模块依赖写入dependencies节点
3）运行npm install 初始化项目的时候，会将模块下载到项目目录下
4）运行npm install --production或者注明NODE_ENV变量值为production时，会自动下载模块到node_modules目录中
```

5、npm install --save-dev moduleName

```
1）安装模块到项目node_modules目录下
2）会将模块依赖写入devDependencies节点
3）运行npm install --production或者注明NODE_ENV变量值为production时，不会自动下载模块到node_modules目录中
```

6、总结

```
1）devDependencies节点下的模块是我们在开发时需要用的
2）dependencies节点下的模块是项目运行必备的
```

