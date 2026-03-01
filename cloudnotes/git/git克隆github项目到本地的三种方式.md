

> 原创 已于 2025-06-18 14:12:02 修改 · 5.2k 阅读 · 12 · 34 · CC 4.0 BY-SA版权 版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。
> 文章链接：https://blog.csdn.net/m0_63564748/article/details/148012046

本文旨在使用git工具将别人发布在github上的项目保存到本地

1.安装git，创建github账户，并使用ssh关联自己的github账号和git，具体教程可以参照下面两篇文章：

[Github入门教程，适合新手学习（非常详细）_github教程-CSDN博客](https://blog.csdn.net/black_sneak/article/details/139600633?spm=1001.2014.3001.5506) 

[史上最全 Git 图文教程（非常详细）零基础入门到精通，收藏这一篇就够了-CSDN博客](https://blog.csdn.net/Javachichi/article/details/140660754?spm=1001.2014.3001.5506) 

2. 找到你要克隆的仓库地址

前往你想要克隆的 GitHub 仓库页面。在仓库页面中，你会看到一个绿色的“Code”按钮，点击它后会弹出一个包含仓库 URL 的对话框。你可以选择HTTPS、SSH 或 GitHub CLI 方式来克隆仓库。

3. 首先介绍最简单的HTTPS方式

<img src="https://i-blog.csdnimg.cn/direct/b89a4ce41dcc48a79714e8e4a13c110c.png" alt="" style="max-height:319px; box-sizing:content-box;" />

这种方式不需要关联自己的github账号就能下载，首先打开git

<img src="https://i-blog.csdnimg.cn/direct/ae8fd3e953084b198aa1d1d264f147e9.png" alt="" style="max-height:320px; box-sizing:content-box;" />

然后使用cd路径 这一命令，切换到你要保存的路径下

<img src="https://i-blog.csdnimg.cn/direct/78b85a22ebeb412d9f83870bac6783f5.png" alt="" style="max-height:64px; box-sizing:content-box;" />

执行git clonehttps://XXXXX命令，把https://开头的地址复制粘贴到命令后，执行这个命令，界面显示done说明克隆成功了。

<img src="https://i-blog.csdnimg.cn/direct/85af630ce2e940d6938247aa61d5b877.png" alt="" style="max-height:123px; box-sizing:content-box;" />

4. 使用SSH方式

该方式首先需要按照一开始给出的教程配置好你的 SSH key 并添加到 GitHub 账户中，然后直接使用git clone命令，运行即可。

**这句命令中，后面的SpectrumInstrumentation/spcm.git 是笔者要克隆的项目，冒号以及前面的指令不管你克隆什么项目都是一样的，不要把git@后面的邮箱写成自己的！** 

```cpp
git clone git@github.com:SpectrumInstrumentation/spcm.git
```

5. 使用GitHubCLI的方式， **这种方式是在windows终端运行命令的，不是git！** 

GitHub CLI 工具名为 `gh，这种方式比较复杂，需要先安装这个工具，再注册账号。` 

首先，安装GitHub CLI

控制面板——右键——运行——输入cmd

<img src="https://i-blog.csdnimg.cn/direct/3e2958d5d00d40f9a5fe5a8810b38381.png" alt="" style="max-height:229px; box-sizing:content-box;" />

在终端输入命令

```cpp
winget install --id GitHub.cli
```

<img src="https://i-blog.csdnimg.cn/direct/7ac3a30e80614de9a19395361102aeac.png" alt="" style="max-height:128px; box-sizing:content-box;" />

安装成功以后会有 提示

<img src="https://i-blog.csdnimg.cn/direct/ed53016f7d0b4da98464991a449be033.png" alt="" style="max-height:121px; box-sizing:content-box;" />

笔者使用的是windows系统，其他系统的安装方式，可参考：

[GitHub CLI 下载与安装教程-CSDN博客](https://blog.csdn.net/gitblog_01226/article/details/143036415) 

登录到 GitHub CLI。

在首次使用 GitHub CLI 前，你需要登录到你的 GitHub 账户。继续在终端输入并运行以下命令：

```cpp
gh auth login
```

按照提示完成登录过程。你可以选择浏览器认证或手动输入令牌的方式进行登录。

登录成功提示：

<img src="https://i-blog.csdnimg.cn/direct/9a0a1c152cbe472597722340e6e5c703.png" alt="" style="max-height:86px; box-sizing:content-box;" />

然后查找并克隆仓库，这里有2种方法：

1. 直接克隆。如果你已经有了仓库的 URL，可以直接使用 `gh repo clone` 命令来克隆

```cpp
gh repo clone SpectrumInstrumentation/spcm
```

2.如果你不确定仓库的确切名称，可以使用交互式搜索功能来找到并克隆仓库：

```cpp
gh repo clone
```

然后根据提示输入你想查找的仓库名或关键词，GitHub CLI 会列出匹配的结果供你选择。