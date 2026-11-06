# Sources 来源引用组件

展示消息引用的来源/参考资源组件。

## 引入

```ts
import {
  AiSources,
  AiSourcesTrigger,
  AiSourcesContent,
  AiSource,
} from '@/uni_modules/aiko-ai-elements/components/sources'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiSources` | 来源引用容器 |
| `AiSourcesTrigger` | 触发器按钮 |
| `AiSourcesContent` | 内容列表区域 |
| `AiSource` | 单个来源项 |

## AiSources

来源引用折叠容器。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `count` | `number` | - | 来源数量（用于显示徽章） |
| `defaultOpen` | `boolean` | `false` | 默认是否展开 |

## AiSourcesTrigger

触发器按钮，显示来源数量。

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 自定义内容 |

## AiSourcesContent

来源列表区域。

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 来源列表 |

## AiSource

单个来源项。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `title` | `string` | - | 来源标题 |
| `url` | `string` | - | 来源链接 |
| `snippet` | `string` | - | 摘要片段 |

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 自定义内容 |

## 使用示例

### 基础用法

```vue
<AiSources :count="sources.length">
  <AiSourcesTrigger>
    引用来源
  </AiSourcesTrigger>
  <AiSourcesContent>
    <AiSource
      v-for="source in sources"
      :key="source.id"
      :title="source.title"
      :url="source.url"
      :snippet="source.snippet"
    />
  </AiSourcesContent>
</AiSources>
```

### 在消息中使用

```vue
<AiMessage from="assistant">
  <AiMessageContent>
    <AiMessageResponse :content="response" />
  </AiMessageContent>
  <AiSources :count="3">
    <AiSourcesTrigger />
    <AiSourcesContent>
      <AiSource title="Vue 3 文档" url="https://vuejs.org" />
      <AiSource title="MDN Web Docs" url="https://developer.mozilla.org" />
      <AiSource title="TypeScript Handbook" url="https://typescriptlang.org" />
    </AiSourcesContent>
  </AiSources>
</AiMessage>
```
