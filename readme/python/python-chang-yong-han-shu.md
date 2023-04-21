# python常用函数

查找帮助

dir(string) #可以查看模块所有的成员变量和函数

\#下面的代码可以把变量和函数分开放到list里面

```
for fv in dir(string):
    name="string.%s"%fv
    if callable(eval(name)):
        funOrC.append(fv)
    else:
        vars.append(fv)
```

有两个函数需要说明,

eval, 功能是将字符串生成语句执行, 比如eval('string.strip()')可以把字符串转化为真正的函数对象

有了eval, 就可以在code中动态执行用户输入的任何语句, 很强大, 不过也有些危险, 可以通过后面的参数对可执行的语句进行限制.

callable, 就是判断对象是否为函数, 可调用

help(string.capwords), 通过这个可以看到每个函数和成员的说明

List

L.append(var)   #追加元素

L.insert(index,var)

L.pop(var)      #返回最后一个元素，并从list中删除之

L.remove(var)   #删除第一次出现的该元素

L.count(var)    #该元素在列表中出现的个数

L.index(var)    #该元素的位置,无则抛异常&#x20;

L.extend(list)  #追加list，即合并list到L上

L.sort()        #排序

sort比较复杂, 给些例子

L = \[2,3,1,4]

L.sort() #\[1,2,3,4]

L.sort(reverse=True) #\[4,3,2,1]

L = \[('b',2),('a',1),('c',3),('d',4)]

L.sort(cmp=lambda x,y:cmp(x\[1],y\[1])) #给出比较两个item的cmp函数

L.sort(key=lambda x:x\[1]) #给出提取比较特征值key的函数

L.sort(key=lambda x:(x\[1],x\[0])) #多关键字比较, 先比较x\[1], 相同比x\[0]&#x20;

0第一个元素，-1最后一个元素，

\-len第一个元 素，len-1最后一个元素

L = range(1,5)      #即 L=\[1,2,3,4],不含最后一个元素

L = range(1, 10, 2) #即 L=\[1, 3, 5, 7, 9]

list comprehension

&#x20;  \[ \<expr1> for k in L if \<expr2> ]

L1 = L      #L1为L的别名，用C来说就是指针地址相同，对L1操作即对L操作。函数参数就是这样传递的

L1 = L\[:]   #L1为L的克隆，即另一个拷贝

String

S.find(substring, \[start \[,end]]) #可指范围查找子串，返回索引值，否则返回-1

S.rfind(substring,\[start \[,end]]) #反向查找

S.index(substring,\[start \[,end]]) #同find，只是找不到产生ValueError异常

S.rindex(substring,\[start \[,end]])#同上反向查找

S.count(substring,\[start \[,end]]) #返回找到子串的个数

string.strip(s)剔除字符串s左右空格

string.lstrip(s), string.rstrip(s)

S.isalpha() #是否全是字母，并至少有一个字符

S.isdigit() #是否全是数字，并至少有一个字符

S.isspace() #是否全是空白字符，并至少有一个字符

S.islower() #S中的字母是否全是小写

S.isupper() #S中的字母是否便是大写

S.istitle() #S是否是首字母大写的

S.capitalize()      #首字母大写

S.lower()           #转小写

S.upper()           #转大写

S.swapcase()        #大小写互换

S.split(' ')   #将string转list，以空格切分

'+'.join(list)   #将list转string，以加号连接

oat(str)  #变成浮点数，float("1e-1")  结果为0.1

int(str)        #变成整型，  int("12")  结果为12

int(str,base)   #变成base进制整型数，int("11",2) 结果为3

maketrans, translate, 这两个函数很多地方讲的比较复杂,其实就是用maketrans建立一个替换表, 用translate去进行替换

string.maketrans(intab, outtab) --> This method returns a translation table that maps each character in the intab string into the character at the same position in the outtab string.

string.maketrans('', '') #没有映射，实际上就是按原始字符保留

string.maketrans('abc', 'ABC') #小写替换成大写

string.translate(table \[,deletechars]) --> Return a copy of the string S, where all characters occurring in the optional argument deletechars are removed, and the remaining characters have been mapped through the given translation table. 说白了就是把deletechars中的删掉, 然后其他的根据替换表进行替换.

Dictionary

dict = {'ob1':'computer', 'ob2':'mouse', 'ob3':'printer'}

每一个元素是pair，包含key、value两部分。key是Integer或string类型，value 是任意类型。

D.get(key, 0)       #同dict\[key]，多了个没有则返回缺省值，0。\[]没有则抛异常

D.has\_key(key)      #有该键返回TRUE，否则FALSE

D.keys()            #返回字典键的列表

D.values()

D.items()

dict1 = dict        #别名

dict2=dict.copy()   #克隆，即另一个拷贝。

Random

random.random()用于生成一个0到1的随机符点数: 0 <= n < 1.0

random.uniform(a, b)，用于生成一个指定范围内的随机符点数，两个参数其中一个是上限，一个是下限

random.randint(a, b)，用于生成一个指定范围内的整数。

random.randrange(\[start], stop\[, step])，从指定范围内，按指定基数递增的集合中 获取一个随机数。

random.shuffle(x\[, random])，用于将一个列表中的元素打乱。

random.choice从序列(list,tuple)中获取一个随机元素

random.sample(sequence, k)，从指定序列中随机获取指定长度的片断。sample函数不会修改原有序列。
