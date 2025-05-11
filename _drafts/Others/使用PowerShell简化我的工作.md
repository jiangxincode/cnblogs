
在这几年的编程学习和工作中，我积累的许多轻量级的小工具，比如Everything，BeyondCompare，BatchRename、HperSnap等等，这些软件都是绿色软件，无需安装，即使重装系统也可以很容易的迁移。但是由于工具比较多，不可能在桌面上为这些工具全部设置快捷方式，于是只能使用命令行进行调用。程序员们应该都知道，如果想要在cmd或者powershell中调用这些小工具，就要把这些工具的可执行文件的所在目录添加到系统环境变量Path之中。但是这样手工去添加太麻烦了，因为要添加的目录比较多，而且之后如果还想加入新的工具就必须继续设置环境变量，最重要的一点是每次重装系统还要重新设置一遍。作为一个程序员怎么去做这么笨的事情呢？于是我写了一个powershell配置脚本，让powershell每次启动时都去读该脚本，设置环境变量。
    首先介绍一下我的工具集的结构：

* Tools/
    * ToolA.exe
    * ToolB.exe
    * ToolC.exe
    * ...
    * Toola/
        * Toolsa.exe
        * Toola工具的其它文件 
    * Toolb/
        * Toolsb.exe
        * Toolb工具的其它文件 
    * ...

下面是我的powershell脚本（profile.ps1）：

    # Put this profile file into %userprofile%\[My] Documents\WindowsPowerShell for only yoursef
    # Put this profile file into $windir%\system32\WindowsPowerShell\v1.0 for every in your computer
    # Set the $BasePath to the directory which your tools are placed

    $BasePath = new-object System.IO.DirectoryInfo "D:\software\tools"

    $Env:Path = $Env:Path + ":" + $BasePath

    Get-ChildItem $BasePath | ForEach-Object -Process {

    if($_ -is [System.IO.DirectoryInfo]) {

        $Env:Path=$Env:Path + ";" + $BasePath.FullName + "\" + $_.Name;

        }
    }

另外这个脚本之后可能会添加一些其它功能，大家可以随时到我的github上看看：https://github.com/jiangxincode/data/blob/master/profile.ps1