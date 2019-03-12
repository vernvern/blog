

步骤| 细节
---|---
输入网址|
dns | 通过dns获取ip地址
socket|tcp通讯
tcp| 建立连接(3次握手)
tcp | 传输数据包 start
负载均衡| LVS(基于tcp/ip做路由转发)、反向代理(应用层转发)
web server| apache、tomcat、uwsgi、gunicorn
后端框架|flask、django、tornado等
数据库 | mysql、postgresql
前端 | html、css、js | 
tcp | 传输数据包 end
tcp|断开连接(4次握手)
显示网页|