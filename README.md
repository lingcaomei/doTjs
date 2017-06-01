# doTjs
doTjs前端javascript模板引擎,Node.js和浏览器同样适用

#### 使用方法：
```
{{= }} 赋值 
{{ }} for循环json 
{{~ }} 循环数组      
{{? }} if 条件语句           
{{! }} html标签是否转义           
{{# }} for compile-time evaluation/includes and partials           
{{## #}} for compile-time defines               
```

#### 语句
```
1、for循环json

{{ for (var key in data){ }} 
{{= key }} 
{{ } }}

2、循环数组：data.array 传进来的数据，item是每项，index是每项的下标

{{~data.array:item:index }}
{{= item}}
{{~}}

3、if判断 

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
  var interText = doT.template($("#J_child").text());
  $("#J_prt1").html(interText(data));
```
- for循环json：
```
格式：{{ }}    

区域：<div id="J_parent"></div>   

数据源： var data = {"name":"莉莉", age:27, tel: 134533298880}

模板： for(var key in it){ } for语句 分别用{{ }} 包裹
  <script id="J_child" type="text/template">
	{{for(var key in it){ }}   
	    <div>KEY: {{=key}}</div>
	    <div>KEY: {{= it[key]}}</div>
	{{} }}
  </script>
  
  //    [[for(var key in it){ ]] 
  //	    <div>KEY: {{=key}}</div>
  //	    <div>KEY: {{= it[key]}}</div>
  //	[[} ]]
调用：             
  var data = {"name":"莉莉", age:27, tel: 134533298880};
  var interText = doT.template($("#J_child").text());
  $("#J_prt1").html(interText(data));
```
- 循环数组：
```
格式：{{~ }}    

区域：<div id="J_parent"></div>   

数据源： var data = {"fruit":["apple","pear","watermelon"]}

模板：
  <script id="J_child" type="text/template">
	{{~ it.fruit:item:index }}
	    <div>{{=index}}、{{=item}}</div>
	{{~}}
  </script>
  
调用：             
  var data = {"name":"莉莉", age:27, tel: 134533298880};
  var interText = doT.template($("#J_child").text());
  $("#J_prt1").html(interText(data));
```
