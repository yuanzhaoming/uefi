---------------------------
## 1 编译
将下载的edk2源码，放到ubuntu上。然后配置基本的环境，按照如下命令：


总结一下操作步骤：
```
$ sudo apt-get install uuid-dev
$ . edksetup.sh 
$ make -C BaseTools
$ build -p EmulatorPkg/EmulatorPkg.dsc -a X64 -b DEBUG -t GCC48 -D BUILD_64  -n 1
```

下面是出现的问题以及解决办法。


如果安装不上uuid-dev，可以使用源码安装：http://nchc.dl.sourceforge.net/project/libuuid/libuuid-1.0.3.tar.gz。



```
$ . edksetup.sh 
: command not found
: command not found
bash: edksetup.sh: line 29: syntax error near unexpected token `$'\r''
'ash: edksetup.sh: line 29: `function HelpMsg()

```

发现报错，这个问题是由于dos与unix之间的格式转换除了问题导致。可以使用如下命令：
```
$ cat -v edksetup.sh
```
发现在29行上多了一个M。

那么可以使用如下方法，将文件转换为unix格式。

```
$ vi edksetup.sh
```
在vi模式下，进入命令行模式，输入set ff=unix，然后再输出set ff，可以看到当前的fileformat=unix，再选择保存(wq)即可。

这一步做完之后，同样对 BaseTools/BuildEnv 做一次这样的操作。













