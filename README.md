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
}
```

### 说明
DatePicker ： 日期选择
materialfilepicker: 文件选择器

