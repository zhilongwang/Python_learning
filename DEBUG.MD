# DEBUGGING PYTHON

### PDG
 How to use pdg.
 
 #### 
   ```{r, engine='python', count_lines}
     import pdb
     pdb.set_trace()
     
   ```
   
  #### 

    * c: 继续执行.  
    * w: 显示当前正在执行的代码行的上下文信息.  
    * a: 打印当前函数的参数列表.  
    * s: 执行当前代码行，并停在第一个能停的地方（相当于单步进入）.  
    * n: 继续执行到当前函数的下一行，或者当前行直接返回（单步跳过）    
 
  ####  基本类型都可以用type()判断\\所有类型本身的类型就是TypeType
 
  ####  对于class的继承关系来说，使用type()就很不方便。我们要判断class的类型，可以使用isinstance()函数。
      * isinstance(h, Husky)
 
  #### 如果要获得一个对象的所有属性和方法，可以使用dir()函数，它返回一个包含字符串的list，比如，获得一个str对象的所有属性和方法.
      * 类似__xxx__的属性和方法在Python中都是有特殊用途的，比如__len__方法返回长度。在Python中，如果你调用len()函数试图获取一个对象的长度，实际上，在len()函数内部，它自动去调用该对象的__len__()方法，所以，下面的代码是等价的：
      ```python 
        len('ABC')
        'ABC'.__len__()
      ```
  ####  仅仅把属性和方法列出来是不够的，配合getattr()、setattr()以及hasattr()，我们可以直接操作一个对象的状态：
     ```python  
      hasattr(obj, 'x') # 有属性'x'吗？
      True
      obj.x
      9
      hasattr(obj, 'y') # 有属性'y'吗？
      False
      setattr(obj, 'y', 19) # 设置一个属性'y'
      hasattr(obj, 'y') # 有属性'y'吗？
      True
      getattr(obj, 'y') # 获取属性'y'
      19
      obj.y # 获取属性'y'
      19
     ```
     
 ####  help([object])调用内置帮助系统。
 
 ####  返回对象的类名称
     type(sucs).__name__
     
 #### inspect 
     ```python  
      import inspect
      type(obj)# 确定对象的类型
      inspect.getdoc(BeautifulSoup) # 查看文档定义
      inspect.getsourcefile(BeautifulSoup) # 再来看看存放的路径
      inspect.getsourcelines(BeautifulSoup) #当想看源代码
      
     ```
   
  #### dill 
     ```python  
      import dill
      type(obj)# 确定对象的类型
      

      dill.source.getsourcefile(BeautifulSoup) # 获得源代码文件路径

      dill.source.getsourcelines(BeautifulSoup) #获得源代码

      dill.source.findsource(BeautifulSoup) #以上的输出和inspect一样，还有findsouce()函数
      
      
     ```


  
