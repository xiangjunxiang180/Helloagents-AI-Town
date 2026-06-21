# 🏙️ 赛博小镇（Helloagents-AI-Town）

> 基于 **HelloAgents** 框架的 AI 智能体小镇 — Agent × 游戏引擎的碰撞

<p align="center">
  <img src="https://img.shields.io/badge/Godot-4.7-blue?logo=godotengine" alt="Godot 4.7">
  <img src="https://img.shields.io/badge/Python-3.10+-green?logo=python" alt="Python 3.10+">
  <img src="https://img.shields.io/badge/FastAPI-0.x-teal?logo=fastapi" alt="FastAPI">
  <img src="https://img.shields.io/badge/HelloAgents-0.2.9-orange" alt="HelloAgents">
  <img src="https://img.shields.io/badge/license-CC%20BY--NC--SA%204.0-lightgrey" alt="License">
</p>

---

## 🎮 项目简介

赛博小镇是 **[《Hello-Agents》](https://github.com/datawhalechina/hello-agents)** 教材**第 15 章**的配套案例，展示如何将 **AI Agent** 与 **2D 游戏引擎**结合，打造一个有智能 NPC、记忆系统和好感度机制的虚拟办公室。

你在一个像素风办公室里，可以和 3 个 AI 同事自由对话 — 他们会记住你说过的话，对你的态度也会随着互动而改变。

---

## ✨ 六大核心系统

| 系统 | 说明 |
|------|------|
| 🗣️ **智能 NPC 对话** | 用自然语言与 NPC 自由对话，AI 根据角色设定个性化回应 |
| 🧠 **记忆系统** | 短期工作记忆维持对话连贯性 + 长期情景记忆存储互动历史 |
| 💖 **好感度系统** | 5 个等级（陌生→熟悉→友善→亲密→挚友），影响 NPC 行为 |
| 🎨 **游戏化交互** | Godot 4.7 引擎打造的 2D 像素办公室，WASD 移动探索 |
| 📊 **实时日志** | 所有对话和互动被完整记录，支持调试分析 |
| 🧩 **模块化架构** | 轻松添加新 NPC、新场景和新功能 |

---

## 🤖 三个 AI 同事

| NPC | 职位 | 位置 | 性格特点 |
|-----|------|------|----------|
| **张三** | Python 工程师 | 🖥️ 工位区 | 技术宅，喜欢讨论算法和框架，偶尔吐槽 Bug |
| **李四** | 产品经理 | 📋 会议室 | 外向健谈，善于沟通协调，喜欢用比喻 |
| **王五** | UI 设计师 | ☕ 休息区 | 细腻敏感，注重美感，追求像素级完美 |

---

## 🏗️ 技术架构

```
┌─────────────────────────────────────────────┐
│              前端层 · Godot 4.7               │
│      2D 渲染 · 玩家控制 · 对话 UI · 场景管理    │
├─────────────────────────────────────────────┤
│              API 层 · FastAPI                │
│       REST 路由 · NPC 状态 · 日志 · CORS       │
├─────────────────────────────────────────────┤
│          智能体层 · HelloAgents 框架           │
│    SimpleAgent · 记忆管理 · 好感度计算 · LLM    │
├─────────────────────────────────────────────┤
│       服务层 · LLM API + SQLite + Embedding   │
│    DashScope/OpenAI · 向量存储 · 持久化数据     │
└─────────────────────────────────────────────┘
```

---

## 🚀 快速开始

### 1. 环境要求

- **Godot** 4.2+（推荐 4.7）
- **Python** 3.10+
- **Git**（可选）

### 2. 启动后端

```bash
cd backend

# 创建 Python 3.10+ 虚拟环境
py -3.10 -m venv venv
venv\Scripts\activate       # Windows
# source venv/bin/activate  # macOS/Linux

# 安装依赖
pip install -r requirements.txt
pip install huggingface_hub sentence-transformers

# 配置 API Key
cp .env.example .env
# 编辑 .env，填入你的 LLM API Key（支持阿里百炼/OpenAI/DeepSeek 等）

# 启动后端
python main.py
```

后端默认运行在 `http://localhost:8000`，访问 `/docs` 查看 API 文档。

### 3. 启动前端

1. 打开 Godot 4.x 项目管理器
2. 点击「导入」→ 浏览到 `helloagents-ai-town/` 文件夹
3. 选择 `project.godot` → 「导入并编辑」
4. 按 **F5** 运行游戏

### 4. 游戏操作

| 按键 | 功能 |
|------|------|
| **W A S D** | 移动 |
| **E** | 与 NPC 对话 |
| **Enter** | 发送消息 |
| **ESC** | 关闭对话框 / 退出游戏 |

---

## ⚙️ LLM 配置

`.env` 支持多种 LLM 服务：

```env
# 阿里百炼 (通义千问) — 推荐
LLM_BASE_URL=https://dashscope.aliyuncs.com/compatible-mode/v1
LLM_MODEL_ID=qwen-plus
LLM_API_KEY=sk-your-key-here

# OpenAI
# LLM_BASE_URL=https://api.openai.com/v1
# LLM_MODEL_ID=gpt-4

# DeepSeek
# LLM_BASE_URL=https://api.deepseek.com/v1
# LLM_MODEL_ID=deepseek-chat
```

---

## 📁 项目结构

```
Helloagents-AI-Town/
├── README.md
├── SETUP_GUIDE.md              # 详细安装指南
├── AFFINITY_SYSTEM_GUIDE.md    # 好感度系统文档
├── DIALOGUE_LOG_GUIDE.md       # 对话日志文档
├── MEMORY_SYSTEM_GUIDE.md      # 记忆系统文档
│
├── backend/                    # FastAPI 后端
│   ├── main.py                 # API 主入口 + 路由
│   ├── agents.py               # NPC Agent 系统
│   ├── models.py               # Pydantic 数据模型
│   ├── config.py               # 配置管理
│   ├── relationship_manager.py # 好感度管理器
│   ├── state_manager.py        # NPC 状态定时更新
│   ├── batch_generator.py      # 批量对话生成
│   ├── logger.py               # 日志系统
│   ├── view_logs.py            # 日志查看工具
│   ├── requirements.txt        # Python 依赖
│   └── memory_data/            # NPC 记忆数据库
│
└── helloagents-ai-town/        # Godot 前端项目
    ├── project.godot           # 项目配置
    ├── scenes/                 # 场景文件 (.tscn)
    ├── scripts/                # GDScript 脚本
    └── assets/                 # 游戏资源
        ├── characters/         # 角色精灵
        ├── interiors/          # 场景地图
        ├── audio/              # BGM + 音效
        └── ui/                 # UI 素材
```

---

## 🔧 常见问题

| 问题 | 解决方案 |
|------|----------|
| `hello-agents` 安装失败 | 需要 Python >= 3.10，用 `py -3.10 -m venv venv` 创建虚拟环境 |
| `requirements.txt` GBK 错误 | 运行前设置 `PYTHONUTF8=1` 环境变量 |
| API 连接失败 | 检查代理设置（`HTTP_PROXY`/`HTTPS_PROXY` 环境变量） |
| Qdrant 连接超时 | 已在 agents.py 中禁用情景记忆（`enable_episodic=False`） |
| 游戏窗口退不出 | 已修复：按 ESC 退出，或点击窗口 ❌ 按钮 |
| Godot 导入报 UID 错误 | 删除 `.godot/` 和 `*.uid` 文件后重新导入 |

---

## 📖 参考资料

- [Hello-Agents 教程](https://github.com/datawhalechina/hello-agents)
- [Hello-Agents 在线文档](https://datawhalechina.github.io/hello-agents/)
- [Godot 官方文档](https://docs.godotengine.org/)
- [FastAPI 文档](https://fastapi.tiangolo.com/)

---

## 📄 许可证

本项目是 [Hello-Agents](https://github.com/datawhalechina/hello-agents) 的配套案例，采用 **CC BY-NC-SA 4.0** 许可证。
