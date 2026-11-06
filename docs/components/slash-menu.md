# EditorSlashMenu 斜杠菜单

输入触发字符（默认 `/`）唤起的命令菜单，支持分组与搜索。

## 引入

```ts
import {
  AiEditorSlashMenu,
  AiEditorSlashMenuTrigger,
} from '@/uni_modules/aiko-ai-elements/components'
import type { SlashMenuGroup, SlashMenuItem } from '@/uni_modules/aiko-ai-elements/components'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiEditorSlashMenu` | 菜单本体（受控 visible） |
| `AiEditorSlashMenuTrigger` | 包裹输入区，自动检测触发字符 |

## AiEditorSlashMenu

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `items` | `SlashMenuGroup[]` | — | 菜单数据（必填） |
| `visible` | `boolean` | `false` | 是否显示（可 v-model） |
| `triggerChar` | `string` | `'/'` | 触发字符 |
| `filterable` | `boolean` | `true` | 显示搜索框 |
| `emptyText` | `string` | `'无匹配结果'` | 空态文案 |
| `maxHeight` | `number` | `300` | 最大高度（px） |
| `position` | `{ top?, left? }` | — | 绝对定位 |

### Events

| 事件 | 载荷 |
|------|------|
| `select` | `SlashMenuItem` |
| `update:visible` | `boolean` |

### 数据类型

```ts
interface SlashMenuItem {
  value: string
  label: string
  icon?: string
  keywords?: string[]
  description?: string
}

interface SlashMenuGroup {
  label: string
  items: SlashMenuItem[]
}
```

## 使用示例

```vue
<template>
  <AiEditorSlashMenuTrigger :items="groups" @select="onSelect">
    <textarea placeholder="输入 / 唤起菜单" />
  </AiEditorSlashMenuTrigger>
</template>

<script setup lang="ts">
import { AiEditorSlashMenuTrigger } from '@/uni_modules/aiko-ai-elements/components'
import type { SlashMenuGroup, SlashMenuItem } from '@/uni_modules/aiko-ai-elements/components'

const groups: SlashMenuGroup[] = [
  {
    label: '常用',
    items: [
      { value: 'code', label: '代码块', icon: 'code-s-slash-line', keywords: ['code'] },
      { value: 'image', label: '图片', icon: 'image-line' },
    ],
  },
]

function onSelect(item: SlashMenuItem) {
  console.log(item.value)
}
</script>
```
