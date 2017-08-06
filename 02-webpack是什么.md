# webpack是什么？

Webpack是一款模块打包工具，你可以它来帮助你打包。但是随着社区的发展，很多开发插件的涌现，这种定义越发模糊起来。一些插件所做的功能任务已经远远超出了打包的范畴，举例来说，有些插件可以帮助我们清理打包目录，还有的插件可以帮助我们处理打包后文件的线上部署。

Webpack在React中非常的受青睐，因为它支持热模块替换（Hot Module Replacement），这也使得webpack迅速变的家喻户晓，甚至扩展到了其他语言的开发中，比如Ruby On Rails。看到webpack中的web这个单词，你可能觉得webpack只能应用于网页开发之中，可不是这样的！webpack可以打包其他的资源，这部分的内容我们将会在 “构建目标文件” 小节中详述。

读到这，如果你恰好对React有所了解，却又不知道Hot Module Replacement(HMR) 为何物，我建议大家先看一下HMR的基本介绍，之后看下这篇文章：[点击阅读](https://segmentfault.com/a/1190000006178770)，记录好如何配置HMR即可，接下来的教程中，我们可能继续给大家扩展HMR的相关知识。

## Webpack的打包建立在模块基础上

当你的项目中配置了webpack的**入口(input)**和**出口(output)**后，就可以使用webpack打包了。打包的过程从你的入口文件开始，入口文件就是一个模块（modules），通过imports可以引入其他模块。

当使用webpack打包项目时，它首先会便利iports，建立一个项目的依赖关系图(dependency graph)，然后根据这个关系图和你的配置文件内容，生成你所需要的输出文件。你可以在代码中设置切分点(split point)，webpack可以根据设置，把工程的代码切分成多个。注意，webpack分析依赖关系图的时候，会通过一些静态的方式生成，而不是靠动态的运行文件来分析，这样性能上的消耗很小。

Webpack 支持ES6，CommonJS, AMD 的模块化方案.内部加载器(loader)机制使得它也可以处理css文件间的依赖关系，你只要安装css-loader后使用@import和url()即可完成css间的相互引用。你还可以使用很多Webpack的插件来帮助你完成指定的任务，比如说压缩代码，代码国际化，热模块加载等等。

![webpack流程](https://github.com/shenglongli/webpack-book/blob/master/imgs/webpack-process.png)






