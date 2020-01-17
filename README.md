# Homepage of Li-Xi Jiang lab

网站由Hugo驱动，
下面的内容主要说明在实验室服务器主机上的配置和维护。

## 配置

如果是第一次/重新部署到Ubuntu16.04上，需要进行配置，否则只需要进行维护。

### 安装Hugo

```
wget -c https://github.com/gohugoio/hugo/releases/download/v0.62.2/hugo_0.62.2_Linux-64bit.tar.gz # 可以下载其他版本
tar -zxvf *tar.gz
#cp ./hugo /usr/local/bin/ # 可以放到专门的程序目录中，也可以后面直接通过路径运行
```

### 拉取apache容器

安装docker-ce，然后`sudo docker pull httpd`。

接着将配置文件从容器中拷贝出来

专门创建一个`apache`目录放置建站需要修改或提供的文件。

在里面新建2个文件夹：`conf`和`logs`。

以交互模式运行一个`httpd`容器，然后从外面拷贝配置文件到`conf`目录下。

```
docker run --name lab_website -idt httpd
sudo docker cp <容器名>:/usr/local/apache2/conf/httpd.conf /public/data/apache/conf/
```

克隆本仓库，在仓库根目录下运行`hugo`。

将`public`目录链接为`apache`下的`www`目录。

```
 ln -s jianglab/public/ www
```


然后使用`sudo`运行下面的代码。

```
 sudo ./run_website.sh jianglab_website
```

文件名：run_website.sh

```
docker run --name $1 -p 80:80 \
  -v /public/data/apache/www/:/usr/local/apache2/htdocs/  \
  --mount type=bind,source=/public/data/apache/conf/httpd.conf,target=/usr/local/apache2/conf/httpd.conf  \
  -v /public/data/apache/logs/:/usr/local/apache2/logs/  \
  -d httpd

```

此时就可以通过http://服务器ip/ 进行访问了。

下面展示下`apache`目录结构：

```
.
├── conf
│   └── httpd.conf
├── logs
│   └── httpd.pid
├── www -> jianglab/public/
└── jianglab
    ├── archetypes
    ├── config.toml
    ├── content
    ├── public
    ├── README.md
    ├── resources
    ├── static
    └── themes
```


## 维护


- 停止`jianglab_website`容器。
- 拉取和更新仓库。
- 使用`hugo`重新生成页面。
- 重新运行`jianglab_website`容器

**特别感谢上海科技大学[王诗翔](https://github.com/XSLiuLab/XSLiuLab.github.io)以及[biaslab](https://github.com/biaslab/biaslab-hugo)，本网站主要根据他们的网站修改而来**。

