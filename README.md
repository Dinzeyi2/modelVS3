Secure your agents at: CodeAstra.dev

## AI Agent Privacy Notice

Astra Sentinel found a possible pattern where sensitive user, customer, or patient data may be passed directly into an AI agent or LLM context.

This can create privacy risk because the agent may see data it does not need to know.

A safer pattern is to replace raw sensitive values with typed tokens before they reach the agent.

Example:

Before: Book appointment for John Smith, DOB 04/12/1988
After: Book appointment for [CVT:NAME:patient_name], DOB [CVT:DOB:patient_dob]

The agent can still perform the workflow, but it never sees the raw sensitive data.

Detected pattern examples:
```json
[
  {
    "pattern": "unprotected_ai_context",
    "evidence": "relationship('run', back_populates='model')"
  }
]
```

This notice was generated from a privacy scan. Please review before merging.

Secure your agents at: CodeAstra.dev

---

# 🤖 ModelVS3 - 自建 Agent 平台
<img width="1716" height="1008" alt="截屏2025-08-11 13 44 48" src="https://github.com/user-attachments/assets/1d0c894b-9cd3-4714-a74d-b9869ca71507" />
<img width="1935" height="1259" alt="截屏2025-08-11 13 47 15" src="https://github.com/user-attachments/assets/880af43c-e070-45a1-a926-b8eb9976b0c9" />
<img width="1912" height="1254" alt="截屏2025-08-11 13 48 33" src="https://github.com/user-attachments/assets/67051d73-d57d-4ff5-9962-fad2648f8c34" />
<img width="1937" height="1257" alt="截屏2025-08-11 13 48 51" src="https://github.com/user-attachments/assets/b0d4dd9c-3303-4a18-9f8e-9817321caa12" />
<img width="1913" height="1262" alt="截屏2025-08-11 13 49 50" src="https://github.com/user-attachments/assets/80ecb3ad-5e4b-430d-99c8-5dc76b3aee31" />
<img width="1932" height="1144" alt="截屏2025-08-11 13 50 25" src="https://github.com/user-attachments/assets/a8fef38e-77e6-40c1-8409-5682dc318ebb" />

> 现代化的多模型 Agent 平台，支持 OpenAI、Anthropic、Google Gemini 等 LLM

## ✨ 核心特性

- 🔄 **多模型接入** - 统一 `/v1/chat/completions` 接口转发到各大 LLM
- 🛠️ **Agent 管理** - YAML/JSON Schema 配置，支持 REACT/FSM/Graph 策略
- 🔧 **工具调用** - OpenAI Function Calling 1.5 规范
- 🧠 **记忆系统** - Redis 短期 + pgvector 长期向量记忆
- 🔒 **安全合规** - JWT/OAuth2、RBAC、速率限制、成本护栏
- 📊 **可观测性** - Prometheus/Grafana 指标监控
- ⚡ **操练场** - 支持同时测试多个模型的对比效果 🆕

## 🆕 操练场


### 功能特色
- **Agent配置展示**：在顶部显示选中Agent的详细信息，支持折叠展开
- **多模型选择**：可以从系统中已配置的模型中选择多个进行对比测试
- **并发执行**：同一条消息同时发送给所有选中的模型，实时对比响应
- **性能指标**：显示每个模型的执行时间、Token使用量、成本估算
- **交互功能**：
  - 对话框折叠/展开
  - 拖拽调整位置
  - 删除不需要的模型
  - 响应质量评分
- **响应式布局**：支持网格和列表视图，自适应不同屏幕尺寸
- **搜索筛选**：按模型名称搜索，按状态筛选

### 使用流程
1. 访问 `/multi-model-workspace` 页面
2. 选择要测试的Agent配置
3. 添加多个模型到对比列表
4. 输入测试消息，点击发送
5. 实时查看各模型的响应结果和性能对比
6. 对响应质量进行评分和记录

### 界面布局
```
┌─────────────────────────────────────────┐
│ 顶部工具栏：Agent选择 + 搜索筛选          │
├─────────────────────────────────────────┤
│ Agent信息区：配置详情展示(可折叠)         │
├─────────────────────────────────────────┤
│ 模型选择区：已选模型 + 添加更多           │
├─────────────────────────────────────────┤
│ 主工作区：                               │
│ ┌─────────┐ ┌─────────┐ ┌─────────┐     │
│ │ GPT-4   │ │Claude-3 │ │Gemini   │     │
│ │ 对话内容 │ │ 对话内容 │ │ 对话内容 │     │
│ │ 性能指标 │ │ 性能指标 │ │ 性能指标 │     │
│ └─────────┘ └─────────┘ └─────────┘     │
├─────────────────────────────────────────┤
│ 底部输入区：消息输入 + 发送按钮           │
└─────────────────────────────────────────┘
```

### 技术特点
- **纯前端实现**：无需修改后端数据结构
- **临时测试**：对话数据不持久化，专注于对比测试
- **实时并发**：使用Promise.allSettled并发调用多个模型
- **用户体验**：流畅的动画、直观的状态指示、响应式设计
- **拖拽排序**：支持拖拽调整模型对话框的位置和顺序 🆕

## 🏗️ 架构图

```
Client ──► API Gateway ──► Router & Adapter ──► Provider LLM
               ▲                ▲
               │                │
               └─► Agent Service ──► Tool Registry / 内外部 API
```

## 🚀 快速开始

### 🚀 一键安装（推荐）

```bash
# 克隆项目
git clone https://github.com/your-org/modelVS3.git
cd modelVS3

# 运行安装脚本（自动设置环境）
chmod +x scripts/dev_setup.sh
./scripts/dev_setup.sh

# 给脚本执行权限
chmod +x scripts/start.sh

# 启动所有服务
./scripts/start.sh
```

### 🔑 默认账户

- **管理员**: admin@example.com / admin123
- **演示用户**: demo@example.com / demo123

### 💻 CLI 工具

```bash
# 查看帮助
python3 cli.py --help

# 健康检查
python3 cli.py health

# 管理 Agent
python3 cli.py agent list
python3 cli.py agent create "助手" "你是一个有用的助手"

# 管理模型和工具
python3 cli.py model list
python3 cli.py tool list

# 部署管理
python3 cli.py deploy docker
python3 cli.py deploy status

# 数据库管理
python3 cli.py db init
python3 cli.py db seed
```

### 手动启动

#### 开发环境

```bash
# 1. 安装 Python 依赖
pip install -r requirements.txt

# 2. 启动数据库服务
docker-compose up -d postgres redis

# 3. 运行数据库迁移
alembic upgrade head

# 4. 启动后端服务
python -m src.main

# 5. 启动前端（另一个终端）
cd frontend && npm install && npm run dev
```

#### 生产部署

```bash
# 构建并启动所有服务
docker-compose up --build -d

# 查看服务状态
docker-compose ps

# 查看日志
docker-compose logs -f
```

## 📖 使用示例

### 创建 Agent

```python
import requests

# 创建财务分析师 Agent
agent_config = {
    "name": "财务分析师",
    "description": "专业的财务数据分析和报告生成 Agent",
    "schema": {
        "version": "2025-07",
        "model": "gpt-4",
        "strategy": "react",
        "system_prompt": "你是一位资深的财务分析师...",
        "tools": [
            {"name": "calculator", "required": True},
            {"name": "web_search", "required": False}
        ],
        "parameters": {
            "temperature": 0.3,
            "max_tokens": 2000
        }
    },
    "status": "active"
}

response = requests.post("http://localhost:8000/api/v1/agents/", json=agent_config)
agent = response.json()
```

### 执行 Agent

```python
# 发送消息给 Agent（新对话）
run_request = {
    "agent_id": agent["id"],
    "messages": [
        {
            "role": "user",
            "content": "请分析一下苹果公司最近的财务状况"
        }
    ],
    "stream": False
}

response = requests.post("http://localhost:8000/api/v1/runs/", json=run_request)
run = response.json()

# 继续对话（发送完整消息历史）
continue_request = {
    "agent_id": agent["id"],
    "messages": [
        # 包含之前的所有对话
        {
            "role": "user", 
            "content": "请分析一下苹果公司最近的财务状况"
        },
        {
            "role": "assistant",
            "content": "根据最新财报，苹果公司财务状况良好..."
        },
        # 新的用户消息
        {
            "role": "user",
            "content": "那么与去年同期相比如何？"
        }
    ],
    "stream": False
}

response = requests.post("http://localhost:8000/api/v1/runs/", json=continue_request)
continued_run = response.json()
```

### 流式执行

```python
import sseclient

# 流式执行 Agent
run_request["stream"] = True
response = requests.post("http://localhost:8000/api/v1/runs/", json=run_request, stream=True)

client = sseclient.SSEClient(response)
for event in client.events():
    if event.data != "[DONE]":
        data = json.loads(event.data)
        print(f"事件类型: {data['type']}")
        if data['type'] == 'llm_response':
            print(f"回复: {data['response']['content']}")
```

## 📖 API 文档

启动服务后访问：
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc
- **OpenAPI JSON**: http://localhost:8000/openapi.json

### cURL 调用示例

```bash
# 执行Agent
curl -X POST "http://localhost:8000/api/v1/runs" \
  -H "Content-Type: application/json" \
  -d '{
    "agent_id": "agent-uuid-here",
    "messages": [
      {
        "role": "user",
        "content": "你好，请帮我处理一个任务"
      }
    ],
    "stream": false,
    "temperature": 0.7,
    "max_tokens": 2000
  }'

# 获取执行结果
curl -X GET "http://localhost:8000/api/v1/runs/{run_id}"

# 获取执行消息历史
curl -X GET "http://localhost:8000/api/v1/runs/{run_id}/messages"
```

**响应示例**：
```json
{
  "id": "109ec3c6-ead4-42c3-a824-9cd63bb2449c",
  "agent_id": "agent-uuid-here",
  "model_id": null,
  "status": "completed",
  "input_tokens": 451,
  "output_tokens": 19,
  "execution_time_ms": 1024,
  "error_message": null,
  "created_at": "2025-07-24T06:07:58.277916Z",
  "completed_at": "2025-07-24T06:07:59.317559Z",
  "response": {
    "id": "c65fcc12-bf66-42e9-9f8c-922ced219916",
    "role": "assistant",
    "content": "你好！请告诉我你需要我帮你处理什么任务？我会尽我所能来帮助你。",
    "tool_calls": null,
    "tool_call_id": null,
    "created_at": "2025-07-24T06:07:58.300316Z"
  },
  "messages": []
}
```

> **对话管理说明**：
> - API 现在只返回 AI 的回复（`response` 字段），不再返回完整的消息历史
> - 前端负责维护完整的对话历史，继续对话时需发送完整的 `messages` 数组
> - `messages` 字段保留为空数组，用于向后兼容（已废弃）

## 🔧 配置说明

### 环境变量

复制 `.env.example` 为 `.env` 并配置：

```bash
# 基础配置
APP_NAME=ModelVS3 Agent Platform
DEBUG=true

# 数据库
DATABASE_URL=postgresql://postgres:password@localhost:5432/modelvs3
REDIS_URL=redis://localhost:6379/0

# LLM API Keys
OPENAI_API_KEY=your-openai-api-key
ANTHROPIC_API_KEY=your-anthropic-api-key
GOOGLE_API_KEY=your-google-api-key

# 速率限制
RATE_LIMIT_REQUESTS_PER_MINUTE=60

# 成本控制
DAILY_BUDGET_USD=100.0
```

### Agent 配置

Agent 使用 YAML 格式配置，示例：

```yaml
version: "2025-07"
name: "客服助手"
model: "claude-3-sonnet"
strategy: "react"
max_iterations: 4
timeout: 60

system_prompt: |
  你是一位专业的客服助手...

memory:
  type: "redis"
  window: 8

tools:
  - name: "knowledge_search"
    description: "搜索知识库"
    required: true

parameters:
  temperature: 0.7
  max_tokens: 1500
```

查看更多示例：`examples/agents/`

### 🐍 Python 客户端

```python
from src.utils.api_client import ModelVS3Client, create_simple_agent

async def main():
    async with ModelVS3Client("http://localhost:8000") as client:
        # 创建 Agent
        agent = await create_simple_agent(
            client=client,
            name="数学助手",
            system_prompt="你是一个数学专家",
            model="gpt-4",
            tools=["calculator"]
        )
        
        # 与 Agent 对话
        response = await client.run_agent(
            agent_id=agent['id'],
            messages=[{"role": "user", "content": "计算 25 * 36"}]
        )
        print(response)

# 运行示例
# python3 examples/usage_examples.py
```

### 🔧 工具开发

创建自定义工具：

```python
# src/core/tools/custom_tool.py
from typing import Dict, Any

async def my_custom_tool(parameters: Dict[str, Any]) -> Dict[str, Any]:
    """自定义工具实现"""
    return {
        "result": "处理完成",
        "data": parameters
    }

# 注册工具
TOOL_REGISTRY["my_custom_tool"] = {
    "function": my_custom_tool,
    "schema": {
        "type": "function",
        "function": {
            "name": "my_custom_tool",
            "description": "我的自定义工具",
            "parameters": {
                "type": "object",
                "properties": {
                    "input": {"type": "string", "description": "输入参数"}
                },
                "required": ["input"]
            }
        }
    }
}
```

## 📦 技术栈

- **后端**: FastAPI + SQLAlchemy + PostgreSQL + Redis
- **前端**: React + TypeScript + Tailwind CSS + Vite
- **监控**: Prometheus + Grafana + OpenTelemetry
- **部署**: Docker + Docker Compose

## 🏗️ 项目结构

```
modelVS3/
├── src/                          # 后端源码
│   ├── core/                     # 核心模块
│   │   ├── agent_executor.py     # Agent 执行引擎
│   │   ├── llm_adapters.py       # LLM 适配器
│   │   ├── tool_executor.py      # 工具执行器
│   │   └── memory.py             # 记忆管理器
│   ├── routers/                  # API 路由
│   ├── models.py                 # 数据库模型
│   ├── schemas.py                # Pydantic 模式
│   ├── config.py                 # 配置管理
│   └── main.py                   # 主应用
├── frontend/                     # 前端源码
│   ├── src/
│   │   ├── components/           # React 组件
│   │   ├── pages/                # 页面组件
│   │   └── App.tsx               # 主应用
│   ├── package.json
│   └── vite.config.ts
├── examples/                     # 示例配置
│   ├── agents/                   # Agent 配置示例
│   └── tools/                    # 工具配置示例
├── tests/                        # 测试文件
├── monitoring/                   # 监控配置
├── scripts/                      # 脚本文件
├── docker-compose.yml            # Docker 编排
├── requirements.txt              # Python 依赖
└── README.md                     # 项目文档
```

## 🤝 贡献指南

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 打开 Pull Request

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情

## 💬 支持

- 📧 邮箱: leslie89757@126.com
- 💬 微信: leslie89757

---

⭐ 如果这个项目对你有帮助，请给我们一个 Star！ 
