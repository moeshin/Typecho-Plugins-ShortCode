# Typecho ShortCode 短代码插件
Typecho ShortCode 是一款用于自定义短代码的Typecho插件
## 函数说明
使用以下函数来自定义短代码，均为公开静态
### ShortCode::set
注册短代码，返回一个`ShortCode`实例

参数名|类型|说明
:-|:-|:-
names|mixed|短代码名称，可以一个字符串或字符串数组
callbacks|mixed|短代码对应回调函数，可以一个回调函数或回调函数数组
overried|bool|覆盖已存在的短代码设置<br>可选，默认`false`
### ShortCode::get
获取已注册短代码列表，返回数组，格式例如：
```php
array{
	[短代码名称] => 回调函数或回调函数名
	...
}
```
### ShortCode::remove
移除已注册的短代码，返回一个`ShortCode`实例

参数名|类型|说明
:-|:-|:-
names|string|短代码名称
callbacks|callback|只有回调函数相同，短代码才会被移除<br>可选，默认`null`
### ShortCode::removeAll
移除所有已注册短的代码，返回一个`ShortCode`实例
### ShortCode::isForce
是否强制处理内容，返回布尔值，当前设置
使用此插件后Markdown或AutoP失效，使用此函数，并传入`true`值

参数名|类型|说明
:-|:-|:-
bool|bool|可选，默认`null`
### ShortCode::handle
字符串处理，返回字符串

参数名|类型|说明
:-|:-|:-
content|string|要处理的字符串
## 短代码回调函数参数说明
参数名|类型|说明
:-|:-|:-
name|string|短代码名称
attr|string|短代码属性
text|string|短代码内容
code|string|整条短代码内容
## 注册短代码例子
### #1 一个对一个
```php
ShortCode::set('video',function ShorCode($name,$attr,$text,$code){
	return '<video controls="controls"'.$attr.'><source src="'.$text.'"></video>';
});
```
### #2 多个对一个
```php
ShortCode::set(['video','audio'],'ShorCode');
function ShorCode($name,$attr,$text,$code){
	switch($name){
		case 'video':
			return '<video controls="controls"'.$attr.'><source src="'.$text.'"></video>';
		case 'audio':
			return '<audio controls="controls"'.$attr.'><source src="'.$text.'"></audio>';
	}
	return $code;
}
```