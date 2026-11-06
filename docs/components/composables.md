# Composables 函数

AI Elements 提供的组合式函数。

## 引入

```ts
import {
  useAIChat,
  useConversationScroll,
  useMarkdownStream,
  useMessageBranch,
  usePromptInputAttachments,
  useTheme,
  useVirtualList,
  usePromptForm,
} from '@/uni_modules/aiko-ai-elements/composables'
```

## 函数列表

| 函数 | 说明 |
|------|------|
| `useVirtualList` | 虚拟列表 |
| `useConversationScroll` | 对话滚动控制 |
| `useMarkdownStream` | Markdown 流式渲染 |
| `useAIChat` | AI Chat 数据适配 |
| `useMessageBranch` | 消息分支管理 |
| `usePromptInputAttachments` | 输入框附件管理 |
| `useTheme` | 主题色与暗色模式 |
| `usePromptForm` | 高级表单状态 |
| `createPromptInputAttachments` | 创建独立附件 API（非 inject） |

## useVirtualList

虚拟列表核心逻辑，支持大数据量渲染。

### 参数

```ts
interface VirtualListOptions {
  items: Ref<VirtualListItem[]>      // 数据源
  containerHeight: Ref<number>        // 容器高度
  scrollTop: Ref<number>              // 滚动位置
  estimatedHeight?: {                 // 预估高度
    user?: number
    assistant?: number
  }
  bufferSize?: number                 // 缓冲区大小，默认 5
  itemGap?: number                    // 间距（rpx）
}
```

### 返回值

```ts
{
  visibleItems: ComputedRef<VirtualListItem[]>  // 可见项
  startIndex: ComputedRef<number>               // 起始索引
  endIndex: ComputedRef<number>                 // 结束索引
  topPlaceholderHeight: ComputedRef<number>     // 顶部占位高度
  bottomPlaceholderHeight: ComputedRef<number>  // 底部占位高度
  totalHeight: ComputedRef<number>              // 总高度
  gapPx: number                                 // 间距（px）
  measureItem: (id: string, height: number) => void   // 测量单项
  measureItems: (measurements: Map<string, number>) => void  // 批量测量
  consumeHeightDelta: () => number              // 消费高度变化
}
```

### 示例

```ts
import { useVirtualList } from '@/uni_modules/aiko-ai-elements/composables/useVirtualList'

const containerHeight = ref(0)
const scrollTop = ref(0)

const virtualList = useVirtualList({
  items: messagesRef,
  containerHeight,
  scrollTop,
  estimatedHeight: { user: 80, assistant: 200 },
  bufferSize: 5,
})
```

## useConversationScroll

对话滚动控制，支持自动跟随和暂停。

### 参数

```ts
interface ConversationScrollOptions {
  containerHeight: Ref<number>   // 容器高度
  totalHeight: Ref<number>       // 总内容高度
  consumeHeightDelta: () => number  // 高度变化消费函数
}
```

### 返回值

```ts
{
  scrollTop: Ref<number>               // 滚动位置
  isAtBottom: Readonly<Ref<boolean>>   // 是否在底部
  followState: Readonly<Ref<'auto' | 'paused'>>  // 跟随状态
  hasNewMessages: Readonly<Ref<boolean>>  // 是否有新消息
  scrollToBottom: () => void           // 滚动到底部
  handleScroll: (e) => void            // 滚动事件处理
  onNewMessage: (streaming?: boolean) => void  // 新消息回调
  onStreamUpdate: () => void           // 流式更新回调
  onResumeFromNewMessage: () => void   // 恢复跟随
  enableAutoFollow: () => void         // 启用自动跟随
  pauseAutoFollow: () => void          // 暂停自动跟随
}
```

### 示例

```ts
import { useConversationScroll } from '@/uni_modules/aiko-ai-elements/composables/useConversationScroll'

const scrollControl = useConversationScroll({
  containerHeight,
  totalHeight: virtualList.totalHeight,
  consumeHeightDelta: virtualList.consumeHeightDelta,
})

// 新消息到达
scrollControl.onNewMessage(true)

// 滚动到底部
scrollControl.scrollToBottom()
```

## useMarkdownStream

Markdown 流式渲染。

### 参数

```ts
interface MarkdownStreamOptions {
  debounceMs?: number              // 防抖延迟（默认 80ms）
  parseIncompleteMarkdown?: boolean // 流式时补全未闭合 ```（默认 true）
  onBlockUpdate?: (blocks: ContentBlock[]) => void  // 块更新回调
}
```

### 返回值

```ts
{
  contentBlocks: Readonly<Ref<ContentBlock[]>>  // 内容块列表
  rawMarkdown: Readonly<Ref<string>>             // 原始 Markdown
  isStreaming: Readonly<Ref<boolean>>            // 是否流式中
  appendChunk: (chunk: string) => void           // 追加增量文本
  syncContent: (content: string, streaming: boolean) => void  // 同步全文（推荐用于 v-model）
  setParseIncompleteMarkdown: (enabled: boolean) => void
  finalize: () => void                           // 完成渲染
  reset: () => void                              // 重置
}
```

### 示例

```ts
import { useMarkdownStream } from '@/uni_modules/aiko-ai-elements/composables/useMarkdownStream'

const { contentBlocks, appendChunk, finalize, reset } = useMarkdownStream()

// 流式追加内容
function onStreamChunk(chunk: string) {
  appendChunk(chunk)
}

// 完成渲染
function onStreamEnd() {
  finalize()
}
```

## useAIChat

AI Chat 数据适配器，将 AI SDK 数据映射为 UI 数据。

### 参数

```ts
interface AIChatOptions {
  messages: Ref<AIMessage[]>    // 原始消息
  input: Ref<string>            // 输入值
  status: Ref<string>           // 状态
  setInput: (value: string) => void
  append: (message: any) => Promise<any>
  reload: () => Promise<any>
  stop: () => void
}
```

### 返回值

```ts
{
  uiMessages: ComputedRef<UIMessage[]>   // UI 消息
  inputText: ComputedRef<string>          // 输入文本
  submitStatus: ComputedRef<string>       // 提交状态
  handleSubmit: (data: { text: string }) => void
  handleStop: () => void
}
```

### 示例

```ts
import { useAIChat } from '@/uni_modules/aiko-ai-elements/composables/useAIChat'
import { useChat } from '@ai-sdk/vue'

const chat = useChat({ api: '/api/chat' })

const { uiMessages, handleSubmit, handleStop } = useAIChat({
  messages: chat.messages,
  input: chat.input,
  status: chat.status,
  setInput: chat.setInput,
  append: chat.append,
  reload: chat.reload,
  stop: chat.stop,
})
```

## useMessageBranch

消息分支管理。

### 参数

```ts
defaultBranch?: number  // 默认分支索引，默认 0
```

### 返回值

```ts
{
  currentBranch: Readonly<Ref<number>>  // 当前分支
  setBranch: (index: number) => void    // 设置分支
}
```

### 示例

```ts
import { useMessageBranch } from '@/uni_modules/aiko-ai-elements/composables/useMessageBranch'

const { currentBranch, setBranch } = useMessageBranch(0)

// 切换到第一个分支
setBranch(0)

// 切换到第二个分支
setBranch(1)
```

## usePromptInputAttachments

输入框附件管理。

### 返回值

```ts
{
  attachments: Ref<AttachmentData[]>
  add: (files: File[] | AttachmentData[]) => void
  remove: (id: string) => void
  clear: () => void
  openFileDialog: (options?: { count?: number; type?: 'all' | 'image' | 'video' | 'file' }) => void
}
```

在 `AiPromptInput` 子树内调用时，各组件共享同一份 `attachments` 状态。

### 示例

```ts
import { usePromptInputAttachments } from '@/uni_modules/aiko-ai-elements/composables/usePromptInputAttachments'

const { attachments, add, remove, openFileDialog } = usePromptInputAttachments()
```

## useTheme

主题色与暗色模式。

### 返回值

```ts
{
  theme: Ref<string>           // 当前主题色 id
  isDark: Ref<boolean>
  setThemeColor: (id: string) => void  // blue | violet | emerald | rose | amber | cyan | pink | slate
  toggleDark: () => void
}
```

### 示例

```ts
import { useTheme } from '@/uni_modules/aiko-ai-elements/composables'

const { setThemeColor, toggleDark } = useTheme()
setThemeColor('violet')
toggleDark()
```

## usePromptForm

高级 Prompt 表单状态（与 `AiPromptForm` 配合）。在表单子树内通过 inject 共享。

```ts
import { usePromptForm } from '@/uni_modules/aiko-ai-elements/composables'

const form = usePromptForm()
```
