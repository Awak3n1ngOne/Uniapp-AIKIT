# Suggestion 建议组件

展示快捷建议/快捷回复的组件。

## 引入

```ts
import {
  AiSuggestions,
  AiSuggestion,
} from '@/uni_modules/aiko-ai-elements/components/suggestion'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiSuggestions` | 建议列表容器 |
| `AiSuggestion` | 单个建议项 |

## AiSuggestions

建议列表容器，横向滚动布局。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `scrollable` | `boolean` | `true` | 是否可滚动 |

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 建议列表 |

## AiSuggestion

单个建议项，可点击选中。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `label` | `string` | - | 建议文本 |
| `icon` | `string` | - | 图标 |
| `disabled` | `boolean` | `false` | 是否禁用 |

### Events

| 事件 | 说明 |
|------|------|
| `click` | 点击事件 |

## 使用示例

### 基础用法

```vue
<AiSuggestions>
  <AiSuggestion
    v-for="item in suggestions"
    :key="item.id"
    :label="item.text"
    @click="handleSelect(item)"
  />
</AiSuggestions>
```

### 带图标

```vue
<AiSuggestions>
  <AiSuggestion label="解释代码" icon="💡" @click="select('explain')" />
  <AiSuggestion label="修复 Bug" icon="🔧" @click="select('fix')" />
  <AiSuggestion label="优化性能" icon="⚡" @click="select('optimize')" />
</AiSuggestions>
```

### 在空状态中使用

```vue
<AiConversation>
  <AiConversationContent>
    <AiConversationEmptyState
      title="开始新对话"
      description="选择一个建议开始"
    >
      <AiSuggestions>
        <AiSuggestion label="写一个排序算法" @click="startChat" />
        <AiSuggestion label="帮我写文档" @click="startChat" />
        <AiSuggestion label="代码审查" @click="startChat" />
      </AiSuggestions>
    </AiConversationEmptyState>
  </AiConversationContent>
</AiConversation>
```

### 在消息中使用

```vue
<AiMessage from="assistant">
  <AiMessageContent>
    <AiMessageResponse :content="response" />
  </AiMessageContent>
  <AiSuggestions>
    <AiSuggestion label="继续" @click="continueChat" />
    <AiSuggestion label="更详细" @click="moreDetail" />
    <AiSuggestion label="换一种方式" @click="tryAnother" />
  </AiSuggestions>
</AiMessage>
```
