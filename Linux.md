# Linux

---

## 1. 什么是 Linux

Linux，一般指GNU/Linux（单独的Linux内核并不可直接使用，一般搭配GNU套件，故得此称呼），是一种免费使用和自由传播的类UNIX操作系统，其内核由林纳斯·本纳第克特·托瓦兹（Linus Benedict Torvalds）于1991年10月5日首次发布，它主要受到Minix和Unix思想的启发，是一个基于POSIX的多用户、多任务、支持多线程和多CPU的操作系统。

## 2. 常见的 Linux 命令

### 1. clear 清屏

### 2. pwd 打印当前所在目录

### 3. ls 列出当前目录下的内容

* ls  列出当前目录下的内容，不包括隐藏文件
* ls -a  列出当前目录下的内容，包括隐藏文件
* ls -l  以长格式列出当前目录下的内容，包括每个文件的读写权限、大小、修改时间等，可以简写为 ll

### 4. cd 切换目录

* cd/cd ~  切换到当前用户家目录
* cd xxx  切换到 xxx 目录
* cd ..  切换到上一级目录
* cd -  切换当上一次所在目录

### 5. mv  移动文件/给文件改名

* mv file.txt /path/to/destination/newfilename.txt  将文件移动到另一个目录（同时可以改名）
* mv oldname.txt newname.txt  文件重命名

### 6. rm 删除文件

* rm -i xxx  删除前进行确认
* rm -f xxx  强制删除
* rm -r xxx  递归删除目录及目录中的所有内容
* rm -rf /  删除根目录！！！！

### 7. cat 查看文件内容

* cat file1.txt / cat file1.txt file2.txt  查看整个文件的内容，可一次查看多个文件
* cat -n file1.txt  查看文件内容时显示行号

### 8. less 分页查看文件内容

* 空格键向下翻页，b 键向上翻页，g 跳转到文件开头，G 跳转到文件末尾，q 退出 less 界面

### 9. head 查看文件的前几行

* head file  查看前 10 行
* head -n 20 file  查看前 20 行

### 10. tail 查看文件的最后几行

* tail file  查看文件的最后 10 行
* tail -n 20 file  查看文件的最后 20 行
* tail -f file  实时追踪文件的新增内容，常用语监控日志，按 Ctrl+C 可以停止追踪

### 11. mkdir 新建文件夹

* mkdir -p  dir1/dir2   新建多级目录

### 12. touch 新建文件

### 13. echo 输出

* echo "xxx"  直接在终端中输出"xxx"
* echo "xxx" > file  创建 file 并写入内容，如果 file 已存在，内容会被覆盖
* echo "xxx" >> file  在 file 末尾追加内容

### 14. vi 打开编辑器

* 按 i 进入插入/编辑模式
* 按 esc 退出编辑模式
* 按 : 进入尾行模式
* 尾行模式输入 wq 保存退出

### 15. jps 查看 Java 进程名和 PID

* 前提是安装了 JDK