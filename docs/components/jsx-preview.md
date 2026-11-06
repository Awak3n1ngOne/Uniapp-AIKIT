# JSXPreview JSX 预览

将类 JSX / HTML 字符串解析为可预览节点，内置 `ai-card-*` 等卡片样式。

> 内部会把自定义标签映射为 `div`/`span`，并以 **HTML 字符串** 传给 `rich-text`，避免 H5 端对 nodes 对象数组就地修改导致的递归更新报错。

## 引入

```ts
import { AiJSXPreview } from '@/uni_modules/aiko-ai-elements/components'
```

## AiJSXPreview

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `code` | `string` | — | JSX/HTML 字符串（必填） |
| `isStreaming` | `boolean` | `false` | 流式生成中 |
| `showError` | `boolean` | `true` | 解析失败时显示错误 |

## 使用示例

```vue
<template>
  <AiJSXPreview :code="code" :is-streaming="streaming" />
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { AiJSXPreview } from '@/uni_modules/aiko-ai-elements/components'

const streaming = ref(false)
const code = ref(`<ai-card>
  <ai-card-header>
    <ai-card-avatar>AI</ai-card-avatar>
    <ai-card-body>
      <ai-card-title>任务完成</ai-card-title>
      <ai-card-desc>智能体 · 刚刚</ai-card-desc>
    </ai-card-body>
  </ai-card-header>
</ai-card>`)
</script>
```
