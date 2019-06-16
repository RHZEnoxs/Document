# GitLab - Backup

### Create Backup
1. SSH 遠端登入
        ssh account@gitlab.remote.com
        
2. 創建備份
        sudo gitlab-rake gitlab:backup:create
        
        Skip:
        sudo gitlab-rake gitlab:backup:create SKIP = db,uploads
3. 備份檔路徑
        
        cd /var/opt/gitlab/backups
        
    訪問此路徑必須有 root 權限才可訪問
        
    >   **console**: 
   
    >       backups: 拒絕不符權限的操作
 
4. 使用 root 權限帳號拉取備份
        scp root@192.168.2.127:/var/opt/gitlab/backups/1558862798_2019_05_26_11.10.4_gitlab_backup.tar C:\
        
5. 使用 root 權限帳號推送備份
        scp 1558862798_2019_05_26_10.10.10_gitlab_backup.tar root@192.168.2.127:/var/opt/gitlab/backups/
6. 停止 GitLab 服務

        sudo gitlab-ctl stop unicorn
        sudo gitlab-ctl stop sidekiq
        
        **驗證狀態**:
        sudo gitlab-ctl status
7. 還原備份
        sudo gitlab-rake gitlab:backup:restore BACKUP = 1558862798_2019_05_26_10.10.10
8. 重新啟動 GitLab 服務
        sudo gitlab-ctl restart
        
        **檢查備份狀態**
        sudo gitlab-rake gitlab:check SANITIZE = true

9. 定時備份
##### BackupGitLab.sh
        #sudo cd /var/opt/gitlab/backups/
        sudo gitlab-rake gitlab:backup:create  
        sudo find /var/opt/gitlab/backups/  -type f -ctime +5 -exec rm -rf {} \;
    ---
        備份檔案並刪除創建時間超過五天以上檔案
##### 使用 Linux 排程定時備份
        crontab -e
        30 03 * * * /home/admin/task/BackupGitLab.sh 
> 剛訪問目錄必須使用 root 權限訪問
        
**參考資料：**<https://www.itread01.com/content/1541499310.html>