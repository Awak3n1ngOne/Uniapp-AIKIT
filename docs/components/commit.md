# Commit 提交信息

展示 Git 提交摘要与变更文件列表，点击 hash 可复制。

## 引入

```ts
import { AiCommit, AiCommitFile } from '@/uni_modules/aiko-ai-elements/components'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiCommit` | 可折叠提交卡片 |
| `AiCommitFile` | 变更文件行 |

## AiCommit

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `hash` | `string` | — | 提交哈希（必填） |
| `message` | `string` | — | 提交说明（必填） |
| `author` | `string` | — | 作者（必填） |
| `date` | `Date` | — | 时间（必填，显示相对时间） |
| `defaultOpen` | `boolean` | `false` | 默认展开文件列表 |

## AiCommitFile

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `path` | `string` | — | 文件路径（必填） |
| `status` | `'added' \| 'modified' \| 'deleted' \| 'renamed'` | — | 变更类型（必填） |
| `additions` | `number` | `0` | 新增行数 |
| `deletions` | `number` | `0` | 删除行数 |

## 使用示例

```vue
<template>
  <AiCommit
    hash="a1b2c3d4e5f6"
    message="feat: add snippet component"
    author="张三"
    :date="new Date()"
    :default-open="true"
  >
    <AiCommitFile path="src/auth/refresh.ts" status="modified" :additions="12" :deletions="4" />
    <AiCommitFile path="src/types/auth.d.ts" status="added" :additions="15" />
  </AiCommit>
</template>

<script setup lang="ts">
import { AiCommit, AiCommitFile } from '@/uni_modules/aiko-ai-elements/components'
</script>
```
