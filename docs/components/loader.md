# Loader 加载组件

轻量加载指示器，适合消息气泡、工具调用等内联等待。

> 需要 18 种 AI 特效动画时，请使用 [Loading](./loading.md)。

## 引入

```ts
import { AiLoader } from '@/uni_modules/aiko-ai-elements/components'
```

## AiLoader

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `size` | `'sm' \| 'md' \| 'lg'` | `'md'` | 尺寸 |
| `mode` | `'pulse' \| 'spin' \| 'dots'` | `'pulse'` | 动画模式 |
| `label` | `string` | — | 加载文字 |
| `color` | `string` | — | 自定义颜色 |

## 使用示例

```vue
<template>
  <AiLoader />
  <AiLoader mode="dots" label="思考中…" />
  <AiLoader mode="spin" size="lg" color="#10b981" />

  <AiMessage from="assistant">
    <AiMessageContent>
      <AiLoader mode="pulse" label="AI 正在思考…" />
    </AiMessageContent>
  </AiMessage>
</template>

<script setup lang="ts">
import {
  AiLoader,
  AiMessage,
  AiMessageContent,
} from '@/uni_modules/aiko-ai-elements/components'
</script>
```
