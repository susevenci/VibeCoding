# 04 · 手札记事本（进阶版）

第 4 讲实战产出，也是本仓库里规模最大、功能最全的一版记事本：多视图切换，首页可跳转到各个功能区。

## 文件

| 文件 | 说明 |
|---|---|
| `notepad.html` | 手札个人记事本（单文件应用） |

## 功能分区

对应原始需求（见 `resources/needs.txt`）里的 7 项：

1. 全部可填写内容支持语音转文字
2. 规划明日行程
3. 记录待办事项（与 2 同页）
4. 快速记录奇思妙想
5. 写日记
6. 学习记录 / 总结
7. 首页可跳转到各功能区，手札风格，数据存本地

## 技术要点

- `localStorage` 键：`shou-zha-notebook-v1`
- 模块级 `state` 对象 → `save()` / `load()`（JSON 序列化）→ 整块重渲染
- **`state` 结构变更时带迁移逻辑**：`load()` 里对缺失字段补默认值、旧格式就地转换
  （参见把旧版 `slots` 对象迁移为数组的 `LEGACY_LABEL` 分支）
- 语音输入用 pre + final + interim + post 拼接，临时结果实时回填但**不覆盖已有内容**
- 导出用 `Blob` + `URL.createObjectURL` + `<a download>`；导入走隐藏 `<input type="file">` + `FileReader`
- 用户输入经 `innerHTML` 落地前统一走 `escapeHTML()` 转义

## 复现

```bash
start notepad.html

# 语音功能建议用静态服务器
python -m http.server 8000
# http://localhost:8000/works/04-手札记事本进阶/notepad.html
```
