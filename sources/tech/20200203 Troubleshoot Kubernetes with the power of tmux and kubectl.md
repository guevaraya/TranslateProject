[#]: collector: (lujun9972)
[#]: translator: ( guevaraya)
[#]: reviewer: ( )
[#]: publisher: ( )
[#]: url: ( )
[#]: subject: (Troubleshoot Kubernetes with the power of tmux and kubectl)
[#]: via: (https://opensource.com/article/20/2/kubernetes-tmux-kubectl)
[#]: author: (Abhishek Tamrakar https://opensource.com/users/tamrakar)

解决 Kubernetes 问题的利器 Tmux 和 kubectl
======
一个 kubectl 插件 用 tmux 使 Kubernetes 疑难问题变得更简单。

![一个坐在笔记本面前的妇女][1]

[Kubernetes][2] 是一个活跃的开源容器管理平台，它提供了可扩展性，高可用性，健壮性和富有弹性的应用程序管理。它的众多特性之一是支持通过原生的客户端程序  [kubectl][3] 运行定制脚本或可执行程序，Kubectl 是很强大的，允许用户在 Kubernetes 集群上用它直接做很多事情。

### 使用别名进行 Kubernetes 的故障排查

使用 Kubernetes 的容器管理的人都知道由于设计上原因带来了其复杂性。例如，迫切的可快速的以及几乎不需要人工干预方式简化故障排查（除过特殊情况）。

在故障排查功能方面，这有很多场景需要考虑。有一个场景，你知道你需要运行什么，但是这个命令的语法（即使作为一个单独的命令运行）过于复杂，或需要一、两次交互才能起作用。

例如，如果你频繁的需要调整到一个系统命名里正在运行的容器，你可能发现自己在重复的写入：

```
`kubectl --namespace=kube-system exec -i -t <your-pod-name>`
```
为了简化故障排查，你可以用这些指令的命令行补全功能。比如，你可以增加下面命令到你的隐藏配置文件（.bashrc 或 .zshrc）：

```
`alias ksysex='kubectl --namespace=kube-system exec -i -t'`
```

这是来自于常见的 [Kubernetes 别名仓][4]的一个例子，它展示了一个 kubectl 简化的功能的方法。像这个场景的简化情况，使用别名很有用。

### 切换到 kubectl 插件

更复杂的故障排查场景是需要执行很多命令，一个一个的执行，然后去调查环境，最后得出结论。单用别名方法是不能解决这种情况的；你需要知道你所部署的Kubernetes 之间逻辑和和相关性，你真是需要的是自动化来短时间输出你想要的。

考虑到你的集群有10到20或50到100个命名空间来提供不同的微服务。在这个常见下进行故障排查，有什么对你有帮助？

  * 你需要某个东西可快速的告知哪个 Pod 哪个 命名空间抛的错误。
  * 你需要牧歌东西可监视一个命名空间的所有 pod 的日志。
  * 你可能也需要监视出现错误的指定命名空间的特定的 pod 的日志。


只要包含以上这些点的任何的解决方案将对定位产品问题很大的帮助，包含对开发和测试周期过程。

你可以用 [kubectl 插件][5] 创建比简易别名更强大的东西。插件类似于其他用任何语言编写的独立脚本，但被设计为 Kubernetes 管理员的主要命令扩展。

创建一个插件，你必须用正确的语法 **kubectl-&lt;your-plugin-name&gt;** 来拷贝这个脚本到导出目录 **$PATH** ，需要赋予可执行权限（**chmod +x**）。

创建插件之后把他移动到你的目录，你需要立即运行。例如，你的目录下有一个 kubectl-krawl 和 kubectl-kmux:


```
$ kubectl plugin list
The following compatible plugins are available:

/usr/local/bin/kubectl-krawl
/usr/local/bin/kubectl-kmux

$ kubectl kmux
```
现在让我们见识下带有 tmux 的 Kubernetes 的有多强大。

### 驾驭强大的 tmux

[Tmux][6] 是一个非常强大的工具，许多管理员和操作团队通过它来返回问题故障，通过易于分屏的方式到窗口上并行调试多个机器以及管理日志。他的一个主要的优点是可基于命令行或自动化的脚本。

我创建[一个 kubectl 插件][7] 用 tmux 使故障排查更加简单。我将通过注释来了解插件背后的逻辑（我们来瞅一瞅插件的整个源码）：

```
#NAMESPACE is namespace to monitor.
#POD is pod name
#Containers is container names

# initialize a counter n to count the number of loop counts, later be used by tmux to split panes.
n=0;

# start a loop on a list of pod and containers
while IFS=' ' read -r POD CONTAINERS
do

           # tmux create the new window for each pod
            tmux neww $COMMAND -n $POD 2&gt;/dev/null

           # start a loop for all containers inside a running pod
        for CONTAINER in ${CONTAINERS//,/ }
        do

        if [ x$POD = x -o x$CONTAINER = x ]; then
        # if any of the values is null, exit.
        warn "Looks like there is a problem getting pods data."
        break
        fi
           
            # set the command to execute
        COMMAND=”kubectl logs -f $POD -c $CONTAINER -n $NAMESPACE”
        # check tmux session
        if tmux has-session -t &lt;session name&gt; 2&gt;/dev/null;
        then
        &lt;set session exists&gt;
        else
        &lt;create session&gt;
        fi

           # split planes in the current window for each containers
        tmux selectp -t $n \; \
        splitw $COMMAND \; \
        select-layout tiled \;

           # end loop for containers
        done

           # rename the window to identify by pod name
        tmux renamew $POD 2&gt;/dev/null
       
            # increment the counter
        ((n+=1))

# end loop for pods
done&lt; &lt;(&lt;fetch list of pod and containers from kubernetes cluster&gt;)

# finally select the window and attach session
 tmux selectw -t &lt;session name&gt;:1 \; \
  attach-session -t &lt;session name&gt;\;
```

运行插件脚本后，它将在当前目录会生成一个同名的镜像。每个 pod 有一个窗口，每个容器（如果有多个）被分割成不同 pos 窗口，日志以数据流形式输出。 漂亮的tmux 如下；如果配置正确，你将会看到哪个窗口是否处于激活运行状态（可看到标签是白色的）。

![kmux 插件的输出][8]

### Conclusion

Aliases are always helpful for simple troubleshooting in Kubernetes environments. When the environment gets more complex, a kubectl plugin is a powerful option for using more advanced scripting. There are no limits on which programming language you can use to write kubectl plugins. The only requirements are that the naming convention in the path is executable, and it doesn't have the same name as an existing kubectl command.

To read the complete code or try the plugins I created, check my [kube-plugins-github][7] repository. Issues and pull requests are welcome.

--------------------------------------------------------------------------------

via: https://opensource.com/article/20/2/kubernetes-tmux-kubectl

作者：[Abhishek Tamrakar][a]
选题：[lujun9972][b]
译者：[译者ID](https://github.com/译者ID)
校对：[校对者ID](https://github.com/校对者ID)

本文由 [LCTT](https://github.com/LCTT/TranslateProject) 原创编译，[Linux中国](https://linux.cn/) 荣誉推出

[a]: https://opensource.com/users/tamrakar
[b]: https://github.com/lujun9972
[1]: https://opensource.com/sites/default/files/styles/image-full-size/public/lead-images/OSDC_women_computing_4.png?itok=VGZO8CxT (一个坐在笔记本面前的妇女)
[2]: https://opensource.com/resources/what-is-kubernetes
[3]: https://kubernetes.io/docs/reference/kubectl/overview/
[4]: https://github.com/ahmetb/kubectl-aliases/blob/master/.kubectl_aliases
[5]: https://kubernetes.io/docs/tasks/extend-kubectl/kubectl-plugins/
[6]: https://opensource.com/article/19/6/tmux-terminal-joy
[7]: https://github.com/abhiTamrakar/kube-plugins
[8]: https://opensource.com/sites/default/files/uploads/kmux-output.png (Output of kmux plugin)
