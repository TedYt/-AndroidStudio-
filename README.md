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

###显性Intent
关键一点就是看在新建对象时，有没有指定ComponenteName属性，因为这个属性明确的指出了调用的类名，例如：
1.
```java
Intent mIntent = new Intent(IntentActivity.this, TestActivity.class);
```
2.
```java
ComponentName componentName = new ComponentName(IntentActivity.this, TestActivity.class);
Intent intent = new Intent();
intent.setComponent(componentName);
```
3.
```java
ComponentName componentName = new ComponentName("com.test.demo", "com.test.demo.MainActivity");
Intent intent = new Intent();
intent.setComponent(componentName);
```
上面三种形式是等价的，都明确指出了要调用的类

###隐性Intent
关键是要在manifest文件中的定义：
```html
<activity android:name=".activity.TestActivity">
    <intent-filter>
        <action android:name="jackaltsc.intent.action.test"/>
        <category android:name="android.intent.category.DEFAULT"/>
    </intent-filter>
</activity>
```

```java
Intent intent = new Intent();
intent.setAction("jackaltsc.intent.action.test");
startActivity(intent);
```

###AppCompat_v7包
这个包的作用是让Android2.1以上都能使用Android4.0版本的界面的支持库
所以在最小sdk版本为4.0以上时，就可以不加这个库。
