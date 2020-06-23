# C# 调用 JAVA方法
### java方法变为dll链接库

## 要求：

1. java 方法的 dk 必须在 1.8 以下 (需要添加本地路径)
2. IKVM 版本 8.1  (需要添加本地路径)  
   下载地址： http://weblog.ikvm.net/2015/08/26/IKVMNET81ReleaseCandidate0.aspx   
   官网: http://www.ikvm.net/devguide/net2java.html

## 使用方法：
1. 
   (方法1) 打包目标 .java 文件为  .class 然后使用以下命令 打包为 .jar 文件 
   ``` 
   jar cvf test.jar -C com/ .
   ``` 
   
   (方法2) 在eclipse 直接export 出 jar文件
2. 在目标文件夹里 ikvmc -target:library test.jar  生成 dll 文件
3. 在需要调用方法的C#项目里引用以下核心dll和其他需要的dll文件（在IKVM安装包的bin里，目的是为了驱动java）
   ``` 
     /bin/IKVM.OpenJDK.Core.dll
     /bin/IKVM.Runtime.dll
     /bin/IKVM.Runtime.JNI.dll 
   ```
4. 在C#项目里引用编译好的 dll 文件
5. 在C#里引用并实例化包和类， 调用方法

## 注意方式
 1. ikvm的版本必须和java版本匹配, ikvm 至少需要8.1版本, java 版本不能超过 1.8，  否则打包时可能出现以下错误
   ```
         Not a class file "aa.class", including it as resource
   ```
 2. 如果引用报错 考虑 是否 c# 引用的 ikvm版本不匹配, 或引用的 dll 不包含  编译指定类库
