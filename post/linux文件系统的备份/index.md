# Linux文件系统的备份

# Linux文件系统的备份

​		最近还是按捺不住自己安装了Manjaro，并且搭配了i3的桌面。由于曾经使用过arch，这一次配置起来倒还是轻车熟路，本打算manjaro只做试验，不做主力系统，所以并没有分配太多磁盘空间（40GB），可是manjaro-i3相比Windows实在是太香，尤其实在我这个好几年前的配置的电脑几乎要带不动win10的情况下，索性打算直接暂用manjaro做学习的主力系统。那么这样的话，40GB的大小就显得不够用了。

​		所以我打算先扩展一下磁盘大小，cfdisk发现磁盘好像不能向左扩展，从Windows身上割下来的20G空间无法融入到linux中，遂在网上查找后，发现了gparted好像可以实现我想要的效果，gparted提示磁盘文件有丢失的风险，最好备份谨慎使用，并且基于arch的manjaro同样是滚动更新，多少还是有不稳定的风险，于是我便找起了备份系统的方法。

一番对比之后选择了rsync

## Rsync的基本特点如下： 

1. 可以镜像保存整个目录树和文件系统； 
2. 可以很容易做到保持原来文件的权限、时间、软硬链接等； 
3. 无须特殊权限即可安装； 
4. 优化的流程，文件传输效率高； 
5. 可以使用rsh、ssh等方式来传输文件，当然也可以通过直接的socket连接； 
6. 支持匿名传输。

最重要的是**增量备份**，即每次只更新变化的那部分。

## 基本用法

### 1 `-r` 参数

本机使用 rsync 命令时，可以作为`cp`和`mv`命令的替代方法，将源目录同步到目标目录。

 ```bash
 $ rsync -r source destination
 ```

上面命令中，`-r`表示递归，即包含子目录。注意，`-r`是必须的，否则 rsync 运行不会成功。`source`目录表示源目录，`destination`表示目标目录。

如果有多个文件或目录需要同步，可以写成下面这样。

 ```bash
 $ rsync -r source1 source2 destination
 ```

上面命令中，`source1`、`source2`都会被同步到`destination`目录。

### 2 `-a` 参数

`-a`参数可以替代`-r`，除了可以递归同步以外，还可以同步元信息（比如修改时间、权限等）。由于 rsync 默认使用文件大小和修改时间决定文件是否需要更新，所以`-a`比`-r`更有用。下面的用法才是常见的写法。

 ```bash
 $ rsync -a source destination
 ```

目标目录`destination`如果不存在，rsync 会自动创建。执行上面的命令后，源目录`source`被完整地复制到了目标目录`destination`下面，即形成了`destination/source`的目录结构。

如果只想同步源目录`source`里面的内容到目标目录`destination`，则需要在源目录后面加上斜杠。

 ```bash
 $ rsync -a source/ destination
 ```

上面命令执行后，`source`目录里面的内容，就都被复制到了`destination`目录里面，并不会在`destination`下面创建一个`source`子目录。

### 3 `-n` 参数

如果不确定 rsync 执行后会产生什么结果，可以先用`-n`或`--dry-run`参数模拟执行的结果。

 ```bash
 $ rsync -anv source/ destination
 ```

上面命令中，`-n`参数模拟命令执行的结果，并不真的执行命令。`-v`参数则是将结果输出到终端，这样就可以看到哪些内容会被同步。

### 4 `--delete` 参数

默认情况下，rsync 只确保源目录的所有内容（明确排除的文件除外）都复制到目标目录。它不会使两个目录保持相同，并且不会删除文件。如果要使得目标目录成为源目录的镜像副本，则必须使用`--delete`参数，这将删除只存在于目标目录、不存在于源目录的文件。

 ```bash
 $ rsync -av --delete source/ destination
 ```

上面命令中，`--delete`参数会使得`destination`成为`source`的一个镜像。

## 排除文件

### 1 `--exclude` 参数

有时，我们希望同步时排除某些文件或目录，这时可以用`--exclude`参数指定排除模式。

 ```bash
 $ rsync -av --exclude='*.txt' source/ destination
 # 或者
 $ rsync -av --exclude '*.txt' source/ destination
 ```

上面命令排除了所有 TXT 文件。

注意，rsync 会同步以"点"开头的隐藏文件，如果要排除隐藏文件，可以这样写`--exclude=".*"`。

如果要排除某个目录里面的所有文件，但不希望排除目录本身，可以写成下面这样。

 ```bash
 $ rsync -av --exclude 'dir1/*' source/ destination
 ```

多个排除模式，可以用多个`--exclude`参数。

 ```bash
 $ rsync -av --exclude 'file1.txt' --exclude 'dir1/*' source/ destination
 ```

多个排除模式也可以利用 Bash 的大扩号的扩展功能，只用一个`--exclude`参数。

 ```bash
 $ rsync -av --exclude={'file1.txt','dir1/*'} source/ destination
 ```

如果排除模式很多，可以将它们写入一个文件，每个模式一行，然后用`--exclude-from`参数指定这个文件。

 ```bash
 $ rsync -av --exclude-from='exclude-file.txt' source/ destination
 ```

### 2 `--include` 参数

`--include`参数用来指定必须同步的文件模式，往往与`--exclude`结合使用。

 ```bash
 $ rsync -av --include="*.txt" --exclude='*' source/ destination
 ```

上面命令指定同步时，排除所有文件，但是会包括 TXT 文件。

## 远程同步

### 1 SSH 协议

rsync 除了支持本地两个目录之间的同步，也支持远程同步。它可以将本地内容，同步到远程服务器。

 ```bash
 $ rsync -av source/ username@remote_host:destination
 ```

也可以将远程内容同步到本地。

 ```bash
 $ rsync -av username@remote_host:source/ destination
 ```

rsync 默认使用 SSH 进行远程登录和数据传输。

由于早期 rsync 不使用 SSH 协议，需要用`-e`参数指定协议，后来才改的。所以，下面`-e ssh`可以省略。

 ```bash
 $ rsync -av -e ssh source/ user@remote_host:/destination
 ```

但是，如果 ssh 命令有附加的参数，则必须使用`-e`参数指定所要执行的 SSH 命令。

 ```bash
 $ rsync -av -e 'ssh -p 2234' source/ user@remote_host:/destination
 ```

上面命令中，`-e`参数指定 SSH 使用2234端口。

### 2 rsync 协议

除了使用 SSH，如果另一台服务器安装并运行了 rsync 守护程序，则也可以用`rsync://`协议（默认端口873）进行传输。具体写法是服务器与目标目录之间使用双冒号分隔`::`。

 ```bash
 $ rsync -av source/ 192.168.122.32::module/destination
 ```

注意，上面地址中的`module`并不是实际路径名，而是 rsync 守护程序指定的一个资源名，由管理员分配。

如果想知道 rsync 守护程序分配的所有 module 列表，可以执行下面命令。

 ```bash
 $ rsync rsync://192.168.122.32
 ```

rsync 协议除了使用双冒号，也可以直接用`rsync://`协议指定地址。

 ```bash
 $ rsync -av source/ rsync://192.168.122.32/module/destination
 ```

## 源目录后面无 “/“ 和有 “/“ 的区别

将 /etc/yum 目录复制到 /tmp/zhang/ 目录下。

```bash
1 # 源目录后面无 "/"
2 [yun@backup ~]$ rsync -avz /etc/yum  /tmp/zhang/
3 [yun@backup ~]$ ll /tmp/zhang/
4 total 0
5 drwxr-xr-x 6 yun yun 100 Nov 14  2018 yum
```

将 /etc/yum/ 目录下的所有文件和目录，复制到 /tmp/zhang/ 目录下。

```bash
1 # 源目录后面有 "/"
2 [yun@backup ~]$ rsync -avz /etc/yum/  /tmp/zhang/
3 [yun@backup ~]$ ll /tmp/zhang/
4 total 4
5 drwxr-xr-x 2 yun yun   6 Apr 13  2018 fssnap.d
6 drwxr-xr-x 2 yun yun  54 Nov 14  2018 pluginconf.d
7 drwxr-xr-x 2 yun yun  26 Nov 14  2018 protected.d
8 drwxr-xr-x 2 yun yun  37 Apr 13  2018 vars
9 -rw-r--r-- 1 yun yun 444 Apr 13  2018 version-groups.conf
```

## 七、配置项

`-a`、`--archive`参数表示存档模式，保存所有的元数据，比如修改时间（modification time）、权限、所有者等，并且软链接也会同步过去。

`--append`参数指定文件接着上次中断的地方，继续传输。

`--append-verify`参数跟`--append`参数类似，但会对传输完成后的文件进行一次校验。如果校验失败，将重新发送整个文件。

`-b`、`--backup`参数指定在删除或更新目标目录已经存在的文件时，将该文件更名后进行备份，默认行为是删除。更名规则是添加由`--suffix`参数指定的文件后缀名，默认是`~`。

`--backup-dir`参数指定文件备份时存放的目录，比如`--backup-dir=/path/to/backups`。

`--bwlimit`参数指定带宽限制，默认单位是 KB/s，比如`--bwlimit=100`。

`-c`、`--checksum`参数改变`rsync`的校验方式。默认情况下，rsync 只检查文件的大小和最后修改日期是否发生变化，如果发生变化，就重新传输；使用这个参数以后，则通过判断文件内容的校验和，决定是否重新传输。

`--delete`参数删除只存在于目标目录、不存在于源目标的文件，即保证目标目录是源目标的镜像。

`-e`参数指定使用 SSH 协议传输数据。

`--exclude`参数指定排除不进行同步的文件，比如`--exclude="*.iso"`。

`--exclude-from`参数指定一个本地文件，里面是需要排除的文件模式，每个模式一行。

`--existing`、`--ignore-non-existing`参数表示不同步目标目录中不存在的文件和目录。

`-h`参数表示以人类可读的格式输出。

`-h`、`--help`参数返回帮助信息。

`-i`参数表示输出源目录与目标目录之间文件差异的详细情况。

`--ignore-existing`参数表示只要该文件在目标目录中已经存在，就跳过去，不再同步这些文件。

`--include`参数指定同步时要包括的文件，一般与`--exclude`结合使用。

`--link-dest`参数指定增量备份的基准目录。

`-m`参数指定不同步空目录。

`--max-size`参数设置传输的最大文件的大小限制，比如不超过200KB（`--max-size='200k'`）。

`--min-size`参数设置传输的最小文件的大小限制，比如不小于10KB（`--min-size=10k`）。

`-n`参数或`--dry-run`参数模拟将要执行的操作，而并不真的执行。配合`-v`参数使用，可以看到哪些内容会被同步过去。

`-P`参数是`--progress`和`--partial`这两个参数的结合。

`--partial`参数允许恢复中断的传输。不使用该参数时，`rsync`会删除传输到一半被打断的文件；使用该参数后，传输到一半的文件也会同步到目标目录，下次同步时再恢复中断的传输。一般需要与`--append`或`--append-verify`配合使用。

`--partial-dir`参数指定将传输到一半的文件保存到一个临时目录，比如`--partial-dir=.rsync-partial`。一般需要与`--append`或`--append-verify`配合使用。

`--progress`参数表示显示进展。

`-r`参数表示递归，即包含子目录。

`--remove-source-files`参数表示传输成功后，删除发送方的文件。

`--size-only`参数表示只同步大小有变化的文件，不考虑文件修改时间的差异。

`--suffix`参数指定文件名备份时，对文件名添加的后缀，默认是`~`。

`-u`、`--update`参数表示同步时跳过目标目录中修改时间更新的文件，即不同步这些有更新的时间戳的文件。

`-v`参数表示输出细节。`-vv`表示输出更详细的信息，`-vvv`表示输出最详细的信息。

`--version`参数返回 rsync 的版本。

`-z`参数指定同步时压缩数据。

----

还好去年双十一购买的云服务器还有一部分磁盘空间可以使用。按照archwiki上的提示，备份整个系统只要

```bash
# rsync -aAXHv --exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"} / /path/to/backup
```

通过使用 `-aAX` 选项集，文件以归档模式传输，确保符号链接、设备、权限、所有权、修改时间、[ACLs](https://wiki.archlinux.org/title/Access_Control_Lists_(简体中文))和扩展属性得以保留，前提是目标[文件系统](https://wiki.archlinux.org/title/File_systems)支持这一功能。选项 `-H` 保留了硬链接，但会使用更多的内存。

`--exclude` 选项使符合给定模式的文件被排除。在上述命令中，`/dev`、`proc`、`/sys`、`/tmp`和`/run` 等目录被包括在内，但这些目录的内容被排除在外。这是因为它们在系统启动时才会被填入内容，但这些目录本身不会被创建。 `/lost+found` 是针对文件系统的。上面的命令依赖于 [bash](https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html) 和 [zsh](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Brace-Expansion) 中可用的括号扩展。当使用不同的 [shell](https://wiki.archlinux.org/title/Shell) 时，应该手动重复 `--exclude` 模式。加入排除选项可以避免被 [shell](https://wiki.archlinux.org/title/Shell) 误扩展，例如，在通过 [SSH](https://wiki.archlinux.org/title/Secure_Shell_(简体中文)) 备份时，这是必要的。以 `*` 结尾的排除路径可以确保目录本身在不存在的情况下被创建。 份，就像 [cron](https://wiki.archlinux.org/title/Cron) 脚本一样。}}

---

## 参考链接

https://www.ruanyifeng.com/blog/2020/08/rsync.html

https://wiki.archlinux.org/title/Rsync_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#%E5%85%A8%E7%9B%98%E7%B3%BB%E7%BB%9F%E5%A4%87%E4%BB%BD




