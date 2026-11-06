# WebPreview 网页预览组件

网页链接预览卡片组件。

## 引入

```ts
import { AiWebPreview } from '@/uni_modules/aiko-ai-elements/components/web-preview'
```

## AiWebPreview

网页预览卡片，显示网页标题、描述、图标等信息。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `url` | `string` | - | 网页地址 |
| `title` | `string` | - | 标题 |
| `description` | `string` | - | 描述 |
| `image` | `string` | - | 预览图 |
| `favicon` | `string` | - | 网站图标 |
| `siteName` | `string` | - | 网站名称 |

### Events

| 事件 | 说明 |
|------|------|
| `click` | 点击事件 |

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 自定义内容 |

## 使用示例

### 基础用法

```vue
<AiWebPreview
  url="https://vuejs.org"
  title="Vue.js - The Progressive JavaScript Framework"
  description="An approachable, performant and versatile framework for building web user interfaces."
  favicon="https://vuejs.org/logo.svg"
  siteName="Vue.js"
/>
```

### 带预览图

```vue
<AiWebPreview
  url="https://example.com/article"
  title="文章标题"
  description="文章摘要内容..."
  image="https://example.com/og-image.png"
/>
```

### 在消息中使用

```vue
<AiMessage from="assistant">
  <AiMessageContent>
    <AiMessageResponse :content="response" />
    <AiWebPreview
      v-for="link in links"
      :key="link.url"
      v-bind="link"
    />
  </AiMessageContent>
</AiMessage>
```

### 自定义内容

```vue
<AiWebPreview :url="url">
  <view class="custom-preview">
    <image :src="image" />
    <view class="info">
      <text class="title">{{ title }}</text>
      <text class="desc">{{ description }}</text>
    </view>
  </view>
</AiWebPreview>
```
