# Attachments 附件组件

展示消息附件（文件、图片等），支持网格 / 列表 / 行内布局、上传进度，并可与 **PromptForm** 集成。

## 引入

```ts
import {
  AiAttachments,
  AiAttachment,
  AiAttachmentPreview,
  AiAttachmentInfo,
  AiAttachmentRemove,
  AiAttachmentHoverCard,
  type AttachmentData,
} from '@/uni_modules/aiko-ai-elements/components'
```

## AiAttachments

附件列表容器，可通过 **slot** 或 **`items`** 声明附件。

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `variant` | `'grid' \| 'list' \| 'inline' \| 'card'` | `'list'` | 布局（子项可省略，自动继承） |
| `context` | `'input' \| 'dialog'` | `'dialog'` | 场景样式 |
| `items` | `AttachmentData[]` | `[]` | 声明式列表（与 slot 二选一） |
| `removable` | `boolean` | `false` | `items` 模式下是否可删 |

### Events

`remove` · `preview` · `download` · `retry-upload` · `retry-download`

## AiAttachment

单个附件项。

### Props

| 属性 | 类型 | 说明 |
|------|------|------|
| `data` | `AttachmentData` | 附件数据（必填） |
| `variant` | 同 Attachments | 布局 |
| `removable` | `boolean` | 是否可删除 |

## 与 PromptForm 集成

在 `AiPromptForm` / `AiPromptFormComposer` 内使用加号菜单添加附件，`AiPromptFormAttachments` 会展示已选文件：

```vue
<AiPromptFormComposer
  placeholder="添加附件后发送..."
  @submit="onSubmit"
/>
```

或组合式：

```vue
<AiPromptForm @submit="onSubmit">
  <AiPromptFormAttachments />
  <AiPromptFormBody>
    <AiPromptFormTextarea />
  </AiPromptFormBody>
  <AiPromptFormFooter>
    <template #left>
      <AiPromptFormActionMenu />
    </template>
  </AiPromptFormFooter>
</AiPromptForm>
```
