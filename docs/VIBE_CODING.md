# AIKO Agent Kit · Vibe Coding 契约

你是 uni-app Vue 3 前端开发者。先读本文件，再读 `component-manifest.json`，最后读将要使用的组件源码与类型。这里的“Agent”指产品里的智能体界面；“编码 Agent”指帮助开发者写代码的工具。

## 1. 开始前写清楚

用五句话说明：目标用户、要完成的动作、目标平台、后端协议、可验证的完成行为。未给后端时先使用本地 Demo Transport，并在界面明确标注“离线模拟”。视觉默认 AIKO Studio；保留已有用户改动，不重置工作区。

## 2. 用已有组件表达需求

| 场景 | 首选 | 导入路径（相对插件目录） |
| --- | --- | --- |
| 最快做一个完整会话页 | AiAgentSession | `components/agent/AiAgentSession.vue` |
| 自定义会话状态与布局 | useAgent | `composables/useAgent.ts` |
| 输入、发送、停止 | AiAgentComposer | `components/agent/AiAgentComposer.vue` |
| 工具输入、结果、审批 | AiAgentTool | `components/agent/AiAgentTool.vue` |
| 运行状态 | AiAgentStatus | `components/agent/AiAgentStatus.vue` |
| 跨端主题根节点 | AiTheme / useTheme | `components/theme/AiTheme.vue` / `composables/useTheme.ts` |
| 富文本回复 | AiMessageResponse | `components/message/AiMessageResponse.vue` |
| 复杂输入、附件、模式菜单 | AiPromptFormComposer | `components/prompt-form/AiPromptFormComposer.vue` |
| 计划、来源、引用、代码等 | 读清单后按需导入 | `component-manifest.json` |

禁止编造组件、props、events 或安装命令。优先单文件按需导入，避免小程序导入整个组件库。根入口 `index.ts` 便于发现 API，不代表应在移动端全量打包。基础组件仍保持原来的组合方式。

## 3. 可复制的最小页面

把整个 `aiko-ai-elements` 目录放入项目 `uni_modules`。本仓库对应 `src/uni_modules`。宿主安装 `vue`（Vue 3）、`markdown-it`、`highlight.js`；SCSS 构建需要 `sass`。H5 编译 AgentSession / Markdown 还需安装 `mermaid`，运行时按需加载；`vue-virtual-scroller` 仅原有可选 H5 Conversation 集成需要。不要让编码 Agent 虚构已发布的 npm 包。

```vue
<template>
  <AiTheme>
    <view class="agent-page">
      <AiAgentSession :transport="transport" title="我的 Agent"
        notice="离线交互演示 · 不调用模型 · 不执行真实工具" />
    </view>
  </AiTheme>
</template>
<script setup lang="ts">
import AiTheme from '@/uni_modules/aiko-ai-elements/components/theme/AiTheme.vue'
import AiAgentSession from '@/uni_modules/aiko-ai-elements/components/agent/AiAgentSession.vue'
import { createDemoAgentTransport } from '@/uni_modules/aiko-ai-elements/agent/demo'
const transport = createDemoAgentTransport()
// initTheme() 在宿主 App.vue 的 onLaunch 中调用一次，见下文。
</script>
<style scoped>
.agent-page { height: calc(100vh - var(--window-top, 0px)); }
</style>
```

宿主 `App.vue`：

```ts
import { onLaunch } from '@dcloudio/uni-app'
import { useTheme } from '@/uni_modules/aiko-ai-elements/composables/useTheme'
const { initTheme } = useTheme()
onLaunch(initTheme)
```

SCSS 原子组件会引用 `$ai-*`。宿主 `uni.scss` 增加：

```scss
@import '@/uni_modules/aiko-ai-elements/common/variables.scss';
```

使用已有字体图标时，在 `App.vue` 全局样式引入 `common/remixicon.scss`。AiTheme 自带全局主题变量。实际页面必须有 AiTheme 根节点：小程序和 App 的逻辑层没有可操作的 DOM，不能靠给 `document.body` 加类实现跨端主题。

## 4. 会话状态契约

`useAgent({ transport, initialMessages? })` 返回：

| API | 行为 |
| --- | --- |
| `messages` / `status` / `error` | Vue refs；界面读取，不手动篡改运行状态 |
| `isRunning` / `isBusy` / `pendingApprovals` | computed；运行中或有未决审批时拒绝新发送 |
| `send(text): Promise<boolean>` | 去除两端空白；空输入/忙碌返回 false；创建 user+assistant，完成后返回 true；传输错误写入 error/status |
| `stop()` | 同步终止、清理连接；已有文字保留；隔离迟到事件；待审批工具标为拒绝 |
| `respondToTool(id, approved): Promise<boolean>` | 只能处理当前待确认工具；所有决定收齐后，把决定随同一 assistant 的历史发给服务端继续 |
| `retry(): Promise<boolean>` | 仅错误/停止且本轮没有工具调用时可重试；复用消息和 turnId，防止用户消息重复 |
| `clear()` | 终止旧请求并清空会话 |

主要路径：`idle → submitted → streaming → ready`；需要批准时结束为 `awaiting-approval`；决定后再进入 `submitted`；任意运行可停止为 `stopped`，错误为 `error`。有工具的失败轮不自动重放；界面提示新建对话，避免重复执行副作用。

Transport 必须同步返回 cleanup，最终调用 resolve/reject，或 emit finish/error。每个实例仅允许一个运行；Vue effect scope 销毁时自动停止。在组件外创建实例，调用者负责 stop。会话历史只保存在内存；`initialMessages` 是副本初始化，可恢复待审批展示，服务端授权必须重新验证。它不表示持久化、断线续传或跨设备同步。

`AiAgentSession` props：`transport` 必填；`title`、`description`、`suggestions: string[]`、`notice` 可选。暴露 `messages/status/send/stop/clear/retry/respondToTool`。它是起步组合组件，不包含模型选择、附件上传或语音识别。换 transport 会清空会话。

`AiAgentComposer`：`v-model` 为字符串；`running` 控制停止按钮；`disabled` 控制输入与发送；`placeholder`、`maxLength` 可选；发出 `submit(text)` / `stop()`；`toolbar` 插槽可扩展提示。生成期间可编辑下一条草稿；不拦截中文输入法 Enter。移动端点击发送，避免多行输入和输入法确认冲突。

`AiAgentTool`：`tool: AgentTool`，可选 `disabled`，发出 `respond(id, approved)`。`AiAgentStatus`：`status: AgentStatus`。所有类型以 `agent/types.ts` 为准。

旧 `useAIChat` 保留，它是外部状态映射适配器，不是请求客户端，也不保证兼容所有版本的 `@ai-sdk/vue`。不要把它当作本次新增的会话运行时。

## 5. 网络、协议和工具执行

| Transport | 目标 | 线格式 |
| --- | --- | --- |
| `createDemoAgentTransport()` | 本地交互、全部目标端 | 定时事件；不联网 |
| `createUniRequestTransport({ url, headers?, timeout? })` | H5 / App-vue / 小程序 | POST JSON，响应 `{ events: AgentEvent[] }`；缓冲完成后呈现，不冒充实时流 |
| `createUniSocketTransport({ url, headers?, timeout? })` | 支持 SocketTask 的目标端 | 打开连接后发送 JSON；每个服务端文本帧恰好一个 AgentEvent |
| `createH5SSETransport({ url, headers?, timeout? })` | 支持 fetch stream 的 H5 | POST，`text/event-stream`；一个 SSE data 事件对应一个 AgentEvent |
| 自定义 `AgentTransport` | 原生 SSE、服务商 SDK 等 | 由适配层转换为 AgentEvent |

生产端使用 HTTPS / WSS；小程序配置 request/socket 合法域名，H5 配置 CORS。WebSocket 浏览器不能自定义鉴权 header：使用安全同站 Cookie 或服务端签发的短期一次性连接 ticket，不把模型 Key 放进 URL。超时默认 60 秒，是本轮总时限。

```ts
import { createUniSocketTransport } from '@/uni_modules/aiko-ai-elements/agent/transports'
const transport = createUniSocketTransport({ url: 'wss://your-server.example/agent' })
// JSON 接入可换为 createUniRequestTransport({ url: 'https://your-server.example/api/agent' })
```

所有生产请求的 body 为 `{ turnId, messages }`。messages 是 UI 状态快照；后端需要转换为自己的模型协议，处理末尾空 assistant。服务器必须将 turnId 与认证用户、服务端会话绑定，做输入验证和幂等检查。相同 turnId 的批准续跑和“重试文本”必须由服务端状态机区分；不能只用 turnId 缓存整轮结果。前端历史、tool.id 和“已批准”标记均不可信。

协议示例：

```json
{"type":"reasoning-delta","delta":"准备计划…"}
{"type":"text-delta","delta":"这里是回复。"}
{"type":"tool-call","id":"call-1","name":"保存草稿","input":{"title":"计划"},"requiresApproval":true}
{"type":"finish"}
```

审批续跑时，服务端验证工具属于本会话、输入未被修改且用户有权限。批准才执行，拒绝则不执行。批准的结果返回 `{"type":"tool-result","id":"call-1","output":{...}}`；失败用 `tool-error`；不要再次发相同 ID 的 tool-call。`source` 需要 HTTP(S) URL；致命失败用 `error`；每轮正常流用 `finish` 结束。`finish` 之前必须结束所有 running/approved 工具；可以留 approval-required，表示等待决定。

SSE 使用 `data: {"type":"text-delta","delta":"你好"}\n\n`，最终 `data: {"type":"finish"}\n\n` 或 `[DONE]`。适配器支持拆包、多行 data、CRLF 和 UTF-8 分片；缺失结束事件会报错。它不直接解析 OpenAI/Anthropic/AI SDK Data Stream 原始协议，不承诺自动识别服务商。不要对 `uni.request.onChunkReceived` 做“所有 uni-app 端都支持 SSE”的假设。

## 6. 视觉与跨端规范

- 基础色：纸面 `#F2F0E9`，墨色 `#12100D`，强调 `#DEF04B`，深色卡片 `#121510`。绿底按钮用黑字，浅底正文不用荧光绿；文字强调用深橄榄色。
- 组件使用 `--ai-*` 语义变量；品牌示意卡可以固定墨色和绿；不向业务页面散落蓝紫渐变、重阴影和 emoji 图标。
- 以 375px 移动视口为基准，间距保持 4px 节奏；常用尺寸用 rpx，点击目标至少 44px，正文 14–16px；大标题、留白、粗细对比优先。
- 可复用 UI 用 view/text/button/textarea/scroll-view。DOM、Clipboard、File、MediaDevices、iframe 等浏览器能力仅出现在 H5 条件编译分支；App renderjs 放在视图层，不能在逻辑层访问 document。
- App 目标为 Vue WebView；不宣称支持 nvue 或 uni-app-x/UTS。高级功能按 `COMPATIBILITY.md` 的边界降级。
- 为发送、停止、拒绝和错误恢复提供明确控件；状态使用文字而非只用颜色；textarea 支持多行和中文输入法；安全区 `env(safe-area-inset-bottom)`；H5 键盘焦点可见。
- Markdown 默认转义原始 HTML。不要直接 v-html 输出未验证的模型原文，不执行模型返回的 JS/Vue 模板。预览组件只接入可信的业务定义。
- 新功能先明确状态，再写 UI；计时器、请求、Socket 和监听器都要清理；多实例会话不能共享消息或连接；不因滚动到历史而强制拉回底部。

## 7. 交付清单

1. 读真实组件 API；最小实现跑通成功、空状态、生成中、停止、错误、审批接受/拒绝。
2. `npm run type-check`；`npm test`；`npm run check:catalog`。
3. `npm run build:h5`；`npm run build:mp-weixin`；`npm run build:app`；改支付宝特性还要跑 `build:mp-alipay`。
4. 新增/删除导出或页面时运行 `npm run catalog`，同步清单、入口、示例与文档。
5. H5 实际交互检查；微信开发者工具检查；Android/iOS 真机检查按实际执行记录。不能以编译成功替代真机验收。
6. 回复说明改动、验证、限制；未配置后端时明确“离线演示，尚未接入真实模型”。未授权不要发布、推送或变更收费配置。

## 8. 给编码 Agent 的提示词

> 使用 uni-app Vue 3 和 AIKO Agent Kit 做一个面向【目标用户】的【场景】Agent 页面。目标端为【微信小程序 / App-vue / H5】。先阅读 AGENTS.md、VIBE_CODING.md、component-manifest.json，再按需读取实际组件类型。按 AIKO Studio 视觉实现，先用 Demo Transport 验证，再接【后端地址与线协议】。完成发送、流式呈现、停止、错误、工具确认与安全区；执行检查命令，报告未验证的目标端。
