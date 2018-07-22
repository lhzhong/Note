**概要**
1. Python基础
2. NumPy基础
3. SciPy
4. Matplotlib
5. 简单图片读写
***


## 1. Python基础
### 1.1 基本数据类型
  
最常用的有数值型(Numbers),布尔型(Booleans)和字符串(String)三种。

* 数值型(Numbers)
```
x = 5
print type(x)                   # Prints "<type 'int'>" 
print x                         # Prints "5"
print x + 1                     # 加; prints "6"
print x - 1                     # 减; prints "4"
print x * 2                     # 乘; prints "10"
print x ** 2                    # 幂; prints "25"
x += 1                          # 自加
print x                         # Prints "6"
x *= 2                          # 自乘
print x                         # Prints "12"
y = 2.5
print type(y)                   # Prints "<type 'float'>"
print y, y + 1, y * 2, y ** 2   # Prints "2.5 3.5 5.0 6.25"
```
> 注：python中没有x++ 和 x-- 操作

* 布尔型(Booleans)

  包含True False和常见的与或非操作

```
t = True
f = False
print type(t)     # Prints "<type 'bool'>"
print t and f     # 逻辑与; prints "False"
print t or f      # 逻辑或; prints "True"
print not t       # 逻辑非; prints "False"
print t != f      # XOR; prints "True" 
```

* 字符串型(String)

  字符串可以用单引号/双引号/三引号声明
  
```
hello = 'hello'   
world = "world"   
print hello                                 # Prints "hello"
print len(hello)                            # 字符串长度; prints "5"
hw = hello + ' ' + world                    # 字符串连接
print hw                                    # prints "hello world"
hw2015 = '%s %s %d' % (hello, world, 2015)  # 格式化字符串
print hw2015                                # prints "hello world 2015"
```
**符串对象有很多有用的函数**
    
```
s = "hello"
print s.capitalize()           # 首字母大写; prints "Hello"
print s.upper()                # 全大写; prints "HELLO"
print s.rjust(7)               # 以7为长度右对齐，左边补空格; prints "  hello"
print s.center(7)              # 居中补空格; prints " hello "
print s.replace('l', '(ell)')  # 字串替换;prints "he(ell)(ell)o"
print '  world '.strip()       # 去首位空格; prints "world"
```

### 1.2 基本容器

* 列表/List

  和数组类似，不过可以包含不同类型的元素，同时大小也是可以调整的
```
xs = [3, 1, 2]   # 创建
print xs, xs[2]  # Prints "[3, 1, 2] 2"
print xs[-1]     # 第-1个元素，即最后一个
xs[2] = 'foo'    # 下标从0开始，这是第3个元素
print xs         # 可以有不同类型，Prints "[3, 1, 'foo']"
xs.append('bar') # 尾部添加一个元素
print xs         # Prints 
x = xs.pop()     # 去掉尾部的元素
print x, xs      # Prints "bar [3, 1, 'foo']"
```

**列表最常用的操作**
* 切片/slicing

  即取子序列/一部分元素，如下
```
nums = range(5)    # 从1到5的序列
print nums         # Prints "[0, 1, 2, 3, 4]"
print nums[2:4]    # 下标从2到4-1的元素 prints "[2, 3]"
print nums[2:]     # 下标从2到结尾的元素
print nums[:2]     # 从开头到下标为2-1的元素  [0, 1]
print nums[:]      # 恩，就是全取出来了
print nums[:-1]    # 从开始到第-1个元素(最后的元素)
nums[2:4] = [8, 9] # 对子序列赋值
print nums         # Prints "[0, 1, 8, 8, 4]"
```
* 循环/loops 

  即遍历整个list，做一些操作，如下
```
animals = ['cat', 'dog', 'monkey']
for animal in animals:
    print animal
# 依次输出 "cat", "dog", "monkey"，每个一行，
```

```
# for循环
d = {'person': 2, 'cat': 4, 'spider': 8}
for animal in d:
    legs = d[animal]
    print 'A %s has %d legs' % (animal, legs)
# Prints "A person has 2 legs", "A spider has 8 legs", "A cat has 4 legs"
# 通过iteritems
d = {'person': 2, 'cat': 4, 'spider': 8}
for animal, legs in d.iteritems():
   print 'A %s has %d legs' % (animal, legs)
# Prints "A person has 2 legs", "A spider has 8 legs", "A cat has 4 legs"
```

可以用enumerate取出元素的同时带出下标
```
animals = ['cat', 'dog', 'monkey']
for idx, animal in enumerate(animals):
    print '#%d: %s' % (idx + 1, animal)
# 输出 "#1: cat", "#2: dog", "#3: monkey"，一个一行
```

* List comprehension 

  这个相当有用，在很长的list生成过程中，效率完胜for循环
```
# for 循环
nums = [0, 1, 2, 3, 4]
squares = []
for x in nums:
    squares.append(x ** 2)
print squares                    # Prints [0, 1, 4, 9, 16]
# list comprehension
nums = [0, 1, 2, 3, 4]
squares = [x ** 2 for x in nums]
print squares                    # Prints [0, 1, 4, 9, 16]
```

list comprehension也是可以加多重条件的
```
nums = [0, 1, 2, 3, 4]
even_squares = [x ** 2 for x in nums if x % 2 == 0]
print even_squares  # Prints "[0, 4, 16]"
```

* 字典/Dict 

  和Java中的Map一样的东东，用于存储key-value对

```
d = {'cat': 'cute', 'dog': 'furry'}  # 创建
print d['cat']                       # 根据key取出value
print 'cat' in d                     # 判断是否有'cat'这个key
d['fish'] = 'wet'                    # 添加元素
print d['fish']                      # Prints "wet"
# print d['monkey']                  # KeyError: 'monkey'非本字典的key
print d.get('monkey', 'N/A')         # 有key返回value，无key返回"N/A"
print d.get('fish', 'N/A')           # prints "wet"
del d['fish']                        # 删除某个key以及对应的value
print d.get('fish', 'N/A')           # prints "N/A"
```

* 元组/turple 
  本质上说，还是一个list，只不过里面的每个元素都是一个两元组对

```
d = {(x, x + 1): x for x in range(10)}  # 创建
t = (5, 6)                              # Create a tuple
print type(t)                           # Prints "<type 'tuple'>"
print d[t]                              # Prints "5"
print d[(1, 2)]                         # Prints "1"
```

### 1.3 类与函数

* 用def定义一个函数
```
def sign(x):
    if x > 0:
        return 'positive'
    elif x < 0:
        return 'negative'
    else:
        return 'zero'

for x in [-1, 0, 1]:
  print sign(x)
# Prints "negative", "zero", "positive"
```
```
def hello(name, loud=False):
    if loud:
        print 'HELLO, %s' % name.upper()
    else:
        print 'Hello, %s!' % name

hello('Bob') # Prints "Hello, Bob"
hello('Fred', loud=True)  # Prints "HELLO, FRED!"
```

* 类/Class
```
class Greeter:
    # Constructor
    def __init__(self, name):
        self.name = name  # Create an instance variable
    # Instance method
    def greet(self, loud=False):
        if loud:
            print 'HELLO, %s!' % self.name.upper()
        else:
            print 'Hello, %s' % self.name
g = Greeter('Fred')  # Construct an instance of the Greeter class
g.greet()            # Call an instance method; prints "Hello, Fred"
g.greet(loud=True)   # Call an instance method; prints "HELLO, FRED!"
```

## 2. NumPy基础
