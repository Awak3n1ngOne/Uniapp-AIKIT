# Snippet 代码片段

轻量行内代码 / 终端命令展示，支持一键复制。

## 引入

```ts
import { AiSnippet } from '@/uni_modules/aiko-ai-elements/components'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiSnippet` | 代码片段容器 |
| `AiSnippetCopyButton` | 复制按钮（也可单独使用） |

## AiSnippet

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `code` | `string` | — | 显示文本（必填） |
| `prefix` | `string` | `''` | 前缀，如 `$` |
| `language` | `string` | `'tsx'` | 语言声明 |
| `copyable` | `boolean` | `true` | 是否显示复制按钮 |
| `copyTimeout` | `number` | `2000` | 复制成功态恢复时间（ms） |
| `variant` | `'filled' \| 'outlined' \| 'borderless'` | `'filled'` | 样式变体 |
| `spotlight` | `boolean` | `false` | 光晕效果 |
| `shadow` | `boolean` | `false` | 阴影 |

## 使用示例

```vue
<template>
  <AiSnippet code="npm install aiko-ai-elements" prefix="$" />
  <AiSnippet code="import { AiSnippet } from 'aiko-ai-elements'" variant="outlined" />
</template>

<script setup lang="ts">
import { AiSnippet } from '@/uni_modules/aiko-ai-elements/components'
</script>
```
