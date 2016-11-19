# Linux操作系统的备份与还原
 
## 1. 备份：

> tar cvpzf /run/media/abelit/AbelitDisk/SystemBackup/archlinuxbackup.tgz --exclude=/proc --exclude=/lost+found --exclude=/run/media --exclude=/mnt --exclude=/sys / 

```
命令解释：
tar：linux常用的打包程序
cvpzf：式tar的参数
 
　　　　　c-创建新文档
                  v-处理过程中输出相关信息
                  p-表示保持相同的权限
                  z-调用gzip来压缩归档文件，与-x联用时调用gzip完成解压缩
                  f-对普通文件操作
linuxbackup.tgz：要打包成的文件名
--exclude=/proc：排除/proc目录，不打包这个目录，后面也同理，记得排除自身打包的文件名
/：表示打包linux根目录所有文件，当然了排除的文件不包含在内
整个过程理解起来意思就是，创建一个新的文件名linuxbackup.tgz压缩文件，它保存式从排除了指定目录后的文件，并且保存原有的权限设置，这里必须记下你排除的目录，恢复的时候需要手动创建。具体哪些目录要排除在外，这个根觉不同的环境和工作需要进行选择就是了。执行后等待一定时间就可以了，将这个linuxbackup.tgz拷贝到其他地方即可，备份完成了。
重点指出：在打包过程中不要进行任何的操作，否则会修改某些文件，在备份完后tar会提示错误。恢复也是一样。
```

## 2. 还原
### 2.1 

>tar xvpfz linuxbackup.tgz -C /  

### 2.2 

```
mkdir proc  
mdkir lost+found  
mkdir mnt   
mkdir sys  
reboot
```
