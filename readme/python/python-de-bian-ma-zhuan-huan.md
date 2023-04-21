# python的编码转换

\#加u的字符串

a = u'\xcc\xe1\xbd\xbb'

b = a.encode('latin-1').decode('gbk').encode('utf-8')

print b

a = '\xcc\xe1\xbd\xbb'

b = a.decode('gbk').encode('utf-8')

print b
