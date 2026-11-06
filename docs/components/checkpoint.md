# Checkpoint 检查点组件

展示对话检查点/状态快照的组件。

## 引入

```ts
import {
  AiCheckpoint,
  AiCheckpointIcon,
  AiCheckpointTrigger,
} from '@/uni_modules/aiko-ai-elements/components/checkpoint'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiCheckpoint` | 检查点容器 |
| `AiCheckpointIcon` | 检查点图标 |
| `AiCheckpointTrigger` | 触发器按钮 |

## AiCheckpoint

检查点容器，可点击恢复到此状态。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `timestamp` | `string \| Date` | - | 时间戳 |
| `label` | `string` | - | 标签 |

### Events

| 事件 | 说明 |
|------|------|
| `click` | 点击恢复 |

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 自定义内容 |

## AiCheckpointIcon

检查点状态图标。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `status` | `'pending' \| 'completed'` | `'completed'` | 状态 |

## AiCheckpointTrigger

触发器按钮，点击恢复到检查点。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `label` | `string` | - | 按钮文字 |

## 使用示例

### 基础用法

```vue
<AiCheckpoint
  :timestamp="checkpointTime"
  label="代码重构前"
  @click="restoreCheckpoint"
>
  <AiCheckpointIcon status="completed" />
  <text>{{ formatTime(checkpointTime) }}</text>
</AiCheckpoint>
```

### 在对话中使用

```vue
<template>
  <view class="conversation">
    <AiMessage v-for="msg in messages" :key="msg.id" :from="msg.from">
      <AiMessageContent>
        <AiMessageResponse :content="msg.content" />
      </AiMessageContent>
    </AiMessage>

    <!-- 检查点 -->
    <AiCheckpoint
      v-for="cp in checkpoints"
      :key="cp.id"
      :timestamp="cp.timestamp"
      :label="cp.label"
      @click="restore(cp.id)"
    />
  </view>
</template>
```

### 带触发器

```vue
<AiCheckpoint :timestamp="now">
  <AiCheckpointIcon />
  <text>已保存检查点</text>
  <AiCheckpointTrigger label="恢复" />
</AiCheckpoint>
```
