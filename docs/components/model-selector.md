# ModelSelector 模型选择器组件

选择 AI 模型的下拉选择器组件。

## 引入

```ts
import {
  AiModelSelector,
  AiModelSelectorTrigger,
  AiModelSelectorContent,
  AiModelSelectorInput,
  AiModelSelectorList,
  AiModelSelectorGroup,
  AiModelSelectorItem,
  AiModelSelectorLogo,
  AiModelSelectorLogoGroup,
  AiModelSelectorName,
  AiModelSelectorDialog,
  AiModelSelectorEmpty,
  AiModelSelectorShortcut,
  AiModelSelectorSeparator,
} from '@/uni_modules/aiko-ai-elements/components/model-selector'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiModelSelector` | 模型选择器容器 |
| `AiModelSelectorTrigger` | 触发器按钮 |
| `AiModelSelectorContent` | 下拉内容 |
| `AiModelSelectorInput` | 搜索输入框 |
| `AiModelSelectorList` | 模型列表 |
| `AiModelSelectorGroup` | 分组容器 |
| `AiModelSelectorItem` | 模型选项 |
| `AiModelSelectorLogo` | 模型 Logo |
| `AiModelSelectorLogoGroup` | Logo 组 |
| `AiModelSelectorName` | 模型名称 |
| `AiModelSelectorDialog` | 对话框模式 |

## AiModelSelector

模型选择器容器，支持 v-model。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `modelValue` | `string` | - | 当前选中的模型 ID |
| `disabled` | `boolean` | `false` | 是否禁用 |
| `modal` | `boolean` | `false` | 是否使用对话框模式 |

### Events

| 事件 | 说明 |
|------|------|
| `update:modelValue` | 选中模型变化 |

## AiModelSelectorItem

单个模型选项。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `value` | `string` | - | 模型 ID |
| `disabled` | `boolean` | `false` | 是否禁用 |

## AiModelSelectorGroup

模型分组容器。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `name` | `string` | - | 分组名称 |

## AiModelSelectorLogo

模型 Logo 图标。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `src` | `string` | - | Logo 图片地址 |
| `alt` | `string` | - | 替代文字 |

## 使用示例

### 基础用法

```vue
<template>
  <AiModelSelector v-model="selectedModel">
    <AiModelSelectorTrigger>
      <AiModelSelectorName :model="selectedModelData" />
    </AiModelSelectorTrigger>
    <AiModelSelectorContent>
      <AiModelSelectorInput placeholder="搜索模型..." />
      <AiModelSelectorList>
        <AiModelSelectorGroup name="OpenAI">
          <AiModelSelectorItem value="gpt-4">
            <AiModelSelectorLogo src="/logos/openai.svg" />
            <AiModelSelectorName>GPT-4</AiModelSelectorName>
          </AiModelSelectorItem>
          <AiModelSelectorItem value="gpt-3.5-turbo">
            <AiModelSelectorLogo src="/logos/openai.svg" />
            <AiModelSelectorName>GPT-3.5 Turbo</AiModelSelectorName>
          </AiModelSelectorItem>
        </AiModelSelectorGroup>
        <AiModelSelectorSeparator />
        <AiModelSelectorGroup name="Anthropic">
          <AiModelSelectorItem value="claude-3-opus">
            <AiModelSelectorLogo src="/logos/anthropic.svg" />
            <AiModelSelectorName>Claude 3 Opus</AiModelSelectorName>
          </AiModelSelectorItem>
        </AiModelSelectorGroup>
      </AiModelSelectorList>
    </AiModelSelectorContent>
  </AiModelSelector>
</template>
```

### 简化版

```vue
<AiModelSelector v-model="model">
  <AiModelSelectorTrigger />
  <AiModelSelectorContent>
    <AiModelSelectorList>
      <AiModelSelectorItem value="gpt-4">GPT-4</AiModelSelectorItem>
      <AiModelSelectorItem value="claude-3">Claude 3</AiModelSelectorItem>
    </AiModelSelectorList>
  </AiModelSelectorContent>
</AiModelSelector>
```

### 对话框模式

```vue
<AiModelSelector v-model="model" modal>
  <AiModelSelectorTrigger>切换模型</AiModelSelectorTrigger>
  <AiModelSelectorDialog>
    <!-- 内容 -->
  </AiModelSelectorDialog>
</AiModelSelector>
```
