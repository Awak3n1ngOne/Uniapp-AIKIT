# Plan 执行计划

智能体分步执行计划，支持流式生成与底部操作区。

## 引入

```ts
import { AiPlan, AiPlanStep, AiPlanFooter } from '@/uni_modules/aiko-ai-elements/components'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiPlan` | 可折叠计划卡片 |
| `AiPlanStep` | 步骤项 |
| `AiPlanFooter` | 底部操作区 |

## AiPlan

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `title` | `string` | — | 标题 |
| `description` | `string` | — | 描述 |
| `isStreaming` | `boolean` | `false` | 流式生成中（骨架态） |
| `defaultOpen` | `boolean` | `false` | 默认展开 |

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 步骤列表 |
| `footer` | 底部操作（配合 `AiPlanFooter`） |

## AiPlanStep

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `title` | `string` | — | 步骤标题（必填） |
| `description` | `string` | — | 步骤说明 |
| `status` | `'pending' \| 'active' \| 'done'` | `'pending'` | 状态 |

## 使用示例

```vue
<template>
  <AiPlan title="项目重构计划" description="拆分为微服务" :default-open="true">
    <AiPlanStep title="分析现有架构" status="done" />
    <AiPlanStep title="设计服务划分" status="active" description="按业务域拆分" />
    <AiPlanStep title="实现网关" status="pending" />
    <template #footer>
      <AiPlanFooter>
        <AiButton variant="ghost" size="sm" @click="onCancel">取消</AiButton>
        <AiButton variant="primary" size="sm" @click="onApprove">批准执行</AiButton>
      </AiPlanFooter>
    </template>
  </AiPlan>
</template>

<script setup lang="ts">
import { AiPlan, AiPlanStep, AiPlanFooter, AiButton } from '@/uni_modules/aiko-ai-elements/components'

function onCancel() {}
function onApprove() {}
</script>
```
