# Portable Markdown Editor

一个轻量、可离线、零构建的 Markdown 编辑器。

项目采用 **HTML + CSS + Vanilla JavaScript** 实现，业务代码集中在一个 `index.html` 中，第三方依赖统一保存在本地 `vendor/` 目录。下载后无需安装、无需启动服务器，直接双击 `index.html` 即可使用；同一套文件也可以直接部署到 GitHub Pages。

> 当前版本：**v1.0.0**

---

## 项目定位

Portable Markdown Editor 并不试图成为一个“大而全”的笔记软件，而是专注于 Markdown 编辑最常用的一组能力：

```text
打开 Markdown
     ↓
编辑内容
     ↓
实时预览
     ↓
自动保存
     ↓
下载 Markdown
```

整个项目坚持几个原则：

- **Portable**：整个目录可以直接复制、下载和使用
- **Zero Build**：没有 npm、Vite、Webpack 或构建流程
- **Local First**：编辑内容优先保存在浏览器本地
- **No Backend**：不依赖 PHP、Python、Node.js 或数据库
- **Pages Ready**：可直接部署到 GitHub Pages
- **Keep It Small**：不为了增加功能而持续扩大项目复杂度

---

## 功能特性

### Markdown 实时编辑与预览

左侧编辑 Markdown，右侧实时显示渲染结果。

支持常见 Markdown / GitHub Flavored Markdown 语法，包括：

- 标题
- 粗体、斜体、删除线
- 引用
- 行内代码
- 代码块
- 无序列表
- 有序列表
- 任务列表
- 链接
- 图片
- 表格
- 分隔线

### 快捷格式工具栏

内置轻量工具栏，可以直接插入常见 Markdown 语法：

```text
H1 / H2
粗体 / 斜体 / 删除线
引用
行内代码 / 代码块
无序列表 / 有序列表 / 任务列表
链接 / 图片 / 表格
```

工具栏不会模拟完整的富文本编辑器，而是作为 Markdown 输入的辅助工具。

### Undo / Redo

内置轻量编辑历史：

- 最多保存 100 个历史快照
- 输入停止后自动创建快照
- 工具栏格式化操作立即记录
- 支持撤销与重做按钮
- 支持常用键盘快捷键

### 本地文件操作

支持：

- 打开 `.md`
- 打开 `.markdown`
- 打开 `.txt`
- 将 Markdown 文件直接拖入页面
- 保留打开文件的文件名
- 下载当前内容为 `.md` 文件

由于普通静态网页受到浏览器安全限制，编辑器不会直接覆盖磁盘中的原文件。“保存”会通过浏览器下载生成新的 Markdown 文件，这也是本项目保持纯静态架构的重要前提。

### 自动保存

正文、文件名以及部分界面状态会自动保存到浏览器 `localStorage`。

重新打开页面后，可以继续上一次未完成的内容。

所有自动保存数据均保存在当前浏览器中，不会上传到服务器。

### 深色 / 浅色主题

支持浅色和深色界面切换，并记住当前主题设置。

### 响应式布局

#### 桌面端

采用左右双栏结构：

```text
┌──────────────────┬──────────────────┐
│                  │                  │
│      Editor      │     Preview      │
│                  │                  │
└──────────────────┴──────────────────┘
```

编辑区与预览区各自独立滚动。

#### 手机端

小屏幕下不强行压缩双栏，而是切换为：

```text
编辑  |  预览
```

一次只展示一个主要面板，使编辑和阅读都保持足够空间。

格式工具栏在手机端采用横向滚动，避免堆叠成多行。

---

## 快捷键

| 操作 | Windows / Linux | macOS |
| --- | --- | --- |
| 粗体 | `Ctrl + B` | `Cmd + B` |
| 斜体 | `Ctrl + I` | `Cmd + I` |
| 插入链接 | `Ctrl + K` | `Cmd + K` |
| 撤销 | `Ctrl + Z` | `Cmd + Z` |
| 重做 | `Ctrl + Y` | `Cmd + Shift + Z` |
| 下载 Markdown | `Ctrl + S` | `Cmd + S` |

编辑区中按 `Tab` 会插入两个空格，而不是让焦点直接跳出编辑器。

---

## 使用方式

### 方式一：本地直接使用

下载或克隆整个项目：

```bash
git clone <your-repository-url>
```

进入目录后直接双击：

```text
index.html
```

无需执行：

```text
npm install
npm run dev
npm run build
```

也不需要本地 Web Server。

> 请保留 `vendor/` 目录及其文件，否则 Markdown 解析功能将无法正常加载。

### 方式二：GitHub Pages

将完整项目上传到 GitHub 仓库后：

1. 打开仓库 **Settings**
2. 进入 **Pages**
3. 在 **Build and deployment** 中选择从分支部署
4. 选择用于发布的分支，例如 `main`
5. 选择根目录 `/ (root)`
6. 保存并等待 GitHub Pages 完成部署

由于入口文件就是根目录的 `index.html`，不需要修改构建配置。

---

## 目录结构

```text
portable-markdown-editor/
│
├── index.html
├── README.md
├── LICENSE
├── NOTICE.md
├── THIRD_PARTY_LICENSES.md
│
└── vendor/
    └── marked/
        ├── marked.js
        └── LICENSE.md
```

### `index.html`

项目的核心文件。

其中包含本项目自行维护的：

```text
HTML
CSS
JavaScript
```

业务代码不再拆分为大量 CSS / JS 文件，便于直接复制、阅读和长期维护。

### `vendor/`

只保存第三方依赖。

第三方源码与业务代码保持物理隔离，不直接修改第三方库文件，便于后续升级和许可证管理。

---

## 技术架构

当前核心链路非常简单：

```text
Markdown Editor
       │
       ↓
     Marked
       │
       ↓
 HTML 安全过滤
       │
       ↓
     Preview
```

其他能力围绕编辑器展开：

```text
                    index.html
                        │
        ┌───────────────┼───────────────┐
        │               │               │
        ↓               ↓               ↓
      Editor          Storage          Layout
        │               │
        ↓               ↓
     History       localStorage
        │
        ↓
     Renderer
        │
        ↓
     Preview
```

虽然业务代码集中在一个 `index.html` 中，但内部仍按照职责划分逻辑区域，避免重新演变成难以维护的大型脚本。

---

## 技术特点

### HTML + CSS + Vanilla JavaScript

项目没有引入 React、Vue、Svelte 等框架。

这不是为了排斥现代框架，而是因为当前项目规模并不需要额外的框架层。

### Zero Build

没有：

- `package.json`
- `node_modules`
- Vite
- Webpack
- Rollup
- Babel

源代码本身就是最终运行版本。

### 本地第三方依赖

第三方库统一保存在：

```text
vendor/
```

因此编辑器不依赖公共 CDN，下载完整目录后可以在没有网络连接的情况下运行核心功能。

### localStorage

当前数据规模很小，因此优先使用浏览器原生 `localStorage`，而不是为了“工程化”引入 IndexedDB、SQLite WASM 或远程数据库。

---

## 安全边界

本项目对 Markdown 预览采用较严格的处理方式：

1. Markdown 中的原始 HTML 默认不会作为可执行 HTML 直接进入预览区域
2. Markdown 渲染结果会再次经过标签与属性白名单过滤
3. `javascript:` 等危险 URL 协议会被过滤
4. 外部链接会增加适当的安全属性

这里的设计目标是：**Markdown 编辑器不应该因为一个附加功能而默认获得执行任意 HTML / JavaScript 的能力。**

不过需要注意：当前过滤逻辑属于本项目的轻量安全边界，并不等同于专业 HTML Sanitizer 或完整安全审计。

因此：

> 不建议将本项目作为处理完全不可信 HTML 内容的安全沙箱。

如果未来开放 Markdown Raw HTML，本项目应优先引入经过长期验证的 HTML Sanitizer，而不是简单放宽现有过滤规则。

---

## 数据与隐私

当前版本没有：

- 用户账号
- 云同步
- 后端 API
- 数据库
- 分析统计代码
- AI API

编辑内容主要保存在：

```text
浏览器 localStorage
```

文件打开与下载也全部通过浏览器本地能力完成。

因此项目非常适合：

- 个人 Markdown 编辑
- README 编写
- 技术文档
- GitHub 文档
- 临时草稿
- 本地知识整理
- 静态工具页面

---

## 为什么不做成“大而全”

Portable Markdown Editor 有意保持较小的功能边界。

例如当前核心版本不会为了功能数量主动加入：

- npm 构建体系
- 前端框架
- 后端服务
- 数据库
- 云同步
- 用户系统
- AI 对话
- 在线网页采集
- 复杂文档管理

判断一个新功能是否应该进入核心版本时，优先考虑：

```text
是否属于 Markdown 编辑核心能力？
          ↓
是否能保持纯静态运行？
          ↓
是否明显增加长期维护成本？
          ↓
是否值得加入？
```

项目目标不是功能越多越好，而是让已有功能保持简单、稳定和容易理解。

---

## 浏览器兼容

建议使用较新的现代浏览器：

- Google Chrome
- Microsoft Edge
- Firefox
- Safari

由于项目主要依赖标准 Web API，通常不需要针对某个浏览器安装扩展。

---

## 第三方依赖

当前主要依赖：

| Library | Version | Purpose | License |
| --- | --- | --- | --- |
| Marked | 4.0.19 | Markdown → HTML | MIT |

具体第三方许可证信息请查看：

```text
THIRD_PARTY_LICENSES.md
```

第三方库自身的许可证文件也保存在对应 `vendor/` 目录中。

---

## 版本

### v1.0.0

首个稳定版本，完成 Markdown 编辑器的核心闭环：

- Markdown 实时编辑与预览
- 基础格式工具栏
- Undo / Redo
- 本地自动保存
- `.md / .markdown / .txt` 文件打开
- 文件拖拽打开
- Markdown 下载
- 深色 / 浅色主题
- 桌面端双栏布局
- 手机端编辑 / 预览切换
- 本地第三方依赖
- GitHub Pages 直接部署
- 基础 Markdown 预览安全边界

---

## 后续方向

后续版本仍会坚持“小步增加、保持核心稳定”的原则。

可能考虑的增强包括：

- Mermaid 图表
- KaTeX 数学公式
- HTML 导出
- Print / PDF
- 更完善的 Markdown 预览样式

这些功能不会为了版本号而强行加入；只有在不明显破坏当前极简架构的情况下才会进入核心版本。

---

## 项目来源与致谢

本项目在以下开源项目的产品思路和代码基础上进行研究、精简与重新设计：

**lengyi-markdown-editor**  
Original repository: https://github.com/woyin2024/lengyi-markdown-editor

原项目作者：**冷逸 / 沃垠AI**  
原项目许可证：**MIT License**

本项目在原项目基础上重新规划了功能边界，并针对以下方面进行了重构和调整：

- 页面与交互结构
- 编辑历史
- 本地文件操作
- Markdown 安全处理策略
- 移动端交互
- 本地第三方依赖管理
- Zero Build / GitHub Pages 使用方式

详细来源说明请查看：

```text
NOTICE.md
```

感谢原作者公开项目源码，使进一步学习、研究和二次开发成为可能。

---

## License

本项目按照仓库中的 `LICENSE` 文件进行许可和分发。

由于本项目包含基于原 MIT 项目进行修改和重构的代码，请保留原项目要求的版权及许可证声明。

第三方依赖按照各自许可证单独授权，具体信息见：

```text
THIRD_PARTY_LICENSES.md
```

---

## 一句话总结

> **下载整个目录，双击 `index.html`，开始写 Markdown。**
