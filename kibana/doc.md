可视化看板 Kibana。在 ES 8.x 版本中，这里有一个极具欺骗性的生产巨坑。

🚨 **避坑指南**：在老版本中，Kibana 往往直接用超级管理员 `elastic` 连 ES。但在 ES 8.x 出于安全防御机制，官方**硬性切断并禁止**使用超级管理员账号作为 Kibana 后台连接 ES 的通信凭证。否则，Kibana 会启动失败并疯狂刷 `value of "elastic" is forbidden`。

**极简启动步骤**：
1. **重置内置账号密码**：借助刚才已经跑起来的 ES 容器，在服务器终端直接重置系统的专属通信账号密码：
   ```bash
   docker exec -it elasticsearch /usr/share/elasticsearch/bin/elasticsearch-reset-password -u kibana_system -i
   ```
2.编写并启动 Docker Compose**：创建 Kibana 的 `docker-compose.yml`，填入刚刚为 `kibana_system` 重置得到的密码

认知盲区提示：当您通过浏览器打开 http://你的IP:5601 看到登录页面时，请务必注意：登入前端 UI 界面依然需要输入默认超级管理员账号 elastic 和它的密码！ kibana_system 账号仅用作 Kibana 看板程序在后台与 ES 通信，无法用于前端网页登录。