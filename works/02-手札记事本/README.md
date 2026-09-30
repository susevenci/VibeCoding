# 02 · 手札记事本

第 2 讲实战产出。单文件 HTML，浏览器直接打开即可运行，数据存在浏览器 `localStorage` 里。

## 文件

| 文件 | 说明 |
|---|---|
| `notebook.html` | 手札记事本主应用（单页多区域） |
| `notebook-checklist.md` | 该应用的逐项验收清单（视觉、工具栏、语音、持久化等） |
| `salon-signup.html` | 报名表单 H5（移动端优先，扫码进入） |

## 技术要点

- `localStorage` 键：`shouzha-notebook-v1`
- 语音输入：Web Speech API（`window.SpeechRecognition || window.webkitSpeechRecognition`），`lang='zh-CN'`
- 用户输入经 `innerHTML` 渲染前统一走 `escape()` 转义
- 除 JSON 外还支持 Markdown 导出

## 复现

```bash
# 直接双击打开
start notebook.html

# 或起静态服务器（语音功能建议走这种方式）
python -m http.server 8000
# http://localhost:8000/works/02-手札记事本/notebook.html
```
