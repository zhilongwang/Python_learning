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
      inspect.getsource(BeautifulSoup) #当想看源代码
      inspect.isclass(add)
      inspect.isfunction(add)
      file = open('debug.txt','w+')
      print >> file, inspect.getsourcelines(angr.engines.successors.SimSuccessors)
      
     ```
   
  #### dill 
     ```python  
      import dill
      type(obj)# 确定对象的类型
      

      dill.source.getsourcefile(BeautifulSoup) # 获得源代码文件路径

      dill.source.getsourcelines(BeautifulSoup) #获得源代码

      dill.source.findsource(BeautifulSoup) #以上的输出和inspect一样，还有findsouce()函数
      
      
     ```
     
     
   #### 
   
     ```python 
       
     import sys 
     def get_cur_info(): 
     print sys._getframe().f_code.co_filename # 当前文件名 
     print sys._getframe(0).f_code.co_name # 当前函数名
     print sys._getframe(1).f_code.co_name # 调用该函数的函数的名字，如果没有被调用，
     print sys._getframe().f_lineno # 当前行号 
     
     ```
  
  #### debug
  
>断点设置

   - b  10 #断点设置在本py的第10行
   或
   - b  ots.py:20 #断点设置到 ots.py第20行
> 删除断点
   - b #查看断点编号
   - cl 2 #删除第2个断点
            
>运行

    - n #单步运行
    - s #细点运行 也就是会下到，方法
    - c #跳到下个断点
    
>查看

    - p param #查看当前 变量值
    - l #查看运行到某处代码
    - a #查看全部栈内变量
    - w 列出目前call stack 中的所在层。
    - d 在call stack中往下移一层
    - u 在call stack中往上移一层。如果在上移一层之后按下 n ,则会在上移之后的一层执行下一个叙述,之前的 function call 就自动返回。
    - cl 清除指定的断点。如果没有带参数,则清除所有断点。
    - disable 取消所有断点的功能,但仍然保留这些断点。
    - enable 恢复断点的功能。
    - ignore 设定断点的忽略次数。如果没指定 count,其初始 为 0。当 count 为 0 时,断点会正常动作。若有指定 count,则每次执行到该中断, count 就少 1,直到 count 数为 0。
    - condition bpnumber [condition]
    - j(ump) lineNo. 跳到某行执行。只有在 call stack 的最底部才能作用。
    - l  列出目前所在档案中的位置。连续地 l 命令会一直列到档案结尾,可以使用指定行数或范围来打印。
    - pp 和 p 命令类似,但是使用 pprint module(没用过 pprint,详情请参考 Python Library Reference)。
    - alias 以一个"别名"代替"一群除错命令",有点类似 c/c 的 macro(详情请参考 Python Library Reference)。
    - unalias 取消某个 alias。
    - [!]statement 在目前的环境(context)中执行叙述。
    
 >跟踪 
    python -mtrace --listfuncs solve.py
