gradle是一个自动构建工具，使用特定的语言Groovy来配置

主要面向java应用，这里只关注android开发

## 相关文件

使用android-studio创建一个应用

发现有些相关的文件

* build.gralde
* settings.gradle
* gradle.properties 传统配置非groovy语言,环境变量配置
* app/build.gradle

### build.gradle
```
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.3.0'
    }
}

allprojects {
    repositories {
        jcenter()
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}


```

上面的代码指定了自动下载的来源及依赖项，以及clean任务

但还不明白如何构建，因为这部分代码在settings.gradle文件中

### settings.gradle

```
include ':app'

```

### app/build.gradle

```
apply plugin: 'com.android.application'

android {
    compileSdkVersion 25
    buildToolsVersion "25.0.0"
    defaultConfig {
        applicationId "com.bwp.b3marketplacemerchantclient"
        minSdkVersion 23
        targetSdkVersion 25
        versionCode 1
        versionName "1.0"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:25.+'
    compile 'com.android.support:design:25.+'
}


```








## 参考

- [用Gradle 构建你的android程序 2013.5](http://www.cnblogs.com/youxilua/archive/2013/05/20/3087935.html)
- [给 ANDROID 初学者的 GRADLE 知识普及](http://stormzhang.com/android/2016/07/02/gradle-for-android-beginners/)