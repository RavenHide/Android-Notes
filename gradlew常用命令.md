# gradlew常用命令

- **gradlew -v **版本号
- **gradlew clean** 清除工程目录下的build文件夹
- **gradlew build** 检查依赖并编译打包

这里注意的是 **gradlew build** 命令把**debug**、**release**环境的包都打出来，如果正式发布只需要打**Release**的包，该怎么办呢，下面介绍一个很有用的命令 **assemble**, 如

- **gradlew assembleDebug** 编译并打Debug包
- **gradlew assembleRelease** 编译并打Release的包

还有打渠道包，如百度 
- **gradlew assembleBaiduRelease** 编译并打Release的百度包

除此之外，assemble还可以和productFlavors结合使用,比如定义了 installRelease ，uninstallRelease 两个productFlavors，则可以如下命令：

- **gradlew installRelease Release** 模式打包并安装
- **gradlew uninstallRelease** 卸载Release模式包