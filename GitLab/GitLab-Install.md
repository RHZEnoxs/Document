在線安裝
https://dotblogs.com.tw/echo/2017/10/19/linux_gitlab_installation



離線安裝

檔案名稱：
gitlab-ce-11.10.4-ce.0.el7.x86_64.rpm
[Source Url](https://packages.gitlab.com/gitlab/gitlab-ce)

安裝指令：
yum install -y gitlab-ce-11.10.4-ce.0.el7.x86_64.rpm

    vi /etc/gitlab/gitlab.rb

重新啓動gitlab-ctl配置服務

    gitlab-ctl reconfigure