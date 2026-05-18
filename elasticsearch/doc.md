* **🚨 【核心避坑配置】免证书 HTTP 传输配置**：
  ES 8.x 默认强行启用了 HTTP 层的 SSL 加密（强制要求客户端走 `https://` 访问），这在单机或轻量化内网测试阶段，会引入极其复杂的自签名 CA 证书链配置工作。
  为了在轻量化架构中用普通的 `http://` 进行平滑连接，我们需要在宿主机映射出的 **`config/elasticsearch.yml`** 配置文件中，追加或修改如下参数：
  ```yaml
  cluster.name: "docker-cluster"
  network.host: 0.0.0.0
  http.port: 9200
  http.cors.enabled: true
  http.cors.allow-origin: "*"
  xpack.security.http.ssl.enabled: false  # 🌟 显式关闭 HTTP 层的 SSL 认证，开启平滑的 HTTP 访问
  ```

> **获取或重置默认管理员密码**：
> 容器首次顺利跑起来后，系统会自动生成一个超级管理员账号，默认账号名固定为：**`elastic`**。
> 至于它的初始密码，您有两种方式可以获取或重置：
>
> **方式一：去日志查看初始密码**
> 直接在服务器终端执行 `docker logs elasticsearch`，在输出的启动日志中，会有一大块明显的日志输出框，里面打印了系统为您生成的初始随机密码。
>
> **方式二：简单粗暴直接重置**
> 如果日志刷得太多找不到了也没关系，我们直接进容器给它强制重置一个好记的新密码。执行以下交互式命令，按提示输入并确认新密码即大功告成：
> ```bash
> docker exec -it elasticsearch /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic -i
> ```
