# python 打包发布

文件：   \~/.pypirc

```
[pypi]
username=yourusername
password=yourpassword
[server-login]
username:yourusername
password:yourpassword
```

```
[distutils]
index-servers =
    pypi
```

```
[pypi]
repository:https://pypi.python.org/pypi
username:yourusername
password:yourpassword
```

python setup.py bdist\_egg，那么会在dist目录中生成foo-1.0-py2.7.egg包

python setup.py bdist\_wininst生成一个exe文件

python setup.py bdist\_rpm，但系统必须有rpm命令的支持

Installation

`$ pip install twine`

Using Twine

1. Create some distributions in the normal way:

`$ python setup.py sdist bdist_wheel`

python3

`$ python setup.py sdist bdist_wheel`

2. Upload with twine to [Test PyPI](https://packaging.python.org/guides/using-testpypi/) and verify things look right. Twine will automatically prompt for your username and password:

username: ...

password:

...

3. Upload to [PyPI](https://pypi.org/):

`$ twine upload dist/*`

`python3`

`python3 -m twine upload dist/*`

4. Done!
