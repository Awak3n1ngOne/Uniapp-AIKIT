# Actions 操作按钮组组件

操作按钮容器组件。

## 引入

```ts
import { AiActions } from '@/uni_modules/aiko-ai-elements/components/actions'
```

## AiActions

操作按钮容器，用于包裹一组操作按钮。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `align` | `'start' \| 'center' \| 'end' \| 'space-between' \| 'space-around'` | `'end'` | 对齐方式 |
| `gap` | `string \| number` | - | 按钮间距（数字视为 rpx） |
| `wrap` | `boolean` | `true` | 是否允许换行 |

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 按钮内容 |

## 使用示例

### 基础用法

```vue
<AiActions>
  <AiButton size="sm" variant="ghost">取消</AiButton>
  <AiButton size="sm" variant="primary">确认</AiButton>
</AiActions>
```

### 左对齐

```vue
<AiActions align="start">
  <AiButton size="sm" variant="ghost">编辑</AiButton>
  <AiButton size="sm" variant="ghost">删除</AiButton>
</AiActions>
```

### 在消息中使用 (AiMessageActions)

```vue
<AiMessage from="assistant">
  <AiMessageContent>
    <AiMessageResponse :content="response" />
  </AiMessageContent>
  <AiMessageActions>
    <AiMessageAction icon="file-copy-line" label="复制" @click="copy" />
    <AiMessageAction icon="refresh-line" label="重新生成" @click="regenerate" />
    <AiMessageAction icon="thumb-up-line" tooltip="点赞" @click="like" />
  </AiMessageActions>
</AiMessage>
```

### 自定义间距

```vue
<AiActions gap="24rpx" align="center">
  <AiButton size="sm">A</AiButton>
  <AiButton size="sm">B</AiButton>
  <AiButton size="sm">C</AiButton>
</AiActions>
```
