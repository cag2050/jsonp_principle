* JSONP原理： 
1. 首先在客户端注册一个callback, 然后把callback的名字传给服务器。 
2. 此时，服务器先生成 json 数据。 
3. 然后以 javascript 语法的方式，生成一个function , function 名字就是传递上来的callback参数值 . 
4. 最后将 json 数据直接以入参的方式，放置到 function 中，这样就生成了一段 js 语法的文档，返回给客户端。 
5. 客户端浏览器，解析script标签，并执行返回的 javascript 文档，此时数据作为参数，传入到了客户端预先定义好的 callback 函数里.

* jsonp 原理，代码示意：  
本地定义的函数===
```
<script>
    function local_func(data) {
        // 函数内容
    }
</script>
```
返回的数据放在srcipt标签里===
```
<script src="http://api.douban.com/v2/movie/in_theaters?callback=local_func"></script>
等价于：
<script>
    ;local_func([返回的数据])
</script>

```

* 2种方式：
1. jsonp 在原生js中的实现:  
通过src="http://api.douban.com/v2/movie/in_theaters?callback=local_func"。   
直接输入访问：http://api.douban.com/v2/movie/in_theaters ，返回的数据是一个对象：{xxx}。  
直接输入访问：http://api.douban.com/v2/movie/in_theaters?callback=? ，返回的数据是一个对象：{xxx}。  
直接输入访问：http://api.douban.com/v2/movie/in_theaters?callback=local_func ，返回的数据是：;local_func({xxx})。  
注意点：  
callback指定的回调函数，是客户端注册的，必须是定义在window下的全局函数。  
例子网址：http://htmlpreview.github.io/?https://github.com/cag2050/jsonp_principle/blob/master/src/jsonp_js.html  
1. jsonp 在jquery ajax中的实现:  
例子网址：http://htmlpreview.github.io/?https://github.com/cag2050/jsonp_principle/blob/master/src/jsonp_jquery.html