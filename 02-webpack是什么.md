# webpack是什么？

Webpack是一款模块打包工具，你可以用它来帮助你打包。但是随着社区的发展，很多开发插件的涌现，这种定义越发模糊起来。一些插件所做的功能任务已经远远超出了打包的范畴，举例来说，有些插件可以帮助我们清理打包目录，还有的插件可以帮助我们处理打包后文件的线上部署。

Webpack在React中非常的受青睐，因为它支持热模块替换（Hot Module Replacement），这也使得webpack迅速变的家喻户晓，甚至扩展到了其他语言的开发中，比如Ruby On Rails。看到webpack中的web这个单词，你可能觉得webpack只能应用于网页开发之中，可不是这样的！webpack可以打包其他的资源，这部分的内容我们将会在 “构建目标文件” 小节中详述。

读到这，如果你恰好对React有所了解，却又不知道Hot Module Replacement(HMR) 为何物，我建议大家先看一下HMR的基本介绍，之后看下这篇文章：[点击阅读](https://segmentfault.com/a/1190000006178770)，记录好如何配置HMR即可，接下来的教程中，我们可能继续给大家扩展HMR的相关知识。

## Webpack的打包建立在模块基础上

当你的项目中配置了webpack的**入口(input)**和**出口(output)**后，就可以使用webpack打包了。打包的过程从你的入口文件开始，入口文件就是一个模块（modules），通过imports可以引入其他模块。

当使用webpack打包项目时，它首先会便利模块引用（imports），建立一个项目的依赖关系图(dependency graph)，然后根据这个关系图和你的配置文件内容，生成你所需要的输出文件。你可以在代码中设置切分点(split point)，webpack可以根据设置，把工程的代码切分成多个。注意，webpack分析依赖关系图的时候，会通过一些静态的方式生成，而不是靠动态的运行文件来分析，这样性能上的消耗很小。

Webpack 支持ES6，CommonJS, AMD 的模块化方案.内部加载器(loader)机制使得它也可以处理css文件间的依赖关系，你只要安装css-loader后使用@import和url()即可完成css间的相互引用。你还可以使用很多Webpack的插件来帮助你完成指定的任务，比如说压缩代码，代码国际化，热模块加载等等。

# Webpack执行流程

![webpack流程](https://github.com/shenglongli/webpack-book/blob/master/imgs/webpack-process.png)

Webpack从入口开始，这些入口一般会引入很多其他的模块，webpack遍历这些模块，开始打包流程。过程中，webpack会根据文件的类型，和对应的loader进行匹配，然后根据匹配结果执行对应的转换操作。

## 解析过程

入口本身就是一个模块，webpack遇到一个模块时，他会根据文件中的依赖去找寻这个模块所需的所有内容。

如果解析失败，webpack会给出运行时错误。如果解析成功，webpack就可以根据loader和其他配置项的定义运行打包流程了。每一个loader在模块内容打包时都负责处理指定部分内容的转换。

对于一个loader来说，它到底要负责哪部分内容的转化呢？定义loader职责的方法有多种，你可以根据文件的类型来决定使用哪个loader，也可以根据文件所在的路径来执行对应的loader。webpack还提供了更加灵活的方式，你甚至可以根据文件在哪里被引用来决定使用什么loader进行解析，怎么样，很酷吧！

解析的过程中，loader模块中的内容也会被解析。loader也可以被其他loader所解析，他们也有自己的配置文件，总之，一旦loader解析没通过，你的webpack一样会报错。

## webpack几乎可以处理任何文件类型

Webpack 会处理构建过程中依赖图谱中的所有模块。如果入口包含任何依赖，每个依赖的模块都会被处理到。无论什么文件类型，webpack都不会放过，这一点不像Babel或者Sass的编译器，他们只负责处理固定的文件类型。

你可以控制webpack遇到不同文件时作出的不同相应。你可以让webpack把某些静态资源打包到js里，这样可以避免额外的网络请求。webpack还提供了一些使用技巧，你可以通过webpack实现css的模块化，避免像以前一样的非模块化css编码。这些webpack带来的灵活性，使得webpack具有非常大的使用价值。

尽管webpack主要被用做打包js，它也可以捕获图片或者字体这样的静态资源并对它们进行单独处理。入口只是webpack构建过程中的开始执行点，具体打包过程时如何的，完全依赖于你怎么做的打包配置。

## 执行流程

Assuming all loaders were found, webpack evaluates the matched loaders from bottom to top and right to left (styleLoader(cssLoader('./main.css'))), running the module through each loader in turn. As a result you get output which webpack will inject in the resulting bundle. The Loader Definitions chapter covers the topic in detail.

If all loader evaluation completed without a runtime error, webpack includes the source in the last bundle. Plugins allow you to intercept runtime events at different stages of the bundling process.

Although loaders can do a lot, they don’t provide enough power for advanced tasks by themselves. Plugins intercept runtime events provided by webpack. A good example is bundle extraction performed by ExtractTextPlugin which, working in tandem with a loader, extracts CSS files out of the bundle and into a file of its own.

Without this step, CSS would end up in the resulting JavaScript as webpack treats all code as JavaScript by default. The extraction idea is discussed in the Separating CSS chapter.




