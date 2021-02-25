## Haskell的安装与运行
#### 安装

1.https://www.haskell.org/platform/ 进入官网，点击第一步Configure Chocolatey。

2.电脑搜索PowerShell，**以管理员身份打开**。

3.输入 Get-ExecutionPolicy，发现被Restricted。

4.输入Set-ExecutionPolicy Bypass -Scope Process。

5.输入Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

一路选择Y

6.输入choco install haskell-dev，完成。

#### 运行Hello World

1.新建文件Hello.hs，内容为

​    main = putStrLn"Hello, World!"

2.cmd 在**文件路径下**运行ghc Hello.hs.

3.输入Hello。看到cmd出现Hello, World.