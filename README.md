# 界园 · 听运亭

> 景由眼见，由心生。博士所问，贫道掷币以观卦象。

**界园 · 听运亭** 是一款明日方舟主题的 AI 算命 Web 应用。罗德岛驻龙门外派风水大师「玄冥子」坐镇界园听运亭，以奇门遁甲、五行八卦为博士们断卦解惑——抽卡运数、关卡吉凶、干员命格，皆可一问。

---

## 技术栈

| 层级 | 技术 |
|------|------|
| 后端框架 | Flask 3 |
| AI 引擎 | LangChain + OpenAI 兼容接口 |
| 大模型 | 硅基流动 (SiliconFlow) — Qwen/Qwen3-8B |
| 联网搜索 | DuckDuckGo Search |
| 限流 | Flask-Limiter |
| 前端 | 原生 HTML + CSS + JavaScript |

---

## 项目结构

```
arkdivine/
├── app.py                  # Flask 主应用入口
├── requirements.txt        # Python 依赖清单
├── .env.example            # 环境变量模板
├── .gitignore              # Git 忽略规则
├── README.md               # 项目说明
├── static/
│   ├── style.css           # 全局样式（界园主题）
│   └── bg.jpg              # 界园背景图
└── templates/
    └── index.html          # 聊天界面模板
```

---

## 快速开始

### 1. 克隆项目

```bash
git clone <仓库地址>
cd arkdivine
```

### 2. 创建虚拟环境并安装依赖

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 3. 配置环境变量

复制模板文件并填入你的硅基流动 API Key：

```bash
cp .env.example .env
```

编辑 `.env` 文件：

```
SILICONFLOW_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxx
SILICONFLOW_BASE_URL=https://api.siliconflow.cn/v1
```

> **获取 API Key**：前往 [硅基流动官网](https://siliconflow.cn/) 注册账号，在「API 密钥」页面创建 Key。新用户通常有免费额度。

### 4. 启动应用

```bash
python app.py
```

访问 **http://127.0.0.1:5001** 即可进入界园听运亭。

---

## 界面风格

以明日方舟「界园志异」资料片为设计灵感，整体视觉风格包含：

- **粉彩渐变天空**：粉红→粉白→粉金的色彩层次
- **青绿点缀**：输入框、按钮以青绿色（mint / 暗色绿松石）提亮
- **描金装饰**：标题、按钮悬停使用金粉光效（#D4AF37 / #FFD700）
- **磨砂玻璃质感**：对话气泡、输入区域使用 `backdrop-filter: blur()` 的毛玻璃效果
- **中式装饰元素**：CSS 纯绘制的金松、飘落松针、云纹、星光粒子、底部「已录」印章
- **响应式布局**：自适应 1200px+ 大屏、平板、手机端

---

## 功能特性

- 输入任意问题（抽卡运势 / 关卡攻略 / 干员配队 / 基建布局），玄冥子以风水玄学作答
- 联网搜索明日方舟最新信息，结合卦象给出「一本正经地胡说八道」的化解方案
- 所有化解方案均为游戏内可执行操作（刷 1-7 补土、换模组、调编队顺序等）
- 泰拉生物术语体系：羽兽、鳞兽、瘤兽、磐蟹、钳兽等，无现实动物名称
- 30 秒/次本地限流 + 全局限流 100 次/分钟

---

## 注意事项

1. **切勿在生产环境使用 `debug=True`**：当前默认以 debug 模式启动，部署前应改为从环境变量读取。
2. **`.env` 文件已加入 `.gitignore`**，切勿将包含真实 Key 的 `.env` 提交到版本控制。
3. **科学算命，娱乐为主**：本应用为明日方舟同人趣味项目，卦象内容由 AI 生成，仅供娱乐，请勿当真。
4. **泰拉术语自动替换**：AI 回答中不会出现「鱼」「鸡」「牛」等现实动物名，全部替换为鳞兽、羽兽、瘤兽等泰拉世界专用术语。
5. **部署建议**：生产环境请使用 Gunicorn + Nginx 反向代理，并将限流存储切换到 Redis。