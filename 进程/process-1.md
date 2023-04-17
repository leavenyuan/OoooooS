# 

### 已知一个进程或端口号或服务名，如何查看进程具体信息

```sh
$ netstat | grep 
$ lsof -i:端口号   #获取PID
(mac) $ vmmap PID
(linux) $ ls -l /proc/{PID}/fd/{FD数}
```
