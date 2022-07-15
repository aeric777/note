# pip

> 2021.11.22

---
## pip status
``` bash
$ pip --version
$ pip --help
$ pip install -U pip    # upgrade pip
```

## package management
``` bash
$ pip list      # list installed package
$ pip list -o   # check upgradable package

$ pip install --upgrade SomePackage # upgrade package
$ pip uninstall SomePackage         # uninstall package

$ pip install Package           # install package
$ pip install Package==1.0.4    # install package with specify version
$ pip show Package      # show package information
$ pip show -f Package   # show more information
```

## 权限问题
``` bash
# 对于权限管理比较严格的系统，有时会导致普通用户的pip无法直接写入系统默认的python包管理文件。此时用户的包管理和系统的包管理不同：
eric$  pip --version
pip 21.3.1 from /home/eric/.local/lib/python3.9/site-packages/pip (python 3.9)

root# pip --version
pip 21.3.1 from /usr/local/lib/python3.9/dist-packages/pip (python 3.9)
# 可以看出系统用户和普通用户pip包的位置不同。同时普通用户执行`pip list` `python -m pip list` 得到的结果也是不同的。系统用户执行上出两个命令得到相同结果。

# 综上，普通用户推荐使用`python -m pip []`
# 直接使用pip查看包和得到的是系统默认文件夹中的信息，需要使用
$ python -m pip list
$ python -m pip install
```

# 独立python环境
``` bash
# 考虑使用miniconda
# 使用用户单独的python环境，尽量不要使用系统python环境
```


# PS
``` bash
# 树莓派中`/usr/lib/python3` `/lib/python3` 内部文件似乎为同一个硬链接
# 路径：`/usr/local/lib/python3.9`  `/lib/python3`
```

# Error
``` bash 
AttributeError: module 'html5lib.treebuilders.etree' has no attribute 'getETreeModule'

solved:
$ pip install pip -U
```

