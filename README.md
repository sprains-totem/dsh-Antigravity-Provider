# DeepSeek Harness Antigravity Suite Plugins

DeepSeek Harness (DSH) 的 Antigravity (Google Cloud Code / Gemini) 定制插件套件。

## 📦 插件列表

| 插件目录 | 插件名称 | 说明 |
| :--- | :--- | :--- |
| `dsh-llm-antigravity` | Antigravity LLM 适配器 | Gemini 3.7 Flash & 思考链流式对话，无缝接入 DSH 模型选择器与 Refresh Token 管理 |
| `dsh-web-search-antigravity` | Antigravity 联网搜索 | 基于 Google Grounding 的高精准联网搜索提供方 |
| `dsh-web-search-selector` | 搜索源选择器 | 在 WebUI 设置中无缝切换 DeepSeek / Antigravity 搜索提供方 |
| `dsh-image-gen-antigravity` | Antigravity 图像生成 | 提供 `generate_image` 工具，基于 Gemini 3.1 Flash Image |

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
运行内置的解禁脚本，解除 WebUI 模型设置、远程访问限制及凭据权限严格检查：
```bash
node unlock-dsh.mjs
```

### 5. 启动 DeepSeek Harness
```bash
dsh web
```
