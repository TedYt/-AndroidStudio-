# -AndroidStudio-

1、Eclipse 导出Gradle项目，然后再由Android studio加载项目，是出现问题
 unrecognized windows sockets error 5 connect
 尝试改变下Gradle的路径。
 另外：Eclipse要导出Gradle项目，ADT版本要在22或者以上

2、Android Gradle Build Error:Some file crunching failed, see logs for details解决办法

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
