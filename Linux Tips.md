# Linux Tips

Table of Contents
=================

   * [Linux Tips](#linux-tips)
      * [Vim 常用命令](#vim-常用命令)
      * [文件系统](#文件系统)
      * [解压缩](#解压缩)
         * [.7z](#7z)
         * [合并.zip](#合并zip)
         * [压缩 ](#压缩)
         * [解压](#解压)
      * [进程](#进程)
      * [Tmux](#tmux)
      * [Cuda](#cuda)

## Vim 常用命令
shift + 4 行尾 

shift +6 行首 

 

/xxx            查找xxx 

n               执行上一次查找 

 

0               到行首 

w               光标往后移动一个词 

b               光标往前移动一个词 

 

x               删除当前一个字符 

dw              删除一个单词 

D               删除到行尾 

dd              删除整行 

 

V               选中整行 

y               将选中部分的内容复制到剪切板 

p               在光标下方粘贴剪切板中的内容 

 

u               撤销上一次修改 

 

numG            移动光标到指定的行（num）。（比如 10G 就是到第 10 行） 

gg              到文件开始 

G               到文件末尾 

 

:wq             保存退出

## 文件系统

df -h  查看文件系统使用情况

查看当前文件夹各个文件大小 
du -h --max-depth=1 

查看各个硬盘大小 

 df -hl 

统计某文件夹下文件的个数 

ls -l |grep "^-"|wc -l 

统计某文件夹下文件夹的个数 

ls -l|grep "^d"| wc -l

查看当前目录下的文件数量（包含子目录中的文件） 注意：R，代表子目录 

ls -lR|grep "^-"| wc -l 

查看当前目录下的文件夹目录个数（不包含子目录中的目录），同上述理，如果需要查看子目录的，加上R 

ls -l|grep "^d"| wc -l 

 

查看当前目录下的文件夹目录个数（不包含子目录中的目录），同上述理，如果需要查看子目录的，加上R 

ls -l|grep "^d"| wc -l

low disk space问题 

使用find / -xdev -size +100M -exec ls -l {} \;查找大文件

## 解压缩

### .7z

7za x \[update\]\ round2_ijcai_18_train_20180425.7z -r -o./ 

7za x  -r -o./

### 合并.zip

例如linux.zip.001, linux.zip.002, linux.zip.003... 

首先 cat linux.zip* > linux.zip #合并为一个zip包 

然后 unzip linux.zip #解压zip包 

OK

### 压缩  

tar –cvf jpg.tar *.jpg //将目录里所有jpg文件打包成tar.jpg  

tar –czf jpg.tar.gz *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用gzip压缩，生成一个gzip压缩过的包，命名为jpg.tar.gz  

tar –cjf jpg.tar.bz2 *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用bzip2压缩，生成一个bzip2压缩过的包，命名为jpg.tar.bz2  

tar –cZf jpg.tar.Z *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用compress压缩，生成一个umcompress压缩过的包，命名为jpg.tar.Z  

rar a jpg.rar *.jpg //rar格式的压缩，需要先下载rar for linux  

zip jpg.zip *.jpg //zip格式的压缩，需要先下载zip for linux 

### 解压 

tar –xvf file.tar //解压 tar包  

tar -xzvf file.tar.gz //解压tar.gz  

tar -xjvf file.tar.bz2 //解压 tar.bz2  

tar –xZvf file.tar.Z //解压tar.Z  

unrar e file.rar //解压rar  

unzip file.zip //解压zip 

## 进程

杀掉进程 

ps -aux | grep python2 

kill -9 31305（进程号）

## Tmux

设置鼠标滚动  
set-option -g mouse on 

 ## Cuda
 
 cuda 版本  

cat /usr/local/cuda/version.txt 

cudnn 版本

cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2 

opencv版本
pkg-config --modversion opencv


I have import error: ImportError: libcudnn.so.6: cannot open shared object file: No such file or directory 

download cudnn6.0 version (not latest 7.0) 
2.sudo rm -rf /usr/local/cuda/include/cudnn.h 
sudo rm -rf /usr/local/cuda/lib64/libcudnn* 

to cudnn untar folders 
sudo cp include/cudnn.h /usr/local/cuda/include/ 
sudo cp lib64/lib* /usr/local/cuda/lib64/ 

cd /usr/local/cuda/lib64/ 
sudo chmod +r libcudnn.so.6.0.21 
sudo ln -sf libcudnn.so.6.0.21 libcudnn.so.6 
sudo ln -sf libcudnn.so.6 libcudnn.so 
sudo ldconfig 
It works for me. 
I think @evilkjoker may be useful, @JekaMas It's unsuccessful for me
