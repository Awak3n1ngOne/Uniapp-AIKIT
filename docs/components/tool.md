# Tool 工具调用组件

展示 AI 工具调用过程的组件。

## 引入

```ts
import {
  AiTool,
  AiToolHeader,
  AiToolContent,
  AiToolInput,
  AiToolOutput,
} from '@/uni_modules/aiko-ai-elements/components/tool'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiTool` | 工具调用容器 |
| `AiToolHeader` | 头部，显示工具名称和状态 |
| `AiToolContent` | 内容区域 |
| `AiToolInput` | 输入参数展示 |
| `AiToolOutput` | 输出结果展示 |

## AiTool

工具调用容器。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `name` | `string` | - | 工具名称 |
| `status` | `'pending' \| 'running' \| 'success' \| 'error'` | `'pending'` | 状态 |
| `defaultOpen` | `boolean` | `false` | 默认是否展开 |

## AiToolHeader

显示工具名称和状态图标。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `name` | `string` | - | 工具名称 |
| `status` | `string` | - | 状态 |

## AiToolInput

展示工具输入参数。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `args` | `Record<string, any>` | - | 输入参数 |

## AiToolOutput

展示工具输出结果。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `result` | `any` | - | 输出结果 |
| `error` | `string` | - | 错误信息 |

## 使用示例

### 基础用法

```vue
<AiTool name="search" status="success">
  <AiToolHeader />
  <AiToolContent>
    <AiToolInput :args="{ query: 'Vue 3 composition API' }" />
    <AiToolOutput :result="searchResult" />
  </AiToolContent>
</AiTool>
```

### 错误状态

```vue
<AiTool name="execute_code" status="error">
  <AiToolHeader />
  <AiToolContent>
    <AiToolInput :args="{ code: 'print(x)' }" />
    <AiToolOutput error="NameError: name 'x' is not defined" />
  </AiToolContent>
</AiTool>
```

### 运行中状态

```vue
<AiTool name="analyze_data" status="running">
  <AiToolHeader />
  <AiToolContent>
    <AiToolInput :args="{ file: 'data.csv' }" />
    <AiToolOutput>
      <AiLoader label="正在分析..." />
    </AiToolOutput>
  </AiToolContent>
</AiTool>
```
