# Task 任务组件

展示 AI 执行任务的进度和结果组件。

## 引入

```ts
import {
  AiTask,
  AiTaskTrigger,
  AiTaskContent,
  AiTaskItem,
  AiTaskItemFile,
} from '@/uni_modules/aiko-ai-elements/components/task'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiTask` | 任务容器 |
| `AiTaskTrigger` | 触发器，显示任务状态 |
| `AiTaskContent` | 任务内容区域 |
| `AiTaskItem` | 任务项 |
| `AiTaskItemFile` | 文件类型任务项 |

## AiTask

任务容器。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `status` | `'pending' \| 'running' \| 'completed' \| 'failed'` | `'pending'` | 任务状态 |
| `defaultOpen` | `boolean` | `true` | 默认是否展开 |

## AiTaskTrigger

显示任务标题和状态图标。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `title` | `string` | - | 任务标题 |

## AiTaskContent

任务内容区域，包含任务项列表。

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 任务项列表 |

## AiTaskItem

单个任务项。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `status` | `'pending' \| 'running' \| 'completed' \| 'failed'` | - | 状态 |
| `label` | `string` | - | 任务描述 |

## AiTaskItemFile

文件类型任务项，带文件图标。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `filename` | `string` | - | 文件名 |
| `path` | `string` | - | 文件路径 |
| `status` | `string` | - | 状态 |

## 使用示例

### 基础用法

```vue
<AiTask status="running">
  <AiTaskTrigger title="修改文件" />
  <AiTaskContent>
    <AiTaskItem status="completed" label="读取项目结构" />
    <AiTaskItem status="running" label="修改 src/App.vue" />
    <AiTaskItem status="pending" label="更新配置文件" />
  </AiTaskContent>
</AiTask>
```

### 文件操作任务

```vue
<AiTask status="running">
  <AiTaskTrigger title="代码重构" />
  <AiTaskContent>
    <AiTaskItemFile
      filename="useUserStore.ts"
      path="src/stores/"
      status="completed"
    />
    <AiTaskItemFile
      filename="api.ts"
      path="src/services/"
      status="running"
    />
    <AiTaskItemFile
      filename="types.ts"
      path="src/types/"
      status="pending"
    />
  </AiTaskContent>
</AiTask>
```

### 完成的任务

```vue
<AiTask status="completed">
  <AiTaskTrigger title="安装依赖" />
  <AiTaskContent>
    <AiTaskItem status="completed" label="安装 @ai-sdk/vue" />
    <AiTaskItem status="completed" label="安装 @anthropic-ai/sdk" />
    <AiTaskItem status="completed" label="更新 package.json" />
  </AiTaskContent>
</AiTask>
```
