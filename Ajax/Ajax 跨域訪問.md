# Ajax 跨域訪問

### 允許 Chrome 跨域訪問 （Mac）
        open /Applications/Google\ Chrome.app --args --allow-file-access-from-files
        open -n -a /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --args --user-data-dir="/tmp/chrome_dev_test" --disable-web-security
### 允許 Chrome 跨域訪問 （Win）
    Chrome.lnk
    目標：
        --args --disable-web-security --user-data-dir=C:\MyChromeDevUserData
    完整：
        "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --args --disable-web-security --user-data-dir=C:\MyChromeDevUserData


``` javascript
        var postUrl = 'http://localhost:8080/appInfo/postInteger';
        var formData = {
            id: 1
        };
        $.post(postUrl, formData, function (data, status) {
            var response = JSON.parse(decodeURIComponent(data));
            if (response.status == 'success') {
                alert(response.desc);
                console.log(response.list);
            } else {
                alert(response.desc);
            }
        }).always(function () {
        });
```


參考資料
<https://alfilatov.com/posts/run-chrome-without-cors/>