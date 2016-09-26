#GRUB2主题包手动安装设置


###1. 复制GRUB2主题包到/boot/grub/themes


###2. 修改GRUB配置文件并更新。

打开/etc/default/grub文件，添加下面这句

>GRUB_THEME=/boot/grub/themes/abelit/theme.txt

更新grub
>grub-mkconfig -o /boot/grub/grub.cfg