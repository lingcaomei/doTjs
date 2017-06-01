# doTjs
doTjs前端javascript模板引擎,Node.js和浏览器同样适用
## 使用方法：
{{= }} 赋值
{{ }}  
{{~ }} for循环数组
{{? }} if 条件语句
{{! }} html标签是否转义
{{# }} for compile-time evaluation/includes and partials
{{## #}} for compile-time defines


## dot.js调用方式：
var tmpText = doT.template(模板);
$('body').html(tmpText(数据源))
