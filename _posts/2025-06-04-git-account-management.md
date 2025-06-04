---
title: Git多平台多账号管理
layout: post
category: article
description: 有时候要负责Git多个账号的登录，或者多平台的操作，如githu.com 或者gitee.com 下面是解决方案
---

## 一、账号管理

有时候要负责Git多个账号的登录，或者多平台的操作，如githu.com 或者gitee.com 下面是解决方案!

## 二、指定位置生成密钥

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"   -f ~/.ssh/user_id_rsa
```



| 参数                          | 含义                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| `-t ed25519`                  | 使用 Ed25519 算法生成密钥（比 RSA 更快更安全）               |
| `-C "your_email@example.com"` | 添加注释，通常用于标识该密钥（如邮箱或用途）                 |
| `-f ~/.ssh/user_id_rsa`       | 指定密钥文件保存位置（不加 `.pub`，公钥会自动生成 `.pub` 文件） |

生成结果：
私钥：~/.ssh/user_github_id_rsa

公钥：~/.ssh/user_github_id_rsa.pub

这已经可以满足单平台了

## 三、多平台多用户

### 密钥生成管理

可以通过文件夹方式来管理密钥如 githu 以及gitee，在生成密钥是时候  用-f 参数来指定生成的文件夹

github

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"   -f ~/.ssh/github/user1_id_rsa
ssh-keygen -t ed25519 -C "your_email@example.com"   -f ~/.ssh/github/user2_id_rsa
```

gitee

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"   -f ~/.ssh/gitee/user1_id_rsa
ssh-keygen -t ed25519 -C "your_email@example.com"   -f ~/.ssh/gitee/user2_id_rsa
```

other

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"   -f ~/.ssh/other/user1_id_rsa
ssh-keygen -t ed25519 -C "your_email@example.com"   -f ~/.ssh/other/user2_id_rsa
```



### 配置多个账户

密钥生成了，就要通过config文件来区分账户跟平台了

1.创建config文件

```bash
cd ~/.ssh  #进入.ssh根目录
touch config #创建config配置文件
```

2.配置config文件

```bash
# [github.com]

## 第一个账号，默认使用的账号
Host github.com
 HostName github.com
 User git
 IdentityFile ~/.ssh/github/user1_id_rsa
## 第二个账号 your_name
Host your_name.github.com # your_name为前缀名，可以任意设置
 HostName github.com
 User git
 IdentityFile ~/.ssh/github/user2_id_rsa
 
# [gitee.com] 

## 第一个账号，默认使用的账号
Host gitee.com
 HostName gitee.com
 User git
 IdentityFile ~/.ssh/gitee/user1_id_rsa
## 第二个账号 your_name
Host your_name.gitee.com # your_name为前缀名，可以任意设置
 HostName gitee.com
 User git
 IdentityFile ~/.ssh/gitee/user2_id_rsa
 
 # [other] 
 ## .....
 
```

> 原理分析:
>
> 1.ssh 客户端是通过类似 git@github.com:githubUserName/repo.git 的地址来识别使用本地的哪个私钥的， 地址中的 User 是@前面的git， Host 是@后面的github.com。
>
> 2.如果所有账号的 User 和 Host 都为 git 和 github.com，那么就只能使用一个私钥。 所以要对User 和 Host 进行配置，让每个账号使用自己的 Host，每个 Host 的域名做 CNAME 解析到 github.com， 如上面配置中的Host your_name.github.com。
>
> 3.配置了别名之后，新的地址就是git@your_name.github.com:githubUserName/repo.git。 这样 ssh 在连接时就可以区别不同的账号了。
>
> 4.其他平台也是同样理解

3.验证配置

输入指令,验证配置是否成功，以github为例，其他平台一样的道理

3.1 默认ssh_key验证

```bash
ssh -T git@github.com
```

3.2 新ssh_key验证, 新秘钥名替换your_name

```bash
ssh -T git@your_name.github.com
```

(注意)如果提示如下信息, 则配置成功

Hi your_name! You've successfully authenticated, but GitHub does not provid

## 四、项目食用

1.设置单独用户名以及邮箱

```bash
# 取消全局 用户名/邮箱 配置
git config  --global --unset user.name
git config  --global --unset user.email

# 单独设置每个repo 用户名/邮箱,进入到.git文件夹
git config user.name "your_name"  //在config后加上--global即全局
git config user.email "your_email@youremail.com"
```

2.远程仓库操作

2.1 绑定远程仓库(默认)

```bash
git remote add origin git@github.com:githubusername/repo.git
```

2.2 绑定多git用户仓库地址

```bash
git remote add origin git@your_name.github.com:githubusername/repo.git
```

2.3 更换远程仓库（按需求）

```bash
git remote set-url origin git@github.com:githubusername/another-repo.git
```

2.4.查看远程仓库地址

```bash
git remote -v
```

2.5 删除仓库地址

```bash
git remote remove origin
```

2.6 推送到远程仓库（区分好main/master）

```bash
git push -u origin main
```

2.7 查看当前项目配置

```bash
git config --list
```



## 五、git高级操作 main与master之间的切换（按需）

自此github 仓库默认分支改成main 之后，之前的老项目推送肯定有问题 ，会遇到本地分支名称跟仓库主分支名称不一致的情况

1.本地分支名称跟仓库分支名称一致

即情景A : 本地是master/仓库是master 或者 情景B: 本地是main / 仓库是main

```bash
git push -u origin master
```

或者

```bash
git push -u origin main
```

然后执行

```bash
git push
```

2.修改当前分支的默认上游（即重新绑定远程分支）

如果你想切换当前本地分支（比如 `main`）的推送目标为远程的 `master`：

```bash
git branch --set-upstream-to=origin/master main
```

或者

```bash
git push -u origin master  # 如果你本地当前分支是 master
```

3.修改远程默认分支（GitHub/Gitee）

远程仓库的默认分支（如 main 或 master）是由平台（GitHub、Gitee）设置的，可以通过网页端手动更改：

GitHub：进入仓库 → Settings → Branches → Default branch

Gitee：进入仓库 → 管理 → 默认分支设置

4.本地分支改名（main <-> master）

```bash
# master 改名为 main
git branch -m master main

# 然后推送新分支并设置 upstream
git push -u origin main

# 可选：删除旧远程 master 分支（慎用）
git push origin --delete master
```

命令汇总

| 目的                           | 命令                                       |
| ------------------------------ | ------------------------------------------ |
| 推送当前分支并设置远程跟踪     | `git push -u origin main`                  |
| 更换当前分支绑定的远程分支     | `git branch --set-upstream-to=origin/main` |
| 查看所有分支及其跟踪信息       | `git branch -vv`                           |
| 修改本地分支名                 | `git branch -m old new`                    |
| 修改远程默认分支（网页上操作） | GitHub/Gitee 设置里更改                    |

## 六、git高级操作 多账户/平台同步（按需）

### 配置文件

1.查看远程仓库

```bash
git remote -v
```

2.先删除已关联的名为origin的远程库：

```bash
git remote rm origin
```

3.然后，再关联GitHub的远程库：

```
git remote add github git@github.com:your_name/仓库名称.git    	#your_name改成你的用户名
```

4.接着，再关联gitee的远程库：

```
git remote add gitee git@gitee.com:your_name/仓库名称.git 		#your_name改成你的用户名
```

5.查看仓库配置 

```
git remote -v
```


gitee   git@gitee.com:your_name/仓库名称.git (fetch)
gitee   git@gitee.com:your_name/仓库名称.git (push)
github  git@github.com:your_name/仓库名称.git (fetch)
github  git@github.com:your_name/仓库名称.git (push)

如果出现以上结果说明配置成功

### 仓库更新

1.上传代码

```bash
git add .
git commit -m "update"
```

提交到github

```bash
git push github master
```

提交到码云

```bash
git push gitee master
```

2.更新代码

```bash
# 从github拉取更新
git pull github

# 从gitee拉取更新
git pull gitee
```
** 踩到的坑**

上述过程中，更新或提交代码时可能会遇到fatal:refusing to merge unrelated histories (拒绝合并无关的历史) 错误，解决办法：

首先将远程仓库和本地仓库关联起来。

```bash
git branch --set-upstream-to=origin/remote_branch  your_branch
```

其中，origin/remote_branch是你本地分支对应的远程分支，your_branch是你当前的本地分支。

然后使用git pull整合远程仓库和本地仓库。

git pull --allow-unrelated-histories    (忽略版本不同造成的影响)
重新更新、提交即可。

注： 如遇到 Git没有共同祖先的两个分支合并 的情形请自行查询！
