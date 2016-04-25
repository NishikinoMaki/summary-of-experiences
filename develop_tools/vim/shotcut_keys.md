## vim 快捷键

#### 替换
##### 对当前行进行替换:
<font style="color:red">:s/XXX/YYY/g</font>

XXX是需要替换的字符串,YYY是替换后的字符串。

##### 全局替换
<font style="color:red">:%s/XXX/YYY/g</font>

##### 对指定部分进行替换:
<font style="color:red">用V进入visual模式,再进行:s/XXX/YYY/g</font>
##### 对指定行范围替换:
<font style="color:red">::100,102s/XXX/YYY/g</font>
    
* 替换字符串中的"/" 用"\"转义，即用"\/"表示

#### 查找
在：中输入?或/ ，然后按n或N向后或向前查找

#### 当vim忘记sudo的时候又想保存怎么办??
<font style="color:red">:w !sudo tee %</font>

* tee 是一个把stdin 保存到文件的小工具。
* %，是vim 当中一个只读寄存器的名字，总保存着当前编辑文件的文件路径。

#### 批量注释
* 方法1  

    批量注释:  
    
    <font style="color:red">ctrl+v 进入列编辑模式,向下或向上移动光标,把需要注释的行的开头标记起来,然后按大写的I(shift+i),再插入注释符,比如"//",再按Esc,就会全部注释了</font> 
    
    批量删除注释:  
    
    <font style="color:red">ctrl+v,进入列编辑模式,横向选中列的个数(如"//"注释符号,需要选中两列),然后按d, 就会删除注释符号</font>    

* 方法2 

  根据行号添加注释：  
 <font style="color:red">:起始行号,结束行号s/^/注释符/g</font>
  
  根据行号取消注释：  
 <font style="color:red">:起始行号,结束行号s/^注释符//g</font>

  例子：   
  
  在10 - 20行添加 // 注释  
  <font style="color:red">:10,50s#^#//#g</font>
    
  在10 - 20行删除 // 注释  
  <font style="color:red">:10,20s#^//##g  s</font>