# KotlinCMS
打造你的专属网站

体验KotlinCMS很简单  
第一步：首先你的安装好Docker.  
第二步：然后安装Docker-Compose.  
第三步：然后新建docker-compose.yml文件，将以下内容复制进文件  
```
version: '2'
services:
  redis:
    restart: always
    image: redis
    container_name: my_redis
    command: redis-server --requirepass 724e4df59e5e97be8c1a7665848b5856
    volumes:
      - ./redisdata:/data
  postgresql:
    restart: always
    image: linqmind/mypgsql:v202110292350
    container_name: my_db
    environment:
      - POSTGRES_USER=kotlincms
      - POSTGRES_DATABASE=kotlincms
      - POSTGRES_PASSWORD=724e4df59e5e97be8c1a7665848b5856

  kotlincms:
    restart: always
    image: linqmind/kotlincms:v2021102300
    container_name: kotlincms
    depends_on:
      - my_redis
      - my_db
    ports:
      - "8088:8088"
```  
然后保存  
第四步：运行服务  
`docker-compose -f ./docker-compose.yml up -d`  
第五步：待服务运行完毕  
访问首页  
http://localhost:8088  
访问后台管理  
http://localhost:8088/admin  
登录的用户名：admin  
登录的密码：1  
