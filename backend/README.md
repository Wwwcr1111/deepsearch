# HelloAgents Deep Research Backend

HelloAgents Deep Research 是一个本地深度研究助手后端，负责研究任务编排、检索、总结和报告生成。

## 环境要求

你可以通过以下命令检查版本：

```bash
python --version  # 应该显示 Python 3.10.x 或更高
node --version    # 应该显示 v16.x.x 或更高
npm --version     # 应该显示 8.x.x 或更高
```

## 启动后端

```bash
# 1. 进入后端目录
cd helloagents-deepresearch/backend

# 2. 安装依赖
# 方式1：使用 uv（推荐，更快的 Python 包管理器）
uv sync

# 方式2：使用 pip
pip install -e .

# 3. 配置环境变量
cp .env.example .env

# 4. 编辑 .env 文件，填入你的 API 密钥
# 后端启动时会自动加载 backend/.env
# 推荐使用 DeepSeek 风格的 OpenAI 兼容接口：
# - LLM_PROVIDER=custom
# - LLM_MODEL_ID=deepseek-chat
# - LLM_BASE_URL=https://api.deepseek.com/v1
# - LLM_API_KEY=<你的 DeepSeek API Key>
# - SEARCH_API（如 duckduckgo、tavily）

# 5. 启动后端
uv run python src/main.py
```

DeepSeek 示例配置：

```env
LLM_PROVIDER=custom
LLM_MODEL_ID=deepseek-chat
LLM_BASE_URL=https://api.deepseek.com/v1
LLM_API_KEY=your-deepseek-api-key
SEARCH_API=duckduckgo
```

如果你希望开启开发热重载，可以使用：

```bash
set RELOAD=true
uv run python src/main.py
```

如果一切正常，你会看到类似的输出：

```text
INFO:     Started server process [12345]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
```

## 常见问题

`401 Authentication Fails`

说明 `.env` 中的 `LLM_API_KEY` 无效，或者仍然是示例值。请确认它已经替换为真实的 DeepSeek API Key。

`model 'llama3.2' not found`

说明当前配置仍在走本地 Ollama 默认模型。请确认 `.env` 中已经设置：

```env
LLM_PROVIDER=custom
LLM_MODEL_ID=deepseek-chat
LLM_BASE_URL=https://api.deepseek.com/v1
```

`WinError 10048`

说明 `8000` 端口已经被其他进程占用。先关闭已有后端进程，再重新启动当前服务。

`TAVILY_API_KEY 未设置` / `SERPAPI_API_KEY 未设置`

这是提示，不是错误。未配置这些搜索源时，系统会回退到 `duckduckgo`。

## 启动前端

打开一个新的终端窗口：

```bash
# 1. 进入前端目录
cd helloagents-deepresearch/frontend

# 2. 安装依赖
npm install

# 3. 启动前端
npm run dev
```

如果一切正常，你会看到类似的输出：

```text
VITE v5.0.0  ready in 500 ms

➜  Local:   http://localhost:5174/
➜  Network: use --host to expose
➜  press h + enter to show help
```

## 开始研究

打开浏览器访问 `http://localhost:5174`，你会看到一个居中的输入卡片。输入研究主题，例如“Datawhale 是一个什么样的组织？”，选择搜索引擎（如果配置了多个），点击“开始研究”按钮。

系统会自动展开为全屏，左侧显示研究信息，右侧实时显示研究进度和结果。整个研究过程大约需要 1-3 分钟，取决于主题的复杂度和搜索引擎的响应速度。

研究完成后，你会看到：

- 任务列表：显示所有子任务及其状态
- 进度日志：显示研究过程中的所有操作
- 最终报告：结构化的 Markdown 报告，包含所有子任务的总结和来源引用
