### 教程信息

名称：自动登录厦门大学嘉庚学院校园网的一种方法

分类：教程

投放：auro[Trusted]

### 在进行教程之前，你需要...

准备以下软件

> MSYS2 - 用于兼容bash样式指令
>
> 浏览器 - edge和chrome通过本次教程测试

请注意，MSYS2是为了能够在bash样式下使用cURL,如果你熟悉cmd样式，请自行调整。

### 教程

1.首先你需要打开浏览器并输入 10.100.1.5[[快捷进入](http://10.100.1..5)] 进入认证页面

![](.\img\Guide_AutoTKKC_CamNetworkLog_01.png)

2.输入你自己的账号密码，此时不要点 连接 按钮

> 记住密码可以勾上

3.按下 F12 打开开发者工具，选择网络选项，此时你应该看到这个页面(近似即可)

![](.\img\Guide_AutoTKKC_CamNetworkLog_02.png)

4.点击登录

5.在刚才的页面中，找到这一项

![](.\img\Guide_AutoTKKC_CamNetworkLog_03.png)

右键并选择 复制 -> 复制为cURL

> 通常选择bash,我不确定cmd方式应该如何正常运作
>
> 使用cmd时我遇到了 请在ePortal上注册设备 的提示
>
> 以下为示例，使用XXX代替隐私内容

```bash
curl 'http://10.100.1.5/eportal/InterFace.do?method=login' \
  -H 'Accept: */*' \
  -H 'Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6' \
  -H 'Content-Type: application/x-www-form-urlencoded; charset=UTF-8' \
  -H 'Cookie: EPORTAL_COOKIE_OPERATORPWD=; EPORTAL_AUTO_LAND=; EPORTAL_COOKIE_DOMAIN=false; EPORTAL_COOKIE_USERNAME=XXXXXXXX; EPORTAL_COOKIE_SAVEPASSWORD=true; EPORTAL_COOKIE_NEWV=true; EPORTAL_COOKIE_PASSWORD=XXXXX; EPORTAL_COOKIE_SERVER=XXXXX; EPORTAL_COOKIE_SERVER_NAME=XXXXX; EPORTAL_USER_GROUP=XXXXX; JSESSIONID=XXXXXX; JSESSIONID=XXXXX' \
  -H 'Origin: http://10.100.1.5' \
  -H 'Proxy-Connection: keep-alive' \
  -H 'Referer: ' \
  -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.0.0 Safari/537.36 Edg/111.0.1661.41' \
  --data-raw 'userId=XXXXXXXX&password=XXXXXXX&此处省略一大段隐私内容&operatorPwd=&operatorUserId=&validcode=&passwordEncrypt=false' \
  --compressed \
  --insecure
```

6.将内容保存为 文件名.sh

推荐这样做,让登陆结果可以轻易链接

```
echo Now auto login...
echo
这里插入你复制的curl代码 | grep -o \"result\":\".......\"
echo
echo If result is not success,It means you need to update your prompt
read -n1 -r -p "Press any key to continue..." key
```

![](.\img\Guide_AutoTKKC_CamNetworkLog_04.png)

7.验证你的结果

此时打开你的sh文件，应该显示如下内容了

![](.\img\Guide_AutoTKKC_CamNetworkLog_05.png)

### 后期工作

在成功之后，你应该把它加进系统启动项

之后每次掉网开一下文件即可