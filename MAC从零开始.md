#### 系统配置

1. 查看磁盘，将`Untitled`重命名为`Machintosh HD`;

```sh
hxer:~ hxer$ diskutil list
/dev/disk0 (internal, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *500.3 GB   disk0
   1:                        EFI EFI                     209.7 MB   disk0s1
   2:          Apple_CoreStorage Untitled                499.4 GB   disk0s2
   3:                 Apple_Boot Recovery HD             650.0 MB   disk0s3

/dev/disk1 (internal, virtual):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:                  Apple_HFS Untitled               +496.3 GB   disk1
                                 Logical Volume on disk0s2
                                 52113102-9A34-4451-B8BB-A20A06A80823
                                 Unlocked Encrypted
hxer:~ hxer$ diskutil rename "Untitled" "Macintosh HD"
```

2. 命令行提示符前是`用户名:~ 主机名$`的形式，如何修改成传统的`user@hostname pwd$`的形式: 

   ```sh
   $ cat ~/.profile
   export PS1="\w\n\u@\h:\W$ "
   ```

   其中`\u`表示`username`，`\h`表示`hostname`，`\W`当前目录，`\w`当前目录的完整目录；`source ~/.profile`生效；上一行为当前目录的完整目录，`$`为当前目录；

   参考：[Hide current working directory in terminal](https://askubuntu.com/questions/16728/hide-current-working-directory-in-terminal)

3. 触摸板一定得按压才能感应: `System Perference` > `Trackpad` > `Tap to click`;

4. Typora中`win+1`是heading 1,但是这同时又是MAC系统的快捷键！如何修改系统快捷键？

5. 修改dock自动隐藏：`system perference` > `dock`;

6. 三指取词：`system perference` > `trackpad` > `Look up & datactors` 下拉菜单；

[修改主机名](https://apple.stackexchange.com/questions/66611/how-to-change-computer-name-so-terminal-displays-it-in-mac-os-x-mountain-lion) 

6. iChain自动生成强密码，但在哪找到密码？

   `Finder` > `Application` > `Utilities` > `Keychain Access`，其实可以直接在`Alfred`中输入`Keychain`;

#### 下载软件

#### Moom

默认以标准程序运行，每次在dock下面放着占空间。需要在程序页面将`run as`改为`menu bar`；

#### Alfred

[wordflow for beginner](https://computers.tutsplus.com/tutorials/alfred-workflows-for-beginners--mac-55446) [知乎·如何在Alfred中写workflow](https://www.zhihu.com/question/22301362) 

#### Snap: 软件快速启动，App Store可直接下载；

#### Homebrew

https://brew.sh/index_zh-cn，为了防止每次安装时都updating导致卡顿，在`~/.zshrc`中添加：`export HOMEBREW_NO_AUTO_UPDATE=true`.

[Cheatsheet](https://www.mediaatelier.com/CheatSheet/): 软件快捷键一览；

#### Iteminal

搜索到可以在`automator` > `run AppleScript` > `no input`:

```typescript
on run {input, parameters}
	
	(* Your script goes here *)
	tell application "Terminal"
		reopen
		activate
	end tell
	
end run
```

保存为`Open Terminal`之后，在`System Perference` > `keyboard` > `shortcut` > `service` > `Gerneral` > `Open Terminal`中设置快捷键；但是设置快捷键无效？

#### 印象笔记

APP Store下载很不稳定，还是直接从网页下载吧；[印象笔记](https://www.yinxiang.com/download/?offer=www_menu) 下载的`dmg`文件为`YinxiangBiji`而不是`Evernote_RELEASE_7.8_457453.dmg`，以**共享到印象笔记**；
