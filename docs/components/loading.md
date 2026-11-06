# Loading AI 加载特效

18 种 AI 风格加载动画。与轻量 `AiLoader` 不同：本组件偏展示 / 全屏等待场景。

> 消息内联等待请优先使用 [Loader](./loader.md)。

## 引入

```ts
import { AiLoading } from '@/uni_modules/aiko-ai-elements/components'
import type { LoadingType, LoadingSize } from '@/uni_modules/aiko-ai-elements/components'
```

## AiLoading

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `type` | `LoadingType` | `'pulse-rings'` | 动画类型 |
| `size` | `'sm' \| 'md' \| 'lg'` | `'md'` | 尺寸 |
| `color` | `string` | — | 主色 |
| `label` | `string` | `''` | 底部文字 |

### LoadingType

`pulse-rings` · `spectrum` · `binary` · `orbital` · `dna-helix` · `multi-rings` · `quantum-grid` · `pixel-build` · `morph` · `thinking` · `signal` · `tunnel` · `core-reactor` · `neural-pulse` · `double-spin` · `bionic-ripple` · `shimmer` · `fractal`

## 使用示例

```vue
<template>
  <AiLoading type="thinking" size="lg" label="AI 思考中…" color="#2563eb" />
  <AiLoading type="pulse-rings" size="md" />
</template>

<script setup lang="ts">
import { AiLoading } from '@/uni_modules/aiko-ai-elements/components'
</script>
```
