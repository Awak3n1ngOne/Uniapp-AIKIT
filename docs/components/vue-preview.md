# VuePreview Vue 预览

将 Vue 风格模板字符串解析为**真实 Vue 组件树**（非 `rich-text`），内置完整卡片组件。

## 引入

```ts
import {
  AiVuePreview,
  AiVueCard,
  AiVueCardHeader,
  AiVueCardAvatar,
  AiVueCardBody,
  AiVueCardTitle,
  AiVueCardDesc,
  AiVueCardContent,
  AiVueCardFooter,
  AiVueCardTag,
  AiVueCardMeta,
} from '@/uni_modules/aiko-ai-elements/components'
```

## 两种用法

### 1. 模板字符串（AI 流式输出场景）

```vue
<AiVuePreview :template="tmpl" :data="{ title: 'GLM-4', reads: '2.1k' }" />
```

支持标签：`view` / `text` / `image`，以及卡片标签：

| 模板标签 | 真实组件 |
|----------|----------|
| `ai-vue-card` / `ai-card` | AiVueCard |
| `ai-vue-card-header` | AiVueCardHeader |
| `ai-vue-card-avatar` | AiVueCardAvatar |
| `ai-vue-card-body` | AiVueCardBody |
| `ai-vue-card-title` | AiVueCardTitle |
| `ai-vue-card-desc` | AiVueCardDesc |
| `ai-vue-card-content` | AiVueCardContent |
| `ai-vue-card-footer` | AiVueCardFooter |
| `ai-vue-card-tag` | AiVueCardTag |
| `ai-vue-card-meta` | AiVueCardMeta |

插值：`{{ title }}`、`{{ a.title }}`（点路径），数据来自 `data` prop。

### 2. 直接组合组件（业务页面）

```vue
<AiVueCard>
  <AiVueCardHeader>
    <AiVueCardAvatar text="AI" color="#2563eb" />
    <AiVueCardBody>
      <AiVueCardTitle>标题</AiVueCardTitle>
      <AiVueCardDesc>副标题</AiVueCardDesc>
    </AiVueCardBody>
  </AiVueCardHeader>
  <AiVueCardContent>正文内容</AiVueCardContent>
  <AiVueCardFooter>
    <AiVueCardTag>标签</AiVueCardTag>
    <AiVueCardMeta>刚刚</AiVueCardMeta>
  </AiVueCardFooter>
</AiVueCard>
```

## AiVuePreview Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `template` | `string` | — | 模板字符串（必填） |
| `data` | `Record<string, unknown>` | `{}` | 插值数据 |
| `isStreaming` | `boolean` | `false` | 流式生成中 |
| `showError` | `boolean` | `true` | 解析失败时显示错误 |

## 卡片模板示例

```html
<ai-vue-card>
  <ai-vue-card-header>
    <ai-vue-card-avatar>AI</ai-vue-card-avatar>
    <ai-vue-card-body>
      <ai-vue-card-title>{{ title }}</ai-vue-card-title>
      <ai-vue-card-desc>{{ subtitle }}</ai-vue-card-desc>
    </ai-vue-card-body>
  </ai-vue-card-header>
  <ai-vue-card-content>{{ content }}</ai-vue-card-content>
  <ai-vue-card-footer>
    <ai-vue-card-tag>Vue</ai-vue-card-tag>
    <ai-vue-card-meta>{{ reads }} 阅读</ai-vue-card-meta>
  </ai-vue-card-footer>
</ai-vue-card>
```
