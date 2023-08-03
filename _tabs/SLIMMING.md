---
icon: fas fa-stream
order: 1
---


## Step 1: DownLoads

[**Slimming**](https://github.com/slimming-fat/slimming-fat.github.io/blob/master/Slimming/tools.7z)


## Step 2: Install
* For windows, run [`install.bat`](https://github.com/slimming-fat/slimming-fat.github.io/blob/master/Slimming/install.bat) directly
* For linux, add executable permissions to the [`install`](https://github.com/slimming-fat/slimming-fat.github.io/blob/master/Slimming/install) file: `chmod +x install`. Then run `/install`.

## Step 3: Run slimming
* Command \\
The `cd` command moves into the project directory\\
Detect single module project (run path: same level directory of single module Pom file)

```java
mvn neu.lab:slimming:1.0:singleModuleCheck
```
Detecting multi-module items (under the absolute path of the item to be detected)\\
**You can run multiple modules only after you have run all single modules**
```java
mvn neu.lab:slimming:1.0:multiModuleCheck
```


* Parameter Specification

The following parameter, defaultValue, is the default parameter; if not set, the default parameter will be the value. The way to set the parameters is to add them on the command line

```
-D<property> = propertyValue
Eg: -DClassCallGraph = true
```

```java
@Parameter(property = "Repair", defaultValue = "true") public boolean Repair; // The output redundancy depends on the repair scheme 
@Parameter(property = "TreeCallGraph", defaultValue = "true") public boolean TreeCallGraph; // Output package-grained call graph (including reflection analysis) 
@Parameter(property = "ClassCallGraph", defaultValue = "false") public boolean ClassCallGraph; // Output project class granularity call graph (including reflection analysis) 
@Parameter(property = "reflect", defaultValue = "true") public boolean reflect; // Class Granularity Reflection Analysis 
@Parameter(property = "outDir", defaultValue = "null") public String outDir; // Set the result output path, the default is the project directory
```

## Step 4: Viewing the results
* Bloated dependency detection reports
Path: In /bloatedOutput folder under project root by default\\
**The output path can be customized by using the call interface or the `-DoutDir` command-line argument**
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

* Bloated dependency repair scheme

The fix is named：`pom-result.xml`\\
Path: View the path After Repair Pom Path in the redundancy detection report log
