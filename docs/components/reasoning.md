# Reasoning 推理过程组件

展示 AI 推理/思考过程的折叠面板组件。

## 引入

```ts
import {
  AiReasoning,
  AiReasoningTrigger,
  AiReasoningContent,
} from '@/uni_modules/aiko-ai-elements/components/reasoning'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiReasoning` | 推理过程容器 |
| `AiReasoningTrigger` | 触发器（展开/收起） |
| `AiReasoningContent` | 内容区域 |

## AiReasoning

推理过程折叠面板容器。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `defaultOpen` | `boolean` | `false` | 默认是否展开 |
| `streaming` | `boolean` | `false` | 是否正在流式输出 |

## AiReasoningTrigger

展开/收起触发器，显示推理状态。

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 自定义标题 |

## AiReasoningContent

推理内容区域。

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 推理内容 |

## 使用示例

### 基础用法

```vue
<AiReasoning>
  <AiReasoningTrigger>
    思考过程
  </AiReasoningTrigger>
  <AiReasoningContent>
    让我分析一下这个问题...
    首先，我们需要考虑...
  </AiReasoningContent>
</AiReasoning>
```

### 流式推理

```vue
<AiReasoning :streaming="isThinking">
  <AiReasoningTrigger>
    {{ isThinking ? '正在思考...' : '思考过程' }}
  </AiReasoningTrigger>
  <AiReasoningContent>
    {{ thinkingContent }}
  </AiReasoningContent>
</AiReasoning>
```

### 在消息中使用

```vue
<AiMessage from="assistant">
  <AiReasoning>
    <AiReasoningTrigger>推理过程</AiReasoningTrigger>
    <AiReasoningContent>{{ reasoning }}</AiReasoningContent>
  </AiReasoning>
  <AiMessageContent>
    <AiMessageResponse :content="response" />
  </AiMessageContent>
</AiMessage>
```
