# 🎯 Event Hunter AI

<div align="center">
  <img src="event-hunter/src/assets/brightdata.svg" alt="Event Hunter AI" width="200"/>
  <p><em>由 AI 驱动的活动发现服务，帮助你寻找行业会议、黑客马拉松与社交机会</em></p>
  
  [![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/downloads/)
  [![FastAPI](https://img.shields.io/badge/FastAPI-0.116+-green.svg)](https://fastapi.tiangolo.com/)
  [![React](https://img.shields.io/badge/React-19.1+-61DAFB.svg)](https://reactjs.org/)
</div>

## 🌟 概览

Event Hunter AI 是一套先进的多智能体系统，利用 AI 来发现并分析行业活动。它结合了深度智能体、通过 BrightData 的 MCP（Model Context Protocol）实现的网页抓取能力，以及优雅的 React 前端，提供全面的活动情报。

### 🎯 它能做什么

- 智能活动发现：使用 AI 智能体搜索会议、黑客松、工作坊与行业活动
- 全面分析：提取包括日期、地点、征稿（CFP）状态与赞助机会在内的详细信息
- 多智能体架构：为搜索与深入分析配备专门的子智能体
- 实时流式：基于 WebSocket 的处理过程实时更新
- 现代化界面：简洁、响应式的 React 前端，表单式构建查询

## 🏗️ 架构

### 后端（Python + FastAPI）
系统基于 `deepagents` 框架实现多智能体架构：

1. 主活动猎手智能体：编排整个流程
2. 活动搜索子智能体：专注通过网络搜索发现活动
3. 活动详情子智能体：从活动页面提取全面信息

关键技术：
- DeepAgents：多智能体编排框架
- BrightData MCP：网页抓取与搜索引擎访问
- LangChain：LLM 集成与提示管理
- FastAPI：现代 Python Web 框架，支持 WebSocket
- Azure OpenAI：使用 GPT-4.1-mini 进行智能处理

### 前端（React + TypeScript）
现代、表单驱动的界面，技术栈包括：
- React 19.1 + TypeScript
- Tailwind CSS 样式
- Framer Motion 动画
- Radix UI 组件
- React Markdown 格式化结果展示

## 🚀 功能

### 🔍 智能活动搜索
- 多条件搜索（行业、地点、时间范围）
- 指定公司相关活动发现
- 高级筛选与定制需求

### 📊 全面活动分析
对每个发现的活动，系统会提取：
- 活动名称与官方链接
- 日期与时间
- 地点（城市、场馆、线上/混合）
- 关键信息与描述
- 征稿（CFP）状态
- 赞助机会

### 🎨 现代化用户界面
- 表单式查询构建：直观输入搜索条件
- 实时流式：AI 处理过程中的即时更新
- 响应式设计：桌面与移动端良好体验
- 深浅色模式支持
- 连接状态指示

### 🔄 实时处理
- WebSocket 流式：搜索与分析过程的实时更新
- 处理时间轴：透明呈现 AI 的决策过程
- 错误处理：稳健的失败管理与重试逻辑

## 📋 前置条件

设置 Event Hunter AI 前，你需要：

### 必需的 API
1. BrightData 账号：用于 MCP 网页抓取能力
   - 在 [BrightData](https://www.bright.cn) 注册
   - 在控制台获取 MCP 令牌
2. Azure OpenAI 访问：使用 GPT-4.1-mini 模型
   - 拥有 Azure 订阅与 OpenAI 服务
   - API Key 与 endpoint URL

### 开发环境
- Python 3.8+
- Node.js 18+ 与 npm/yarn
- Git 版本控制

## ⚡ 快速开始

### 1. 克隆仓库
```bash
git clone https://github.com/bright-cn/event-hunter.git
cd event-hunter
```

### 2. 后端设置

#### 安装 Python 依赖
```bash
pip install -r requirements.txt
```

#### 配置环境变量
```bash
cp .env.example .env
```

编辑 `.env` 并填入你的凭据：
```env
# BrightData MCP Configuration
BRIGHTDATA_API_TOKEN=your_brightdata_api_token_here

# Azure OpenAI Configuration  
OPENAI_API_KEY=your_azure_openai_api_key
OPENAI_BASE_URL=https://your-resource.openai.azure.com/openai/v1/
```

#### 启动后端服务器
```bash
python main.py
```

API 服务器将运行在 `http://localhost:8000`

### 3. 前端设置

#### 进入前端目录
```bash
cd event-hunter
```

#### 安装依赖
```bash
npm install
```

#### 启动开发服务器
```bash
npm run dev
```

前端将运行在 `http://localhost:5173`

## 📖 使用指南

### 使用网页界面

1. 打开应用：访问 `http://localhost:5173`
2. 填写搜索表单：
   - 地点：输入城市、国家，或输入 “Online” 以搜索线上活动
   - 日期范围：选择开始与结束日期
   - 行业垂直：从预设类别中选择（如 AI、金融科技等）
   - 公司（可选）：指定关注的公司
   - 其他需求（可选）：添加具体条件
3. 提交查询：点击 “Find Events” 开始 AI 驱动搜索
4. 查看结果：实时查看处理过程并获取完整的活动列表

### 直接使用 API

#### REST 接口
```bash
curl -X POST "http://localhost:8000/query" \
  -H "Content-Type: application/json" \
  -d '{"query": "Find AI hackathons in San Francisco for Q1 2025"}'
```

#### WebSocket 连接
```javascript
const ws = new WebSocket('ws://localhost:8000/ws/query');
ws.send(JSON.stringify({
  query: "Find blockchain conferences in Europe for 2025"
}));
```

## 🛠️ 开发

### 项目结构
```
event-hunter/
├── main.py                 # FastAPI backend server
├── requirements.txt        # Python dependencies
├── .env.example           # Environment variables template
├── .gitignore            # Git ignore rules
└── event-hunter/         # React frontend
    ├── src/
    │   ├── EventDiscoveryForm.tsx  # Main component
    │   ├── main.tsx               # App entry point
    │   ├── components/ui/         # UI components
    │   └── assets/               # Static assets
    ├── package.json              # Frontend dependencies
    └── vite.config.ts           # Vite configuration
```

### 后端开发

后端采用精心设计的多智能体架构：

```python
# Agent hierarchy
Main Event Hunter Agent
├── Event Search Sub-Agent    # Finds events using search engines
└── Event Details Sub-Agent   # Extracts detailed event information
```

关键组件：
- 智能体初始化：设置 MCP 工具与 LLM 连接
- WebSocket 处理：管理实时通信
- 流式响应：在处理过程中持续输出更新
- 错误处理：稳健的失败管理

### 前端开发

关键特性：
- 表单校验：实时输入校验
- WebSocket 集成：AI 响应的实时流式显示
- 响应式设计：移动优先
- 可访问性：符合 WCAG 的 UI 组件

#### 可用脚本
```bash
npm run dev      # Start development server
npm run build    # Build for production  
npm run preview  # Preview production build
npm run lint     # Run ESLint
```

## 🔧 配置

### 环境变量

| 变量 | 描述 | 必需 |
|------|------|------|
| `BRIGHTDATA_API_TOKEN` | BrightData API 访问令牌 | 是 |
| `OPENAI_API_KEY` | Azure OpenAI API Key | 是 |
| `OPENAI_BASE_URL` | Azure OpenAI endpoint URL | 是 |

### 模型配置

系统通过 Azure OpenAI 使用 **GPT-4.1-mini**。你可以在 `main.py` 中修改模型：

```python
model = init_chat_model(
    model="gpt-4.1-mini",        # Change model here
    model_provider="openai",
    api_key=openai_api_key,
    base_url=openai_base_url,
    default_query={"api-version": "preview"}
)
```

## 🔍 API 参考

### REST 接口

#### `GET /`
健康检查

#### `GET /health`  
包含智能体就绪状态的详细健康信息

#### `POST /query`
同步处理活动查询

请求体：
```json
{
  "query": "Find AI conferences in NYC for 2025"
}
```

响应：
```json
{
  "query": "Find AI conferences in NYC for 2025",
  "response": "**Event Name**: AI Summit NYC...",
  "status": "completed"
}
```

### WebSocket 接口

#### `WS /ws/query`
实时流式活动查询

消息类型：
- `start`：开始处理查询
- `stream`：增量输出内容
- `complete`：处理完成
- `error`：发生错误

## 🐛 故障排除

### 常见问题

后端问题

“Agent not initialized”
- 检查 `.env` 中的 API Key
- 验证 BrightData MCP 令牌有效
- 确保 Azure OpenAI endpoint 可访问

连接超时
- 检查网络连通性
- 确认防火墙允许外发 HTTPS
- 确认未触发 API 速率限制

前端问题

“WebSocket connection failed”
- 确保后端运行在 8000 端口
- 检查 CORS 配置
- 确认无代理/防火墙阻断 WebSocket

构建失败
- 清理并重装依赖：`rm -rf node_modules && npm install`
- 检查 Node.js 版本兼容
- 验证依赖是否正确安装

### 调试模式

在后端启用详细日志：

```python
import logging
logging.basicConfig(level=logging.DEBUG)
```

## 🤝 贡献

欢迎贡献！请遵循以下流程：

1. Fork 本仓库
2. 创建功能分支：`git checkout -b feature/amazing-feature`
3. 提交更改：`git commit -m 'Add amazing feature'`
4. 推送分支：`git push origin feature/amazing-feature`
5. 发起 Pull Request

### 开发规范

- 代码风格：Python 遵循 PEP 8，TypeScript 遵循 ESLint 规则
- 测试：为新功能添加测试
- 文档：更新 README 与代码注释
- 安全：不要提交任何 API Key 或敏感数据

## 📄 许可证

本项目基于 MIT 许可证开源，详见 [LICENSE](LICENSE)。

## 🙏 致谢

- [BrightData](https://www.bright.cn) 提供 MCP 网页抓取能力
- [DeepAgents](https://github.com/langchain-ai/deepagents) 提供多智能体框架
- [LangChain](https://langchain.com) 提供 LLM 编排
- [FastAPI](https://fastapi.tiangolo.com/) 提供强健的后端框架
- [React](https://reactjs.org/) 与 [Tailwind CSS](https://tailwindcss.com/) 提供现代化前端

## 📞 支持

如需支持或提问：

- Issues：[GitHub Issues](https://github.com/bright-cn/event-hunter/issues)
- 文档：请查阅本 README 与代码内联注释
- 社区：在仓库中参与讨论

---

<div align="center">
  <p><strong>使用 BrightData MCP、DeepAgents 与现代 Web 技术精心打造 ❤️</strong></p>
</div>
