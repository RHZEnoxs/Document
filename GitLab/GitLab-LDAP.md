# Gitlab - LDAP 設定過程

## 設定檔
        vi /etc/gitlab/gitlab.rb
上面的需要做gitlab-ctl reconfigure
        
        vi /opt/gitlab/embedded/service/gitlab-rails/config/gitlab.yml
改完作 gitlab-ctl restart就可以
        

###### gitlab推薦 第一種方法

## 修改 gitlab.rb

```
gitlab_rails['ldap_enabled'] = true

###! **remember to close this block with 'EOS' below**
 gitlab_rails['ldap_servers'] = YAML.load <<-'EOS'
   main: # 'main' is the GitLab 'provider ID' of this LDAP server
     label: 'LDAP'
     host: '_your_ldap_server' # LDAP Server 網址
#     port: 389
     uid: 'sAMAccountName'
     bind_dn: 'USER_ACCOUNT' # AD 管理者帳號
     password: 'USER_PASSWORD' # AD 管理者密碼
#     encryption: 'plain' # "start_tls" or "simple_tls" or "plain"
#     verify_certificates: true
#     smartcard_auth: false
     active_directory: true
     allow_username_or_email_login: true # 可以讓使用者使用 名稱或Email 帳號登入
#     lowercase_usernames: false
     block_auto_created_users: false # 如果 true ， 需要管理者解鎖才可使用
     base: 'dc=enoxs,dc=com'
#     user_filter: ''
#     ## EE only
#     group_base: ''
#     admin_group: ''
#     sync_ssh_keys: false
#
#   secondary: # 'secondary' is the GitLab 'provider ID' of second LDAP server
#     label: 'LDAP'
#     host: '_your_ldap_server'
#     port: 389
#     uid: 'sAMAccountName'
#     bind_dn: '_the_full_dn_of_the_user_you_will_bind_with'
#     password: '_the_password_of_the_bind_user'
#     encryption: 'plain' # "start_tls" or "simple_tls" or "plain"
#     verify_certificates: true
#     smartcard_auth: false
#     active_directory: true
#     allow_username_or_email_login: false
#     lowercase_usernames: false
#     block_auto_created_users: false
#     base: ''
#     user_filter: ''
#     ## EE only
#     group_base: ''
#     admin_group: ''
#     sync_ssh_keys: false
EOS
```
## 驗證
gitlab-rake gitlab:ldap:check RAILS_ENV=production




參考資料：

<http://g23988.blogspot.com/2015/07/gitlabldap.html>

<https://ssorc.tw/6358>