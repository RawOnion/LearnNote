Anaconda解决了python的两大痛点：

1. 提供了包管理功能
2. 提供了环境管理功能



# Anaconda功能：

1. Anaconda 附带了一大批常用数据科学包，它附带了 conda、Python 和 150 多个科学包及其依赖项。
2. Anaconda 是在 conda（一个跨平台，适用于多语言的**包及其依赖项管理器和环境管理器**）上发展出来的。在数据分析中，你会用到很多第三方的包，而conda（包管理器）可以很好的帮助你在计算机上安装和管理这些包，包括安装、卸载和更新包。
3. 管理环境。很多项目使用的包版本不同，比如不同的pandas版本，不可能同时安装两个 Numpy 版本，你要做的应该是，为每个 Numpy 版本创建一个环境，然后项目的对应环境中工作。这时候conda就可以帮你做到。



# conda包管理器和环境管理器终端命令

conda 是 Anaconda 下用于包管理和环境管理的工具，功能上类似 pip 和 vitualenv 的组合。

conda 的环境管理与 virtualenv 是基本上是类似的操作：

```conda
#查看帮助
conda -h

#创建名字为tensorflow的环境,并在这个环境下安装python版本为3.7的包
conda create --name <env_name> <package_names>
conda create --name tensorflow python=3.7

#激活环境
activate tensorflow
#linux/mac下激活环境
source activate tensorflow

#退出当前环境
deactivate tensorflow

#删除该环境
conda remove -n tensorflow --all
#或者
conda env remove -n tensorflow 

#查看所有安装的环境
conda info -e
```



conda 的包管理功能与pip 是一样的：

```conda
#安装numpy
conda install numpy

#查看已安装的包
conda list

#包更新
conda update numpy 

#删除包
conda remove numpy
```



# 修改本地镜像地址

Anaconda 的镜像地址默认在国外，用 conda 安装包的时候会很慢，目前可用的国内镜像源地址有清华大学的。修改 ~/.condarc (Linux/Mac) 或 C:\Users\当前用户名\.condarc (Windows) 配置：

```txt
channels:
 - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
 - defaults
show_channel_urls: true
```



如果使用conda安装包的时候还是很慢，那么可以考虑使用pip来安装，同样把 pip 的镜像源地址也改成国内的，豆瓣源速度比较快。修改 ~/.pip/pip.conf (Linux/Mac) 或 C:\Users\当前用户名\pip\pip.ini (Windows) 配置：

```txt
[global]
trusted-host =  pypi.douban.com
index-url = http://pypi.douban.com/simple
```



# 参考

[1] [Anaconda](https://www.zhihu.com/question/58033789)

[2] [Anaconda介绍、安装及使用教程](https://zhuanlan.zhihu.com/p/32925500)