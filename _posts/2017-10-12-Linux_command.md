### 开关机
```
shutdown
     -r             关机重启
     -h             关机不重启
     now            立刻关机
halt                关机
reboot              重启
```
### 用户，组
```
su root
```
### 关键词
```
pwd   当前的位置
~     home   
.     当前文件夹  
..    上级文件夹
clear 清屏
```
### cd
```
cd ~                   进入home
cd folder_a            进去当前文件夹下的folder_a文件夹
cd /var/www/folder_b   进去根目录下的var下的wwww下的folder_b文件夹
```
### ls  ll
```
ls 查看文件
ls -l 查看文件详情
ls -a 查看所有文件
ll 查看所有文件详情（包括隐藏文件）
```
### tree
```
tree 树状显示目录（主要安装扩展包 sudo apt install tree） 
```
### mkdir
```
mkdir folder_name                创建文件夹
mkdir -m 700  folder_name        并且只有文件主有读、写和执行权限，其他人无权访问
mkdir -m-p 700  test/folder_name 递归创建
```
### touch echo
```
touch file_name            创建空文件
echo content > file_name   创建非空文件
```
### cat
```
cat file_name  查看整个文件内容
      tail -n 1000：显示最后1000行

      tail -n +1000：从1000行开始显示，显示1000行以后的

      head -n 1000：显示前面1000行
```
### rm
```
rm file_a  删除文件
rm -r folder_a 删除非空文件夹，递归删除
rm -f  folder_a    强制删除
```
### mv
```
mv file_a file_b 移动文件到当前目录下 并命名为file_b（重命名）
mv file_a test/file_b 移动文件到test目录下 并命名为file_b（移动并重命名）
```
### cp
```
cp  file_a file_b
cp -f file_a file_b 将文件file_a复制成file_b，因为目的文件已经存在，所以指定使用强制复制的模式
cp  -r file_a file_b    递归复制
cp  -p file_a file_b    保留源文件或目录的属性，包括所有者、所属组、权限与时间
```
### 权限
```
r 表示可读取，w 表示可写入，x 表示可执行
所有者  所在组  其他组
chmod 777 file_name   -r递归更改
```
### VIM
```
普通模式
：命令模式
v 可视模式

yy  复制当前行  
dd  剪切当前行
p    粘贴
set nu  显示行号
set nonu 隐藏行号
/keyword   搜索
:n 到指定行
:w 保存
:q 退出
:w !sudo tee %
v +jkbn 可视模式下选择   y 复制 p粘贴   d剪切 p粘贴
```
### 查找文件
```
find / -name filename          按文件名查找文件
find / -type f -name "*.log"   按文件类型查找文件
find /PATH -name "*.h" | xargs grep -in "helloworld"   查找带有helloword的.h文件
```
### 安装应用
```
安装应用 sudo  apt install tree  （centos中是yum）
删除应用 sudo  apt remove tree
```
### 进程
```
ps aux  查看进程
ps aux | grep php-fpm   //查看包含php-fpm的进程
kill pid //关闭进程
top | grep md 动态显示当前耗费资源最多进程信息
```
### 网络
```
ifconfig          查看网络情况
    如果提示未安装net-tools
    sudo apt install net-tools

ping              测试网络连通(是否连通，丢包)
```
