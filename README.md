# doTjs
doTjs前端javascript模板引擎,Node.js和浏览器同样适用

#### 使用方法：
{{= }} 赋值 
{{ }}  
{{~ }} for循环数组 
{{? }} if 条件语句 
{{! }} html标签是否转义 
{{# }} for compile-time evaluation/includes and partials 
{{## #}} for compile-time defines 


#### dot.js调用方式：
```
var tmpText = doT.template(模板);
$('body').html(tmpText(数据源))

```

注意：
数据源data，在模板中为it

#### 调用例子：

- 赋值：
格式：{{= }}
数据源： var data = {"name":"莉莉", age:27}
模板：
调用：
