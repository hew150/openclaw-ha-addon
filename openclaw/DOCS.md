# OpenClaw Agent Pro 🦞

这是专为 Home Assistant 打造的满血极客版 OpenClaw AI 大脑。基于 Debian 重装甲底包构建，不仅为你提供了一个智能对话终端，还赋予了 AI **真正的计算机操作权限、浏览器自动化能力以及满血的开发工具链**。

## 🌟 核心特性
* **零负担秒装**：采用云端预编译 Docker 镜像，树莓派等弱算力设备也能在 10 秒内极速安装，0 编译负担。
* **原生无头浏览器 (Chromium)**：AI 可自主打开网页、抓取动态数据、甚至“看”懂页面结构。
* **满级开发工具链**：内置 Python3、Node.js、pnpm、ripgrep (rg)、fd、bat 等现代极客工具，AI 写代码、搜文件如虎添翼。
* **HA Assist 语音管家**：提供兼容 OpenAI 的标准 API 接口，可直接接入 Home Assistant 原生语音助手。

---

## ⚙️ 基础配置说明 (Configuration)

在插件的“配置”面板中，你可以设置以下基础参数：

* **`provider`**: 默认的大模型供应商 (如 `nvidia`, `openai`, `groq`, `openrouter` 等)。
* **`api_key`**: 对应供应商的 API 密钥。如果需要配置多模型密钥，请使用 Web 控制台配置 `.env` 文件。
* **`gateway_bind_mode`**:
  * `auto` / `lan`：允许局域网访问（**推荐**）。不仅可以自己访问控制台，还能让 HA 语音助手调用。
  * `localhost`：仅限本地内部调用，极度安全。
* **`http_proxy`**: (可选) 全局网络代理，例如 `http://192.168.1.2:7890`。配置后，AI 爬取外网、调用 API 将全部通过此代理。

---

## 💻 极客控制台 (Web Terminal)

本插件在底层集成了一个极其轻量的终端后门 (ttyd)。
安装并启动插件后，点击侧边栏的 **"OpenClaw UI"** (或者通过 `http://你的HA_IP:8099` 访问)，即可直接进入插件的 Debian 底层沙箱。

### 🔐 进阶：配置多模型密钥沙箱
如果你想同时使用多个渠道的模型（比如用 Groq 聊天，用 NVIDIA 做视觉分析），单靠 UI 面板是不够的。

1. 打开 Web 控制台 (8099 端口)。
2. 输入 `nano /config/.openclaw/.env`。
3. 在里面写入你所有的密钥，例如：
   ```env
   OPENAI_API_KEY="sk-xxxx"
   GROQ_API_KEY="gsk_xxxx"
   NVIDIA_API_KEY="nvapi-xxxx"
