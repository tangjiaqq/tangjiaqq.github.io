---
title: Android私服依赖
date: 2019-06-11 12:48:03
description: Android私服依赖发布（本地文件夹）
categories:
- Android
tags: 
- Gradle
- 私服
---

```groovy
//这种方式是只包含一个aar进去不含任何源码把aar 转换为在线依赖
apply plugin: 'maven-publish'
task generateSourcesJar(type: Jar) {
    from android.sourceSets.main.java.srcDirs
    classifier 'sources'
}
publishing {
    publications {
        maven(MavenPublication) {
            groupId "包名"
            artifactId "${project.name}"
            // 发布的aar包含这个文件
            artifact("*.aar")
             //如果还需要上传lib的代码需要添加下面的这句话  命令与之对应
            afterEvaluate { artifact(tasks.getByName("bundleReleaseAar")) }
             // 上传source，这样使用方可以看到方法注释
            artifact generateSourcesJar
            
            version "1.0.0"
        }
    }
    repositories {
        maven {
            //私服的本地路径
            url = "${getRootDir()}/repo"
        }
    }
}
task generateLib {
    dependsOn publishMavenPublicationToMavenRepository
    group 'publishing'
    doLast {
        exec {
            commandLine "git", "add", "${getRootDir()}/repo"
        }
    }
}
//如何使用  项目根的build.gradle文件夹中添加
 maven { url "${getRootDir()}/repo" }
```

