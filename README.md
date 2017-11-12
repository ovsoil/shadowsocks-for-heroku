> Fork from [shadowsocks-heroku](https://github.com/mrluanma/shadowsocks-heroku)

# shadowsocks-heroku
[Heroku](https://www.heroku.com/) 提供免费的云服务，我们可以用它来搭建自己的shaowsocks服务.
shadowsocks-heroku 使用WeSocket代替[shadowsocks](https://github.com/clowwindy/shadowsocks) 的sockets。

完成下面的步骤，你就可以用 Google 了👻。

*如果你打不开[这个](http://shadowsocks-for-heroku.herokuapp.com/)链接，那下面的方法可能不适合你的网络=_=。*

### 一. 准备

*如果你无法访问下面的注册地址，也可以直接跳到第四步，先试用我已经部署好的SS服务*

1. 需要一个heroku账号。
Heroku 提供免费账号, 虽然有一些限制，但用作VPS是够了，注册地址：https://signup.heroku.com/

2. 需要一个github账号。
Github 是一个代码库 注册地址: https://github.com

3. 点击当前页面右上角的`Fork`按钮，Fork 本项目到你的github账号下。
    ![](https://github.com/ovsoil/shadowsocks-for-heroku/blob/master/img/fork.png)

### 二. 部署服务

heroku 可以通过关联 GitHub 账号，直接部署 GitHub 账号下的项目到云上：

1. 登陆 Heroku 帐号，后进入 Dashboard ——> Create New App ——> 输入 App Name
    **记住App Name 后面启动client的命令会用到**
    ![](https://github.com/ovsoil/shadowsocks-for-heroku/blob/master/img/create-app.png)
2. 完成上一步后，会跳转到 Deploy 页面，找到 Deployment method 选择 GitHub 关联上自己的 GitHub 帐号。

3. 关联上 shadowsocks-for-heroku 项目，如下图所示：
    ![](https://github.com/ovsoil/shadowsocks-for-heroku/blob/master/img/connect-github.png)
4. 点击 Deploy Branch，就可以把代理服务器部署到heroku上了，如下图：
    ![](https://github.com/ovsoil/shadowsocks-for-heroku/blob/master/img/deploy-from-github.png)

### 三. 设置加密算法和密码

进入Setting 页面 ——> Reveal Config Vars，设置参数如下图：
设置一个密码，并选择一个加密算法，**记住这两个，后面启动client的命令会用到**。
可以使用以下加密算法：
- rc4-md5
- aes-256-cfb
- camellia-256-cfb
![](https://github.com/ovsoil/shadowsocks-for-heroku/blob/master/img/config-vars.png)


### 四. 安装本地client：

1. 安装nodejs
    * Windows:
        下载nodejs并安装。[下载页面](http://nodejs.cn/download/)

    * Mac:

        打开Terminal (command + space, 输入terminal)  
        安装brew: `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`  
        安装nodejs: `brew install node`  

2. [下载](https://github.com/ovsoil/shadowsocks-for-heroku/archive/master.zip) 本项目，并解压到一个指定目录。
建议解压到用户目录下(Mac也是类似的解压到与`下载`等目录同级的位置)，如下图所示：
    ![](https://github.com/ovsoil/shadowsocks-for-heroku/blob/master/img/unpack.png)

3. 安装并启动本地client, 先**通过命令行进入解压目录**
    * Windows:
        通过开始菜单打开Node.js command prompt (Nodejs安装完成之后，点击Windows徽标键打开开始菜单，输入node，一般第一个搜索匹配项就是)  
        进入解压目录：`cd shadowsocks-for-heroku-master` (如果是在按照上面的说明解压到用户目录)  
        执行`npm install`, 安装依赖的库
    * Mac:
        打开Terminal (command + space, 输入terminal)  
        `cd shadowsocks-for-heroku-master`  
        `npm install`

4. 输入以下命令启动本地代理

    ```bash
       node local.js -s App名称.herokuapp.com -l 1080 -m 加密算法 -k 密码 -r 80`
    ```
   为了更方便启动，可以把`start_proxy.bat`(Windows)或者`start_proxy.sh`(Mac)里面的命令根据你的信息修改一下，以后就可以通过`./start_proxy.bat`或者`./start_proxy.sh`命令启动本地代理了。
    * 如果是试用我预先部署好的SS服务，可以直接执行已有的`start_proxy`脚本。

**全部配置完成之后，每次开机只要执行以上3，4两步，就可以打开Chrome上Google了。**

### 五. 启动本地代理并配置Chrome浏览器

1. 下载Chrome浏览器扩展[SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega/releases/download/v2.3.21/SwitchyOmega.crx)

2. 安装SwitchyOmega：打开浏览器的扩展程序页面 `chrome://extensions`, 把SwitchyOmega.crx文件拖放到浏览器扩展程序页面安装。

3. 配置：SwitchyOmega：`代理协议：SOCKS5 代理服务器：127.0.0.1 代理端口：1080`，如下图：
    ![](https://github.com/ovsoil/shadowsocks-for-heroku/blob/master/img/proxy.png)
4. 配置自动切换代理
    ![](https://github.com/ovsoil/shadowsocks-for-heroku/blob/master/img/auto-switch.png)
5. Let's Go 👻。
    ![](https://github.com/ovsoil/shadowsocks-for-heroku/blob/master/img/google.png)
