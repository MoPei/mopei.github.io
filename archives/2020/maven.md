# Maven key points
## Maven 依赖范围
Maven 依赖范围是用来控制依赖和三种classpath(编译classpath、测试classpath、运行classpath)之间的关系
Maven 有以下几种依赖范围：
- compile:编译依赖范围，如果没有指定，默认使用该依赖范围，使用该依赖范围的Maven依赖对编译、测试、运行三种classpath都有效。典型的例子是spring-core在编译、测试、运行的时候都需要使用该依赖
- test:测试依赖范围。使用此依赖范围的Maven依赖，只对测试classpath有效，在编译主代码或者运行项目的使用时将无法使用此类依赖。典型的例子就是junit，它只在编译测试代码及运行测试代码时才需要
- provided:已提供依赖范围，使用该依赖范围的Maven依赖，对于编译和测试classpath有效，但是在运行时无效。典型的是servlet-api，编译和测试项目的时候需要该依赖，但是在运行项目时，由于容器已经提供，就不需要Maven重复引入
- runtime: 运行时依赖范围，使用该依赖范围的Maven依赖，对于测试和运行classpath有效，但是在编译主代码时无效，典型的时jdbc驱动实现，项目主代码的编译只需要jdk提供的jdbc接口，只有在执行测试或者运行项目的时候才需要实现上述接口的具体jdbc驱动
- system: 系统依赖范围，该依赖于三种classpath的关系于provided依赖范围完全一致，但是使用system范围的依赖时必须通过systempath元素显示地指定依赖文件的路径，由于此依赖不时通过Maven仓库解析的，而且往往与本机系统绑定，可能造成构建的不可移植
- import：导入依赖范围，该依赖范围不会对三种classpath产生实际的影响

|依赖范围|对于编译classpath有效|对于测试classpath有效|对于运行classpath有效|例子|
|----|----|----|----|----|
|compile|Y|Y|Y|spring-core|
|test|Y|Y|-|junit|
|provided|Y|Y|-|servlet-api|
|runtime|-|-|Y|jdbc驱动实现|
|system|Y|Y|-|本地的|

## 依赖传递
