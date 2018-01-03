# 使用 DllPlugin

### 认识 DLL

在介绍 DllPlugin 前先给大家介绍下 DLL。 用过 Windows 系统的人应该会经常看到以 .dll 为后缀的文件，这些文件称为动态链接库，在一个动态链接库中可以包含给其他模块调用的函数和数据。

要给 Web 项目构建接入动态链接库的思想，需要完成以下事情：

* 把网页依赖的基础模块抽离出来，打包到一个个单独的动态链接库中去。一个动态链接库中可以包含多个模块。
* 当需要导入的模块存在于某个动态链接库中时，这个模块不能被再次被打包，而是去动态链接库中获取。
* 页面依赖的所有动态链接库需要被加载。

为什么给 Web 项目构建接入动态链接库的思想后，会大大提升构建速度呢？ 原因在于包含大量复用模块的动态链接库只需要编译一次，在之后的构建过程中被动态链接库包含的模块将不会在重新编译(不用每次打包时从node_module中分析)，而是直接使用动态链接库中的代码。 由于动态链接库中大多数包含的是常用的第三方模块，例如 react、react-dom，只要不升级这些模块的版本，动态链接库就不用重新编译。

### 使用 AutoDLLPlugin，必须先加载dll bundle再加载自己的bbundle，通常需要在html中额外的标script签，
比如`<script src="dist/vendor.dll.js"></script>`


### 和CommonsChunkPlugin不太一样， 我合并了jquery和datatables，用CommonsChunkPlugin可以成功，换这样不能用
参考：https://github.com/asfktz/autodll-webpack-plugin