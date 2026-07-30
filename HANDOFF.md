# 交接文档：热带植物成长记 原型项目

> **面向读者**：完全没有上下文的下一个会话。
> **最后更新**：2026-07-24（v2 升级落地后）
> **本次会话范围**：下载 UI 设计 Skill → 治愈信笺风整站 v2 升级 → 写本交接文档

---

## TL;DR（先看这里）

- **项目**：植物养护 App「热带植物成长记」的高保真 HTML 原型，**4 种视觉风格**。
- **本次主目标**：`热带植物成长记_治愈信笺风.html` 的 v2 UI 升级（字体/配色/动画/组件），**已完成并验证**。
- **用户最新硬性偏好**：所有新功能/升级**只改治愈信笺风这一个文件**，其他 3 个原型作为基线保留，不要主动动。
- **当前 v2 升级位置**：`热带植物成长记_治愈信笺风.html` 内联的 `v2-1 ~ v2-20` 块（约 690 行）+ 独立备份 `skills/frontend-design/letter-v2-patch.css`。
- **本地预览**：`cd C:\Users\10008705\Desktop\私人\植物成长记; node server.js` → `http://localhost:3000/`。

---

## 1. 项目一句话总结

为「热带植物成长记」植物养护 App 制作**高保真 HTML 原型**，目前共 **4 种视觉风格**（其中"治愈信笺风"是本会话从零创建并完成 v2 升级的）。所有原型是单文件 HTML，可直接在浏览器打开。

- **主工作目录**：`C:\Users\10008705\Desktop\私人\植物成长记\`（Windows，中文路径）
- **本地预览**：`node server.js` → `http://localhost:3000/`
- **部署目标**：GitHub Pages（仓库 `https://github.com/HongGong1011/--UI-`）

---

## 2. 4 个原型文件清单

| 文件 | 风格 | 大小 | 切页机制 | 是否可改 |
|------|------|-----|---------|----------|
| `热带植物成长记_温暖手账风.html` | 温暖手账风 | 178.7 KB | 硬编码导航 | 🚫 基线 |
| `热带植物成长记_美式拼贴撕纸风.html` | 美式拼贴撕纸风 | 223 KB | JS 页面系统 | 🚫 基线 |
| `热带植物成长记_VisionPro风格.html` | Vision Pro 玻璃拟态 | 227.7 KB | JS 页面系统 | 🚫 基线 |
| `热带植物成长记_治愈信笺风.html` | **治愈信笺风** | **345 KB** | JS 页面系统 | ✅ **唯一工作目标** |

> **铁律**（来自 2026-07-22 用户指示 `6a604b86b99e15fc91ee4b9b`）：所有新功能/优化**只更新到治愈信笺风**。其他 3 个文件**作为基线保留**，不要主动改，除非用户明确说"也改某某"。

---

## 3. 治愈信笺风（本次工作核心）

### 3.1 视觉定位
**1910s 巴黎旧书信的珍藏柜** —— 火漆印章、邮票齿孔、活页装订、勃艮第红、纸张纤维纹理、Crimson Pro 衬线体。

### 3.2 v2 升级内容（本次新做）

| 维度 | 升级点 |
|------|--------|
| **字体（6 个）** | `ItalianaDisplay` / `CrimsonPro` / `Gloock` / `DMMono` / `NothingYouCouldDo` / `YoungSerif` |
| **配色（+11 ink token）** | 朱红系（#6B1F1F）、古铜系（#8B6F47）、苔藓系（#4A5D3A）、棕褐系（#3D2B1F） |
| **背景** | 主背景 `#F4EAD5` + SVG `feTurbulence` 噪点 + 4 层径向暖光 |
| **阴影（5 套）** | `--shadow-paper-flat / -card / -lift / -float / -wax` |
| **5 个核心动画** | `unfold`（信纸展开）/ `pageTurn`（翻页）/ `stampPress`（火漆盖章）/ `inkBleed`（墨水晕染）/ `paperFloatIn`（纸张飘入） |
| **9 个新组件类** | `.wax-seal-v2` / `.postmark-v2` / `.envelope-card` / `.letter-card` / `.stamp-v2` / `.sticky-note` / `.btn-letterpress` / `.btn-wax` / `.section-header-v2` |
| **自动覆盖** | `.bottom-nav`、12 个卡片类、所有 button 字体字距、`.tag-wax` / `.tag-leaf` 标签 |

### 3.3 集成关键细节（必读）

#### v2 patch 存放位置（**两版不一致**，改前看清楚）
- **独立备份**：`skills/frontend-design/letter-v2-patch.css`（630 行，使用原始字体名 `Gloock` / `DMMono`）
- **内联到 HTML**：`热带植物成长记_治愈信笺风.html` 的 `</style>` 之前约 690 行，标号 `v2-1 ~ v2-20`（**已重命名为 `GloockLocal` / `DMMonoLocal` 避免与外网字体冲突**）
- **修改原则**：**永远先改内联版**（这是真正生效的版本），独立版作为可读参考

#### 集成时已修复的 3 个 bug
1. ❌ 给 `.phone-screen` 加 `opacity:0` 起始动画 → ✅ 改为只对 `.phone.active .screen-content` 加
2. ❌ `v2PageEnter` 带 `rotate()` → ✅ 只保留 `translateY(6px → 0)`（rotate 让 screenshot 工具超时）
3. ❌ 覆盖 `h1/h2/h3` 字体 → ✅ 只覆盖 `.page-title / .screen-title / .section-title`

### 3.4 文件结构速查
```
热带植物成长记_治愈信笺风.html  (345 KB)
├─ <style>
│  ├─ [1-16]  原 v1 CSS（约 6470 行）
│  └─ [v2-1 ~ v2-20]  v2 升级补丁（约 690 行）  ← 想改 v2 找这里
├─ <body>
│  └─ 19 个 .phone 节点（19 个子页面）
│     - home / detail / add-record / reminders / calendar / event-list
│     - memorial / receipt / shelf / herbarium / species-guide
│     - polaroid / pest-guide / supply / wishlist / group-photo
│     - my-plants / more / discover / profile
└─ <script>
   ├─ navMap（tab 索引到 phone 索引的映射）
   ├─ switchPage(pageName) —— 核心切页
   ├─ highlightNav(pageName)
   └─ 80+ 业务函数
```

---

## 4. 当前页面系统（5 标签 19 子页面）

底部导航：🏠花园 / 🌱我的植物 / ✏️记录 / 📅养护日历 / 🔍发现

| 标签 | 子页面 |
|------|--------|
| 🏠 花园 | 日程、成长记录(拍立得)、心愿单、养护小组、植物大会(合照) |
| 🌱 我的植物 | 自定义模式、花友会模式、品种收藏模式(科属分组) |
| ✏️ 记录 | 添加植物(Phase 2)、添加记录 |
| 📅 养护日历 | 养护日历(31天网格+6色事件)、事件养护(养护小票)、养护提醒 |
| 🔍 发现 | 品种图鉴、病虫害图鉴、叶片诊断、药品药剂管理、植物社区、主页(个人中心)、**记忆纸箱** |

`navMap` 配置（v2 patch 不需要动这部分）：
```js
const navMap = {
  home:0, polaroid:0, 'group-photo':0, wishlist:0,
  'my-plants':1, detail:1, shelf:1,
  'add-record':2, 'add-plant':2,
  calendar:3, reminders:3, receipt:3, 'event-list':3,
  'species-guide':4, 'pest-guide':4, herbarium:4, supply:4, memorial:4, profile:4
};
```

---

## 5. 本会话完成的工作

1. **下载 2 个 UI 设计 Skill** → `skills/frontend-design/`（Anthropic 官方）+ `skills/ui-ux-pro-max/`（5 个子 skill）
2. **创建 v2 升级独立 patch** → `skills/frontend-design/letter-v2-patch.css`（630 行）
3. **集成到主文件** → 把 patch 内联到 `热带植物成长记_治愈信笺风.html` 的 `</style>` 之前
4. **修 3 个集成 bug**（opacity 破坏切页 / rotate 让截图超时 / h2 字体被覆盖）
5. **浏览器验证** → 启动 `node server.js`，4 个核心 tab 切换正常，4/6 字体加载成功，body 背景 `#F4EAD5` 生效，控制台无报错
6. **截图** → `screenshots/01-home.png`（其他 tab 截图工具超时，见第 6 节）

---

## 6. 当前已知问题

| 问题 | 严重度 | 说明 |
|------|--------|------|
| `screenshots/` 只截了首页 | 低 | `browser_take_screenshot` 在 v2 动画下超时。**解决**：用 `browser_evaluate` 执行 `await page.screenshot({path, fullPage})`，或先把动画临时关掉再截 |
| `letter-v2-patch.css` 独立版与内联版字体名不一致 | 低 | 独立版用 `Gloock` / `DMMono`、内联版用 `GloockLocal` / `DMMonoLocal`。**改 v2 永远改内联版** |
| 部分字体（`NothingYouCouldDo` / `YoungSerif`）未触发加载 | 无 | 字体已声明但当前元素未使用，按需加载机制正常 |
| 「记录」标签的"添加植物"是 Phase 2 占位 | 中 | 表单交互未完成，等用户要求时再补 |
| 「养护小组」「花友会模式」「叶片诊断」「植物社区」是占位 | 中 | 等用户要求时再做实际内容 |

---

## 7. 下一步建议（按优先级）

> ⚠️ **这些都是建议，等用户下指令再动手。**用户没明确说要做的话，不要主动开始。

### 高优先级
1. **修复截图工具**（用 `browser_evaluate` 绕过超时），补齐 5 个核心 tab 的对比截图
2. **是否同步 v2 到其他 3 个原型？** —— 需问用户。当前 v2 是治愈信笺风独占视觉语言，跨风格同步可能破坏其他风格的辨识度

### 中优先级（用户提了再做）
3. 「记录」标签"添加植物"表单完成
4. 「养护小组」「花友会模式」实际内容
5. 「叶片诊断」AI 识别
6. 「植物社区」功能

### 低优先级
7. 温暖手账风页面系统升级为 JS 切页（当前是硬编码导航）
8. 网络恢复后 push 到 GitHub

---

## 8. 完整文件清单

| 文件/目录 | 说明 |
|----------|------|
| `热带植物成长记_温暖手账风.html` | 温暖手账风原型（基线） |
| `热带植物成长记_美式拼贴撕纸风.html` | 美式拼贴撕纸风原型（基线） |
| `热带植物成长记_VisionPro风格.html` | Vision Pro 玻璃拟态原型（基线） |
| **`热带植物成长记_治愈信笺风.html`** | **治愈信笺风 v2 升级版（主工作文件）** |
| `index.html` | 旧入口页（3 种风格，**未含治愈信笺风**） |
| `原型预览/原型预览.html` | 新入口页（4 种风格 2×2 网格，**推荐用这个**） |
| `对比预览.html` | 3 种风格 iframe 并排对比（不含治愈信笺风） |
| `app.html` | 单页 app |
| `热带植物成长记_思维导图.html` | 交互式思维导图（5 模块 18 子页面） |
| `热带植物成长记_思维导图.xmind` / `.pdf` | 思维导图其他格式 |
| `高保真流程图.html` | 4 级架构 + 5 条数据流 + 18×5 导航矩阵 |
| `热带植物成长记_功能文档.docx` | 11 章 Word 功能文档 |
| `plant-photos/` | 8 张 AI 生成植物照片 |
| `plant-app-ia-analysis/` | 信息架构分析报告 + 67 个 canvas 字体 |
| `skills/frontend-design/SKILL.md` | frontend-design skill（Anthropic 官方） |
| **`skills/frontend-design/letter-v2-patch.css`** | **本次创建的 v2 升级独立 patch** |
| `skills/ui-ux-pro-max/` | UI/UX Pro Max skill（5 个子 skill） |
| `screenshots/01-home.png` | 治愈信笺风 v2 首页截图 |
| `conversation-recovery/conversation-recovery.html` | 已删除对话的恢复文档 |
| **`HANDOFF.md`** | **本交接文档** |
| `server.js` | 自定义 Node.js 本地服务器（绑定 `0.0.0.0:3000`） |

---

## 9. 踩过的坑（绝对不要再踩）

### 9.1 v2 集成（高危）
- **`.phone-screen` 上不能加 `opacity:0` 起始动画**：原 HTML 用 `.phone { display: none }` 切页，全局 opacity 起始 0 会让所有页面切过去后变白屏。**只对 `.phone.active .screen-content` 加**
- **CSS `transform: rotate()` 会让 screenshot 工具超时**：v2-18 动画最终只保留 `translateY`
- **不要覆盖 `h1/h2/h3` 字体**：原 h2 用 Georgia 是有意的副标题字体，覆盖会破坏标题层级。只覆盖 `.screen-title / .page-title` 这些 display 意图明确的类
- **字体 family 重名**：原 patch 用 `font-family: 'Gloock'`，与外网 Gloock 字体冲突，集成时已重命名为 `GloockLocal` / `DMMonoLocal`

### 9.2 文件操作
- **大文件读取限制**：4 个原型文件都超过 64KB（治愈信笺风 345KB），**不能一次性 Read**
  - 解法：`Grep` 搜索定位 + `Read` 分段读取（`offset`/`limit`）
- **PowerShell 不支持 `&&`**：用 `;` 替代
- **Windows 路径不区分大小写**，但 shell 命令可能敏感，写文件名时保持原样

### 9.3 本地服务器
- `serve` 命令在 Windows 上有兼容问题（`Unknown endpoint scheme`）
- **用项目自带的 `server.js`**，绑定 `0.0.0.0:3000`，支持手机同网访问
- **中文文件名跳转用 `window.location.href = '../xxx.html'` 相对路径最稳**
- 不要用 `browser_navigate` 传带中文文件名的 URL（工具自己的 URL 编码不一致，容易 404）

### 9.4 PowerShell 规则
- 单引号字面量、双引号会插值 → **路径优先用单引号**
- `New-Item` 不会自动创建父目录
- 命令链用 `;` 不是 `&&`
- 数字参数**不能传字符串**（`wait_ms_before_check: "5"` 会失败，要传数字 `5`）

### 9.5 Python 环境（如有需要）
- Windows 上 `ModuleNotFoundError: No module named 'encodings'` → 别折腾虚拟环境
- 用 `pip install --break-system-packages` 或直接用 Node.js

### 9.6 MCP 浏览器工具
- `browser_take_screenshot` 在 CSS transform 动画下可能 timeout → 用 `browser_evaluate` + `await page.screenshot({path, fullPage})` 绕过
- `browser_wait_for` 的 `time` 参数必须是数字不是字符串
- `fullPage: true` 必须是 boolean 不是字符串
- `evaluate` **必须用 `return` 显式返回值**，否则返回 `null`
- 截图不接受绝对路径，保存到 `%TEMP%\trae\screenshots\`，然后手动 `Copy-Item` 到目标位置

---

## 10. 关键决策记录（用户已明确说过的事）

| 日期 | 决策 | 证据 |
|------|------|------|
| 2026-07-22 | **所有新功能/优化只更新到治愈信笺风** | session memory `6a604b86b99e15fc91ee4b9b` |
| 2026-07-24 | 选用 v2 升级方向：排版字体/配色质感/交互动效/组件细节 | 用户在 v2 优化问卷中的选择 |
| 2026-07-24 | v2 升级落地后，本会话结束，要求写交接文档 | 当前 user message |

**推断的用户偏好**（非显式指令，作为新会话的参考）：
- 通信语言：中文
- 关心"质感""温度""细节"等感性指标
- 喜欢"新功能默认只在一处"的工作模式（避免四份文件散乱同步）

---

## 11. 项目记忆位置

- **项目级记忆**：`C:\Users\10008705\.trae-cn\memory\projects\-c-Users-10008705-Desktop---------\`
  - `20260721/ ~ 20260724/` 按日期文件夹
  - 每个文件夹下有 `session_memory_*.jsonl`（消息级）+ `topics.md`（主题摘要）
  - 当前 session：`6a632da8fc305d8ca982c459`
- **用户级记忆**：`C:\Users\10008705\.trae-cn\memory\user_profile.md`
  - 通信语言：中文
  - 图片要求：严格遵循指定标准

---

## 12. 新会话快速启动指南

```powershell
# 1. 进入项目目录（中文路径，必须单引号）
cd 'C:\Users\10008705\Desktop\私人\植物成长记'

# 2. 启动本地服务器（项目自带 server.js）
node server.js
# 输出：Server running at http://localhost:3000/

# 3. 浏览器跳转（避免中文文件名 URL 编码问题）
#    直接打开：原型预览/原型预览.html
#    或在浏览器 console：window.location.href = '../热带植物成长记_治愈信笺风.html'
```

**接到新任务时的判断流程**：
1. **用户说"继续优化治愈信笺风 / 加 v3 / 改 v2 某处"** → 在 `热带植物成长记_治愈信笺风.html` 的 `v2-1 ~ v2-20` 块改
2. **用户说"同步到其他 3 个原型"** → 移植 v2 patch，**先确认用户真的想要**（可能破坏其他风格的辨识度）
3. **用户说"加新功能"** → 按 2026-07-22 之后的规则，**只在治愈信笺风里加**
4. **用户说"截图""对比""验证"** → 用 `browser_evaluate` + `await page.screenshot()`，不要直接用 `browser_take_screenshot`
5. **用户什么都没说就让你干活** → 先停下来问清楚要做什么

---

*本会话最后做的事：写这份交接文档*
*时间：2026-07-24*
