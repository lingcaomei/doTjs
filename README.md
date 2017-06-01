# doTjs
doTjs前端javascript模板引擎,Node.js和浏览器同样适用

#### 使用方法：
```
{{= }} 赋值 
{{ {}} for循环json 
{{~ }} 循环数组      
{{? }} if 条件语句           
{{! }} html标签是否转义           
{{# }} for compile-time evaluation/includes and partials           
{{## #}} for compile-time defines               
```

#### 语句
```
- 1、for循环json
{{ for var key in data { }} 
{{= key }} 
{{ } }}

-2、循环数组：data.array 传进来的数据，item是每项，index是每项的下标
{{~data.array:item:index }}
{{= item}}
{{~}}

-3、if判断   
{{? }} if
{{?? }} else if
{{??}} else

```

#### dot.js调用方式：
```
var tmpText = doT.template(模板);
$('body').html(tmpText(数据源));
```

注意：
数据源data，在模板中为it

#### 调用例子：

- 赋值：
```
格式：{{= }}  

区域：<div id="J_parent"></div>   

数据源： var data = {"name":"莉莉", age:27}

模板：  
  <script id="J_child" type="text/template">
	<div>Hi, My name is {{=it.name}}!</div>
	<div>{{=it.age || ''}}</div>
  </script>
  
调用：             
  var data = {"name":"Jake","age":27};
  var interText = doT.template($("#J_child1").text());
  $("#J_prt1").html(interText(data));
```
