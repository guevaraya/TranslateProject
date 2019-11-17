[#]: collector: (lujun9972)
[#]: translator: (guevaraya )
[#]: reviewer: ( )
[#]: publisher: ( )
[#]: url: ( )
[#]: subject: (Getting Started With ZFS Filesystem on Ubuntu 19.10)
[#]: via: (https://itsfoss.com/zfs-ubuntu/)
[#]: author: (John Paul https://itsfoss.com/author/john/)

在 Ubuntu 19.10 上学习入门 ZFS 文件系统
======

一个主要的 [Ubuntu 19.01][1] 的新特性 就是支持 [ZFS][2]。现在你可以很容易的不要太多操作就可以在Ubuntu 系统上安装 ZFS了。

一般情况下，安装 Linux 是会选择 Ext4 文件系统。但是如果是安装 Ubuntu 19.10，在启动阶段可以看到 ZFS 选项了。你绝对不能在双系统上用它，因为它会擦除这个磁盘。

![你可以在安装 Ubuntu 19.10 的时候选择 ZFS][3]

让我们看看 ZFS 有多重要以及如何在已经安装 ZFS 的 Ubuntu 上 使用它。

### ZFS 与其他文件系统有哪些区别？

ZFS 的设计初衷是：处理海量存储和避免数据损坏。ZFS 可以处理 256 千万亿的泽它字节(ZB)。（因此这就是ZFS的Z。）它可以处理最大16艾字节（EB）的文件。

如果你仅有一个单磁盘的笔记本电脑，你可以体验 ZFS 的数据保护特性。即写及时拷贝特性确保正在使用的数据不会被覆盖，相反，新的数据会被写到一个新的块中，同时文件系统的元数据会被更新到新块中。ZFS 可容易的创建文件系统的快照。这个快照可追踪文件系统的更改，并共享数据块确保节省数据空间。

ZFS 为磁盘上的每个文件分配一个校验和。它会不断的校验文件的状态和校验和。如果发现文件被损坏了，它就会尝试修复文件。

我写过一个文章详细介绍 [什么是 ZFS以及它有哪些特性[2].如果你感兴趣可以去阅读下。

注：

请谨记 ZFS 的数据保护特性会导致性能下降。

### Ubuntu下使用 ZFS [适用于中高级用户] 

![][4]

一旦你在你的主磁盘上干净安装了 Ubuntu 下的 ZFS，你就可以开始体验它的特性。

请注意安装 ZFS 这个过程需要命令行。我还没用过它的 GUI 工具。

#### 创建一个 ZFS 池

_**The section only applies if you have a system with more than one drive. If you only have one drive, Ubuntu will automatically create the pool during installation.**_

Before you create your pool, you need to find out the id of the drives for the pool. You can use the command _**lsblk**_ to show this information.

To create a basic pool with three drives, use the following command:

```
sudo zpool create pool-test /dev/sdb /dev/sdc /dev/sdd.
```

Remember to replace _**pool-test**_ with the pool name of your choice.

This command will set up “a zero redundancy RAID-0 pool”. This means that if one of the drives becomes damaged or corrupt, you will lose data. If you do use this setup, it is recommended that you do regular backups.

You can alos add another disk to the pool by using this command:

```
sudo zpool add pool-name /dev/sdx
```

#### Check the status of your ZFS pool

You can check the status of your new pool using this command:

```
sudo zpool status pool-test
```

![Zpool Status][6]

#### Mirror a ZFS pool

To ensure that your data is safe, you can instead set up mirroring. Mirroring means that each drive contains the same data. With mirroring setup, you could lose two out of three drives and still have all of your information.

To create a mirror, you can use something like this:

```
sudo zpool create pool-test mirror /dev/sdb /dev/sdc /dev/sdd
```

#### Create ZFS Snapshots for backup and restore

Snapshots allow you to create a fall-back position in case a file gets deleted or overwritten. For example, let’s create a snapshot, delete some folder in my home directory and restore them.

First, you need to find the dataset you want to snapshot. You can do that with the

```
zfs list
```

![Zfs List][7]

You can see that my home folder is located in **rpool/USERDATA/johnblood_uwcjk7**.

Let’s create a snapshot named **1910** using this command:

```
sudo zfs snapshot rpool/USERDATA/[email protected]
```

The snapshot will be created very quickly. Now, I am going to delete the _Downloads_ and _Documents_ directories.

Now to restore the snapshot, all you have to do is run this command:

```
sudo zfs rollback rpool/USERDATA/[email protected]
```

The length of the rollback depends on how much the information changed. Now, you can check the home folder and the deleted folders (and their content) will be returned to their correct place.

### To ZFS or not?

This is just a quick glimpse at what you can do with ZFS on Ubuntu. For more information, check out [Ubuntu’s wiki page on ZFS.][5] I also recommend reading this [excellent article on ArsTechnica][8].

This is an experimental feature and if you are not aware of ZFS and you want to have a simple stable system, please go with the standard install on Ext4. If you have a spare machine that you want to experiment with, then only try something like this to learn a thing or two about ZFS. If you are an ‘expert’ and you know what you are doing, you are free to experiment ZFS wherever you like.

Have you ever used ZFS? Please let us know in the comments below. If you found this article interesting, please take a minute to share it on social media, Hacker News or [Reddit][9].

--------------------------------------------------------------------------------

via: https://itsfoss.com/zfs-ubuntu/

作者：[John Paul][a]
选题：[lujun9972][b]
译者：[译者ID](https://github.com/译者ID)
校对：[校对者ID](https://github.com/校对者ID)

本文由 [LCTT](https://github.com/LCTT/TranslateProject) 原创编译，[Linux中国](https://linux.cn/) 荣誉推出

[a]: https://itsfoss.com/author/john/
[b]: https://github.com/lujun9972
[1]: https://itsfoss.com/ubuntu-19-04-release-features/
[2]: https://itsfoss.com/what-is-zfs/
[3]: https://i2.wp.com/itsfoss.com/wp-content/uploads/2019/05/zfs-ubuntu-19-10.jpg?ssl=1
[4]: https://i0.wp.com/itsfoss.com/wp-content/uploads/2019/11/Using_ZFS_Ubuntu.jpg?resize=800%2C450&ssl=1
[5]: https://wiki.ubuntu.com/Kernel/Reference/ZFS
[6]: https://i0.wp.com/itsfoss.com/wp-content/uploads/2019/10/zpool-status.png?ssl=1
[7]: https://i2.wp.com/itsfoss.com/wp-content/uploads/2019/10/zfs-list.png?ssl=1
[8]: https://arstechnica.com/information-technology/2019/10/a-detailed-look-at-ubuntus-new-experimental-zfs-installer/
[9]: https://reddit.com/r/linuxusersgroup
