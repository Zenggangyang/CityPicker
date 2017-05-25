CityPicker
===

[![API](https://img.shields.io/badge/API-14%2B-yellow.svg?style=flat)](https://android-arsenal.com/api?level=14)</br>
一个仿大众点评的城市快速选择器</br>
支持页面样式修改，多元化自定义

ScreenShot
---

| ![](https://github.com/yuruizhe/CityPicker/blob/master/screenshot/Screenshot_2017-05-22-11-22-58.png) | ![](https://github.com/yuruizhe/CityPicker/blob/master/screenshot/Screenshot_2017-05-22-11-23-08.png) | ![](https://github.com/yuruizhe/CityPicker/blob/master/screenshot/Screenshot_2017-05-22-11-22-45.png) |
|---|----|:---:|


Version Log
---
* ``V0.3.0``
  * 简化api调用形式，修改为Rx形式
* ``V0.2.2``
  * 修复进入页面会闪退问题
  * 修复修改右边滑动索引栏颜色时左边拼音标签颜色未修改问题
  * 启动城市选择页面时增加一个步骤见 [Step3](#step3)
* ``V0.1.0``
  * 初始导入

Import
---
###### Maven
``` xml
  <dependency>
  <groupId>com.desmond</groupId>
  <artifactId>CityPicker</artifactId>
  <version>xxx</version>
  <type>pom</type>
</dependency>
``` 
###### Gradle
``` gradle
compile 'com.desmond:CityPicker:xxx'
```
Wiki
---
### Functions
* 支持自定义基础城市列表（beta）
* 支持历史点击城市查询
* 支持自定义热门城市列表
* 支持选择城市返回自定义对象（目前已经囊括：城市名称，城市code（baidu）等）
* 提供方法支持页面样式轻度自定义。或继承CityPickerActivity重写部分UI样式
* 基础数据依赖sqlite提供高效的查询效率
* 与三方定位库解耦
* 支持沉浸式状态栏

### Use
##### Step1
``` xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
 <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```
对于Android 6.0还需要配置动态权限</br>
``` java
Manifest.permission.WRITE_EXTERNAL_STORAGE
```
##### Step2
``` xml
 <activity android:name="com.desmond.citypicker.ui.CityPickerActivity"
           android:screenOrientation="portrait">
 </activity>
```

##### Step3
启动城市选择页面及相关自定义配置
``` java
        CityPicker.with(getContext())        

        //自定义热门城市，输入数据库中的城市id（_id）
        .setHotCitiesId("2", "9", "18", "11", "66", "1", "80", "49", "100");

        //设置定位城市
        .setGpsCity("南京市","315");

        //设置最多显示历史点击城市数量，0为不显示历史城市
        .setMaxHistory(6);

        // 自定义城市基础数据列表，必须放在项目的assets文件夹下，并且表结构同citypicker项目下的assets中的数据库表结构相同
        // 该方法当前为beta版本，不推荐使用
        .setCustomDBName("xx.sqlite");

        // 设置标题栏背景
        .setTitleBarDrawable(...);

        // 设置返回按钮图片
        .setTitleBarBackBtnDrawable(...);

        // 设置搜索框背景
        .setSearchViewDrawable(...);

        // 设置搜索框字体颜色
        .setSearchViewTextColor(...);

        // 设置搜索框字体大小
        .setSearchViewTextSize(...);

        // 设置右边检索栏字体颜色
        .setIndexBarTextColor(...);

        // 设置右边检索栏字体大小
        .setIndexBarTextSize(...);

        // 是否使用沉浸式状态栏，默认使用
        .setUseImmerseBar(true);
        
        // 回调
        .setOnCityPickerCallBack(new IOnCityPickerCheckedCallBack()
        {
           @Override
           public void onCityPickerChecked(BaseCity baseCity)
           {
               //获取选择城市编码
               baseCity.getCode();
        
               //获取选择城市名称
               baseCity.getCityName();
        
               // 获取选择城市拼音全拼（历史城市可能为空）
               baseCity.getCityPinYin();
        
               //获取选择城市拼音首字母（历史城市可能为空）
               baseCity.getCityPYFirst();
           }
         })
         
        .open();
      
 ```


### Be careful
* 基础数据库名称定义为：**city.sqlite**。在引入的工程中千万不可创建**同名的数据库**，否则可能会发生异常！

* 自定义基础数据库必须重写``city.sqlite``中的``tb_city`` 和 ``tb_history``, 允许增加字段，但不可删除或修改字段


Demo
---
手机扫描下方二维码下载demo尝鲜</br>
![](https://www.pgyer.com/app/qrcode/ecVs)

Thanks
---
* https://github.com/gjiazhe/WaveSideBar
* https://github.com/square/sqlbrite

Contact author
---
QQ 350248823</br>
欢迎issues，作者看到后会第一时间回复
