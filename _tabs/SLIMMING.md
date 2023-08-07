---
icon: fas fa-stream
order: 1
---


## Step 1: DownLoads

[**Slimming**](https://github.com/slimming-fat/slimming-fat.github.io/blob/master/Slimming/tools.7z)


## Step 2: Install
* For **windows**, run [`install.bat`](https://github.com/slimming-fat/slimming-fat.github.io/blob/master/Slimming/install.bat)
* For **linux**, run [`install`](https://github.com/slimming-fat/slimming-fat.github.io/blob/master/Slimming/install)

## Step 3: Run
#### Detect single module project
```java
mvn neu.lab:slimming:1.0:singleModuleCheck
```
#### Detect multi-module project
```java
mvn neu.lab:slimming:1.0:multiModuleCheck
```
#### Optional Parameters

| Name           | Type    | Description                                              |
| :-------------:| :-----: | :------------------------------------------------------- |
| `Repair`         | `boolean` | If this is true, Slimming creates a debloated version of the pom without unused dependencies called pom-result.xml.**Default value is**: `true`|
| `TreeCallGraph`  | `boolean` | If this is true, Slimming can obtain a dependency call graph.**Default value is**: `true`   |
| `ClassCallGraph` | `boolean` | If this is true, Slimming can obtain a class call graph.**Default value is**: `false` |
| `reflect`        | `boolean` | If this is true, Slimming performs class-level reflection analysis.**Default value is**: `true`                        |
| `outDir`         | `String`  | Customize the storage path for storing the analysis results of bloated dependencies  |

## Step 4: Obtain the results
#### Bloated dependency detection reports

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
[INFO] After Repair Pom Path:D:/Maven/project/spring-boot/demo/pom-result.xml    // Bloated dependency repair scheme path
Print TreeCallGraph.dot, red is bloated, gray is unload
```
