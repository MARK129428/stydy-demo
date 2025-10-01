# 浏览器、JS 与 V8 引擎工作原理笔记

---

## 1. 浏览器引擎 vs JS 引擎

### 1.1 浏览器引擎

- 解析 HTML、CSS、图片等资源  
- 构建 DOM 树（Document Object Model）  
- 构建 CSSOM 树（CSS Object Model）  
- 生成渲染树（Render Tree）  
- 布局（Layout / Reflow）、绘制（Painting）  
- 处理 UI 事件、滚动、重绘等  

常见浏览器引擎：

| 浏览器 | 渲染引擎 |
|--------|-----------|
| Chrome、Edge | Blink |
| Firefox | Gecko |
| Safari | WebKit |
| IE | Trident |

---

### 1.2 JS 引擎

- 解析和执行 JS 代码  
- 构建 AST（抽象语法树）  
- 编译为字节码或机器码执行  
- 提供浏览器 API（DOM、BOM 等）  
- 管理内存（垃圾回收）  

常见 JS 引擎：

| 浏览器 | JS 引擎 |
|--------|---------|
| Chrome、Edge | V8 |
| Firefox | SpiderMonkey |
| Safari | JavaScriptCore / Nitro |
| IE | Chakra |

---

### 1.3 浏览器渲染与 JS 执行协作流程

```mermaid
flowchart TD
    A[浏览器接收 HTML] --> B[解析 HTML → 构建 DOM]
    B --> C[解析 CSS → 构建 CSSOM]
    C --> D[生成渲染树 Render Tree]
    D --> E[布局 Layout & 绘制 Painting]
    B --> F[遇到 <script> → JS 引擎执行 JS]
    F --> G[修改 DOM / CSSOM]
    G --> D
    E --> H[最终显示到屏幕]

