# AI Testcase Agent

基于 PRD / 飞书文档 / UI 图片生成测试用例，并支持规则评测、人工基准 F1、LLM Judge、幻觉检测、修正和导出。

## 技术栈

- Streamlit：前端展示
- FastAPI：后端接口
- LangGraph：Agent 闭环编排
- Volcengine Ark / OpenAI-compatible API：大模型调用

## 安装依赖

```powershell
pip install -r requirements_ai_testcase_agent.txt
```

可选增强依赖：

```powershell
pip install langgraph langchain-core sentence-transformers
```

## 启动后端

```powershell
python -m uvicorn fastapi_backend:app --host 127.0.0.1 --port 8001
```

后端文档：

```text
http://127.0.0.1:8001/docs
```

## 启动前端

```powershell
python -m streamlit run ai_testcase_agent_app_v7_fast_langgraph.py --server.port 8502
```

前端地址：

```text
http://localhost:8502
```

前端侧边栏中的 FastAPI 后端地址填写：

```text
http://127.0.0.1:8001
```

