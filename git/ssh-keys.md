# 同一台电脑设置多个ssh-key #

生成私钥

    ssh-keygen -t rsa -C "thondery@163.com" -f ~/.ssh/github
    ssh-keygen -t rsa -C "thondery@163.com" -f ~/.ssh/oschina
    ssh-keygen -t rsa -C "thondery@163.com" -f ~/.ssh/gitcafe
    ssh-keygen -t rsa -C "thondery@163.com" -f ~/.ssh/coding

配置私钥

    vi ~/.ssh/config

内容如下

    #github
    Host github
        HostName github.com
        User git
        IdentityFile ~/.ssh/github

    #oschina
    Host oschina
        HostName git.oschina.net
        User git
        IdentityFile ~/.ssh/oschina

    #gitcafe
    Host gitcafe
        HostName gitcafe.com
        User git
        IdentityFile ~/.ssh/gitcafe

    #coding
    Host coding
        HostName coding.net
        User git
        IdentityFile ~/.ssh/coding

登录各自网站添加ssh-key

测试ssh-key

    ssh -T github
    ssh -T oschina
    ssh -T gitcafe
    ssh -T coding

设置用户名和邮箱

    git config --global user.name "thondery"
    git config --global user.email "thondery@163.com"
