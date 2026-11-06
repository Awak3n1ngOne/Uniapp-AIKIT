# Terminal 终端输出

终端风格输出面板，支持流式光标与清空。

## 引入

```ts
import { AiTerminal } from '@/uni_modules/aiko-ai-elements/components'
```

## AiTerminal

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `output` | `string` | — | 输出文本（必填） |
| `isStreaming` | `boolean` | `false` | 流式中（闪烁光标） |
| `autoScroll` | `boolean` | `true` | 内容变化时滚到底部 |
| `title` | `string` | `'Terminal'` | 标题 |
| `showHeader` | `boolean` | `true` | 显示头部 |
| `onClear` | `(() => void) \| null` | `null` | 传入则显示清空按钮 |

## 使用示例

```vue
<template>
  <AiTerminal
    :output="output"
    title="bash"
    :is-streaming="streaming"
    :on-clear="() => (output = '')"
  />
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { AiTerminal } from '@/uni_modules/aiko-ai-elements/components'

const streaming = ref(false)
const output = ref(`$ npm run test
✓ All tests passed
`)
</script>
```
