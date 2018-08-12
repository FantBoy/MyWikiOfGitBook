# nohup的基本使用

> nohup以守护进程的形式启动进程时，会生成nohup.out文件，进程的任何输出信息全在里面都能看到。

但是，随着进程的长时间运行，nohup.out占用空间会越来越大，甚至占满磁盘。
正确的使用姿势是：
```
00 16 * * 1-7 /home/**-log/rmcore > /dev/null 2>&1
```

在末尾加上  /dev/null 2>&1 这样的写法.

**这条命令的意思是将标准输出和错误输出全部重定向到/dev/null中,也就是将产生的所有信息丢弃**

#### command > file 2>file  与command > file 2>&1 的差异

 - command > file 2>file ：将命令所产生的标准输出信息,和错误信息送到file 中
 - command > file 2>file ：stdout和stderr都直接送到file中, file会被打开两次,这样stdout和stderr会互相覆盖,这样写相当于使用了FD1和FD2两个同时去抢占file 的管道. 而 `command > file 2>&1` 这条命令就将stdout直接送向file, stderr 继承了FD1管道后,再被送往file,此时,file 只被打开了一次,也只使用了一个管道FD1,它包括了stdout和stderr的内容.

>从IO效率上,前一条命令的效率要比后面一条的命令效率要低,所以在编写shell脚本的时候,较多的时候我们会用command > file 2>&1 这样的写法.