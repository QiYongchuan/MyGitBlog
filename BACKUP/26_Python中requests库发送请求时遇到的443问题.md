# [Python中requests库发送请求时遇到的443问题](https://github.com/QiYongchuan/MyGitBlog/issues/26)

报错信息：
```
    raise SSLError(e, request=request)
requests.exceptions.SSLError: HTTPSConnectionPool(host='wttr.in', port=443): Max retries exceeded with url: /%E5%A4%A9%E6%B4%A5?lang=zh (Caused by SSLError(SSLEOFError(8, 'EOF occurred in violation of protocol (_ssl.c:997)')))
```
看到443 以及 SSLError报错，心里大概有了方向：应该还是代理及网络的原因。

问GPT，答：

![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/285cf4b8-0374-4be8-b0a4-771045bdfafd)

期间Google、csdn搜索的方法：
![image](https://github.com/QiYongchuan/MyGitBlog/assets/105039020/9d55e0fd-fe19-4c3f-9bf6-8f5c195a7e19)
在发送请求的同时，关闭SSL验证，以及添加配置代理服务器设置。
仍无法解决。

最后解决方法：关闭梯子