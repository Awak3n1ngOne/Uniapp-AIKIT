# PromptForm 输入组件

本组件库的**唯一** Prompt 输入组件。推荐使用 `AiPromptFormComposer` 一站式拼装；也可按需组合子组件。

## 引入

```ts
import {
  AiPromptFormComposer,
  AiPromptForm,
  AiPromptFormBody,
  AiPromptFormFooter,
  AiPromptFormTextarea,
  AiPromptFormActionMenu,
  AiPromptFormAttachments,
  AiPromptFormModes,
  AiPromptFormContext,
  AiPromptFormVoiceInput,
  AiPromptFormVoiceChat,
} from '@/uni_modules/aiko-ai-elements/components'
import type { PromptFormMessage } from '@/uni_modules/aiko-ai-elements/components'
```

## 推荐：AiPromptFormComposer

完整对话输入：上部文字 + `/` 斜杠菜单；底部左侧加号菜单，右侧上下文用量 + 语音按钮。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `status` | `'idle' \| 'streaming'` | `'idle'` | 提交 / 流式状态 |
| `placeholder` | `string` | 见组件默认 | 占位文案 |
| `maxTokens` / `usedTokens` | `number` | — | 上下文用量 |
| `usage` | `LanguageModelUsage` | — | Token 分项 |
| `showContext` | `boolean` | 自动 | 是否显示上下文圆环 |

### Events

`submit` · `stop` · `action-select` · `slash-select` · `voice-start` · `voice-end` · `voice-chat-start` · `voice-chat-end`

### 示例

```vue
<template>
  <AiPromptFormComposer
    :status="status"
    :max-tokens="128000"
    :used-tokens="usedTokens"
    :usage="usage"
    placeholder="输入消息，/ 唤起快捷指令..."
    @submit="onSubmit"
    @stop="onStop"
  />
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { AiPromptFormComposer } from '@/uni_modules/aiko-ai-elements/components'
import type { PromptFormMessage, LanguageModelUsage } from '@/uni_modules/aiko-ai-elements/components'

const status = ref<'idle' | 'streaming'>('idle')
const usedTokens = ref(4800)
const usage = ref<LanguageModelUsage>({ inputTokens: 3200, outputTokens: 1600 })

function onSubmit(message: PromptFormMessage) {
  status.value = 'streaming'
  // message.text / message.files / message.modes
}

function onStop() {
  status.value = 'idle'
}
</script>
```

## 组合式拼装

```vue
<AiPromptForm :status="status" :max-tokens="128000" :used-tokens="usedTokens" @submit="onSubmit">
  <AiPromptFormAttachments />
  <AiPromptFormModes />
  <AiPromptFormBody>
    <AiPromptFormTextarea placeholder="自定义组合各子组件..." />
  </AiPromptFormBody>
  <AiPromptFormFooter>
    <template #left>
      <AiPromptFormActionMenu @select="onAction" />
    </template>
    <template #right>
      <AiPromptFormContext />
      <AiPromptFormVoiceInput />
      <AiPromptFormVoiceChat />
    </template>
  </AiPromptFormFooter>
</AiPromptForm>
```

## PromptFormMessage

```ts
interface PromptFormMessage {
  text: string
  files?: AttachmentData[]
  modes?: ('think' | 'deep-research' | 'web-search')[]
}
```
