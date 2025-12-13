# iNotebook

一款支持自部署的个人知识写作应用，助你更高效地组织和管理笔记。

- iNotebook 在线沙盒体验：[https://inotebook-sandbox.vercel.app](https://inotebook-sandbox.vercel.app)
- iNotebook Docker Hub：[https://hub.docker.com/r/aidenzou/i-notebook](https://hub.docker.com/r/aidenzou/i-notebook)
- [更新日志](./CHANGELOG.md)

## 功能描述

- 块编辑
- 编辑保护
- 标题自动编号
- 空行提示
- 标题目录
- 收藏置顶
- 自动标签
- 密码锁定
- 笔记地图
- 访问单篇笔记
- 导出导入
- 打印笔记 或 导出 PDF
- ...

除此之外，基于笔记地图对接第三方产品，让数据高效流转，快速搭建本地个人知识库

## 部署

### 方式一：Volume + Docker

1.创建 volume：

```
docker volume create note_data
```

2.创建容器并关联 volume

```
docker run -d -it -v note_data:/appdata -e DATABASE_URL=file:/appdata/db/notebook.sqlite -e AUTH_UNLOCKCODE=pass --name i-notebook -p 4000:3000 aidenzou/i-notebook:latest
```

说明：使用 `note_data` volume，数据库文件地址为 `note_data/db/notebook.sqlite`，锁屏密码为 `pass`

### 方式二：Docker Compose

1.docker-compose.yaml：

```yarm
name: inotebook
services:
  note:
    image: aidenzou/i-notebook:0.9.0
    ports:
      - 4001:3000
    volumes:
      - ./notebook/data:/appdata
      - ./notebook/uploads:/app/uploads
    environment:
      DATABASE_URL: file:/appdata/database.sqlite
      AUTH_UNLOCKCODE: pass
      SITE_URL: http://localhost:4001
```

2.在后台启动并运行容器应用：

```shell
docker-compose up -d
```

### ENV

| 环境变量 | 描述 |
| ---- | ---- |
| DATABASE_URL | sqlite 文件地址 |
| AUTH_UNLOCKCODE | 解锁密码 |
| SITE_URL | 部署后服务访问地址 |

## 功能演示

![iNotebook](public/1.png)
![iNotebook](public/2.png)
![iNotebook](public/3.png)
![iNotebook](public/11.png)
![iNotebook](public/12.png)
