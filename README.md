# DeepSeek Harness Antigravity Suite Plugins

> DeepSeek Harness (DSH) 的 Google Cloud Code / Antigravity 定制全套插件套件。

---

## 📦 插件清单

| 插件目录 | 插件名称 | 说明 |
| :--- | :--- | :--- |
| `dsh-llm-antigravity` | Antigravity LLM 核心驱动与看板 | Gemini 3.7 Flash & 思考链流式对话、**实时额度监控与 5h/周度滑动窗口统计**、**Token 用量与前缀缓存分析看板（~97% 缓存命中率）**、**第三方模型 (Claude/GPT-OSS) 兼容与动态 Token 截断**、**原生多模态媒体工具 (`read_video`, `read_audio`, `read_pdf`)**、模型别名自动映射与 Refresh Token 管理 |
| `dsh-web-search-antigravity` | Antigravity 联网搜索 | 基于 Google Grounding 的高精准实时网络信息检索提供方 |
| `dsh-web-search-selector` | 搜索源选择器 | 在 WebUI 设置中无缝切换 DeepSeek 官方搜索 / Antigravity 搜索提供方 |
| `dsh-image-gen-antigravity` | Antigravity 图像生成 | 提供 `generate_image` 工具，基于 Gemini 3.1 Flash Image 支持多比例生图 |

---

## ✨ 核心功能亮点 (dsh-llm-antigravity)

### 1. 多模型支持与第三方兼容 (Gemini / Claude / GPT-OSS)
- **原生 Gemini 3.x 家族**：`gemini-3.7-flash-high/medium/low/tiered`（完整支持思维链 Thought Signature 稳定中继）、`gemini-pro-agent`、`gemini-3.6-flash`、`gemini-3.1-flash-lite`。
- **第三方 Frontier 模型完美接入**：
  - `claude-sonnet-4-6` / `claude-opus-4-6-thinking`：内置自动输出 Token 动态截断至 `64000`，彻底避免 Google 上游对 `65536` 报 `400 INVALID_ARGUMENT`；
  - `gpt-oss-120b-medium`：自动截断至 `16384` 并智能剔除非思考模型的 `thinkingConfig` 参数；
  - 模型别名与迁移自动映射（`gemini-3.1-pro-high` $\to$ `gemini-pro-agent`，`claude-3-5-sonnet` $\to$ `claude-sonnet-4-6`）。

### 2. ⚡ 实时额度监控与价值估算看板
- 基于 Google Cloud Code `v1internal:retrieveUserQuotaSummary` 与 `fetchAvailableModels` 实时查询；
- 支持 **5 小时滑动窗口 (`5h`)** 与 **每周限额 (`weekly`)** 进度条展示与状态告警（🟢 充足 / 🟡 预警 / 🔴 告急）；
- 精确重置倒计时与 UTC 时刻显示；
- 集成官方 1:1 费率估算与非满额初始配额的增量边际校准。

### 3. 📊 Token 用量统计与前缀缓存深度分析
- 自动捕获流式 `usageMetadata`，本地持久化保存（`~/.dsh/antigravity_usage.json`）；
- 核心指标：总请求数、实际输入 Tokens、实际输出 Tokens、**前缀缓存命中数与缓存节省率（~97% 命中率）**、思考链 Token 消耗；
- 支持 14 天长周期调用流水聚合分析与近 50 条调用明细，支持一键清空重置。

### 4. 🎥 原生全模态媒体解析工具链
- `read_video`：直接读取分析本地视频文件（MP4, MOV, WebM, MKV, AVI, OGG，上限 300MB）；
- `read_audio`：读取分析本地音频文件波形、语调与时序（MP3, WAV, M4A, FLAC, Opus, AAC，上限 100MB）；
- `read_pdf`：直接解析 PDF 文档排版、表格、Jupyter Notebook 与 CSV（上限 100MB）。

---

## 🚀 快速安装与配置

### 1. 复制插件到 DSH 插件目录
```bash
# 创建插件与依赖目录
mkdir -p ~/.dsh/profiles/web/plugins ~/.dsh/profiles/web/node_modules

# 复制插件
cp -r dsh-llm-antigravity dsh-web-search-antigravity dsh-web-search-selector dsh-image-gen-antigravity ~/.dsh/profiles/web/plugins/
cp -r dsh-llm-antigravity dsh-web-search-antigravity dsh-web-search-selector dsh-image-gen-antigravity ~/.dsh/profiles/web/node_modules/
```

### 2. 配置 Cordis Patch
将 `cordis.patch.yml.example` 复制到 `~/.dsh/profiles/web/cordis.patch.yml`：
```bash
cp cordis.patch.yml.example ~/.dsh/profiles/web/cordis.patch.yml
```

### 3. 配置 Refresh Token 凭据
在 `~/.dsh/.credentials.yaml` 中写入：
```yaml
ANTIGRAVITY_REFRESH_TOKEN: "your_oauth_refresh_token_here"
```

### 4. 执行深度解禁补丁（可选但推荐）
运行内置的解禁脚本，解除 WebUI 模型设置、远程访问限制、多模态 Composer 附件类型限制及凭据权限严格检查：
```bash
node unlock-dsh.mjs
```

### 5. 启动 DeepSeek Harness
```bash
dsh web
```

---

## 📜 开源协议
本项目基于 MIT License 协议开源。
