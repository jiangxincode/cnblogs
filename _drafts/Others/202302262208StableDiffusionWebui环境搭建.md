# stable-diffusion-webui环境搭建与使用

## 条件准备

* Git(2.38.1)
* Python(3.10.9)
* Pillow(9.4.0)
* 有科学上网工具

必须的是一台显存4g以上电脑，英伟达的显卡。最好有科学上网工具，否则最后一步的部署会经常中断，需要反复尝试。

## 安装git

下载地址https://git-scm.com/downloads

下载好，安装，一直next即可，在Select Components这一步可以把Windows Explorer integration的勾去掉，这个如果不去掉，鼠标右键菜单会加入git相关的操作。

## 安装python3.10.6

下载地址https://www.python.org/downloads/

安装时，要打勾Add Python 3.10 to PATH，之后一直next即可。

## 部署stable-diffusion-webui

新建一个文件夹，文件名随意，用于存放stable-diffusion-webui和模型。

进入你新建的文件夹，右键页面空白处，点击在终端中打开，执行指令 git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git，下图是执行成功后的样子，成功后可关掉界面。


## 下载模型文件

模型决定了生成图片的风格和质量。新手可以下载这个默认的模型，下载地址https://huggingface.co/CompVis/stable-diffusion-v-1-4-original/tree/main，下载sd-v1-4.ckpt，点击这个右边的小箭头即可。

下载后，回到步骤4中新建的那个文件夹，把下载好的模型文件，我这里使用的是（sd-v1-4.ckpt）放到stable-diffusion-webui\models\Stable-diffusion这个文件夹下（如果是NovelAi的模型，将ckpt和pt文件都放在此文件夹下）

## 部署stable-diffusion-webui

双击webui.bat，自动开始部署，如果不使用科学上网，这个过程会很慢且容易报错。非常建议使用科学上网。

若使用科学上网，在你的上网软件里看一下代理端口（port），下图是我的。


然后在任务栏点击


搜索Windows powershell，运行这行命令：git config --global http.proxy http://127.0.0.1:7890，这里7890是我的端口，要改成你自己的。

然后再运行webui-user.bat，部署过程中，可能会出现报错，或提示更新pip，不用管，多部署几次就好，我个人3次成功。


出现这个就代表成功了。

## 开始ai作画

见上图，部署完成后会有一个链接


链接复制到浏览器中打开，会出现以下界面，这里我在左上角输入apple，点击右上角generate，生成了一张关于苹果的图片。左下角可以调整图片参数和生成图片数量。


教程结束，谢谢大家支持，欢迎在评论区交流讨论。 作者：46789FG https://www.bilibili.com/read/cv21748847 出处：bilibili