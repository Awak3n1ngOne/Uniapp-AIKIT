# VoiceSelector 音色选择

按分组展示的 TTS 音色选择器。

## 引入

```ts
import { AiVoiceSelector } from '@/uni_modules/aiko-ai-elements/components'
import type { VoiceGroup, VoiceItem } from '@/uni_modules/aiko-ai-elements/components'
```

## AiVoiceSelector

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `voices` | `VoiceGroup[]` | — | 音色分组（必填） |
| `value` | `string` | `''` | 当前选中 |
| `defaultValue` | `string` | `''` | 初始选中 |

### Events

| 事件 | 载荷 |
|------|------|
| `value-change` | `value: string` |

### 数据类型

```ts
interface VoiceItem {
  value: string
  label: string
  gender?: 'male' | 'female'
  accent?: string
  description?: string
}

interface VoiceGroup {
  label: string
  items: VoiceItem[]
}
```

## 使用示例

```vue
<template>
  <AiVoiceSelector :voices="groups" @value-change="onChange" />
</template>

<script setup lang="ts">
import { AiVoiceSelector } from '@/uni_modules/aiko-ai-elements/components'
import type { VoiceGroup } from '@/uni_modules/aiko-ai-elements/components'

const groups: VoiceGroup[] = [
  {
    label: '中文',
    items: [
      { value: 'zh-female', label: '小云', gender: 'female', accent: '🇨🇳', description: '温柔自然' },
      { value: 'zh-male', label: '小智', gender: 'male', accent: '🇨🇳', description: '沉稳专业' },
    ],
  },
]

function onChange(v: string) {
  console.log(v)
}
</script>
```
