# InlineCitation 行内引用组件

消息中的行内引用/脚注组件。

## 引入

```ts
import {
  AiInlineCitation,
  AiInlineCitationText,
  AiInlineCitationCard,
  AiInlineCitationCardBody,
  AiInlineCitationCardTrigger,
  AiInlineCitationCarousel,
  AiInlineCitationCarouselHeader,
  AiInlineCitationCarouselContent,
  AiInlineCitationCarouselItem,
  AiInlineCitationCarouselIndex,
  AiInlineCitationCarouselPrev,
  AiInlineCitationCarouselNext,
  AiInlineCitationSource,
  AiInlineCitationQuote,
} from '@/uni_modules/aiko-ai-elements/components/inline-citation'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiInlineCitation` | 行内引用容器 |
| `AiInlineCitationText` | 引用数字标记 |
| `AiInlineCitationCard` | 引用卡片 |
| `AiInlineCitationCardBody` | 卡片内容 |
| `AiInlineCitationCardTrigger` | 卡片触发器 |
| `AiInlineCitationCarousel` | 引用轮播 |
| `AiInlineCitationCarouselItem` | 轮播项 |
| `AiInlineCitationSource` | 来源链接 |
| `AiInlineCitationQuote` | 引用片段 |

## AiInlineCitation

行内引用容器，显示为上标数字标记。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `index` | `number` | - | 引用序号 |
| `sources` | `CitationSource[]` | - | 引用来源列表 |

## AiInlineCitationText

引用数字标记（上标）。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `index` | `number` | - | 序号 |

## AiInlineCitationCard

引用悬浮卡片。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `source` | `CitationSource` | - | 来源数据 |

## AiInlineCitationCarousel

多来源轮播展示。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `sources` | `CitationSource[]` | - | 来源列表 |

## 使用示例

### 基础用法

```vue
<template>
  <text>
    Vue 3 引入了 Composition API
    <AiInlineCitation :index="1" :sources="[source1]" />
    ，提供了更好的代码组织方式
    <AiInlineCitation :index="2" :sources="[source2, source3]" />
  </text>
</template>
```

### 带卡片

```vue
<AiInlineCitation :index="1" :sources="[source]">
  <AiInlineCitationText :index="1" />
  <AiInlineCitationCard :source="source">
    <AiInlineCitationCardBody>
      <AiInlineCitationQuote>{{ source.snippet }}</AiInlineCitationQuote>
      <AiInlineCitationSource :url="source.url" :title="source.title" />
    </AiInlineCitationCardBody>
  </AiInlineCitationCard>
</AiInlineCitation>
```

### 多来源轮播

```vue
<AiInlineCitation :index="1" :sources="multipleSources">
  <AiInlineCitationText :index="1" />
  <AiInlineCitationCarousel :sources="multipleSources">
    <AiInlineCitationCarouselHeader>
      <AiInlineCitationCarouselPrev />
      <AiInlineCitationCarouselIndex />
      <AiInlineCitationCarouselNext />
    </AiInlineCitationCarouselHeader>
    <AiInlineCitationCarouselContent>
      <AiInlineCitationCarouselItem
        v-for="s in multipleSources"
        :key="s.id"
      >
        <AiInlineCitationQuote>{{ s.snippet }}</AiInlineCitationQuote>
        <AiInlineCitationSource :url="s.url" />
      </AiInlineCitationCarouselItem>
    </AiInlineCitationCarouselContent>
  </AiInlineCitationCarousel>
</AiInlineCitation>
```
