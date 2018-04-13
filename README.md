# Linux服务器CentOS7常用软件安装教程

linux

---

## gitlab
### 安装
新建 /etc/yum.repos.d/gitlab-ce.repo，内容为

    [gitlab-ce]
    name=Gitlab CE Repository
    baseurl=https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/yum/el$rel    easever/
    gpgcheck=0
    enabled=1
再执行

    sudo yum makecache
    sudo yum install gitlab-ce

### 使用自己的nginx服务器
[nginx配置](https://docs.gitlab.com/omnibus/settings/nginx.html#using-an-existing-passenger-nginx-installation)




