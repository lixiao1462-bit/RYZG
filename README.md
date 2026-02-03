# 人员在岗监测系统

基于 AI 视觉识别技术的生产级人员在岗监测系统，支持多路视频流实时分析、人员位置追踪、岗位识别和智能告警。

## 项目简介

- **后端技术栈**: Python 3.10+, FastAPI, PostgreSQL, Redis, InfluxDB
- **前端技术栈**: Vue 3, TypeScript, OpenLayers, Element Plus
- **AI 推理**: YOLOv8, DeepSORT, TensorRT
- **部署方式**: Docker + Docker Compose

## 核心功能

### 1. 实时监控中心
- 实时 2D 地图展示 (OpenLayers)
- 人员点位与轨迹追踪
- 在岗统计与缺岗列表
- 实时告警推送

### 2. 地图管理
- 地图上传与删除
- 地图比例尺设置
- 地图零点设置
- 多地图管理

### 3. 视频监控资源管理
- 视频资源区域列表 (从API获取)
- 视频监控资源点位 (从API获取)
- 海康/大华/宇视视频API集成

### 4. 告警管理
- 告警逻辑设置
- 告警列表与处理
- 告警统计与分析
- 钉钉/短信多渠道通知

### 5. AI模型管理
- AI模型列表与上传
- AI模型配置
- AI模型测试
- 模型激活切换

### 6. 电子围栏管理
- 电子围栏列表
- 添加/修改/删除围栏
- 电子围栏配置
- 电子围栏测试

### 7. 用户与权限管理
- 用户列表与CRUD
- 角色管理
- 权限管理

### 8. 数据字典管理
- 数据字典列表
- 添加/修改/删除字典

### 9. 日志管理
- 操作日志
- 登录日志

### 10. 系统设置
- 系统参数配置

## 技术架构

```
┌─────────────────────────────────────────────────────────┐
│                     前端 (Vue 3)                      │
│              OpenLayers + Element Plus                 │
└────────────────────┬────────────────────────────────────┘
                     │ WebSocket + HTTP
┌────────────────────┴────────────────────────────────────┐
│              Nginx 反向代理                           │
└────────────────────┬────────────────────────────────────┘
                     │
┌────────────────────┴────────────────────────────────────┐
│              FastAPI 后端                              │
│  ┌─────────────┬─────────────┬─────────────────────┐  │
│  │  认证授权   │  业务逻辑   │  WebSocket推送      │  │
│  └─────────────┴─────────────┴─────────────────────┘  │
│  ┌─────────────┬─────────────┬─────────────────────┐  │
│  │  视频接入   │  AI推理     │  告警通知          │  │
│  └─────────────┴─────────────┴─────────────────────┘  │
└────────────────────┬────────────────────────────────────┘
                     │
┌────────────────────┴────────────────────────────────────┐
│  PostgreSQL  │  Redis  │  InfluxDB  │  文件存储     │
└───────────────────────────────────────────────────────────┘
```

## 快速开始

### 前置要求

- Docker 20.10+
- Docker Compose 2.0+
- NVIDIA GPU (推荐，用于AI推理)

### 环境配置

1. 复制环境变量配置文件:
```bash
cp config/.env.example config/.env
```

2. 编辑 `config/.env` 文件，填入实际配置

### 启动服务

```bash
# 启动所有服务
docker-compose up -d

# 查看服务状态
docker-compose ps

# 查看日志
docker-compose logs -f backend
```

### 访问系统

- 前端地址: http://localhost
- API 文档: http://localhost:8000/docs
- 默认账号: admin / admin123

## 项目结构

```
personnel-monitoring-system/
├── services/              # 后端服务
│   ├── app/              # FastAPI 应用
│   │   ├── api/         # API 路由
│   │   ├── core/        # 核心配置
│   │   ├── models/      # 数据库模型
│   │   ├── schemas/     # Pydantic Schemas
│   │   ├── services/    # 业务服务
│   │   ├── websocket/   # WebSocket
│   │   └── main.py      # 应用入口
│   ├── requirements.txt
│   └── Dockerfile
├── frontend/             # 前端应用
│   ├── src/
│   │   ├── api/        # API 请求
│   │   ├── components/ # 组件
│   │   ├── layouts/    # 布局
│   │   ├── pages/      # 页面
│   │   ├── router/     # 路由
│   │   ├── store/      # 状态管理
│   │   └── main.ts
│   ├── package.json
│   └── vite.config.ts
├── docker/              # Docker 配置
│   ├── docker-compose.yml
│   └── nginx/
├── config/              # 配置文件
├── models/              # AI 模型文件
├── logs/                # 日志文件
├── uploads/             # 上传文件
└── README.md
```

## 开发指南

### 后端开发

```bash
cd services

# 安装依赖
pip install -r requirements.txt

# 启动开发服务器
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

### 前端开发

```bash
cd frontend

# 安装依赖
npm install

# 启动开发服务器
npm run dev
```

## 部署说明

详细部署文档请参考 [部署指南](docs/DEPLOYMENT.md)

## 许可证

MIT License

## 联系方式

如有问题或建议，请提交 Issue 或 Pull Request。
