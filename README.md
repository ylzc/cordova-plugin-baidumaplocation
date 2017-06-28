基于aruis/cordova-plugin-baidumaplocation 进行修改

基于百度地图Android版定位SDK（v7.1，全景定位）以及百度地图IOS SDK （v3.2.1）


```shell
cordova plugin add cordova-plugin-baidumaplocation --variable ANDROID_KEY="<API_KEY_ANDROID>" --variable IOS_KEY="<API_KEY_IOS>"
# 此处的API_KEY_XX来自于第一步，直接替换<API_KEY_XX>，也可以最后跟 --save 参数，将插件信息保存到config.xml中
# 如果只需要Android端或者IOS端，可以只填写一个相应的AK，但是都不填肯定不行
```

#### 三，使用方法

```javascript
// 进行定位
baidumap_location.getCurrentPosition(function (result) {
    console.log(JSON.stringify(result, null, 4));
}, function (error) {

},{timeout:3000});
```

获得定位信息，返回JSON格式数据:

```javascript
{
    "time": "2017-02-25 17:30:00",//获取时间
    "latitude": 34.6666666,//纬度
    "lontitude": 117.8888,//经度
    "radius": 61.9999999,//半径
 
    //--------Android 独享 begin
    "locType": 161,//定位类型                                            
    "locTypeDescription": "NetWork location successful!",//定位类型解释   
    "userIndoorState": 1,//是否室内                                     
    //--------Android 独享 end
    
    //--------IOS 独享 begin
    "title": "我的位置",//定位标注点标题信息
    "subtitle": "我的位置",//定位标注点子标题信息
    //--------IOS 独享 end
}
```
具体字段内容请参照：
>[Android版 BDLocation v7.1](http://wiki.lbsyun.baidu.com/cms/androidloc/doc/v7.1/index.html)

>[IOS版 BMKUserLocation](http://wiki.lbsyun.baidu.com/cms/iossdk/doc/v3_2_0/html/interface_b_m_k_user_location.html#aba4b76e55f4605c5554fe16aca1b4fbf) 

如果Android版获取到的信息是：

```json
{
    "locType": 505,
    "locTypeDescription": "NetWork location failed because baidu location service check the key is unlegal, please check the key in AndroidManifest.xml !",
    "latitude": 5e-324,
    "lontitude": 5e-324,
    "radius": 0,
    "userIndoorState": -1,
    "direction": -1
}
```

