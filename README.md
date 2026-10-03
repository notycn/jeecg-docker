# jeecgboot-docker
	使用GitHub Actions自动构建jeecgboot的docker镜像，比在自己机器上构建的快
	构建完毕后，然后下载镜像并安装
**docker yaml：

```services:
  jeecg-backend:
    image: ghcr.nju.edu.cn/ghcr.io/notycn/jeecg-backend:v3.9.5
    container_name: jeecg-backend
    restart: unless-stopped
    environment:
      TZ: Asia/Shanghai
      SPRING_PROFILES_ACTIVE: dev
      SPRING_DATASOURCE_DYNAMIC_DATASOURCE_MASTER_URL: "jdbc:mysql://192.168.2.3:3306/jeecg-boot?characterEncoding=UTF-8&useUnicode=true&useSSL=false&tinyInt1isBit=false&allowPublicKeyRetrieval=true&serverTimezone=Asia/Shanghai"
      SPRING_DATASOURCE_DYNAMIC_DATASOURCE_MASTER_USERNAME: mysql用户名
      SPRING_DATASOURCE_DYNAMIC_DATASOURCE_MASTER_PASSWORD: mysql密码
      SPRING_DATA_REDIS_HOST: 192.168.2.3
      SPRING_DATA_REDIS_PORT: 6379
      SPRING_DATA_REDIS_PASSWORD: ""
      JAVA_OPTS: "-Xms256m -Xmx768m"
    volumes:
      - ./upload:/jeecg-boot/upload
    ports:
      - "28431:8080"

  jeecg-frontend:
    image: ghcr.nju.edu.cn/ghcr.io/notycn/jeecg-frontend:latest
    container_name: jeecg-frontend
    restart: unless-stopped
    depends_on:
      - jeecg-backend
    ports:
      - "28432:80"
