# DeepSeek Harness Antigravity Suite Plugins

DeepSeek Harness (DSH) 的 Antigravity (Google Cloud Code / Gemini) 定制插件套件。

## 📦 插件列表

| 插件目录 | 插件名称 | 说明 |
| :--- | :--- | :--- |
| `dsh-llm-antigravity` | Antigravity LLM 适配器 | Gemini 3.7 Flash & 思考链流式对话，无缝接入 DSH 模型选择器 |
| `dsh-web-search-antigravity` | Antigravity 联网搜索 | 基于 Google Grounding 的高精准联网搜索提供方 |
| `dsh-web-search-selector` | 搜索源选择器 | 在 WebUI 设置中无缝切换 DeepSeek / Antigravity 搜索源 |
| `dsh-image-gen-antigravity` | Antigravity 图像生成 | 提供 `generate_image` 工具，基于 Gemini 3.1 Flash Image |

## 🚀 快速使用

1. 将所需插件复制到 DSH profile 的 `plugins/` 或 `node_modules/` 目录。
2. 将 `cordis.patch.yml.example` 中的配置合并至 `~/.dsh/profiles/web/cordis.patch.yml`。
3. 运行 `dsh web` 即可自动加载并生效所有插件。
