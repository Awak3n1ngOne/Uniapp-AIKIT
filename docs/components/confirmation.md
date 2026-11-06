# Confirmation 工具审批

工具调用前的用户审批流程：请求 → 批准 / 拒绝。

## 引入

```ts
import {
  AiConfirmation,
  AiConfirmationTitle,
  AiConfirmationRequest,
  AiConfirmationAccepted,
  AiConfirmationRejected,
  AiConfirmationActions,
  AiConfirmationAction,
} from '@/uni_modules/aiko-ai-elements/components'
import type { ConfirmationState } from '@/uni_modules/aiko-ai-elements/components'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiConfirmation` | 根容器，注入审批状态 |
| `AiConfirmationTitle` | 标题 |
| `AiConfirmationRequest` | 待审批说明 |
| `AiConfirmationAccepted` | 已批准态 |
| `AiConfirmationRejected` | 已拒绝态 |
| `AiConfirmationActions` | 操作区 |
| `AiConfirmationAction` | 单个按钮 |

## AiConfirmation

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `approval` | `{ id: string; approved?: boolean }` | — | 审批数据；无则隐藏 |
| `state` | `ConfirmationState` | `'approval-requested'` | 当前状态 |

### ConfirmationState

`input-streaming` · `input-available` · `approval-requested` · `approval-responded` · `output-denied` · `output-available`

## AiConfirmationAction

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `variant` | `'default' \| 'outline' \| 'destructive'` | `'outline'` | 按钮样式 |

### Events

| 事件 | 说明 |
|------|------|
| `click` | 点击 |

## 使用示例

```vue
<template>
  <AiConfirmation :approval="approval" :state="state">
    <AiConfirmationTitle>删除文件</AiConfirmationTitle>
    <AiConfirmationRequest>
      工具 delete_file 请求删除 /tmp/example.txt，是否批准？
    </AiConfirmationRequest>
    <AiConfirmationActions v-if="state === 'approval-requested'">
      <AiConfirmationAction variant="destructive" @click="respond(false)">拒绝</AiConfirmationAction>
      <AiConfirmationAction variant="default" @click="respond(true)">批准</AiConfirmationAction>
    </AiConfirmationActions>
    <AiConfirmationAccepted v-if="approval.approved === true">
      已批准，操作将继续。
    </AiConfirmationAccepted>
    <AiConfirmationRejected v-if="approval.approved === false">
      已拒绝，操作已取消。
    </AiConfirmationRejected>
  </AiConfirmation>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { ConfirmationState } from '@/uni_modules/aiko-ai-elements/components'
import {
  AiConfirmation,
  AiConfirmationTitle,
  AiConfirmationRequest,
  AiConfirmationAccepted,
  AiConfirmationRejected,
  AiConfirmationActions,
  AiConfirmationAction,
} from '@/uni_modules/aiko-ai-elements/components'

const approval = ref<{ id: string; approved?: boolean }>({ id: '1' })
const state = ref<ConfirmationState>('approval-requested')

function respond(ok: boolean) {
  approval.value = { id: '1', approved: ok }
  state.value = ok ? 'approval-responded' : 'output-denied'
}
</script>
```
