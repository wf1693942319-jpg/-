# MCAV Platform

Multi-model Cross-model Adversarial Verification — 让两个异构大模型互相质疑、辩护、收敛，降低单模型幻觉的 Web 应用。

> 核心想法：GPT 和 DeepSeek 的训练数据、对齐方式不同，犯错的地方也不一样。让它们就同一个问题互相找茬，能把单模型的错纠出来。

## 架构

```
前端 (React + Vite)
    │ HTTP / SSE
后端 (FastAPI)
    ├─ 编排引擎（主答 → 质疑 → 辩护 → 收敛/裁判）
    ├─ 模型适配层（OpenAI / DeepSeek / Claude / 通义）
    └─ 密钥管理 / 日志 / 缓存
```

## 快速开始

### 后端

```bash
cd src/backend
pip install -r requirements.txt
python main.py
```

默认 `http://localhost:8000`。

### 前端

```bash
cd src/frontend
npm install
npm run dev
```

默认 `http://localhost:5173`，代理 `/api/*` 到后端。

### 跑测试

```bash
cd tests
pytest -v
```

## 支持的模型

| 厂商 | 默认模型 | 备注 |
|---|---|---|
| OpenAI | gpt-4o-mini | 境外需科学上网 |
| DeepSeek | deepseek-chat | 性价比高 |
| Anthropic | claude-sonnet-4-6 | 推荐做裁判 |
| 阿里云 | qwen-turbo | 国内直连 |

本地模型只要暴露 OpenAI 兼容接口（vLLM / Ollama / LM Studio），用 OpenAI 适配器填本地 `base_url` 就能跑。

## 文档

- [REQUIREMENTS.md](docs/REQUIREMENTS.md) — 需求文档
- [DESIGN.md](docs/DESIGN.md) — 技术设计
- [TESTING.md](docs/TESTING.md) — 测试报告
- [USAGE.md](docs/USAGE.md) — 用户手册

## 项目状态

V1.0.0，MVP 可演示，离生产可用还差：

- Postgres 落盘（现在 SESSIONS 是 in-memory）
- embedding 版本的分歧检测（现在用字符 Jaccard 近似）
- 系统性 benchmark（计划在 TriviaQA 子集上跑）
- 真实接口自动化测试
- 监控埋点

## License

MIT. 详见 [LICENSE](LICENSE)。

## Contributing

欢迎 PR。先看 [CONTRIBUTING.md](CONTRIBUTING.md)。
