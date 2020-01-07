# Centos的图形化界面确实容易崩溃，操作一快就直接卡死，行吧，只能放弃平易近人的桌面，完全用黑乎乎的命令行操作了。

## 环境
> `host机:centos7.7（minimal）` kvm虚拟化 `虚机：win7`  

## u盘安装centos
> 这一步跟我前一篇文章重复了，就不赘述了 [上一篇](https://github.com/Ricechips/centos7-kvm-win10/blob/master/README.md)

## kvm安装
> 这里多一步连接网络 *dhclient -v*
> 其他步骤移步上一篇
> ps:virt-manager可以不用装了，图形化管理的东西

## 显卡透传
> - 配置iommu 
> - 这一步要注意是否还有一个/boot/efi/EFI/centos/grub.cfg文件，若有，则在linuxefi  ... quiet后面加上 intel_iommu=on，应该有2-3处，然后grub2-mkconfig更新并重启
> - 找到显卡pci编号并与宿主机解绑打上vfio驱动

## 安装OVMF
> - 安装wget: *curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo*  
> yum install wget
> - 如果想看ifconfig: yum install net-tools

## 安装win7
> - 我是直接将打好驱动的win7镜像直接用移动硬盘拷贝到这个命令行界面，当然，配置文件xml也捎上了。
> - centos挂载移动硬盘：

## usb透传
> lsusb命令安装：*yum -y install usbutils*
> lsusb查询要透传的usb设备得到id号  
> 在配置文件中安装，具体位置：
```c
<hostdev mode='subsystem' type='usb' managed='yes'>
  <source>
    <vendor id=' '/>
    <product id=' '/>
    <address bus=' ' device=' '/> #这一行若是同一牌子的键鼠就要添加
  </source>
 </hostdev>
```
### 一些心得

