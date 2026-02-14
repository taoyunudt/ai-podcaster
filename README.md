# AI 播客生成器 🎙️

一个基于人工智能的播客生成工具，可以根据文本、网址或文档自动生成高质量的播客音频。

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Python](https://img.shields.io/badge/python-3.9+-green)
![License](https://img.shields.io/badge/license-MIT-orange)

## ✨ 功能特性

- 📝 **多种输入方式**：支持文本输入、网址自动抓取、DOCX/PDF 文档上传
- 🤖 **智能脚本生成**：基于通义千问大模型自动生成对话式播客脚本
- 🎙️ **高质量 TTS 语音合成**：使用千问 TTS 引擎生成自然流畅的语音
- 🎵 **智能音频合成**：自动合并多段对话，添加静音间隔和音量调整
- 🎨 **现代化 Web 界面**：三栏响应式布局，操作直观简单
- 📱 **全平台支持**：支持桌面端、平板和移动设备访问

## 📁 项目结构

```
ai-podcaster/
├── api_server.py              # FastAPI 后端服务主文件
├── generator.py               # 对话生成器模块
├── tts_qwen3.py              # 千问 TTS 语音合成引擎
├── merger_advanced.py        # 音频合并模块（高级版）
├── merger_simple.py          # 音频合并模块（简化版）
├── script_generator.py       # 播客脚本生成器
├── config.py                # 配置文件（包含 API 密钥，不提交到 Git）
├── config.example.py        # 配置文件示例
├── main.py                  # 命令行入口
│
├── static/                   # 前端静态文件目录
│   ├── index.html           # 主页面（三栏布局）
│   ├── css/
│   │   └── style.css        # 样式文件
│   └── js/
│       └── app.js           # 前端交互逻辑
│
├── utils/                    # 工具模块目录
│   ├── document_analyzer.py # 文档分析器（网址、Word、PDF）
│   ├── file_utils.py        # 文件工具函数
│   └── log_utils.py         # 日志工具
│
├── audio/                    # 生成的临时音频文件
├── output/                   # 最终输出的播客音频
├── logs/                     # 日志文件
├── requirements.txt         # Python 依赖清单
├── .gitignore             # Git 忽略配置
├── FRONTEND_README.md      # 前端使用指南
└── README.md               # 项目说明文档（本文件）
```

## 🚀 功能模块详解

### 1. API 服务（api_server.py）

FastAPI 后端服务，提供 RESTful API：

| 端点 | 方法 | 说明 |
|------|------|------|
| `/` | GET | 前端页面 |
| `/health` | GET | 健康检查 |
| `/api/analyze/url` | POST | 分析网址内容 |
| `/api/analyze/document` | POST | 分析上传的文档 |
| `/api/generate/script` | POST | 生成播客脚本 |
| `/api/generate/audio` | POST | 根据脚本生成音频 |
| `/api/audio/{filename}` | GET | 获取生成的音频文件 |

### 2. 脚本生成器（script_generator.py）

基于通义千问大模型生成对话式播客脚本：
- 支持自定义播客时长（3-30 分钟）
- 自动提取主题或使用指定主题
- 生成主持人（智小宝）和嘉宾（智初）的对话
- 使用 Markdown 格式，易于阅读和编辑

### 3. TTS 引擎（tts_qwen3.py）

千问 TTS 语音合成引擎：
- 支持多种说话人声音
- 可调节语速、音量、采样率
- 支持实时流式输出
- 高质量自然语音

### 4. 音频合并（merger_advanced.py）

高级音频合并功能：
- 自动添加对话间隔静音
- 音量标准化处理
- 支持 MP3、WAV 等多种格式
- 可调节比特率和采样率

### 5. 文档分析器（utils/document_analyzer.py）

支持多种输入源：
- **网址**：自动抓取网页内容并提取文本
- **Word 文档**：读取 .docx 文件内容
- **PDF 文档**：读取 .pdf 文件内容
- 自动提取主题和摘要

### 6. 前端界面（static/）

现代化三栏布局：
- **左栏**：内容输入区（文本/网址/文档）
- **中栏**：脚本生成和编辑区
- **右栏**：音频生成和播放区
- 响应式设计，支持各种设备

## 🔧 部署条件

### 系统要求

- **操作系统**：macOS / Linux / Windows
- **Python 版本**：Python 3.9 或更高版本
- **内存**：建议 4GB 以上
- **磁盘空间**：建议 2GB 以上

### 必需的 API 密钥

本项目需要以下阿里云 API 服务：

1. **通义千问 API**（用于生成脚本和对话）
   - 获取地址：https://dashscope.console.aliyun.com/
   - 需要申请：DashScope API Key

2. **千问 TTS API**（用于语音合成）
   - 获取地址：https://nls-portal.console.aliyun.com/
   - 需要申请：TTS AppKey
   - 需要申请：AccessKey ID 和 AccessKey Secret

### 依赖软件

- **FFmpeg**（音频处理必需）
  - macOS: `brew install ffmpeg`
  - Ubuntu/Debian: `sudo apt install ffmpeg`
  - Windows: 下载安装包或使用 choco

## 📦 部署流程

### 方式一：本地部署（推荐）

#### 1. 克隆项目

```bash
git clone https://github.com/taoyunudt/ai-podcaster.git
cd ai-podcaster
```

#### 2. 创建虚拟环境（可选但推荐）

```bash
python3 -m venv venv
source venv/bin/activate  # macOS/Linux
# 或
venv\Scripts\activate     # Windows
```

#### 3. 安装依赖

```bash
pip install -r requirements.txt
```

#### 4. 配置 API 密钥

```bash
# 复制配置文件示例
cp config.example.py config.py

# 编辑 config.py，填入你的 API 密钥
# 需要填入以下四个密钥：
# - DASHSCOPE_API_KEY
# - TTS_APPKEY
# - ALI_ACCESS_KEY_ID
# - ALI_ACCESS_KEY_SECRET
```

**config.py 配置示例：**

```python
# 阿里云百炼 API Key（用于生成对话）
DASHSCOPE_API_KEY = "sk-xxxxxxxxxxxxxxxx"

# 阿里云语音合成 AppKey（用于生成语音）
TTS_APPKEY = "xxxxxxxxxxxxxx"

# 阿里云 AccessKey（用于TTS API调用）
ALI_ACCESS_KEY_ID = "LTAI5txxxxxxxxxxxxx"
ALI_ACCESS_KEY_SECRET = "xxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

#### 5. 启动服务

```bash
python3 api_server.py
```

服务启动后，会显示：
```
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
```

#### 6. 访问应用

在浏览器中打开：
```
http://localhost:8000
```

### 方式二：Docker 部署（进阶）

创建 `Dockerfile`：

```dockerfile
FROM python:3.9-slim

# 安装 FFmpeg
RUN apt-get update && apt-get install -y ffmpeg

# 设置工作目录
WORKDIR /app

# 复制依赖文件
COPY requirements.txt .

# 安装 Python 依赖
RUN pip install --no-cache-dir -r requirements.txt

# 复制项目文件
COPY . .

# 暴露端口
EXPOSE 8000

# 启动服务
CMD ["python3", "api_server.py"]
```

构建和运行：

```bash
# 构建镜像
docker build -t ai-podcaster .

# 运行容器
docker run -d -p 8000:8000 --name ai-podcaster ai-podcaster
```

### 方式三：云服务部署

可以部署到支持 Python 的云平台：

- **Vercel**：使用 Serverless Functions
- **Railway**：一键部署 Docker 容器
- **阿里云 ECS / 腾讯云 CVM**：VPS 部署
- **AWS EC2 / Google Cloud**：云服务器部署

## 📖 使用说明

### Web 界面使用

访问 `http://localhost:8000`，按照三个步骤操作：

#### 步骤 1：输入内容

1. 选择输入方式：
   - **文本输入**：直接在文本框中输入内容
   - **网址输入**：输入网址，点击"分析网址"
   - **文档上传**：点击或拖拽上传 DOCX/PDF 文档

2. 设置播客时长（3-30 分钟）
3. 可选填写主题（留空则自动提取）

4. 点击"✨ 生成脚本"

#### 步骤 2：生成脚本

1. 系统自动生成播客脚本
2. 查看脚本内容，可直接编辑修改
3. 点击"🎵 生成音频"

#### 步骤 3：生成音频

1. 等待音频生成完成
2. 在线播放生成的音频
3. 点击"⬇️ 下载音频"保存到本地

### API 调用示例

#### 生成脚本

```bash
curl -X POST http://localhost:8000/api/generate/script \
  -H "Content-Type: application/json" \
  -d '{
    "content": "人工智能的发展历史",
    "input_type": "text",
    "duration_minutes": 5,
    "theme": "AI技术发展"
  }'
```

#### 生成音频

```bash
curl -X POST http://localhost:8000/api/generate/audio \
  -H "Content-Type: application/json" \
  -d '{
    "script": "主持人：今天我们来聊聊人工智能的历史...\n嘉宾：人工智能最早起源于20世纪50年代..."
  }'
```

#### 下载音频

```bash
curl -O http://localhost:8000/api/audio/podcast_xxxxxxxx.mp3
```

## 🔧 开发指南

### 本地开发

```bash
# 1. 克隆项目
git clone https://github.com/taoyunudt/ai-podcaster.git
cd ai-podcaster

# 2. 安装依赖
pip install -r requirements.txt

# 3. 配置密钥
cp config.example.py config.py
# 编辑 config.py

# 4. 启动开发服务器
python3 api_server.py
```

### 添加新功能

- **后端 API**：修改 `api_server.py`
- **TTS 引擎**：修改 `tts_qwen3.py`
- **脚本生成**：修改 `script_generator.py`
- **前端界面**：修改 `static/` 下的文件
- **工具函数**：添加到 `utils/` 目录

### 代码风格

项目遵循 PEP 8 Python 编码规范。

### 测试

```bash
# 运行单元测试（如果存在）
python3 -m pytest tests/

# 测试 API 健康状态
curl http://localhost:8000/health
```

## 🛠️ 常见问题

### 1. FFmpeg 未安装

**错误信息**：
```
FileNotFoundError: [Errno 2] No such file or directory: 'ffmpeg'
```

**解决方案**：

```bash
# macOS
brew install ffmpeg

# Ubuntu/Debian
sudo apt update
sudo apt install ffmpeg

# Windows
# 从 https://ffmpeg.org/download.html 下载并安装
```

### 2. API 密钥无效

**错误信息**：
```
HTTPError: 401 Unauthorized
```

**解决方案**：

检查 `config.py` 中的 API 密钥是否正确配置：
```python
DASHSCOPE_API_KEY = "sk-xxxxx"  # 检查是否有效
TTS_APPKEY = "xxxxx"  # 检查是否有效
```

### 3. 端口被占用

**错误信息**：
```
OSError: [Errno 48] Address already in use
```

**解决方案**：

```bash
# 查找占用 8000 端口的进程
lsof -ti:8000 | xargs kill -9

# 或使用其他端口启动
python3 -m uvicorn api_server:app --port 8080
```

### 4. 依赖安装失败

**解决方案**：

```bash
# 升级 pip
pip install --upgrade pip

# 使用国内镜像源
pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple
```

## 📝 技术栈

- **后端框架**：FastAPI
- **Web 服务器**：Uvicorn
- **AI 模型**：通义千问 (DashScope API)
- **TTS 引擎**：千问 TTS API
- **音频处理**：FFmpeg、Pydub
- **前端技术**：HTML5、CSS3、JavaScript（纯静态）
- **文档处理**：python-docx、PyPDF2
- **HTTP 客户端**：httpx

## 📄 许可证

本项目采用 [MIT License](LICENSE) 开源协议。

## 👥 贡献

欢迎贡献代码、报告问题或提出建议！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 提交 Pull Request

## 📧 联系方式

- **作者**：taoyunudt
- **GitHub**：https://github.com/taoyunudt
- **项目地址**：https://github.com/taoyunudt/ai-podcaster

## 🙏 致谢

- [通义千问](https://tongyi.aliyun.com/) - 提供强大的 AI 能力
- [FastAPI](https://fastapi.tiangolo.com/) - 现代化的 Python Web 框架
- [FFmpeg](https://ffmpeg.org/) - 强大的音频处理工具

## 📅 更新日志

### v1.0.0 (2026-02-14)

✨ **初始版本发布**

- ✨ 完整的 AI 播客生成功能
- ✨ 支持文本/网址/文档三种输入方式
- ✨ 三栏响应式布局 Web 界面
- ✨ 自动脚本生成
- ✨ 高质量 TTS 语音合成
- ✨ 智能音频合并
- ✨ RESTful API 接口
- ✨ 完整的文档和配置示例

## 🌟 Star History

如果这个项目对你有帮助，请给个 Star ⭐️

---

**Made with ❤️ by taoyunudt**
