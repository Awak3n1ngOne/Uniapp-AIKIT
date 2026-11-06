# CodeDiff 代码差异

对比新旧代码，支持统一视图与分屏视图。

## 引入

```ts
import { AiCodeDiff } from '@/uni_modules/aiko-ai-elements/components'
```

## AiCodeDiff

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `oldContent` | `string` | — | 旧内容（必填） |
| `newContent` | `string` | — | 新内容（必填） |
| `language` | `string` | `''` | 语言 |
| `fileName` | `string` | `''` | 文件名（头部） |
| `showHeader` | `boolean` | `true` | 是否显示头部 |
| `variant` | `'filled' \| 'outlined' \| 'borderless'` | `'filled'` | 样式 |
| `viewMode` | `'unified' \| 'split'` | `'unified'` | 视图模式（可 v-model） |

### Events

| 事件 | 载荷 |
|------|------|
| `update:viewMode` | `'unified' \| 'split'` |

### Slots

| 插槽 | 说明 |
|------|------|
| `actions` | 头部操作区 |

## 使用示例

```vue
<template>
  <AiCodeDiff
    file-name="utils.ts"
    language="typescript"
    :old-content="oldCode"
    :new-content="newCode"
    v-model:view-mode="mode"
  />
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { AiCodeDiff } from '@/uni_modules/aiko-ai-elements/components'

const mode = ref<'unified' | 'split'>('unified')
const oldCode = `function greet(name) {
  return "Hello, " + name
}`
const newCode = `function greet(name: string): string {
  return \`Hello, \${name}\`
}`
</script>
```
