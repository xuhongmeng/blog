## Nginx搭建简单的图片服务器
---
## 参考资料
[官网](http://nginx.org/)
[下载地址](http://nginx.org/en/download.html)

---
## Nginx常用简单的几个命令
* 启动
    ```
    start nginx
    ```
* 验证配置是否正确
    ```
    nginx -s conf/nginx.conf
    ```
* 重新加载
    ```
    nginx -s reload
    ```
* 快速停止
    ```
    nginx -s stop
    ```
* 完全停止
    ```
    nginx -s quit
    ```


### 步骤
#### Windows版本

1. 下载Windows版本 (如：nginx/Windows-1.14.0 )
1. 解压拷贝到C盘。形成的目录类似:（C:\nginx-1.14.0）,在终端进入这个目录。
1. 启动nginx。start nginx
1. 在浏览器访问.http://localhost，显示如下内容为正常启动:
    ```
    Welcome to nginx!
    If you see this page, the nginx web server is successfully
    installed and working. Further configuration is required.

    For online documentation and support please refer to nginx.org.
    Commercial support is available at nginx.com.

    Thank you for using nginx.
    ``` 
1. 拷贝图片到路径(和配置和url访问有关)到： C:\pic\abc\efg\1.jpg
1. 修改配置nginx.conf
        location /C/ {
			alias C:/pic/;
            #root   html;
            #index  index.html index.htm;
		}
1. 重新加载: nginx -s reload
1. 在浏览器上面访问:http://localhost/C/abc/1.jpg
就可以访问到图片

### 注意问题
