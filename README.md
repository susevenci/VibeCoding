# VibeCoding

「Vibe Coding 入门」课程的讲义与实战作品合集。

课程用 AI 编程工具从零做出一个个可以直接用的小东西——每个作品都是**单文件 HTML**，
用浏览器直接打开就能跑，不需要安装、构建或任何依赖。

## 📖 教程

| 目录 | 说明 |
| --- | --- |
| [docs/vibe-coding-101](docs/vibe-coding-101/) | 全部 31 篇课程讲义（课程大纲 + 第 1~30 讲 Markdown）。按讲次编号排列，可直接点击进入对应的讲次目录。 |

## 🎨 实战作品

每篇讲义配一个动手产出，目录名以讲次编号开头，点进各目录即可看到该作品的中文说明。

| 讲次 | 作品 | 说明 | 在线打开 |
| --- | --- | --- | --- |
| 第 2 讲 | [02-手札记事本](works/02-手札记事本/) | 手札风记事本（单页多区域）+ 报名表单 H5 | [notebook.html](works/02-手札记事本/notebook.html) · [salon-signup.html](works/02-手札记事本/salon-signup.html) |
| 第 4 讲 | [04-手札记事本进阶](works/04-手札记事本进阶/) | 功能最全的一版记事本：多视图切换，含行程 / 待办 / 灵感 / 日记 / 学习记录 | [notepad.html](works/04-手札记事本进阶/notepad.html) |
| 第 11 讲 | [11-个人简历网页](works/11-个人简历网页/) | 个人简历单页（单文件版） | [resume.html](works/11-个人简历网页/resume.html) |
| 第 11 讲 | [11-个人简历网页-专业版](works/11-个人简历网页-专业版/) | 简历进阶版：拆分 HTML / CSS / JS，含深色模式与 A4 打印 | [index.html](works/11-个人简历网页-专业版/index.html) |
| 第 12 讲 | [12-每日待办清单](works/12-每日待办清单/) | 每日待办清单，含日期同步与完成计数 | [todo.html](works/12-每日待办清单/todo.html) |

> GitHub 无法给文件夹加悬浮提示，所以「点进去看到中文说明」是靠**每个作品目录自带 `README.md`**
> 实现的——打开目录时它会在文件列表下方自动渲染。

## 📎 其它

| 文件 | 说明 |
| --- | --- |
| [resources/needs.txt](resources/needs.txt) | 记事本应用的原始口述需求记录 |
| [resources/CODEBUDDY.md](resources/CODEBUDDY.md) | 仓库协作指引：开发约定、目录说明、常用命令 |

## 技术约定

- **单文件、零依赖**：每个作品都是 HTML + 内联 CSS + 内联 JS，唯一允许的外部资源是 CDN 上的 Google Fonts。
- **数据存本地**：一律用 `localStorage`，各应用独立键名（`todos`、`shouzha-notebook-v1`、`shou-zha-notebook-v1`）。
- **语音输入**：核心能力，基于浏览器 Web Speech API，`lang='zh-CN'`，需 Chrome / Edge。
- **安全**：用户输入经 `innerHTML` 渲染前一律转义。
- **风格**：手札 / 手帐风——牛皮纸底色、手写体、胶带与印章装饰。
- **移动端优先**：手机偶尔访问，小屏必须可用。
