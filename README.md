# Research Agent - 学术论文研究智能助手

<div align="center">

  ![Version](https://img.shields.io/badge/version-1.0.0-blue)
  ![Python](https://img.shields.io/badge/python-3.11+-green)
  ![Vue](https://img.shields.io/badge/vue-3.5+-brightgreen)
  ![License](https://img.shields.io/badge/license-MIT-orange)

  **一个基于AI的智能学术论文助手，帮助您搜索、理解和整理学术研究**

  [功能特性](#功能特性) · [快速开始](#快速开始) · [项目架构](#项目架构) · [API文档](#api文档) · [贡献指南](#贡献指南)

</div>

---

## 项目简介

Research Agent 是一个功能完整的智能学术论文助手应用，结合了前沿的大语言模型技术和专业的论文搜索工具。用户可以通过自然语言对话的方式，快速搜索arXiv上的学术论文，获取论文摘要、核心观点和研究方法。

### 核心能力

- **智能对话** - 基于DeepSeek大模型的自然语言交互
- **论文搜索** - 集成arXiv API，实时搜索最新学术论文
- **流式响应** - 实时流式输出，提供流畅的对话体验
- **会话管理** - 支持多会话管理，保存对话历史
- **工具调用** - 智能体可自主调用外部工具完成复杂任务

---

## 功能特性

### 用户端功能

| 功能 | 描述 |
|------|------|
| 智能对话 | 支持多轮对话，保持上下文连续性 |
| 流式输出 | 实时显示AI回复，提升用户体验 |
| 会话管理 | 创建、编辑、删除对话会话 |
| 响应式设计 | 完美适配桌面和移动端设备 |
| Markdown渲染 | 支持代码高亮和格式化文本 |

### 智能体能力

- **arXiv论文搜索** - 自动调用arXiv工具搜索相关论文
- **论文摘要生成** - 提取论文核心内容和创新点
- **研究建议** - 基于搜索结果给出研究建议
- **上下文记忆** - 记住对话历史，支持连续对话

---

## 项目架构

### 技术栈

#### 后端技术
- **框架**: FastAPI - 现代高性能Python Web框架
- **ORM**: SQLAlchemy - 强大的Python SQL工具包
- **数据库**: SQLite - 轻量级关系型数据库
- **AI引擎**:
  - LangChain - AI应用开发框架
  - LangChain-DeepSeek - DeepSeek模型集成
  - LangChain-arXiv - arXiv工具集成
- **API**: OpenAI API兼容接口

#### 前端技术
- **框架**: Vue 3 + TypeScript
- **UI库**: Element Plus
- **状态管理**: Pinia
- **HTTP客户端**: Axios
- **构建工具**: Vite

### 系统架构图

```
┌─────────────────────────────────────────────────────────────┐
│                         用户界面                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │ 会话列表面板  │  │  聊天面板    │  │  消息输入框  │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                      Vue 3 前端应用                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   组件层     │  │  状态管理    │  │   API层      │      │
│  │ Components   │  │   Pinia      │  │   Axios      │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                       FastAPI 后端                           │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      │
│  │   API层      │  │  服务层      │  │   数据层     │      │
│  │   api.py     │  │ services.py  │  │ crud/models  │      │
│  └──────────────┘  └──────────────┘  └──────────────┘      │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                        外部服务                              │
│  ┌──────────────┐              ┌──────────────┐            │
│  │ DeepSeek API │              │  arXiv API   │            │
│  │   大语言模型  │              │  论文搜索    │            │
│  └──────────────┘              └──────────────┘            │
└─────────────────────────────────────────────────────────────┘
```

### 目录结构

```
research_agent/
├── backend/                          # 后端服务目录
│   ├── app/
│   │   ├── __init__.py
│   │   ├── main.py                  # FastAPI应用主入口
│   │   ├── config.py                # 配置管理
│   │   ├── database.py              # 数据库连接配置
│   │   ├── models.py                # SQLAlchemy数据模型
│   │   ├── schemas.py               # Pydantic数据模式
│   │   ├── crud.py                  # 数据库CRUD操作
│   │   ├── services.py              # 业务逻辑服务层
│   │   └── api.py                   # API路由定义
│   ├── requirements.txt             # Python依赖包
│   ├── pyproject.toml               # 项目配置
│   └── research_agent.db            # SQLite数据库文件
│
├── frontend/                         # 前端应用目录
│   ├── src/
│   │   ├── api/                     # API接口封装
│   │   │   └── chat.ts              # 聊天相关API
│   │   ├── components/              # Vue组件
│   │   │   ├── ChatPanel.vue        # 主聊天面板
│   │   │   ├── DeleteModal.vue      # 删除确认模态框
│   │   │   ├── EditTitleModal.vue   # 编辑标题模态框
│   │   │   ├── MessageInput.vue     # 消息输入组件
│   │   │   ├── MessagesList.vue     # 消息列表组件
│   │   │   ├── SessionHeader.vue    # 会话头部组件
│   │   │   ├── SessionInfo.vue      # 会话信息组件
│   │   │   └── SessionsPanel.vue    # 会话列表面板
│   │   ├── stores/                  # Pinia状态管理
│   │   │   └── chat.ts              # 聊天状态管理
│   │   ├── types/                   # TypeScript类型定义
│   │   │   └── chat.ts              # 聊天相关类型
│   │   ├── App.vue                  # 根组件
│   │   ├── main.ts                  # 应用入口
│   │   └── style.css                # 全局样式
│   ├── package.json                 # Node.js依赖配置
│   └── vite.config.ts               # Vite构建配置
│
├── .gitignore                        # Git忽略配置
├── README.md                         # 项目说明文档
└── 快速安装.md                        # 快速安装指南
```

---

## 核心模块说明

### 后端模块

#### 1. API层 ([backend/app/api.py](backend/app/api.py))
定义所有HTTP接口路由，包括：
- `POST /api/sessions` - 创建新会话
- `GET /api/sessions` - 获取所有会话
- `GET /api/sessions/{session_id}` - 获取指定会话
- `PUT /api/sessions/{session_id}` - 更新会话标题
- `DELETE /api/sessions/{session_id}` - 删除会话
- `POST /api/sessions/{session_id}/messages` - 发送消息（支持流式/非流式）

#### 2. 服务层 ([backend/app/services.py](backend/app/services.py))
包含核心业务逻辑：

**ResearchAgentService**
- 初始化DeepSeek大语言模型
- 配置arXiv工具
- 处理用户消息并生成AI回复
- 支持流式和非流式两种响应模式
- 管理对话上下文

#### 3. 数据层
- **models.py** - 定义数据表结构（ChatSession、ChatMessage）
- **schemas.py** - 定义API请求/响应数据模式
- **crud.py** - 数据库CRUD操作封装
- **database.py** - 数据库连接和会话管理

#### 4. 配置管理 ([backend/app/config.py](backend/app/config.py))
使用Pydantic Settings管理配置：
- DeepSeek API密钥和模型配置
- 数据库连接URL
- 服务器运行参数
- Agent参数（温度、最大Token数）

### 前端模块

#### 1. 组件层 ([frontend/src/components/](frontend/src/components/))
- **ChatPanel.vue** - 主聊天界面容器
- **SessionsPanel.vue** - 会话列表侧边栏
- **MessagesList.vue** - 消息展示列表
- **MessageInput.vue** - 消息输入和发送
- **SessionHeader.vue** - 会话头部操作栏
- **SessionInfo.vue** - 会话信息显示
- **EditTitleModal.vue** - 标题编辑弹窗
- **DeleteModal.vue** - 删除确认弹窗

#### 2. 状态管理 ([frontend/src/stores/chat.ts](frontend/src/stores/chat.ts))
使用Pinia管理应用状态：
- 当前会话ID
- 会话列表
- 消息列表
- 流式响应处理
- API连接状态

#### 3. API层 ([frontend/src/api/chat.ts](frontend/src/api/chat.ts))
封装后端API调用：
- 会话管理接口
- 消息发送接口（支持SSE流式响应）

---

## 快速开始

### 环境要求

- **Python**: 3.11+
- **Node.js**: 18+
- **npm**: 9+

### 安装步骤

#### 1. 克隆项目

```bash
git clone https://github.com/OACHNIB/research_agent.git
cd research_agent
```

#### 2. 配置环境变量

在 `backend` 目录下创建 `.env` 文件：

```env
# DeepSeek API配置
DEEPSEEK_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxx
DEEPSEEK_MODEL=deepseek-chat
DEEPSEEK_BASE_URL=https://api.deepseek.com

# 数据库配置
DATABASE_URL=sqlite:///./research_agent.db

# 服务器配置
HOST=0.0.0.0
PORT=8000
DEBUG=true

# Agent配置
AGENT_TEMPERATURE=0.1
AGENT_MAX_TOKENS=2000
```

> 获取DeepSeek API密钥：https://platform.deepseek.com/

#### 3. 启动后端服务

```bash
# 创建Python虚拟环境（推荐）
conda create -n research-agent python=3.11
conda activate research-agent

# 安装依赖
cd backend
pip install -r requirements.txt

# 启动服务
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

后端服务将在 `http://localhost:8000` 启动

#### 4. 启动前端服务

```bash
# 新开一个终端窗口
# 安装依赖
cd frontend
npm install

# 启动开发服务器
npm run dev
```

前端应用将在 `http://localhost:3000` 启动

#### 5. 访问应用

在浏览器中打开 `http://localhost:3000` 即可开始使用

---

## API文档

启动后端服务后，访问以下地址查看完整API文档：

- **Swagger UI**: `http://localhost:8000/docs`
- **ReDoc**: `http://localhost:8000/redoc`

### 主要API端点

| 方法 | 端点 | 描述 |
|------|------|------|
| POST | `/api/sessions` | 创建新会话 |
| GET | `/api/sessions` | 获取所有会话 |
| GET | `/api/sessions/{session_id}` | 获取指定会话详情 |
| PUT | `/api/sessions/{session_id}` | 更新会话标题 |
| DELETE | `/api/sessions/{session_id}` | 删除会话 |
| POST | `/api/sessions/{session_id}/messages` | 发送消息（支持流式响应） |

---

## 配置说明

### Agent配置项

在 `.env` 文件中可配置以下参数：

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `DEEPSEEK_API_KEY` | DeepSeek API密钥 | - |
| `DEEPSEEK_MODEL` | 使用的模型名称 | `deepseek-chat` |
| `DEEPSEEK_BASE_URL` | API基础URL | `https://api.deepseek.com` |
| `AGENT_TEMPERATURE` | 生成随机性（0-1） | `0.1` |
| `AGENT_MAX_TOKENS` | 最大生成Token数 | `2000` |

### 数据库配置

默认使用SQLite数据库，数据库文件位于 `backend/research_agent.db`

---

## 开发指南

### 后端开发

```bash
cd backend

# 安装开发依赖
pip install -r requirements.txt

# 运行测试（如果有）
pytest

# 代码格式化
black app/
isort app/
```

### 前端开发

```bash
cd frontend

# 安装依赖
npm install

# 开发模式
npm run dev

# 构建生产版本
npm run build

# 预览生产构建
npm run preview
```

---

## 常见问题

### Q1: 如何获取DeepSeek API密钥？
访问 [DeepSeek开放平台](https://platform.deepseek.com/) 注册并创建API密钥。

### Q2: 支持其他大模型吗？
目前支持任何OpenAI API兼容的模型，只需修改 `.env` 中的 `DEEPSEEK_BASE_URL` 和 `DEEPSEEK_API_KEY`。

### Q3: 如何更换数据库？
修改 `.env` 中的 `DATABASE_URL`，支持PostgreSQL、MySQL等其他数据库。

### Q4: 流式响应不工作怎么办？
确保后端和前端都正确配置了CORS，检查防火墙设置。

---

## 贡献指南

欢迎贡献代码！请遵循以下步骤：

1. Fork本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启Pull Request

### 代码规范

- **Python**: 遵循PEP 8规范
- **TypeScript**: 使用ESLint和Prettier格式化
- **提交信息**: 使用Conventional Commits规范

---

## 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

---

## 致谢

本项目使用了以下优秀的开源项目：

- [FastAPI](https://fastapi.tiangolo.com/) - 现代化的Python Web框架
- [Vue.js](https://vuejs.org/) - 渐进式JavaScript框架
- [LangChain](https://langchain.com/) - AI应用开发框架
- [Element Plus](https://element-plus.org/) - Vue 3 UI组件库
- [DeepSeek](https://www.deepseek.com/) - 大语言模型API
- [arXiv](https://arxiv.org/) - 学术论文预印本库

---

## 联系方式

- GitHub: [OACHNIB/research_agent](https://github.com/OACHNIB/research_agent)
- Issues: [提交问题](https://github.com/OACHNIB/research_agent/issues)

---

<div align="center">

  **如果这个项目对您有帮助，请给一个 Star ⭐**

  Made with ❤️ by OACHNIB

</div>
