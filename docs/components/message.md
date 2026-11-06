# Message 消息组件

消息气泡组件，用于展示用户和 AI 的对话消息。

## 引入

```ts
import {
  AiMessage,
  AiMessageContent,
  AiMessageResponse,
  AiMessageActions,
  AiMessageAction,
  AiMessageBranch,
  AiMessageBranchSelector,
  AiMessageToolbar,
} from '@/uni_modules/aiko-ai-elements/components/message'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiMessage` | 消息容器，控制布局方向 |
| `AiMessageContent` | 消息气泡内容区 |
| `AiMessageResponse` | AI 回复内容，支持 Markdown 流式渲染 |
| `AiMessageActions` | 消息操作按钮组 |
| `AiMessageAction` | 单个操作按钮 |
| `AiMessageBranch` | 消息分支容器 |
| `AiMessageBranchSelector` | 分支选择器 |
| `AiMessageToolbar` | 消息工具栏 |

## AiMessage

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `from` | `'user' \| 'assistant'` | - | 消息来源（必填） |

### 布局规则

- `from="user"`：右对齐，`align-self: flex-end`
- `from="assistant"`：左对齐，`align-self: flex-start`

## AiMessageContent

消息气泡容器，根据 `from` 自动应用不同样式。

### 样式差异

| 来源 | 背景 | 边框 | 圆角 |
|------|------|------|------|
| user | accent-light | 无 | 右下角小圆角 |
| assistant | 白色 | 有 | 左下角小圆角 |

## AiMessageResponse

AI 回复内容渲染器，集成 Markdown 流式渲染。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `content` | `string` | - | Markdown 内容 |
| `streaming` | `boolean` | 自动推断 | 流式中请设为 `true`，结束后 `false`；省略时根据 content 前缀增长推断 |
| `parseIncompleteMarkdown` | `boolean` | `true` | 流式时是否为未闭合 ``` 补全闭合符 |

## AiMessageActions

消息操作按钮容器，默认右对齐。

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 操作按钮 |

## AiMessageAction

单个操作按钮。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `label` | `string` | - | 按钮文字 |
| `icon` | `string` | - | 图标 |
| `tooltip` | `string` | - | 提示文字 |

### Events

| 事件 | 说明 |
|------|------|
| `click` | 点击事件 |

## AiMessageBranch

消息分支容器。通过作用域插槽拿到当前分支索引，自行渲染对应内容。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `branchCount` | `number` | — | 分支总数（必填） |
| `defaultBranch` | `number` | `0` | 初始分支索引 |

### Events

| 事件 | 载荷 | 说明 |
|------|------|------|
| `branchChange` | `index: number` | 分支切换 |

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 作用域 `{ branch }`，当前分支索引 |

## AiMessageBranchSelector

分支切换器（‹ n / N ›）。**必须放在 `AiMessageBranch` 内部**（依赖 inject）；`branchCount > 1` 时才显示。无独立 props。

## AiMessageToolbar

消息底部工具栏，通常同时放置 `AiMessageActions` 与 `AiMessageBranchSelector`。

## 使用示例

### 基础消息

```vue
<AiMessage from="user">
  <AiMessageContent>
    你好，请介绍一下自己
  </AiMessageContent>
</AiMessage>

<AiMessage from="assistant">
  <AiMessageContent>
    <AiMessageResponse :content="aiResponse" />
  </AiMessageContent>
  <AiMessageActions>
    <AiMessageAction label="复制" @click="handleCopy" />
    <AiMessageAction label="重新生成" @click="handleRegenerate" />
  </AiMessageActions>
</AiMessage>
```

### 带分支的消息

```vue
<AiMessage from="assistant">
  <AiMessageContent>
    <AiMessageBranch :branch-count="3" :default-branch="0" @branch-change="onBranchChange">
      <template #default="{ branch }">
        <AiMessageResponse :content="responses[branch]" />
      </template>
    </AiMessageBranch>
  </AiMessageContent>
  <AiMessageToolbar>
    <AiMessageActions>
      <AiMessageAction label="复制" @click="handleCopy" />
    </AiMessageActions>
    <!-- BranchSelector 须在 Branch 内部；若放在 Toolbar，请把 Branch 包住 Toolbar，或把 Selector 放进 Branch 插槽内 -->
  </AiMessageToolbar>
</AiMessage>
```

推荐把选择器与内容放在同一 `AiMessageBranch` 内：

```vue
<AiMessageBranch :branch-count="responses.length" :default-branch="0">
  <template #default="{ branch }">
    <view>
      <AiMessageResponse :content="responses[branch]" />
      <AiMessageBranchSelector />
    </view>
  </template>
</AiMessageBranch>
```
