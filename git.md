#1.问题
输入ssh root@ 主机时
![Alt  text](https://upload-images.jianshu.io/upload_images/14827719-eb61c0b8d9411cb9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

重点是下面两句
```
ECDSA host key for 119.23.76.19 has changed and you have requested strict checking.
Host key verification failed.
```
目标主机密钥已更改，验证失败。

#2.解决方案
直接上图
```
ssh-keygen -R 192.168.233.14 #目标主机IP
ssh root@192.168.233.14
```
![Alt  text](https://upload-images.jianshu.io/upload_images/14827719-07a8a9311dda66a6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)