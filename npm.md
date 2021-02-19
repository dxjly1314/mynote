# NPM

## 设置代理

1、设置http代理

```
npm config set proxy=http://代理服务器地址:8080
```

2、取消代理

```
npm config delete proxy
```

3、npm设置淘宝镜像

```
npm config set registry=https://registry.npm.taobao.org
```

4、npm取消淘宝镜像

```
npm config delete registry
```

5、查看代理信息（当前配置）

```
npm config list
```

## 切换阿里镜像

1、切换方法

```
$ npm config set registry https://registry.npm.taobao.org
```

2、检测是否修改成功

```
// 可通过下面方式来查看是否成功
npm config get registry
```

3、如果想用回国外的源，切换回来就行

```
npm config set registry https://registry.npmjs.org/
```

# NRM

## nrm安装与使用

### 1、什么是nrm

  nrm是一个npm源管理工具，使用它可以快速切换npm源。

### 2、安装

  使用如下命令安装：

```
npm install -g nrm
```

  安装完后可使用 nrm -V 显示版本，注意是大写V。

![img](.\npm.assets\775046-20190412104747251-1025523496.png)

### 3、切换npm源

  使用 nrm ls 查看所有源，可以看到列表中左侧为名称，右侧为地址。带*的为当前配置。

  ![img](.\npm.assets\775046-20190412103444265-133936145.png)

  使用 nrm use [registry] 切换源，国内我们可以切换为taobao。再使用 nrm ls 可以看到*改至taobao前，说明切换成功。也可以打开.npmrc文件，可以看到源已经设置为taobao地址。也可使用npm的 npm config list 命令查看配置。

  ![img](.\npm.assets\775046-20190412103835792-1298368212.png)

  ![img](.\npm.assets\775046-20190412104309324-403442398.png)

  nrm还提供了测速功能，命令为 nrm test [registry] ，不知道选哪个源时，可以先测一波，哪个快用哪个。不加registry时，可测所有的。

  ![img](.\npm.assets\775046-20190412104555351-1584107274.png)![img](.\npm.assets\775046-20190412111133285-118809942.png)

### 4、命令提示

  下面列出所有命令的中文示意：

1.  `nrm -V `：查看当前nvm版本。
2.  nrm -h ：显示所有命令。
3.  nrm current ：显示当前源名称。
4.  nrm use <registry> ：切换源。
5.  nrm add <registry> <url> [home] ：添加一个源。比如公司自己的私有源等。
6.  nrm set-auth <registry> <value> [always] ：设置自定义源的授权信息。
7.  nrm set-email <registry> <value> ：给自定义源设置路径。
8.  nrm set-hosted-repo <registry> <value> ：设置发布到自定义源的npm托管仓储。
9.  nrm del <registry> ：删除自定义源。
10.  nrm home <registry> [browser] ：浏览器中打开源首页。
11.  nrm publish [options] [<tarball>|<folder>] ：发布包到自定义源，如果没有使用自定义源，则直接发布到npm。
12.  nrm test [registry] ：测试源的访问速度。不加registry时，测试所有的。