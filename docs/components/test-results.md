# TestResults 测试结果

展示单元 / 集成测试的汇总、套件与单条结果。

## 引入

```ts
import {
  AiTestResults,
  AiTestSuite,
  AiTest,
} from '@/uni_modules/aiko-ai-elements/components'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiTestResults` | 汇总容器（进度条 + 统计） |
| `AiTestSuite` | 可折叠测试套件 |
| `AiTest` | 单条测试 |

## AiTestResults

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `summary` | `{ passed, failed, skipped, total, duration? }` | — | 汇总数据（必填） |

## AiTestSuite

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `name` | `string` | — | 套件名（必填） |
| `status` | `'passed' \| 'failed' \| 'skipped' \| 'running'` | — | 状态（必填） |
| `defaultOpen` | `boolean` | `false` | 默认展开 |
| `passed` / `failed` / `skipped` | `number` | `0` | 子项统计 |

## AiTest

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `name` | `string` | — | 测试名（必填） |
| `status` | `'passed' \| 'failed' \| 'skipped' \| 'running'` | — | 状态（必填） |
| `duration` | `number` | — | 耗时（ms） |
| `error` | `{ message, stack? }` | — | 失败时错误信息 |

## 使用示例

```vue
<template>
  <AiTestResults :summary="{ passed: 2, failed: 1, skipped: 0, total: 3, duration: 700 }">
    <AiTestSuite name="auth" status="failed" :default-open="true" :passed="2" :failed="1">
      <AiTest name="login" status="passed" :duration="120" />
      <AiTest name="logout" status="passed" :duration="45" />
      <AiTest
        name="refreshToken"
        status="failed"
        :duration="300"
        :error="{ message: 'Token expired' }"
      />
    </AiTestSuite>
  </AiTestResults>
</template>

<script setup lang="ts">
import { AiTestResults, AiTestSuite, AiTest } from '@/uni_modules/aiko-ai-elements/components'
</script>
```
