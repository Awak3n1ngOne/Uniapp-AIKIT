# Conversation 对话容器

对话容器组件，用于承载消息列表、滚动控制和空状态展示。支持传统模式和虚拟列表模式。

## 引入

```ts
import {
  AiConversation,
  AiConversationContent,
  AiConversationScrollButton,
  AiConversationEmptyState,
  AiConversationNewMessage,
} from '@/uni_modules/aiko-ai-elements/components/conversation'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiConversation` | 对话容器，提供上下文 |
| `AiConversationContent` | 消息内容区域，支持虚拟列表 |
| `AiConversationScrollButton` | 滚动到底部按钮 |
| `AiConversationEmptyState` | 空状态展示 |
| `AiConversationNewMessage` | 新消息提示按钮 |

## AiConversation

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `messages` | `UIMessage[]` | `[]` | 消息列表（虚拟列表模式） |
| `virtualized` | `boolean` | `false` | 是否启用虚拟列表 |

### UIMessage 类型

```ts
interface UIMessage {
  id: string
  from: 'user' | 'assistant'
  content: string
  reasoning?: string
  tools?: any[]
  sources?: any[]
}
```

### Expose

| 方法 | 说明 |
|------|------|
| `onNewMessage(streaming?)` | 新消息到达时调用 |
| `onStreamUpdate()` | 流式消息更新时调用 |

## AiConversationContent

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 消息内容，虚拟列表模式下提供 `{ item, index }` |

## AiConversationEmptyState

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `icon` | `string` | - | 图标 |
| `title` | `string` | - | 标题（必填） |
| `description` | `string` | - | 描述 |

## 使用示例

### 传统模式

```vue
<template>
  <AiConversation>
    <AiConversationContent>
      <AiConversationEmptyState
        v-if="messages.length === 0"
        title="开始新对话"
        description="输入消息开始与 AI 对话"
      />
      <AiMessage
        v-for="msg in messages"
        :key="msg.id"
        :from="msg.from"
      >
        <AiMessageContent>
          <AiMessageResponse :content="msg.content" />
        </AiMessageContent>
      </AiMessage>
    </AiConversationContent>
    <AiConversationScrollButton />
  </AiConversation>
</template>
```

### 虚拟列表模式（大数据量）

```vue
<template>
  <AiConversation :messages="messages" virtualized>
    <AiConversationContent v-slot="{ item }">
      <AiMessage :from="item.from">
        <AiMessageContent>
          <AiMessageResponse :content="item.content" />
        </AiMessageContent>
      </AiMessage>
    </AiConversationContent>
    <AiConversationScrollButton />
    <AiConversationNewMessage />
  </AiConversation>
</template>
```
