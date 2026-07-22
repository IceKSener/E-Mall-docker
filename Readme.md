# E-Mall 项目 docker 打包与部署

编译 [EMall 后端项目](https://github.com/xixibuxixi2005/E-Mall-backend) 后打包成三个jar文件分别丢进 `mall-ai-service` `mall-biz-service` `mall-gateway` 文件夹下，比如：

```text
mall-ai-service/
├─Dockerfile
└─mall-ai-service-1.0-SNAPSHOT.jar
mall-biz-service/
├─Dockerfile
└─mall-biz-service-1.0-SNAPSHOT.jar
mall-gateway/
├─Dockerfile
└─mall-gateway-1.0-SNAPSHOT.jar
```

并将 [EMall 前端项目](https://github.com/xixibuxixi2005/E-Mall-frontend) 编译后的`dist`文件夹放入`mall-frontend`中

```text
mall-frontend/
├─dist/
├─Dockerfile
└─nginx.conf
```

编写`emall.env`存放到当前项目中，设置对应的环境变量

```
MYSQL_NAME=数据库用户名
MYSQL_PSWD=数据库密码
DS_KEY=Deepseek大模型密钥
SF_KEY=硅基流动embedding模型密钥
EMALL_MAIL_USERNAME=验证码发件邮箱
EMALL_MAIL_PASSWORD=验证码发件邮箱密钥
MINIO_ACCESS_KEY=MinIO访问密钥
MINIO_SECRET_KEY=MinIO密码
```

最后在根目录运行

```bash
docker compose up -d
```

即可自动下载依赖并启动E-Mall项目，完成部署

（部署后会在当前目录下生成`volumes`文件夹，为Milvus与MinIO的实际文件存放位置，若需要迁移项目需要先删除容器并将`volumes`文件夹移到迁移目录下）