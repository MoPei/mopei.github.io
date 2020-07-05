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
### 传递性依赖和依赖范围的关系

依赖范围不仅可以控制依赖与三种classpath的关系，还对传递性依赖产生影响。第一直接依赖的范围和第二直接依赖的范围决定了传递性依赖的范围
如图：最左边一列表示第一直接依赖范围，最上面一行表示第二直接依赖范围，中间的交叉单元格则表示传递性依赖范围

||compile|test|provided|runtime|
|----|----|----|----|----|
|compile|compile|--|--|runtime|
|test|test|--|-|test|
|provided|provided|--|provided|provided|
|runtime|runtime|-||runtime|


### 依赖调解

Maven的依赖调解原则是首先路径最近优先，对于相同路径，在POM中依赖声明的顺序决定了谁会被解析，顺序最靠前的那个依赖优胜

### 可选依赖

如果项目A依赖B，B依赖于X和Y，但是B对X和Y的依赖是可选的，如果所有的依赖的范围都是compile的，那么X和Y就是A的compile范围传递依赖，到那会死X和Y是可选依赖，依赖将不会得以传递，也就是X和Y将不会对A有任何影响

## 生命周期和插件

### 生命周期想详解


三套生命周期分别为clean、default、site，clean生命周期的目的是清理项目，default生命周期的目的是构建项目，而site生命周期的目的是建立项目站点

- clean生命周期
包含以下三个阶段：
- pre-clean：执行一些清理前需要的工作
- clean：清理上一次生成的文件
- post-clean：执行一些清理后需要完成的工作

- default生命周期

defalut生命周期定义了真正构建时所需要执行的所有步骤，它是生命周期中最核心的部分，包含以下阶段

- validate
- initialize
- generate-sources
- process-sources
- generate-resources
- process-resources
- compile
- process-classes
- generate-test-sources
- process-test-sources
- generate-test-resources
- process-test-resources
- test-compile
- process-test-classes
- test
- prepare-package
- package
- pre-integration-test
- integration-test
- post-integration-test
- verify
- install
- deploy


