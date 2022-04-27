#### 3. 命令行使用

关于这块的文档aws有详细的介绍，官方文档为[如何为 AWS 设置开发环境 | 模块 3](https://aws.amazon.com/cn/getting-started/guides/setup-environment/module-three/)

首先需要安装amazon命令行工具即aws cli，点击以下链接找对应系统

https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

然后打开终端界面，出现以下即显示安装成功

```
aws --version
aws-cli/2.2.17 Python/3.9.6 Darwin/20.5.0 source/x86_64 prompt/off
```

```
aws configure

AWS Access Key ID [None]: ANOTREALACCESSKEYID
AWS Secret Access Key [None]: ANOTREALSECRETACCESSKEY
Default region name [None]: eu-west-1
Default output format [None]: json
```

密码可以在下载的new_user_credentials.csv查看，也可以在iam用户控制中心里查看自己的access_key。

##### 创建新的access key
如果没有new_user_credentials.csv或者不知道自己的secret access key，可以在个人界面的安全凭证section自己创建新的“用于访问 CLI、开发工具包和 API 的访问密钥”。

配置好了输入命令可查看到结果


```
aws ec2 describe-vpcs

# Output
{
    "Vpcs": [
        {
            "CidrBlock": "10.0.0.0/16",
            "DhcpOptionsId": "dopt-d12345",
            "State": "available",
            "VpcId": "vpc-0123456789abcdef",
            "OwnerId": "123456789012",
```

正确设置后，在 **~/.aws** (Linux / MacOS) 或 **%UserProfile%\.aws** (Windows) 中可以查看**config** 和 **credentials**。**credentials** ，打开后会包含之前输入的access_key和secret_access_key，成功后的config,credentials文件里应该是这样的

```
[default]
aws_access_key_id = AKNOTREALACCESSKEYID
aws_secret_access_key = AyNOTREALSECRETACCESSKEY
```

```
[default]
region = us-east-1
output = json
```

#### 4.连接ec2
目前的ec2是linux 20.04系统，首先我们需要登录amazon ec2平台，通过组长给大家发送的邮箱链接登录iam账户后

在窗口搜索ec2点击进入
https://console.aws.amazon.com/console/home
![](https://i.imgur.com/CMBp6kV.png)

点击正在运行的实例instances，目前已创建的instance在us-east-1区域
![](https://i.imgur.com/3qonoWN.png)

选择连接进入ec2
![](https://i.imgur.com/Mm3Gxwu.png)


目前有两种方式连接ec2，第一种就是通过网页的方式直接访问，即ec2 instant connect

![](https://i.imgur.com/P4YLexB.png)



另一种方式就是通过ssh访问，这一步需要先配置好cli

之后进入之前保存路径，即xx.pem的路径下，比如我是在downloads里，然后修改xx.pem的权限，最后确认一下

```
cd Downloads
chmod 400 home.pem
ls -l home.pem
-r--------@ 1 yikunjian  staff  1678  4 11 22:12 home.pem
```

成功后使用ssh示例里的命令行连接即可
![](https://i.imgur.com/I96k3Dp.png)


![](https://i.imgur.com/BpNkMjP.png)

这步骤会询问是否创建sha256 key，输入yes
即可发现使用命令行登录成功
![](https://i.imgur.com/F4OOiDq.png)

##### 关于如何获取.pem
有两种方法：

a. 可以通过网页上detail的pair-key这里来获取
![](https://i.imgur.com/bxyXy4i.png)
点击pair-key的创建，即可创建属于你的.pem

    可以用组名+姓名的方式创建.pem key，比如backend-guoba_home吗，backend-guoba_work，以区分每个人的.pem

b. 如果设置好cli，也可以在自己的local machine输入

```
aws ec2 create-key-pair \                   
    --key-name backend_alice \
    --key-type ed25519 \
    --query "KeyMaterial" \
    --output text > backend_alice.pem
```
会自动将你的public key加入到ec2 default region的key pair。



#### 5.1 vpn
> **在国内的目前连接ec2需要使用vpn，因此需要你有付费or免费的vpn**

免费vpn有[蓝灯](https://getlantern.org/zh_CN/),支持windows和linux系统

关于命令行走代理，这篇文章说的比较详细
[Linux 让终端走代理的几种方法](https://zhuanlan.zhihu.com/p/46973701)
