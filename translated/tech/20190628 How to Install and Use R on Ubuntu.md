[#]: collector: (lujun9972)
[#]: translator: (guevaraya)
[#]: reviewer: ( )
[#]: publisher: ( )
[#]: url: ( )
[#]: subject: (How to Install and Use R on Ubuntu)
[#]: via: (https://itsfoss.com/install-r-ubuntu/)
[#]: author: (Sergiu https://itsfoss.com/author/sergiu/)

如何在Ubuntu上安装和使用R语言
======

_**简介: 这个教程是指导如何在Ubuntu上安装R语言。同时可以学习到如何在Ubuntu上用不同方法运行简单的R语言程序**_

[R][1] ，和Python一样，他是在统计计算和图形处理上最常用的编程语言，易于处理数据。随着数据分析，数据可视化，数据科学(机器学习热）的火热化，对于想深入这一领域的人来说，它是一个很好的工具。

R语言的优点是他的语法非常简练，你可以结合现实生活找到它的很多教程或指南。

本文将介绍包含如何在Ubuntu下安装R语言，也会介绍在Linux下如何运行第一个R程序。

![][2]

### 如何在Ubuntu上安装R语言

**R** 默认在Ubuntu的软件库里。用以下命令很容易安装：

```
sudo apt install r-base
```

请注意可能会安装一个老版本。在我写这篇文字的时候，Ubuntu已经提供的3.4的，但是最新的是3.6.

_我建议如果不是万不得已就直接使用Ubuntu的配套版本。_

如果想安装最新的版本（或特殊情况指定版本），你必须用**[CRAN][3]** （Comprehensive R Archive Network）。这个是R最新版本的镜像，点击进入页面学习如何在Ubuntu上安装R语言。

**如何在Ubuntu上安装最新3.6版本的R环境 (单击展开)**

如需获取3.6的版本，需要添加镜像到你的源索引里。我已经简化其命令如下：

```
sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran35/"
```

下面你需要添加密钥到服务器中：

```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
```

然后更新服务器信息并安装R环境：

```
sudo apt update
sudo apt install r-base
```

就这样安装完成。

[][4]

建议阅读在Linux下如何制作可启动 Windows 10的U盘的文章

### 如何在Ubuntu下使用R语言编程

R的用法多样，我将介绍运行多个运行R语言的方式。

#### R语言的交互模式

安装了R语言后，你可以在控制台上直接运行：

```
R
```

这样会打开交互模式：

![R Interactive Mode][5]

R语言的控制与 **Python** 和 **Haskell** 的交互模式很类似. 你可以输入 **R** 命令做一些基本的数学运算，例如：

```
> 20+40
[1] 60

> print ("Hello World!")
[1] "Hello World!"
```

你可以测试绘图：

![R Plotting][6]

如果想 **退出** 可以用 **q()** 或  按下 **CTRL+c** 键. 接着你会被提示是否保存工程 ****镜像; 一个工程 **** 创建变量的环境。

#### 用R脚本运行程序


第二种运行R程序的方式是直接在Linux命令行下运行。你可以用**RScript**执行，它是一个包含**r-base**的工具。


首先，你需要用[Linux下常用的编辑器][7]保存R程序到文件。文件的扩展名必须是.r。

下面是一个打印 "Hello World" 的R程序。你可以保存其为hello.r。

```
print("Hello World!")
a <- rnorm(100)
plot(a)
```

运行R程序，用下面命令：

```
Rscript hello.r
```

你会得到如下输出结果：

```
[1] "Hello World!"
```

结果将会保存到当前工作目录，文件名为**Rplots.pdf**:

![Rplots.pdf][8]

**小提示**_**Rscript**_默认不会加载_**methods**_包。确保在脚本中显式加载它。

#### 在Ubuntu下用RStudio运行R语言

The most common way to use **R** is using [RStudio][10], a great cross-platform open source IDE. You can [install it using deb file in Ubuntu][11]. Download the deb file from the link below. You’ll have to scroll down a bit to locate the DEB files for Ubuntu.

[Download RStudio for Ubuntu][12]

Once you download the DEB file, just double click on it to install it.

Once installed, search for it in the menu and start it. The home window of the application should pop up:

![RStudio Home][13]

Here you have a working console, just like the one you got in the terminal with the **R** command.

[][14]

Suggested read  Setting Up Python Environments In Linux and Unix Systems

To create a file, in the top bar click on **File** and select **New File &gt; Rscript** (or **CTRL+Shift+n)**:

![RStudio New File][15]

Press **CTRL+s** to save the file and choose a location and a name it:

![RStudio Save File][16]

After doing so, click on **Session &gt; Set Working Directory &gt; To Source File Location** to change the working directory to the location of your script:

![RStudio Working Directory][17]

You are now ready to go! Write in your code and click run. You should be able to see output both in the console and in the plotting window:

![RStudio Run][18]

**Wrapping Up**

In this article, I showed you step by step how to get started using the **R** programming language on an Ubuntu system. I covered several ways you can go about this: **R console** – useful for testing, **Rscript** – for the terminal lover, **RStudio** – the IDE for your needs.

Whether you are willing to get into data science or simply love statistics, **R** is a good addition to your programming arsenal, being the perfect tool for analyzing data.

If you are absolutely new to R, let me recommend you this excellent book that will teach you fundamentals of R. It’s available on Amazon Kindle.

Preview | Product | Price |
---|---|---|---
![Learn R in a Day][19] ![Learn R in a Day][19] | [Learn R in a Day][20] |  | [Buy on Amazon][21]

Do you use **R**? Are you just getting into it? Let us know more about how and why you use or want to learn to use **R**!

--------------------------------------------------------------------------------

via: https://itsfoss.com/install-r-ubuntu/

作者：[Sergiu][a]
选题：[lujun9972][b]
译者：[译者ID](https://github.com/译者ID)
校对：[校对者ID](https://github.com/校对者ID)

本文由 [LCTT](https://github.com/LCTT/TranslateProject) 原创编译，[Linux中国](https://linux.cn/) 荣誉推出

[a]: https://itsfoss.com/author/sergiu/
[b]: https://github.com/lujun9972
[1]: https://www.r-project.org/
[2]: https://i2.wp.com/itsfoss.com/wp-content/uploads/2019/06/install-r-on-ubuntu.jpg?resize=800%2C450&ssl=1
[3]: https://cran.r-project.org/
[4]: https://itsfoss.com/bootable-windows-usb-linux/
[5]: https://i1.wp.com/itsfoss.com/wp-content/uploads/2019/06/r_interactive_mode.png?fit=800%2C516&ssl=1
[6]: https://i0.wp.com/itsfoss.com/wp-content/uploads/2019/06/r_plotting.jpg?fit=800%2C434&ssl=1
[7]: https://itsfoss.com/best-modern-open-source-code-editors-for-linux/
[8]: https://i1.wp.com/itsfoss.com/wp-content/uploads/2019/06/rplots_pdf.png?fit=800%2C539&ssl=1
[9]: https://www.dummies.com/programming/r/how-to-install-load-and-unload-packages-in-r/
[10]: https://www.rstudio.com/
[11]: https://itsfoss.com/install-deb-files-ubuntu/
[12]: https://www.rstudio.com/products/rstudio/download/#download
[13]: https://i1.wp.com/itsfoss.com/wp-content/uploads/2019/06/rstudio_home.jpg?fit=800%2C603&ssl=1
[14]: https://itsfoss.com/python-setup-linux/
[15]: https://i0.wp.com/itsfoss.com/wp-content/uploads/2019/06/rstudio_new_file.png?fit=800%2C392&ssl=1
[16]: https://i1.wp.com/itsfoss.com/wp-content/uploads/2019/06/rstudio_save_file.png?fit=800%2C258&ssl=1
[17]: https://i0.wp.com/itsfoss.com/wp-content/uploads/2019/06/rstudio_working_directory.png?fit=800%2C394&ssl=1
[18]: https://i0.wp.com/itsfoss.com/wp-content/uploads/2019/06/rstudio_run.jpg?fit=800%2C626&ssl=1
[19]: https://i1.wp.com/images-na.ssl-images-amazon.com/images/I/51oIJTbUlnL._SL160_.jpg?ssl=1
[20]: https://www.amazon.com/Learn-R-Day-Steven-Murray-ebook/dp/B00GC2LKOK?SubscriptionId=AKIAJ3N3QBK3ZHDGU54Q&tag=chmod7mediate-20&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B00GC2LKOK (Learn R in a Day)
[21]: https://www.amazon.com/Learn-R-Day-Steven-Murray-ebook/dp/B00GC2LKOK?SubscriptionId=AKIAJ3N3QBK3ZHDGU54Q&tag=chmod7mediate-20&linkCode=xm2&camp=2025&creative=165953&creativeASIN=B00GC2LKOK (Buy on Amazon)
