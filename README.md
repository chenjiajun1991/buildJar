# buildJar
**通用的打包jar gradle插件**

## 支持特性

1. 按需打包jar：
   * 全项目打包jar
   * 指定输出Jar包的包名路径列表
   * 指定输出Jar包的class列表
   * 过滤指定包名路径列表
   * 过滤指定class
   * 过滤指定jar
2. 支持混淆打包jar
3. 支持applymapping

## 使用说明

1. 引入依赖

   ```groovy
   dependencies {
           classpath 'com.android.tools.build:gradle:2.1.3'
           classpath 'com.adison.gradleplugin:jar:1.0.1'
       }
   ```

   ​

2. 应用插件

   ```groovy
   apply plugin: 'jar-gradle-plugin'
   BuildJar{
       //输出目录
       outputFileDir= project.buildDir.path+"/jar"
       //输出原始jar包名
       outputFileName="test.jar"
       //输出混淆jar包名
       outputProguardFileName="test_proguard.jar"
       //混淆配置
       proguardConfigFile="proguard-rules.pro"
       //是否需要默认的混淆配置proguard-android.txt
       needDefaultProguard=true
       applyMappingFile="originMapping/mapping.txt"
       //需要输出jar的包名列表,当includePackage&includeClass为空时，则默认全项目输出,支持多包,如 includePackage=['com/adison/testjarplugin/include','com/adison/testjarplugin/include1'...]
       includePackage=['com/adison/testjarplugin/include']
      //需要输出jar的类名列表
     includeClass=['com/adison/testjarplugin/include/TestInclude.class']
       //不需要输出jar的jar包列表,如['baidu.jar','baidu1.jar'...]
       excludeJar=[]
       //不需要输出jar的类名列表,如['baidu.calss','baidu1.class'...]
       excludeClass=['com/adison/testjarplugin/TestExcude.class']
       //不需要输出jar的包名列表,如 excludePackage=['com/adison/testjarplugin/exclude','com/adison/testjarplugin/exclude1'...]
       excludePackage=['com/adison/testjarplugin/exclude']
   }
   ```

3. 使用

   * 打包普通jar

     ```groovy
     mac or linux
     ./gradlew buildJar

     windows
     gradlew.bat buildJar
     ```

   * 打包混淆jar

     ```groovy
     mac or linux
     ./gradlew buildProguardJar

     windows
     gradlew.bat buildProguardJar
     ```


   > 可参见[使用demo](https://github.com/adisonhyh/TestJarPlugin/)

4. 注意：

   > 1. 当includePackage&includeClass为空时，则全项目输出
   >
   >    ```groovy
   >     includePackage=[]
   >     includeClass=[]
   >    ```
   >
   > 2. 优先级：exclude > include，即当exclude和include的class或package相同时，优先exclude

## 更新说明

### 1.0.2

- 增加指定输出Jar包的class列表

### 1.0.1

- 修复bug

### 1.0.0
* 支持按需打包jar：
   * 全项目打包jar
   * 指定输出Jar包的包名路径列表
   * 过滤指定包名路径列表
   * 过滤指定class
   * 过滤指定jar
* 支持混淆打包jar
* 支持applymapping

## LICENSE

   Apache License 2.0