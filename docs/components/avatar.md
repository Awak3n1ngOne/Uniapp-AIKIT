# Avatar 头像

头像与头像组，支持图片、文字首字母、多种形状与颜色。

## 引入

```ts
import { AiAvatar, AiAvatarGroup } from '@/uni_modules/aiko-ai-elements/components'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiAvatar` | 单个头像 |
| `AiAvatarGroup` | 重叠头像组 |

## AiAvatar

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `src` | `string` | `''` | 图片 URL |
| `title` | `string` | `''` | 无图时显示文字（取首字母） |
| `size` | `number \| 'sm' \| 'md' \| 'lg'` | `'md'` | 尺寸（sm/md/lg → 32/48/64） |
| `shape` | `'circle' \| 'square'` | `'circle'` | 形状 |
| `variant` | `'filled' \| 'outlined' \| 'borderless' \| 'soft'` | `'filled'` | 变体 |
| `color` | `'default' \| 'accent' \| 'success' \| 'warning' \| 'danger'` | `'default'` | 颜色 |
| `loading` | `boolean` | `false` | 加载中 |
| `bordered` | `boolean` | `false` | 边框 |
| `fallbackDelay` | `number` | `0` | 图片延迟显示 fallback（ms） |

## AiAvatarGroup

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `max` | `number` | `5` | 最多显示个数 |
| `total` | `number` | `0` | 总数；大于 max 时显示 `+N` |
| `size` / `color` / `bordered` | 同 Avatar | — | 下发给子头像 |

## 使用示例

```vue
<template>
  <AiAvatar title="AI" color="accent" size="md" />
  <AiAvatar src="https://example.com/avatar.png" shape="square" />

  <AiAvatarGroup :total="8" :max="3">
    <AiAvatar title="AB" color="accent" />
    <AiAvatar title="CD" />
    <AiAvatar title="EF" color="success" />
  </AiAvatarGroup>
</template>

<script setup lang="ts">
import { AiAvatar, AiAvatarGroup } from '@/uni_modules/aiko-ai-elements/components'
</script>
```
