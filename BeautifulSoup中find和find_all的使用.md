[来源出处](https://blog.csdn.net/weixin_42970378/article/details/83108206)

### #导入beautifulsoup模块


```python
from bs4 import BeautifulSoup
```

### #HTML例子


```python
html = '''
<html>
    <head>
        <title>
            index
        </title>
    </head>
    <body>
         <div>
                <ul>
                     <li id="flask"class="item-0"><a href="link1.html">first item</a></li>
                    <li class="item-1"><a href="link2.html">second item</a></li>
                    <li class="item-inactie"><a href="link3.html">third item</a></li>
                    <li class="item-1"><a href="link4.html">fourth item</a></li>
                    <li class="item-0"><a href="link5.html">fifth item</a>
                 </ul>
         </div>
        <li> hello world </li>
    </body>
</html>
'''
```

### #构建beautifulsoup实例


```python
soup = BeautifulSoup(html,'lxml')
```

- 第一个参数是要匹配的内容
- 第二个参数是beautifulsoup要采用的模块,即规则
- html.parser是python内置的结构匹配方法，但是效率不如lxml所以不常用
- lxml 采用lxml模块
- html5lib,该模块可以将内容转换成html5对象
- 若想要以上功能,就需要具备对应的模块，比如使用lxml就要安装lxml

### #在bs4当中有很多种匹配方法,但常用有两种:

## 1.find查找一次

只返回第一个匹配到的对象

   语法：   find(name, attrs, recursive, text, **wargs)


```python
li = soup.find('li')
```


```python
print('find_li:',li)
```

    find_li: <li class="item-0" id="flask"><a href="link1.html">first item</a></li>
    


```python
print('li.text(返回标签的内容):',li.text)
```

    li.text(返回标签的内容): first item
    


```python
print('li.attrs(返回标签的属性):',li.attrs)
```

    li.attrs(返回标签的属性): {'id': 'flask', 'class': ['item-0']}
    


```python
print('li.string(返回标签内容为字符串):',li.string)
```

    li.string(返回标签内容为字符串): first item
    

### #find可以通过"属性 = 值"的方法进行select


```python
li = soup.find(id = 'flask')
```


```python
print(li,'\n')
```

    <li class="item-0" id="flask"><a href="link1.html">first item</a></li> 
    
    

### #因为class是python的保留关键字，所以无法直接查找class这个关键字

### # 有两种方法可以进行class属性查询
- 第一种:在attrs属性用字典进行传递参数


```python
find_class = soup.find(attrs={'class':'item-1'})
```


```python
print('findclass:',find_class,'\n')
```

    findclass: <li class="item-1"><a href="link2.html">second item</a></li> 
    
    

- 第二种:BeautifulSoup中的特别关键字参数class_


```python
beautifulsoup_class_ = soup.find(class_ = 'item-1')
```


```python
print('BeautifulSoup_class_:',beautifulsoup_class_,'\n')
```

    BeautifulSoup_class_: <li class="item-1"><a href="link2.html">second item</a></li> 
    
    

## 2.find_all 查找所有

返回所有匹配到的结果，区别于find（find只返回查找到的第一个结果）

语法：find_all(name, attrs, recursive, text, limit, **kwargs)


```python
li_all = soup.find_all('li')
```


```python
for li_all in li_all:
	print('---')
	print('匹配到的li:',li_all)
	print('li的内容:',li_all.text)
	print('li的属性:',li_all.attrs)
```

    ---
    匹配到的li: <li class="item-0" id="flask"><a href="link1.html">first item</a></li>
    li的内容: first item
    li的属性: {'id': 'flask', 'class': ['item-0']}
    ---
    匹配到的li: <li class="item-1"><a href="link2.html">second item</a></li>
    li的内容: second item
    li的属性: {'class': ['item-1']}
    ---
    匹配到的li: <li class="item-inactie"><a href="link3.html">third item</a></li>
    li的内容: third item
    li的属性: {'class': ['item-inactie']}
    ---
    匹配到的li: <li class="item-1"><a href="link4.html">fourth item</a></li>
    li的内容: fourth item
    li的属性: {'class': ['item-1']}
    ---
    匹配到的li: <li class="item-0"><a href="link5.html">fifth item</a>
    </li>
    li的内容: fifth item
    
    li的属性: {'class': ['item-0']}
    ---
    匹配到的li: <li> hello world </li>
    li的内容:  hello world 
    li的属性: {}
    

### #最灵活的使用方式


```python
li_quick = soup.find_all(attrs={'class':'item-1'})
```


```python
for li_quick in li_quick:
	print('最灵活的查找方法:',li_quick)
```

    最灵活的查找方法: <li class="item-1"><a href="link2.html">second item</a></li>
    最灵活的查找方法: <li class="item-1"><a href="link4.html">fourth item</a></li>
    
