---
icon: fas fa-stream
order: 1
---


## DownLoads

[**Slimming**](https://github.com/slimming-fat.github.io/main/Slimming/tools.7z)


## Install

* windows，直接执行其中的 `install.bat` 。
* linux，对 `install` 文件添加可执行权限：`chmod +x install`。后执行 `./install`。

## 基本使用方式

### 命令行使用方式（使用插件）

`cd` 命令进入项目目录下。

#### 命令

检测单模块项目（运行路径：单模块Pom文件同级目录）

```java
mvn neu.lab:slimming:1.0:singleModuleCheck
```
检测多模块项目（在待检测项目的绝对路径下）
**运行完所有单模块，才可以运行多模块**
```java
mvn neu.lab:slimming:1.0:multiModuleCheck
```


## 参数说明

### 命令行方式使用参数说明

以下参数defaultValue是默认参数，不设置将以默认参数为值。设置参数的方法是在命令行中添加

```
-D<property名称>=<需要设置的参数值>
```

```java
@Parameter(property = "Repair", defaultValue = "true") public boolean Repair; // 输出冗余依赖修复方案 
@Parameter(property = "TreeCallGraph", defaultValue = "true") public boolean TreeCallGraph; // 输出项目包粒度调用图（包含反射分析） 
@Parameter(property = "ClassCallGraph", defaultValue = "false") public boolean ClassCallGraph; // 输出项目类粒度调用图（包含反射分析） 
@Parameter(property = "reflect", defaultValue = "true") public boolean reflect; // 加入类粒度反射分析 
@Parameter(property = "springReflectAPI", defaultValue = "true") public boolean springReflectAPI; // 加入Spring框架封装的反射API分析
@Parameter(property = "tomcatReflectAPI", defaultValue = "false") public boolean tomcatReflectAPI; // 加入Tomcat框架封装的反射API分析
@Parameter(property = "bugReport", defaultValue = "false") public boolean bugReport; // 在GitHub中，提交PR时使用
@Parameter(property = "outDir", defaultValue = "null") public String outDir; // 设置结果输出路径，默认为项目目录
```

## 检测结果说明
### 冗余依赖检测报告
路径：默认检测项目根路径下/bloatedOutput文件夹中
**输出路径可以自定义，通过使用调用接口或者命令行参数-DoutDir**
```java
ALL DEPENDENCY[9]:
 USED DEPENDENCY[4]:
  USED SELF DIRECT DEPENDENCY[1]:
        org.springframework.boot:spring-boot-configuration-processor:2.0.6.RELEASE:provided [86 KB]
  USED SELF INDIRECT DEPENDENCY[3]:
        ch.qos.logback:logback-core:1.2.3:compile [460 KB]
        com.fasterxml:classmate:1.3.4:compile [63 KB]
        com.fasterxml.jackson.core:jackson-core:2.9.7:compile [316 KB]
  USED INHERIT DIRECT DEPENDENCY[0]:
  USED INHERIT INDIRECT DEPENDENCY[0]:
 UNUSED DEPENDENCY[5]:
  UNUSED SELF DIRECT DEPENDENCY[1]:
        org.springframework.boot:spring-boot-starter-web:2.0.6.RELEASE:compile [588 bytes]
  UNUSED SELF INDIRECT DEPENDENCY[4]:
        org.springframework.boot:spring-boot-starter-tomcat:2.0.6.RELEASE:compile [591 bytes]
        org.springframework.boot:spring-boot-starter-logging:2.0.6.RELEASE:compile [613 bytes]
        org.springframework.boot:spring-boot-starter:2.0.6.RELEASE:compile [593 bytes]
        org.springframework.boot:spring-boot-starter-json:2.0.6.RELEASE:compile [645 bytes]
  UNUSED INHERIT DIRECT DEPENDENCY[0]:
  UNUSED INHERIT INDIRECT DEPENDENCY[0]:
[INFO] Repair Case
[INFO] After Repair Pom Path:D:\Maven\project\spring-boot\demo\pom-result.xml    // 冗余依赖修复方案路径
Print TreeCallGraph.dot, red is bloated, gray is unload
```

### 详细检测结果
#### 冗余依赖检测日志
路径：默认检测项目根路径下/bloatedOutput文件夹中的res.txt
<table>
    <tr> 
    	<th>指标</th>
        <th>含义</th>
   </tr>
   <tr> 
		<td>Project info>>>>D:\Maven\project\spring-boot\demo</td>
   		<td>检测项目路径</td>
   </tr>
    <tr>
        <td>Project Name>>>>neu.lab:demo:1.0</td>
        <td>检测项目3坐标（groupId:artifactId:version</td>
    </tr>
    <tr>
        <td>OriginalSize>>>>14KB</td>
        <td>项目第三方库依赖大小</td>
    </tr>
    <tr>
        <td>BloatedSize>>>>4KB</td>
        <td>项目第三方库冗余依赖大小</td>
    </tr>
    <tr>
        <td>All Dependency>>>>1</td>
        <td>检测项目中依赖个数</td>
    </tr>
    <tr>
        <td>Used Dependencies>>>>3</td>
        <td>项目使用的依赖个数</td>
    </tr>
    <tr>
        <td>Used Self Direct Dependency>>>>1</td>
        <td>项目使用的自身直接依赖个数</td>
    </tr>
    <tr>
        <td>Used Self Indirect Dependency>>>>2</td>
        <td>项目使用的自身间接依赖个数</td>
    </tr>
    <tr>
        <td>Used Inherit Direct Dependency>>>>0</td>
        <td>使用的继承直接依赖个数（继承父模块的直接依赖）</td>
    </tr>
    <tr>
        <td>Used Inherit indirect Dependency>>>>0</td>
        <td>使用的继承间接依赖个数（继承父模块的间接依赖）</td>
    </tr>
    <tr>
        <td>Unused Dependencies>>>>2</td>
        <td>冗余依赖个数</td>
    </tr>
    <tr>
        <td>Unused Self Direct Dependency>>>>0</td>
        <td>自身直接冗余依赖个数</td>
    </tr>
    <tr>
        <td>Unused Self Indirect Dependency>>>>0</td>
        <td>自身间接冗余依赖个数</td>
    </tr>
    <tr>
         <td>Unused Inherit Direct Dependency>>>>1</td>
         <td>继承直接冗余依赖个数（继承父模块的直接依赖）</td>
    </tr>
    <tr>
         <td>Unused Inherit Indirect Dependency>>>>1</td>
         <td>继承间接冗余依赖个数（继承父模块的间接依赖）</td>
    </tr>
    <tr>
         <td>checkBloated>>>>2</td>
         <td>静态分析得到的冗余依赖个数</td>
    </tr><tr>
         <td>realBloated>>>>2</td>
         <td>真正去除的冗余依赖个数</td>
    </tr><tr>
         <td>unDeleteSelfDirectDependencies>>>>0</td>
         <td>未消解的自身直接冗余依赖个数</td>
    </tr>
    <tr>
         <td>unDeleteSelfIndirectDependencies>>>>0</td>
         <td>未消解的自身间接冗余依赖个数</td>
    </tr>
    <tr>
      <td>unDeleteUnusedInheritDirectDependencies>>>>0</td>
      <td>未消解的继承直接冗余依赖个数</td>
    </tr>
    <tr>
      <td>unDeleteUnusedInheritIndirectDependencies>>>>0</td>
      <td>未消解的继承间接冗余依赖个数</td>
    </tr>
    <tr>
    </tr>
    <tr>
      <td>configSootTime>>>>4058</td>
      <td>sootUp提取基本信息时间</td>
    </tr>
    <tr>
      <td>buildClassExtendGraphTime>>>>15</td>
      <td>构造类继承和接口实现关系图的时间</td>
    </tr>
    <tr>
      <td>buildCallGraphTime>>>>473</td>
      <td>构造方法粒度和类粒度调用图时间</td>
    </tr>
    <tr>
      <td>levelTime>>>>4</td>
      <td>方法参数正向传播时间（反射分析）</td>
    </tr>
    <tr>
      <td>stringTime>>>>0</td>
      <td>字符串拼接时间（反射分析）</td>
    </tr>
    <tr>
      <td>licenseCheckTime>>>>7</td>
      <td>开源许可证冲突分析时间</td>
    </tr>
    <tr>
      <td>bugCheckTime>>>>120</td>
      <td>安全漏洞检测时间</td>
    </tr>
      <tr>
      <td>maintenanceTimeCheckTime>>>>2542</td>
      <td>过时依赖检测时间</td>
    </tr>
      <tr>
      <td>checkTime>>>>10772</td>
      <td>冗余依赖检测时间</td>
    </tr>
      <tr>
      <td>repairTime>>>>4465</td>
      <td>冗余依赖修复时间</td>
    </tr>
      <tr>
      <td>mvnTestTime>>>>2132</td>
      <td>mvn test运行时间</td>
    </tr>
      <tr>
      <td>SpringAPI>>>>36</td>
      <td>检测项目中出现Spring框架封装反射的API的个数</td>
    </tr>
      <tr>
      <td>.class>>>>5028</td>
      <td>检测项目中Java原生反射.class出现的次数</td>
    </tr>
     <tr>
      <td>forName>>>>95</td>
      <td>检测项目中Java原生反射forName出现的次数</td>
    </tr>
     <tr>
      <td>loadClass>>>>122</td>
      <td>检测项目中Java原生反射loadClass出现的次数</td>
    </tr>
     <tr>
      <td>getClass>>>>1699</td>
      <td>检测项目中Java原生反射getClass出现的次数</td>
    </tr>
     <tr>
      <td>reflectEdges>>>>6944</td>
      <td>检测项目中类粒度反射总个数</td>
    </tr>
    <tr>
       <td>springReflectAPI>>>>&ltorg.springframework.core.GenericTypeResolver:java.lang.Class&nbsp;TypeArgument(java.lang.reflect.Method,java.lang.Class)&gt         
        </td>
        <td>检测项目中Spring框架封装的反射API名称</td>
     </tr>
     <tr>
      <td><strong>1:</strong>unSolvedReflect>>>>UnReflectEntity{<br> 
                                 <strong>2:</strong>type='&ltjava.lang.Object: java.lang.Class getClass()&gt', <br>
                                 <strong>3:</strong>source='org.springframework.boot.web.embedded.jetty.JettyWebServer',<br>
                                <strong>4:</strong>sootMethod=&ltorg.springframework.boot.web.embedded.jetty.JettyWebServer:
                                                     java.lang.Integer&nbsp;getLocalPort(org.eclipse.jetty.server.Connector)&gt,<br> 
                                 <strong>5:</strong>line=187, <br>
                                 <strong>6:</strong>param='null' <br>
                                 }</td>
      <td><strong>1:</strong>检测项目未解析类粒度反射<br>
          <strong>2:</strong>未解析的反射类型<br>   
          <strong>3:</strong>该反射出现的类<br>
          <strong>4:</strong>该反射出现的方法<br>
          <strong>5:</strong>该反射对应源码中行数（开始行数）<br>
          <strong>6:</strong>反射API中的常量参数<br>
      </td>
     </tr>
</table>

#### 冗余依赖修复方案

修复方案名称为：pom-result.xml
路径：查看冗余检测报告日志中After Repair Pom Path后的路径


#### 冗余依赖可视化

可视化文件名称：TreeCallGraph.dot
路径：检测项目根路径下
![微信图片_20230413104220副本](D:\课题\冗余依赖\华为\冗余依赖试用工具及其相关资料(SootUp版本)\冗余依赖试用工具使用说明_files\微信图片_20230413104220副本.png)



红色框：冗余依赖
灰色框：发生依赖冲突的依赖
红色虚线边：未加载的依赖边
可视化网站：http://viz-js.com/，将生成的.dot文件的内容粘贴到可视化网站中即可得到上述类型的可视化图
