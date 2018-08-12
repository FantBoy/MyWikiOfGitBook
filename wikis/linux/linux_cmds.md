# Linux 常用基本指令


查看`time_wait`数量

```
netstat -n | awk '/^tcp/ {++S[$NF]} END {for(a in S) print a, S[a]}'
```

查看系统版本
```
uname -a
```