如何在Linux下开发程序避免重复性压迫损伤 
======
![workrave-image][1]

[重复性压迫损伤][2] （RSI）是职业性损伤综合征, 非特异性手臂疼痛或工作引起的上肢障碍. 重复性压迫损伤 (RSI) 是由于过低使用双手从事重复性任务，如打字，写和使用鼠标. 不幸的是，大部分人不了解什么是重复性压迫损伤 (RSI)以及他的危害有多大. 你可以使用名叫Workrave的开源软件轻松的预防重复性压迫损伤 (RSI).

### 重复性压迫损伤 (RSI)有哪些症状？

我从[page][3]引用过来的, 看看哪些说的是你：

  1. 疲惫缺乏忍耐力？
  2. 手掌或上肢乏力
  3. 疼痛麻木甚至失去知觉？
  4. 沉重：你有没有感觉手很沉？
  5. 笨拙: 你有没有感觉抓不紧东西？
  6. 你有没有感觉手上无力？很难打开罐子或切菜无力？
  7. 缺乏协调和控制？
  8. 手总是冰凉的？
  9. 意识需要提高？稍微注意下身体就发现有毛病了。
  10. 是否过敏？
  11. 频繁的自我按摩(潜意识的)？
  12. 共鸣的疼痛？ 当别人在谈论手痛的时候，你是否也感觉到了手疼？



### 如何减少开发者的重复性压迫损伤风险（RSI）

  * 使用计算机的时候每个30分钟间隔休息一下。借助软件如 workrave 预防重复性压迫损伤风险（RSI）。
  * 有规律的锻炼可以预防各种损伤，包括重复性压迫损伤
  * 使用合理的姿势。调整你的电脑桌和椅子使身体保持一个肌肉放松状态

### Workrave

Workrave is a free open source software application intended to prevent computer users from developing RSI or myopia. The software periodically locks the screen while an animated character, "Miss Workrave," walks the user through various stretching exercises and urges them to take a coffee break. The program frequently alerts you to take micro-pauses, rest breaks and restricts you to your daily limit. The program works under MS-Windows and Linux, UNIX-like operating systems.

#### Install workrave

Type the following [apt command][4]/[apt-get command][5] under a Debian / Ubuntu Linux:
`$ sudo apt-get install workrave`
Fedora Linux user should type the following dnf command:
`$ sudo dnf install workrave`
RHEL/CentOS Linux user should enable EPEL repo and install it using [yum command][6]:
```
### [ **tested on a CentOS/RHEL 7.x and clones** ] ###
$ sudo yum install epel-release
$ sudo yum install https://rpms.remirepo.net/enterprise/remi-release-7.rpm
$ sudo yum install workrave
```
Arch Linux user type the following pacman command to install it:
`$ sudo pacman -S workrave`
FreeBSD user can install it using the following pkg command:
`# pkg install workrave`
OpenBSD user can install it using the following pkg_add command
```
$ doas pkg_add workrave
```

#### How to configure workrave

Workrave works as an applet which is a small application whose user interface resides within a panel. You need to add workrave to panel to control behavior and appearance of the software.

##### Adding a New Workrave Object To Panel

  * Right-click on a vacant space on a panel to open the panel popup menu.
  * Choose Add to Panel.
  * The Add to Panel dialog opens.The available panel objects are listed alphabetically, with launchers at the top. Select workrave applet and click on Add button.

![Fig.01: Adding an Object \(Workrave\) to a Panel][7]
Fig.01: Adding an Object (Workrave) to a Panel

##### How Do I Modify Properties Of Workrave Software?

To modify the properties of an object workrave, perform the following steps:

  * Right-click on the workrave object to open the panel object popup.
  * Choose Preference. Use the Properties dialog to modify the properties as required.

![](https://www.cyberciti.biz/media/new/tips/2009/11/linux-gnome-workwave-preferences-.png)
Fig.02: Modifying the Properties of The Workrave Software

#### Workrave in Action

The main window shows the time remaining until it suggests a pause. The windows can be closed and you will the time remaining on the panel itself:
![Fig.03: Time reaming counter ][8]
Fig.03: Time reaming counter

![Fig.04: Miss Workrave - an animated character walks you through various stretching exercises][9]
Fig.04: Miss Workrave - an animated character walks you through various stretching exercises

The break prelude window, bugging you to take a micro-pause:
![Fig.05: Time for a micro-pause remainder ][10]
Fig.05: Time for a micro-pause remainder

![Fig.06: You can skip Micro-break ][11]
Fig.06: You can skip Micro-break

##### References:

  1. [Workrave project][12] home page.
  2. [pokoy][13] lightweight daemon that helps prevent RSI and other computer related stress.
  3. [A Pomodoro][14] timer for GNOME 3.
  4. [RSI][2] from the wikipedia.



### about the author

The author is the creator of nixCraft and a seasoned sysadmin and a trainer for the Linux operating system/Unix shell scripting. He has worked with global clients and in various industries, including IT, education, defense and space research, and the nonprofit sector. Follow him on [Twitter][15], [Facebook][16], [Google+][17].

--------------------------------------------------------------------------------

via: https://www.cyberciti.biz/tips/repetitive-strain-injury-prevention-software.html

作者：[Vivek Gite][a]
译者：[译者ID](https://github.com/译者ID)
校对：[校对者ID](https://github.com/校对者ID)

本文由 [LCTT](https://github.com/LCTT/TranslateProject) 原创编译，[Linux中国](https://linux.cn/) 荣誉推出

[a]:https://www.cyberciti.biz/
[1]:https://www.cyberciti.biz/media/new/tips/2009/11/workrave-image.jpg (workrave-image)
[2]:https://en.wikipedia.org/wiki/Repetitive_strain_injury
[3]:https://web.eecs.umich.edu/~cscott/rsi.html##symptoms
[4]:https://www.cyberciti.biz/faq/ubuntu-lts-debian-linux-apt-command-examples/ (See Linux/Unix apt command examples for more info)
[5]:https://www.cyberciti.biz/tips/linux-debian-package-management-cheat-sheet.html (See Linux/Unix apt-get command examples for more info)
[6]:https://www.cyberciti.biz/faq/rhel-centos-fedora-linux-yum-command-howto/ (See Linux/Unix yum command examples for more info)
[7]:https://www.cyberciti.biz/media/new/tips/2009/11/add-workwave-to-panel.png (Adding an Object (Workrave) to a Gnome Panel)
[8]:https://www.cyberciti.biz/media/new/tips/2009/11/screenshot-workrave.png (Workrave main window shows the time remaining until it suggests a pause.)
[9]:https://www.cyberciti.biz/media/new/tips/2009/11/miss-workrave.png (Miss Workrave Sofrware character walks you through various RSI stretching exercises )
[10]:https://www.cyberciti.biz/media/new/tips/2009/11/time-for-micro-pause.gif (Workrave RSI Software Time for a micro-pause remainder )
[11]:https://www.cyberciti.biz/media/new/tips/2009/11/Micro-break.png (Workrave RSI Software Micro-break )
[12]:http://www.workrave.org/
[13]:https://github.com/ttygde/pokoy
[14]:http://gnomepomodoro.org
[15]:https://twitter.com/nixcraft
[16]:https://facebook.com/nixcraft
[17]:https://plus.google.com/+CybercitiBiz
