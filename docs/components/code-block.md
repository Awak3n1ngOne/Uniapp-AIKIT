# CodeBlock 代码块组件

代码块展示组件，支持语法高亮、复制、语言选择等功能。

## 引入

```ts
import {
  AiCodeBlock,
  AiCodeBlockCopyButton,
  AiCodeBlockHeader,
  AiCodeBlockTitle,
  AiCodeBlockFilename,
  AiCodeBlockActions,
  AiCodeBlockLanguageSelector,
} from '@/uni_modules/aiko-ai-elements/components/code-block'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiCodeBlock` | 代码块容器 |
| `AiCodeBlockCopyButton` | 复制按钮 |
| `AiCodeBlockHeader` | 头部区域 |
| `AiCodeBlockTitle` | 标题 |
| `AiCodeBlockFilename` | 文件名 |
| `AiCodeBlockActions` | 操作区域 |
| `AiCodeBlockLanguageSelector` | 语言选择器 |

## AiCodeBlock

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `code` | `string` | - | 代码内容 |
| `language` | `string` | - | 语言标识 |
| `filename` | `string` | - | 文件名 |
| `showLineNumbers` | `boolean` | `true` | 是否显示行号 |
| `highlightLines` | `number[]` | - | 高亮行号 |

### Slots

| 插槽 | 说明 |
|------|------|
| `header` | 自定义头部 |
| `default` | 代码内容 |

## AiCodeBlockHeader

代码块头部容器。

### Slots

| 插槽 | 说明 |
|------|------|
| `default` | 头部内容 |

## AiCodeBlockCopyButton

复制按钮。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `text` | `string` | - | 要复制的文本 |

### Events

| 事件 | 说明 |
|------|------|
| `copy` | 复制成功 |

## AiCodeBlockLanguageSelector

语言选择器。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `modelValue` | `string` | - | 当前语言 |
| `languages` | `string[]` | - | 语言列表 |

## 使用示例

### 基础用法

```vue
<AiCodeBlock
  code="console.log('Hello, World!')"
  language="javascript"
/>
```

### 带文件名

```vue
<AiCodeBlock
  :code="fileContent"
  language="typescript"
  filename="src/utils/helper.ts"
  :show-line-numbers="true"
/>
```

### 自定义头部

```vue
<AiCodeBlock :code="code" :language="lang">
  <template #header>
    <AiCodeBlockHeader>
      <AiCodeBlockFilename>app.vue</AiCodeBlockFilename>
      <AiCodeBlockActions>
        <AiCodeBlockLanguageSelector v-model="lang" :languages="['vue', 'javascript', 'typescript']" />
        <AiCodeBlockCopyButton :text="code" />
      </AiCodeBlockActions>
    </AiCodeBlockHeader>
  </template>
</AiCodeBlock>
```

### 高亮特定行

```vue
<AiCodeBlock
  :code="code"
  language="python"
  :highlight-lines="[3, 4, 5]"
/>
```
