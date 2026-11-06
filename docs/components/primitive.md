# Primitive 基础组件

底层通用组件，供业务组件与页面复用。

## 引入

```ts
import {
  AiButton,
  AiDialog,
  AiTooltip,
  AiCollapsible,
  AiSelect,
  AiSelectItem,
  AiIcon,
} from '@/uni_modules/aiko-ai-elements/components'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiButton` | 按钮 |
| `AiDialog` | 模态框 |
| `AiTooltip` | 提示 |
| `AiCollapsible` | 折叠面板 |
| `AiSelect` / `AiSelectItem` | 下拉选择 |
| `AiIcon` | Remix Icon |

## AiButton

| 属性 | 类型 | 默认值 |
|------|------|--------|
| `variant` | `'primary' \| 'ghost' \| 'outline' \| 'destructive'` | `'ghost'` |
| `size` | `'sm' \| 'md' \| 'lg'` | `'md'` |
| `disabled` | `boolean` | `false` |

事件：`click`

## AiDialog

| 属性 | 类型 | 默认值 |
|------|------|--------|
| `modelValue` | `boolean` | —（必填，可用 `v-model`） |
| `title` | `string` | — |
| `closeOnOverlay` | `boolean` | `true` |

事件：`update:modelValue`

## AiTooltip

| 属性 | 类型 | 默认值 |
|------|------|--------|
| `content` | `string` | —（必填） |
| `delay` | `number` | `500` |

## AiCollapsible

| 属性 | 类型 | 默认值 |
|------|------|--------|
| `defaultOpen` | `boolean` | `false` |

插槽：`trigger`（`{ open }`）、`content`  
Expose：`{ open, toggle }`

## AiSelect / AiSelectItem

**AiSelect**

| 属性 | 类型 | 默认值 |
|------|------|--------|
| `modelValue` | `string` | — |
| `placeholder` | `string` | `'请选择'` |

事件：`update:modelValue`

**AiSelectItem**：`value`、`label`（均必填）

## AiIcon

| 属性 | 类型 | 默认值 |
|------|------|--------|
| `name` | `string` | —（必填，如 `send-plane-fill`） |
| `size` | `number` | `16` |
| `color` | `string` | — |

## 使用示例

```vue
<template>
  <AiButton variant="primary" size="sm" @click="open = true">
    <AiIcon name="settings-3-line" :size="18" /> 设置
  </AiButton>

  <AiDialog v-model="open" title="选择模型">
    <AiSelect v-model="model" placeholder="请选择">
      <AiSelectItem value="gpt-4o" label="GPT-4o" />
      <AiSelectItem value="claude-sonnet" label="Claude Sonnet" />
    </AiSelect>
  </AiDialog>

  <AiCollapsible :default-open="true">
    <template #trigger="{ open: isOpen }">
      <text>{{ isOpen ? '收起' : '展开' }}</text>
    </template>
    <template #content>
      <text>折叠内容</text>
    </template>
  </AiCollapsible>

  <AiTooltip content="复制到剪贴板">
    <AiButton size="sm">复制</AiButton>
  </AiTooltip>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import {
  AiButton,
  AiDialog,
  AiTooltip,
  AiCollapsible,
  AiSelect,
  AiSelectItem,
  AiIcon,
} from '@/uni_modules/aiko-ai-elements/components'

const open = ref(false)
const model = ref('')
</script>
```
