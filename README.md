
#第三方获取口袋native方法
__调用方式__
```
	window.location.href = 'native://takePhotoFromCamara/callback/|';
```	
	或者
	
```
	var element = document.createElement("element");
	var url = 'talkingdata:{"functionName":"trackEvent","arguments":[]}';
	element.setAttribute("src",url);
	document.body.appendChild(emement);
	element.parentNode.removeChild(element);
	element = null;
```

__返回值处理__

所有的返回值`JSON String`都需要`url decode`一下，经过webview会自动做URL编码转换

##H5调用口袋Native函数
####请求调用本地方法####
**格式**
    
    native://<method>/<callback>/<param1>|<param2>
    
**参数**

|参数 | 类型 | 说明 | 示例 |
|----|----|-----|----|
|`native://`|string|前缀(请求头)|`native://GOBACK_TO_PAEBANK//|`|
|`method`|string|调用的函数名|`getContents`|
|`callback`|string|返回值,js获取后调用的函数名||
|`param1|param2`|string|需要的参数，使用`|`分割开|
**示例**

	
	
**方法列表**

|功能|方法|参数 |      开始提供支持版本                 |                                         
|:---|---|---|---|
|返回native|`native://GOBACK_TO_PAEBANK//|`|无||
|关闭加载动画|`native://endLoading//|`|无||
|获取拍照照片|`native://takePhotoFromCamara/callback/|`|无||
|获取相册图片|`native://takePhotoFromPhotoLibrary/callback/|`|无||
|获取图库图片|`native://takePhotoFromAlbum/callback/|`|无||
|获取本地通讯录|`native://getContacts/callback/|`|无||
|分享功能|`native://share_mgm//{json参数}|`|`{share_url:分享链接,image_url:图片链接,context:内容,mgmFlowId:id,flag:pabank_share_type_msg}`||
|打开网页|`native://forwardWebUrl//urlString|webTitle`|参数为url和标题||
|利用口袋h5跳转锚点|`native://handleSkipMenu//{参数json}|`|json格式就行||
|获取设备信息|`native://getAppInfo/getAppInfo/|`|返回值：`{appVersion:”2.7.3”,systemType:”iOS/Android’,systemVersion:’10.0'}`||
|直接跳转锚点|`native://handleThirdSkipMenu//{JSON}|`|参数{'menuIndex' ：string , 'param' ：{} }|


##TalkingData

**格式**


    talingdata:{"functionName":"XXXX","arguments":[参数]}

**参数**

|参数 | 类型 | 说明 | 示例|
|----|----|----|----|
|`talkingdata:`|string|前缀||
|`functionName`|string|调用的函数名称|trackEvent|
|`arguments`|array|string类型的数组| eventId 为 homeView ，eventLabel为login，数组为`["homeView","login"]`|

**示例**



**方法**

_getDeviceId_   

`talkingdata:{"functionName":"getDeviceId",@"arguments":["deviceId"]}`

|参数|类型|说明|示例|
|---|---|---|---|
|getDeviceId|string|函数名，固定值|
|deviceId|string|返回值的key||


_setLocation_

`talkingdata:{"functionName":"setLocation:",@"arguments":["latitude","longitude"]}`

|参数|类型|说明|示例|
|---|---|---|---|
|setLocation|string|函数名，固定值||
|latitude|string|返回值的key||
|longitude|string|返回值的key|



_trackEvent_

`talkingdata:{"functionName":"trackEvent:",@"arguments":["eventId"]}`

|参数|类型|说明|示例|
|---|---|---|---|
|trackEvent|string|函数名，固定值||
|eventId|string|跟踪的事件名|`"arguments":["首页"]`|

_trackEventWithLabel_

`talkingdata:{"functionName":"trackEventWithLabel:",@"arguments":["eventId","eventLabel"]}`

|参数|类型|说明|示例|
|---|---|---|---|
|trackEvent|string|函数名，固定值||
|eventId|string|跟踪的事件名|`"arguments":["首页","登录"]`|
|eventLabel|string|跟踪事件标签|同上|

_trackPageBegin_  、 _trackPageEnd_

`talkingdata:{"functionName":"trackPageBegin:",@"arguments":["pageName"]}`
`talkingdata:{"functionName":"trackPageEnd:",@"arguments":["pageName"]}`


|参数|类型|说明|示例|
|---|---|---|---|
|trackPageBegin|string|监控页面开始|
|trackPageEnd|string|监控页面结束|
|pageName|string|要跟踪的页面名|`"更多"`页面|


##错误信息

发现H5调用的方法没有找到的时候。统一返回一个JSON数据。
```
{
	errcode:’01’,
	errmsg:’方法没找到’
}
```
