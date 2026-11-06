# Persona 助手形象组件

AI 助手形象/头像组件，支持状态动画。

## 引入

```ts
import { AiPersona } from '@/uni_modules/aiko-ai-elements/components/persona'
```

## AiPersona

AI 助手形象组件，显示不同状态的动画效果。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `status` | `'idle' \| 'thinking' \| 'speaking'` | `'idle'` | 状态 |
| `src` | `string` | - | 自定义头像图片 |
| `size` | `number` | `64` | 尺寸（rpx） |

### 状态说明

| 状态 | 效果 |
|------|------|
| `idle` | 静态显示 |
| `thinking` | 脉冲光环动画 |
| `speaking` | 活跃状态动画 |

## 使用示例

### 基础用法

```vue
<AiPersona status="idle" />
```

### 思考状态

```vue
<AiPersona status="thinking" />
```

### 自定义头像

```vue
<AiPersona
  status="speaking"
  src="/images/assistant-avatar.png"
  :size="80"
/>
```

### 在对话中使用

```vue
<template>
  <view class="chat-header">
    <AiPersona :status="aiStatus" />
    <text>AI 助手</text>
  </view>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps<{
  isStreaming: boolean
  isThinking: boolean
}>()

const aiStatus = computed(() => {
  if (props.isStreaming) return 'speaking'
  if (props.isThinking) return 'thinking'
  return 'idle'
})
</script>
```

### 在消息中使用

```vue
<AiMessage from="assistant">
  <view class="message-header">
    <AiPersona :status="messageStatus" :size="48" />
  </view>
  <AiMessageContent>
    <AiMessageResponse :content="response" />
  </AiMessageContent>
</AiMessage>
```
