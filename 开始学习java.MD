# java要点
1.  JDK(编译器等)包含 JRE(运行类库等) 包含JVM(虚拟机) 
2. mac在IntelliJ IDEA里报错: 
objc[8715]: Class JavaLaunchHelper is implemented in both /Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home/bin/java (0x102c804c0) and /Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home/jre/lib/libinstrument.dylib (0x102d5c4e0). One of the two will be used. Which one is undefined.

解决方法：

在idea中，进行修改idea.properties

打开idea --> 工具栏Help --> Edit Custom Properties...
添加内容
```
#custom IntelliJ IDEA properties
idea_rt
idea.no.launcher=true
```
重启idea就可以了
