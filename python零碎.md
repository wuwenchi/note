## 静态方法，类方法，`@property`

### 把类的方法装饰为类的属性

可以通过`@property`来把一个方法装饰为类的属性

可以通过`@<类属性名称>.setter`来设置类属性的值

可以通过`@<类属性名称>.delete`来删除类jj属性的值

例如：

```
class A:
	def __init__(self, name = "asdf"):
		self.__name = name
	
	@property
	def name(self):
		return self.__name
	
	@nmake.setter
	def name(self, name):
		self.__name = name

if __name__ == "__main__":
	a = A()
	print(a.name) # 这里的name其实是一个方法，但是可以使用属性的方式进行调用
	a.name = "ddd"
	print(a.name)
```

### 把类的实例当做函数

如果类里面实现了`__call__()`函数，则让类的实例可以像函数一样调用，例如；

```
class A:
	def __call__(self):
		printf('sdf')

a = A()
a()
```

### 类的属性和方法重名：

优先输出类属性

### 类的静态方法：

1、需要使用装饰器：`@staticmethod`

2、定义的时候，不需要写`self`参数

3、可以引用、访问类属性，但不能引用、访问实例属性

4、调用：类或者实例都可以进行调用

5、它只是一个放在类里面的普通函数而已，只不过归属于类，方便代码管理（通常实现类的相关工具）



### 类的类方法

1、需要使用装饰器：`@classmethod`

2、定义的时候，必须提供参数`cls`

3、不能引用、访问实例属性

4、可以用类或者实例进行调用

5、继承时，传入的类变量cls是子类，而不是父类

6、与类相关的操作，但不依赖或改变类的实例

7、一般用于工厂方法，创建类实例

8、在类内调用静态方法时，不需要硬编码类名，直接使用`cls.<method_name>`

例如：

```
class A:
	@staticmethod
	def spins_ml(spins):
		return spins * 0.2
	
	@classmethod
	def get_A(cls, water, scour):
		return cls(water, cls.spins_ml(scour))
		
a = A.get_A(100, 9)
```

## 类的特殊方法

### 元类

1、所有的类都是元类(type)的实例

2、可以自定义元类，来实现对类的预处理：`__new__()`

###  构造序列

## 类装饰器

```:
def deco(a_class):
	class new_class:
		def __init__(self, age, color):
			self.old = a_class(age)
			self.colr = color
		def display(self):
			print(self.color)
			print(self.old.age)
		return new_class
@deco
class Cat:
	def __init__(self, age):
		self.age = age
	def display(self):
		print(self.age)
a = Cat(12, "black")  # 如果没有装饰器的话，则只能传入一个age参数
a.display()
```



## 组合多个字符串

```
test = ["a", "b", "c"]
print "".join(test)
```

## 用枚举顺序遍历列表

```
test = ["a", "b", "c"]
for i,v enumerate(test):
	print(i,":", v)
```

## 列表构建字典

```
dict(zip(list1, list2))
```

## 三元操作符的 if

```
[表达式返回的值] if [表达式] else [表达式为假的返回值]
```

例如：

```
x = (classA if y==1 else classB)(param1, param2)
```

这个表示：如果y等于1，则构建classA的对象，否则构建classB的对象。

## 分隔符

```
test = "abc:::abc bac   wdfw/adf"
out = [x for x in test.split(":| |/") if x]
```

