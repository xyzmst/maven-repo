# How to use

Simply add the repository to your build.gradle file:
```
repositories {
    maven {
        url 'https://raw.githubusercontent.com/xyzmst/maven-repo/master/'
    }
    mavenCentral()
}
```
And you can use the artifacts like this:
```
dependencies {
    compile 'org.xyzmst:wxsdk:1.0'
    compile 'org.xyzmst:alisdk:1.0'
    compile 'org.xyzmst:ViewPagerIndicator:2.4.1'
    compile 'org.xyzmst:DatePicker:2.2.0'
    compile 'org.xyzmst:materialfilepicker:1.0.8'
    compile 'org.xyzmst:pay:1.0.4'
    compile 'de.greenrobot:eventbus:2.2.1'
    compile 'org.xyzmst:sprinkles:2.1.12'
    compile 'org.xyzmst:android-gif-drawable:1.1.17'
}
```

### 说明
- pay: 支付集成
  1.0.2 修复了 因java中package是关键字，而订单详情的返回值为package ，"Sign=WXPay"无法添加到订单详情导致无法打开微信的问题
- DatePicker ： 日期选择    
- materialfilepicker: 文件选择器
- sprinkles :数据库
- android-gif-drawable：gif
