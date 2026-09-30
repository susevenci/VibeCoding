# CODEBUDDY.md

This file provides guidance to CodeBuddy Code when working with code in this repository.

## 项目性质

这是一个「Vibe Coding 入门」课程的**练习 / 作品仓库**,不是传统软件工程仓库。

- **没有**构建系统、包管理、依赖安装、测试、lint。
- 所有交付物都是**单文件 HTML**(HTML + 内联 `<style>` + 内联 `<script>`),用浏览器直接打开即可运行。
- 每个作品自包含、互不引用;目录之间没有任何 import 关系。

因此,「开发」在这里指的是:直接编辑那个 HTML 文件,然后在浏览器里打开验收。

## 目录结构

- `docs/vibe-coding-101/` — 31 篇课程讲义 Markdown(30 讲 + 课程大纲),每篇独占一个目录。**纯参考资料,不是代码**。需要课程语境、教学口吻、提示词方法论时读这里。
- `works/` — 各讲实战的产出物,**目录名以讲次号开头**:
  - `works/11-个人简历网页/resume.html` + `1.txt` — 实战 1:个人简历网页。`1.txt` 是版式需求与个人信息来源。
  - `works/12-每日待办清单/todo.html` — 实战 2:每日待办清单。
  - `works/02-手札记事本/salon-signup.html` — 报名表单 H5(移动端优先,扫码进入)。
  - `works/02-手札记事本/notebook.html` + `notebook-checklist.md` — 手札记事本(单页多区域)。checklist 是它的逐项验收清单。
  - `works/04-手札记事本进阶/notepad.html` — 手札个人记事本,规模最大、功能最全的一版(多视图切换)。
  - `works/11-个人简历网页-专业版/` — 简历进阶版(`index.html` + `resume.css` + `resume.js` 三文件拆分)。
- `resources/needs.txt` — 记事本需求的原始口述记录(内容有重复,是草稿性质)。
- `README.md` — 仓库总索引:教程 / 作品 / 杂项三节的目录表,以及技术约定汇总。
- `.workbuddy/` — 工具生成的缓存目录,**已被 `.gitignore` 忽略,不要提交**。

## 常用命令

本仓库没有 build / lint / test。开发与验收只有两步:

```bash
# 1) 直接用浏览器打开目标文件(语音功能依赖 Chrome / Edge)
#    双击文件,或用命令行打开
start 4/notepad.html        # Windows
open  4/notepad.html        # macOS

# 2) 或起一个静态服务器
#    (file:// 协议下部分浏览器会限制麦克风权限,建议用这个)
python -m http.server 8000
#    然后访问 http://localhost:8000/4/notepad.html
```

## 架构与约定

改动这些 HTML 时必须遵守的、从现有代码中总结出的模式:

**运行形态**
- 保持**单文件、零外部依赖**;唯一允许的外部资源是 CDN 上的 Google Fonts 字体。不要拆分 CSS / JS 文件,不要引入框架、打包器或 npm。
- 每个应用独立可用,不存在跨目录复用;不要为「共享」而抽出公共文件。

**状态与持久化**
- 一律使用 `localStorage`,每个应用有独立的 key 命名空间:`shouzha-notebook-v1`(notebook)、`shou-zha-notebook-v1`(notepad)、`todos`(todo)。
- 模式是:模块级 `state` 对象 → `save()` / `load()`(JSON 序列化)→ 整块重渲染函数(如 `renderTodos()`)。改完数据要调用 `save()` 并触发对应渲染。
- **修改 `state` 结构时必须补迁移逻辑**:`load()` 中对缺失字段补默认值、对旧格式做就地转换。参考 `4/notepad.html` 中把旧版 `slots` 对象迁移为数组的 `LEGACY_LABEL` 分支。
- 导出 / 导入是各应用的标配功能:导出用 `Blob` + `URL.createObjectURL` + `<a download>`;导入走隐藏的 `<input type="file">` + `FileReader`。JSON 之外,`notebook.html` 还提供 Markdown 导出。

**语音输入(贯穿多个应用的核心能力)**
- 每个文本输入区都要挂语音按钮,基于 Web Speech API:`window.SpeechRecognition || window.webkitSpeechRecognition`。
- 统一参数:`lang = 'zh-CN'`、`interimResults = true`、`continuous = true`;临时结果(interim)实时回填且**不能覆盖已有内容**(notepad.html 用 pre + final + interim + post 拼接)。
- 浏览器不支持时按钮要降级并提示改用 Chrome / Edge,不能报错中断。

**安全**
- 任何用户输入经 `innerHTML` 落地前**必须转义**。各文件已内置 `escape()`(notebook.html)/ `escapeHTML()`(notepad.html、todo.html),新代码沿用,不要另起一套。

**界面**
- 全部 UI 文案为简体中文(`lang="zh-CN"`),保持中文,不要改成英文。
- 主打「手札 / 手帐风」视觉:牛皮纸底色、手写体(Ma Shan Zheng / ZCOOL KuaiLe / Caveat / Kalam / Noto Serif SC)、胶带与印章装饰、横线纹理。设计令牌集中在 `:root` CSS 变量里——调色、调字体请改变量,不要散落硬编码。
- 移动端优先 / 响应式,断点大致在 900px 与 640px;手机偶尔会访问,小屏必须可用。

## 需求来源

改动 `4/notepad.html` 或 `2/notebook.html` 之前,先读 `needs.txt`(用户原始需求)和 `2/notebook-checklist.md`(逐项验收标准:视觉、工具栏、各功能模块、语音、持久化、浏览器兼容性)。新需求按这两份文档对齐,而不是凭空设计。
