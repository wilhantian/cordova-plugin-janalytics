# cordova-plugin-janalytics
极光的 Cordova 数据统计插件。
> 此插件包含jcore，当你的APP总使用了不止一个极光服务，请使用`cordova-plugin-janalytics-no-jcore`

## Install
- 通过cordova plugin 安装，要求 Cordova CLI 5.0+：
``` shell
cordova plugin add cordova-plugin-janalytics --variable API_KEY=极光KEY --variable CHANNEL=渠道名
```
- 或直接通过 url 安装：
``` shell
cordova plugin add https://github.com/wilhantian/cordova-plugin-janalytics --variable API_KEY=极光KEY --variable CHANNEL=渠道名
```
- 或下载到本地安装：
``` shell
cordova plugin add Your_Plugin_Path  --variable API_KEY=极光KEY --variable CHANNEL=渠道名
```
> 注意: CHANNEL不能为纯数字

## Usage
> - 用例中的'success', 'error'参数代表成功回调函数与失败回调函数.
> - extMap为附加参数，仅能纯属一个小于10个字段的1级key-value对象
>   正确用例：`{ a:1, b:2, c: 3}`
>   错误用例：`{a: {c: 1, b:2}}`
>
>   下面将不再提及

- 设置是否开启debug模式(开启后将打印更多调试信息)
  Janalytics.setDebugModel(enable, success, error);

``` javascript
Janalytics.setDebugModel(true, 
	function(){
        alert("操作成功");
	}, 
	function(err){
		alert(err);
	}
);
```

- 记录页面启动
  Janalytics.onPageStart(pageName, success, error)

``` javascript
Janalytics.onPageStart("登陆页面", function(){}, function(err){});
```

- 记录页面结束
  Janalytics.onPageEnd(pageName, success, error)

``` javascript
Janalytics.onPageEnd("登陆页面", function(){}, function(err){});
```

- 自定义计数事件
  Janalytics.onCountEvent(eventId, extMap, success, error)

``` javascript
Janalytics.onCountEvent("计数事件测试", {a:1, b:2}, function(){}, function(err){});
```

- 自定义计算事件
  Janalytics.onCalculateEvent(eventId, eventValue, extMap, success, error)

``` javascript
Janalytics.onCalculateEvent("计算事件测试", 1.2, {a:1, b:2}, function(){}, function(err){});
```

- 登陆事件
  Janalytics.onLoginEvent(loginMethod, loginSuccess, extMap, success, error)

``` javascript
Janalytics.onLoginEvent("QQ登陆", true, {a:1, b:2}, function(){}, function(err){});
```

- 注册事件
  Janalytics.onRegisterEvent(registerMethod, registerSuccess, extMap, success, error)

``` javascript
Janalytics.onRegisterEvent("手机号注册", true, {a:1, b:2}, function(){}, function(err){});
```

- 浏览事件
  Janalytics.onRegisterEvent(
    browseId, //浏览ID [string]
    browseName,//浏览名 [string]
    browseType,//浏览类型 [string]
    browseDuration,//浏览时长 [long]
    extMap,
    success, error
  )

- 购买事件
  Janalytics.onPurchaseEvent(
    purchaseGoodsid, //商品ID [string]
    purchaseGoodsName, //商品名 [string]
    purchasePrice, //商品价格 [float]
    purchaseSuccess, //是否购买成功  [booleabn]
    purchaseCurrency, //货币类型  [string] ("USD":美元，"CNY":人民币)
    purchaseGoodsType, //商品类型 [string]
    purchaseGoodsCount, //商品数量 [int]
    extMap,
    success, error
  )