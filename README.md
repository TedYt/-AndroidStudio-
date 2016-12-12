# -AndroidStudio-

###Eclipse 导出Gradle项目，然后再由Android studio加载项目，是出现问题
 unrecognized windows sockets error 5 connect
 尝试改变下Gradle的路径。
 另外：Eclipse要导出Gradle项目，ADT版本要在22或者以上

###Android Gradle Build Error:Some file crunching failed, see logs for details解决办法

在主工程文件夹下的build点gradle文件里，加两句：

aaptOptions点cruncherEnabled = false

aaptOptions点useNewCruncher = false

例如：

android {

compileSdkVersion 22

buildToolsVersion "23.0.1"

aaptOptions.cruncherEnabled = false

aaptOptions.useNewCruncher = false

defaultConfig {

minSdkVersion 5

targetSdkVersion 17

}

###JNI ERROR (app bug): accessed stale weak global reference 0xa71acllf (index 45127 in ...)

出错的原因可能是函数返回值不对应。比如C++里方法的返回值jint，但是java里的却写成了string


###新建project或者module，生成build.gradle的模版文件的路径
<Android studio>/plugins/android/lib/templates/gradle-projects/NewAndroidModule

###工程顶层的build.gradle 和 settings.gradle等一些文件的模版文件的路径
<Android studio>/plugins/android/lib/templates/gradle-projects/NewAndroidProject


###aar包的使用
1、将aar包放在在module根目录下的libs目录（例如app/libs）中

2、在module的build.gradle加上下面的内容：
```java
dependecies {
  compile (name:'aar包名不带aar扩展名', ext:'aar')
}

repositories {
   flatDir(){
      dir 'libs'
   }
}
```

###配置JNI代码
由NDK编译转Cmake编译时，注意CPPFlags的添加：
Android.mk中有一个LOCAL_CPPFLAGS，对应Cmake中的配置为：
在build.gradle中增加如下代码：
```java
android{
    ...
    defaultConfig {
    ...
       externalNativeBuild{
          cmake {
               cppFlags "-ftti -fexceptions -D_UNICODE ..."
          }
       }
    }
}
```
