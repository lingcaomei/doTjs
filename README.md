# doTjs
doTjs前端javascript模板引擎,Node.js和浏览器同样适用

#### 使用方法：
```
{{= }} 赋值 
{{ }} for循环json 
{{~ }} 循环数组      
{{? }} if 条件语句           
{{! }} html标签不转义           
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
- if条件判断：
```
格式：{{? }}    

区域：<div id="J_parent"></div>   

数据源： var data = {"name":"Jake","age":31}

模板：
  <script id="J_child" type="text/template">
	{{? it.name }}
	    <div>Oh, I love your name, {{=it.name}}!</div>
	{{?? it.age === 0}}
	    <div>Guess nobody named you yet!</div>
	{{??}}
	    You are {{=it.age}} and still don't have a name?
	{{?}}
  </script>
  
调用：             
  var data = {"name":"Jake","age":31};
  var interText = doT.template($("#J_child").text());
  $("#J_prt1").html(interText(data));
```
- html标签不转义：
```
格式：{{! }}    

区域：<div id="J_parent"></div>   

数据源： var data = {"html":"<div style='background: #f00; height: 30px; line-height: 30px;'>html元素</div>"}

模板：
  <script id="J_child" type="text/template">
	{{! it.html}}
  </script>
  
调用：             
  var data = {"html":"<div style='background: #f00; height: 30px; line-height: 30px;'>html元素</div>"};
  var interText = doT.template($("#J_child").text());
  $("#J_prt1").html(interText(data));
```
- 编译时为片段中符合规则的语句赋值：
```
格式：片段{{##def.snippet: html片段 #}}{{#def.snippet}} ，若值中包含规则语句使用（包含在片段中）：{{#def.joke}}   

区域：<div id="J_parent"></div>   

模板：
  <script id="J_child" type="text/template">
	{{##def.snippet:
	    <div>{{=it.name}}</div>{{#def.joke}}
	#}}
	{{#def.snippet}}
  </script>
  
调用：             
  var dataPart = {"name":"Jake","age":31};
  var defPart = {"joke":"<div>{{=it.name}} who?</div>"};
  var interText = doT.template($("#J_child").text(), undefined, defPart);
  $("#J_prt").html(interText(dataPart));
```
