# Context 上下文窗口

展示模型上下文 Token 使用率、分项用量与估算成本。

## 引入

```ts
import { AiContext } from '@/uni_modules/aiko-ai-elements/components'
import type { LanguageModelUsage } from '@/uni_modules/aiko-ai-elements/components'
```

## AiContext

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `maxTokens` | `number` | — | 上下文上限（必填） |
| `usedTokens` | `number` | — | 已用 Token（必填） |
| `usage` | `LanguageModelUsage` | — | 分项用量 |
| `inputCostPer1k` | `number` | `0` | 输入每千 Token 成本 |
| `outputCostPer1k` | `number` | `0` | 输出每千 Token 成本 |
| `placement` | `'top' \| 'bottom'` | `'bottom'` | 详情弹层方向 |
| `compact` | `boolean` | `false` | 紧凑模式 |

### LanguageModelUsage

```ts
interface LanguageModelUsage {
  inputTokens?: number
  outputTokens?: number
  reasoningTokens?: number
  cacheReadTokens?: number
}
```

## 使用示例

```vue
<template>
  <AiContext
    :max-tokens="128000"
    :used-tokens="64000"
    :usage="{ inputTokens: 35000, outputTokens: 28000, reasoningTokens: 1000 }"
    :input-cost-per1k="0.005"
    :output-cost-per1k="0.015"
  />
</template>

<script setup lang="ts">
import { AiContext } from '@/uni_modules/aiko-ai-elements/components'
</script>
```
