# 平台边界

目标是 **uni-app Vue 3：H5、App-vue、Vue 小程序**。没有把 uni-app-x / UTS / nvue 当作已支持的平台。最终执行证据见 [VALIDATION.md](./VALIDATION.md)，本表描述实现能力。

| 能力 | H5 | 微信/支付宝小程序 | App-vue |
| --- | --- | --- | --- |
| Agent Session / Composer / Tool / Status | 共用组件 | 共用组件 | 共用组件 |
| AiTheme + Studio 明暗变量 | 节点继承，兼容浏览器根节点 | 节点 class 继承 | 节点 class 继承 |
| 离线演示 | 定时器模拟 | 同样逻辑 | 同样逻辑 |
| JSON 请求 | uni.request；跨域受 CORS 限制 | 合法 request 域名 | uni.request；宿主网络配置 |
| WebSocket 实时事件 | uni.connectSocket；不能自定义 header | 合法 socket 域名与基础库支持 | uni.connectSocket |
| POST SSE | fetch stream + TextDecoder + AbortController | 未提供内置分块适配；使用 Socket / JSON 或自定义 Transport | 未提供内置原生 SSE；使用 Socket / JSON 或原生插件适配 |
| Markdown / 代码 | 共用解析、H5 渲染 | rich-text，样式与交互按平台降级 | renderjs，WebView |
| Mermaid | 动态加载，strict 模式 | 代码内容降级 | 现有 renderjs 路径；需宿主环境验证，不视为本次已验收 |
| 虚拟列表 | 原有滚动实现 / 可选第三方插件 | 原有 scroll-view 实现 | 原有 scroll-view 实现 |
| WebPreview | iframe，受目标站点 CSP/X-Frame 限制 | 链接卡片；宿主提供 webview 路由或复制链接 | 同左，宿主负责合法链接与页面 |
| VuePreview | 限定标签模板 → Vue 组件树 | 明确提示不支持动态预览，并显示模板原文 | 现有 Vue render 路径，未真机验收 |
| JSXPreview | 限定卡片标记 → rich-text | 同样限定标记；样式按平台降级 | 同左；不是执行任意 React/JSX |
| MicSelector / VoiceSelector | 展示宿主提供的数据并发事件 | 同左 | 同左 |
| PromptForm 语音控件 | UI 状态与 start/end 事件 | 同左 | 同左 |
| 实际录音、ASR、实时语音 | 需要宿主适配 | 需要宿主权限与录音 API 适配 | 需要原生/宿主适配 |
| 附件 | 选择/展示；业务上传需宿主实现 | 选择受平台 API 限制；业务上传需宿主实现 | 同左 |

## 接入要求

1. 宿主 uni-app 项目已经安装 Vue 3 与相应 DCloud 编译器；拷贝完整 `uni_modules/aiko-ai-elements`，按需导入文件。
2. Markdown 依赖 `markdown-it`、`highlight.js`。H5 编译 `AiAgentSession` / Markdown 时还需要安装 `mermaid`（运行时按需加载）。SCSS 需要 `sass`。`vue-virtual-scroller` 仅现有 H5 可选 Conversation 集成需要。
3. 在 App.vue 调用 `useTheme().initTheme()` 一次；页面用 AiTheme；使用旧 SCSS 组件时在 uni.scss 导入 variables.scss。主题不跨原生窗口自动共享；宿主嵌入到其他窗口需要自行同步。
4. 后端使用本文档协议；本项目没有内置代理服务器或供应商 Key 管理。WebSocket 在 H5 不能依赖自定义 header；用安全同站 Cookie 或短期 ticket。HTTP headers 仅存业务登录凭证。
5. 不将需要浏览器 API 的库无条件导入小程序或 App 逻辑层。AiAgentSession 没有自动读取设备、上传附件或执行工具。

官方语义参考：[uni.request](https://uniapp.dcloud.net.cn/api/request/request)、[WebSocket](https://uniapp.dcloud.net.cn/api/request/websocket.html)。不同目标端与基础库版本的实现仍需实际验证。

## 包体积与性能

组件库按需导入。演示工程包含所有示例、代码高亮语言、字体和可选媒体，并不等于最小业务包。示例已把 `pages/demos` 注册为分包，首页与指南为主包；`npm run check:mp-size` 对构建输出执行每包 2 MiB 的保守工程预算检查。发布自己的小程序时仍应只注册需要的页面，并按目标平台限制分包。

`main.ts` 不再把 Mermaid 挂到 window；H5 Mermaid 组件在需要图表时动态加载。新 AgentSession 滚动监听仅跟踪当前消息长度、工具状态与会话状态，不在每个 delta 上序列化整个历史。它是普通滚动会话容器，不是无限历史虚拟列表；长历史产品应组合原有虚拟列表、分页与服务端历史。

主题配色遵循参考图；绿底黑字，浅底正文使用深色。主题/字体渲染与软键盘高度差异需要各端验收，不能以截图代表系统键盘行为。
