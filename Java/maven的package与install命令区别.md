# maven的package与install命令区别

之前一直不明白package与  install的区别，今天测试了下。

 如果b项目依赖a项目，而a打了包(package),jar仅仅时打到了a项目的target下。这时编译b项目，还是会报错，找不到所依赖的a项目，说明b项目在本地仓库是没有找到它所依赖的a项目。然后，我install a项目这时，有以下日志,[INFO] Installing G:\projects\a\target\a-0.0.1-SNAPSHOT.jar to F:\repository\com\chenjun\a\0.0.1-SNAPSHOT\a-0.0.1-SNAPSHOT.jar
[INFO] Installing G:\projects\a\pom.xml to F:\repository\com\chenjun\a\0.0.1-SNAPSHOT\a-0.0.1-SNAPSHOT.pom,说明a项目已安装到本地仓库了,并且是jar和pom同时安装的.

这时候去compileb项目，编译通过.

总之，**package是把jar打到本项目的target下，而install时把target下的jar安装到本地仓库，供其他项目使用.**
