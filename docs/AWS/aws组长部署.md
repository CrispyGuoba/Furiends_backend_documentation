## amazon iam

> amazon对于开发者的身份验证识别以及授权，目前访问有两种方式

#### 1. 访问方式

- 控制台访问

  - 使用账户或别名，iam用户名和密码

  - 如果已启动，mfa会提示输入身份验证代码

- 编程方式访问

  - access key 或者secret access key(需要自己在个人电脑初始化配置)

  - 提供对api,cli，软件开发工具包和其他开发工具的访问


##### 1.1 控制台访问方式

目前控制台访问即通过amazon 云科技管理控制台，输入12位账户id,用户名和密码, 每一个主体可以有多个iam账户

![](https://i.imgur.com/UgzM6CG.png)

##### 1.2 编程访问方式

![](https://i.imgur.com/EKSUKFu.png)


#### 2. 配置密钥私钥

通过创建用户，设置组别，aws会自动配置每个用户的access key和secret accesskey以及密钥私钥,一共是两个文件:
**new_user_credentials.csv**
**xx.pem**


2.1. 第一步，进入iam控制面板的用户界面

![](https://i.imgur.com/8cxWC3v.png)


2.2. 添加用户，可以一系列添加用户，这一步可由组长完成(目前所有组员已分配到账号，组长暂无需再为组员分配账号)，访问类型勾选编程+aws控制台

![](https://i.imgur.com/SPZTYLh.png)

2.3. 将每个组员设置对应的部门，目前应该是front + backend + ai三个，由各个组长为组员创立用户(目前所有组员已分配到账号，组长暂无需再为组员分配账号)

![](https://i.imgur.com/mV39TYG.png)


2.4. 第一次登陆会需要重设密码，大家根据邮件所发送的链接注册登录即可

![](https://i.imgur.com/AlFxkxE.png)
