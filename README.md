
## 🌟 愿景：

3 天的比赛时间变为 1 小时 <br> 
自动完整一份可以获奖级别的建模论文


## ✨ 功能特性

- 🔍 自动分析问题，数学建模，编写代码，纠正错误，撰写论文
- 💻 Code Interpreter
    - local Interpreter: 基于 jupyter , 代码保存为 notebook 方便再编辑
    - 云端 code interpreter: [E2B](https://e2b.dev/) 和 [daytona](https://app.daytona.io/)
- 📝 生成一份编排好格式的论文
- 🤝 multi-agents: 建模手，代码手，论文手等
- 🔄 multi-llms: 每个 agent 设置不同的、合适的模型
- 🤖 支持所有模型: [litellm](https://docs.litellm.ai/docs/providers)
- 💰 成本低：workflow agentless，不依赖 agent 框架
- 🧩 自定义模板：prompt inject 为每个 subtask 单独设置需求

## 🚀 后期计划

- [x] 添加并完成 webui、cli
- [ ] 完善的教程、文档
- [ ] 提供 web 服务
- [ ] 英文支持（美赛）
- [ ] 集成 latex 模板
- [ ] 接入视觉模型
- [x] 添加正确文献引用
- [x] 更多测试案例
- [x] docker 部署
- [ ] human in loop: 引入用户的交互（选择模型，@agent重写，等等）
- [ ] feedback: evaluate the result and modify
- [x] codeinterpreter 接入云端 如 e2b 等供应商..
- [ ] 多语言: R 语言, matlab
- [ ] 绘图 napki,draw.io,plantuml,svg, mermaid.js
- [ ] 添加 benchmark
- [ ] web search tool
- [ ] RAG 知识库
- [ ] A2A hand off: 代码手多次反思错误，hand off 更聪明模型 agent
- [ ] chat / agent mode


> [!CAUTION]
> 项目处于实验探索迭代demo阶段，有许多需要改进优化改进地方，我(项目作者)很忙，有时间会优化更新
> 欢迎贡献


案例参考 [demo](./demo/) 文件夹下
**如果你有跑出来好的案例可以提交 PR 在该目录下**

## 📖 使用教程


提供三种部署方式，请选择最适合你的方案：
1. [docker(最简单)](#-方案一docker-部署推荐最简单)
2. [本地部署](#-方案二-本地部署)
3. [脚本本地部署(社区)](#-方案三自动脚本部署来自社区)


下载项目

```bash
git clone https://github.com/jihe520/MathModelAgent.git # 克隆项目
```




### 🐳 方案一：Docker 部署（推荐：最简单）

> 确保电脑安装了 docker 环境


1. 配置环境变量

```bash
cp backend/.env.dev.example backend/.env.dev
cp frontend/.env.example frontend/.env.development
```

填入配置
- backend/.env.dev
- frontend/.env.development

2. 启动服务

```bash
docker-compose up -d
```

3. 访问

现在你可以访问：
- 前端界面：http://localhost:5173
- 后端API：http://localhost:8000


### 💻 方案二: 本地部署

> 确保电脑中安装好 Python, Nodejs, **Redis** 环境


1. 配置环境变量

复制`/backend/.env.dev.example`到`/backend/.env.dev`(删除`.example` 后缀)

推荐模型能力较强的、参数量大的模型。

复制`/fronted/.env.example`到`/fronted/.env.development`(删除`.example` 后缀)


2. 安装依赖

启动后端

> [!CAUTION]
> 启动 Redis, 下载和运行问 AI

```bash
cd backend # 切换到 backend 目录下
pip install uv # 推荐使用 uv 管理 python 项目
uv sync # 安装依赖
# 启动后端
# 激活 python 蓄虚拟环境
source .venv/bin/activate # MacOS or Linux
venv\Scripts\activate.bat # Windows
# MacOS or Linux 运行这条命令
ENV=DEV uvicorn app.main:app --host 0.0.0.0 --port 8000 --ws-ping-interval 60 --ws-ping-timeout 120 --reload
# Windows 运行这条命令
set ENV=DEV ; uvicorn app.main:app --host 0.0.0.0 --port 8000 --ws-ping-interval 60 --ws-ping-timeout 120
```

启动前端

```bash
cd frontend # 切换到 frontend 目录下
npm install -g pnpm
pnpm i #确保电脑安装了 pnpm 
pnpm run dev
```


### 🚀 方案三：自动脚本部署（来自社区）
有没有自动部署的脚本 ？
[mmaAutoSetupRun](https://github.com/Fitia-UCAS/mmaAutoSetupRun)



[教程](./docs/md/tutorial.md)

运行的结果和产生在`backend/project/work_dir/xxx/*`目录下
- notebook.ipynb: 保存运行过程中产生的代码
- res.md: 保存最后运行产生的结果为 markdown 格式

需要自定义自定义提示词模板 template ？
Prompt Inject : [prompt](./backend/app/config/md_template.toml)

网络状况太差难以配置Docker等设置？
网络不畅时的配置过程示例：[网络环境极差时的MathModelAgent配置过程](docs/md/网络环境极差时的MathModelAgent配置过程.md)


- 项目处于**开发实验阶段**（我有时间就会更新），变更较多，还存在许多 Bug，我正着手修复。
- 希望大家一起参与，让这个项目变得更好
- 非常欢迎使用和提交  **PRs** 和 issues 
- 需求参考 后期计划

clone 项目后，下载 **Todo Tree** 插件，可以查看代码中所有具体位置的 todo

`.cursor/*` 有项目整体架构、rules、mcp 可以方便开发使用

## 📄 版权License

个人免费使用，请勿商业用途，商业用途联系我（作者）

[License](./docs/md/License.md)

## 🙏 Reference

Thanks to the following projects:
- [OpenCodeInterpreter](https://github.com/OpenCodeInterpreter/OpenCodeInterpreter/tree/main)
- [TaskWeaver](https://github.com/microsoft/TaskWeaver)
- [Code-Interpreter](https://github.com/MrGreyfun/Local-Code-Interpreter/tree/main)
- [Latex](https://github.com/Veni222987/MathModelingLatexTemplate/tree/main)
- [Agent Laboratory](https://github.com/SamuelSchmidgall/AgentLaboratory)
- [ai-manus](https://github.com/Simpleyyt/ai-manus)


