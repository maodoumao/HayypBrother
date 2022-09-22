SDK 接入步骤
1.在项目根目录下的build.gradle文件中增加以下代码

    buildscript {
        repositories {
            //添加远程仓库
           maven {
                url "https://hello-rummy.oss-accelerate-overseas.aliyuncs.com/gameConfig/1007/repo/"
            }
        }
        dependencies {
            ....
            //添加依赖库
            classpath "com.happy.brother:junkcode:1.0.1"
        }
    }

    allprojects{
        repositories {
            .....
            //添加远程仓库
            maven {
                url "https://hello-rummy.oss-accelerate-overseas.aliyuncs.com/gameConfig/1007/repo/"
            }
            ....
        }
    }

2.在app/build.gradle应用

 apply plugin: 'com.android.application'
 apply plugin: 'com.brother.junkcode'

//这两个要写32 compileSdkVersion 32 targetSdkVersion 32

android {
    compileSdkVersion 32
    defaultConfig {
        ....
        targetSdkVersion 32
        multiDexEnabled true
        ....
    }
...

dependencies {
    ......
    //添加需要的库
    implementation 'com.happy.brother:game2dx:1.0.1@aar'
    implementation 'com.happy.brother:brother1007:1.0.2@aar'
    implementation 'com.google.android.gms:play-services-ads-identifier:17.0.1'
    implementation 'com.google.android.gms:play-services-ads:19.6.0'
    implementation "com.android.billingclient:billing:5.0.0"
    implementation 'com.google.android.play:core:1.9.1'
    implementation 'androidx.work:work-runtime:2.7.1'
    implementation 'androidx.appcompat:appcompat:1.0.2'
    implementation 'com.android.support:multidex:1.0.3'
    ......
}

//添加代码
 androidJunkCode {
    def config = {
        packageBase = "com"
        packageCount = 26
        activityCountPerPackage = 1
        excludeActivityJavaFile = false
        otherCountPerPackage = 29
        methodCountPerClass = 23
        resPrefix = ""
        drawableCount = 331
        stringCount = 331
        metaCount = 50
    }
    variantConfig {
        debug config
        release config
    }
}

3.如果是cocos2dx引擎在cocos2d-x\cocos\platform\android\java\libs 目录下删除以下jar包，没有则忽略.

    com.android.vending.expansion.zipfile.jar
    okhttp-3.12.7.jar
    okio-1.15.0.jar
    删除后在libcocos2dx/build.gradle 增加以下代码
    dependencies {
        ....
        implementation 'com.happy.brother:game2dx:1.0.1@aar'
    }



4.AndroidManifest.xml 修改启动activity

    <activity
        .....
        <!--你的启动 activity 去掉-->
        <!-- <intent-filter> -->
        <!--    <action android:name="android.intent.action.MAIN" /> -->
        <!--    <category android:name="android.intent.category.LAUNCHER" /> -->
        <!-- </intent-filter> -->

        <!-- 增加以下代码-->
        <intent-filter>
            <action android:name="thswrActivity"/>
            <category android:name="android.intent.category.DEFAULT"/>
            <category android:name="tornado"/>
        </intent-filter>
    </activity>

5.测试好发布apk和aab包 jks签名文件 密码 发给我们，坐等上包


============================================================================================================================================
