# AI Elements 组件使用文档

面向 UniApp Vue3 的 AI 对话 / 智能体界面组件库。读完本文档后，你应能按需引入任意组件并拼出完整对话页。

## 安装与引入

插件安装到 `uni_modules/aiko-ai-elements` 后：

```ts
// 推荐：从总入口按需导入
import {
  AiConversation,
  AiMessage,
  AiPromptFormComposer,
} from '@/uni_modules/aiko-ai-elements/components'

// 或从模块入口
import { AiMessage } from '@/uni_modules/aiko-ai-elements/components/message'

// Composables
import { useTheme, useAIChat } from '@/uni_modules/aiko-ai-elements/composables'
```

主题样式（`main.ts`）：

```ts
import '@/uni_modules/aiko-ai-elements/common/theme-colors.scss'
```

设计变量（`uni.scss`）：

```scss
@import '@/uni_modules/aiko-ai-elements/common/variables.scss';
```

综合演示页：`pages/demos/agent-showcase/index`。

---

## 文档索引

### 布局与对话

| 组件 | 说明 | 文档 |
|------|------|------|
| Conversation | 对话容器、滚动、空状态、虚拟列表 | [conversation.md](./conversation.md) |
| Message | 消息气泡、Markdown、分支、工具栏 | [message.md](./message.md) |
| PromptForm | 唯一 Prompt 输入（斜杠菜单 / 附件 / 语音 / 上下文） | [prompt-form.md](./prompt-form.md) |

### AI 能力

| 组件 | 说明 | 文档 |
|------|------|------|
| Reasoning | 推理过程折叠 | [reasoning.md](./reasoning.md) |
| Tool | 工具调用输入 / 输出 | [tool.md](./tool.md) |
| Confirmation | 工具审批 | [confirmation.md](./confirmation.md) |
| Plan | 执行计划与步骤 | [plan.md](./plan.md) |
| Sources | 来源引用列表 | [sources.md](./sources.md) |
| InlineCitation | 行内引用与卡片 | [inline-citation.md](./inline-citation.md) |
| Suggestion | 快捷建议 | [suggestion.md](./suggestion.md) |
| Task | 任务列表 | [task.md](./task.md) |
| Checkpoint | 对话检查点 | [checkpoint.md](./checkpoint.md) |
| Context | Token 用量与成本 | [context.md](./context.md) |
| ModelSelector | 模型选择器 | [model-selector.md](./model-selector.md) |
| Persona | AI 角色动画 | [persona.md](./persona.md) |

### 代码与工程

| 组件 | 说明 | 文档 |
|------|------|------|
| CodeBlock | 代码高亮、复制、语言切换 | [code-block.md](./code-block.md) |
| CodeDiff | 代码差异对比 | [code-diff.md](./code-diff.md) |
| Snippet | 轻量命令 / 片段 | [snippet.md](./snippet.md) |
| Terminal | 终端输出 | [terminal.md](./terminal.md) |
| FileTree | 文件树 | [file-tree.md](./file-tree.md) |
| Commit | Git 提交信息 | [commit.md](./commit.md) |
| TestResults | 测试结果树 | [test-results.md](./test-results.md) |
| JSXPreview | JSX / 卡片预览 | [jsx-preview.md](./jsx-preview.md) |
| VuePreview | Vue 模板预览 | [vue-preview.md](./vue-preview.md) |

### 媒体与输入外设

| 组件 | 说明 | 文档 |
|------|------|------|
| Image | AI 图片 | [image.md](./image.md) |
| Attachments | 附件列表 | [attachments.md](./attachments.md) |
| WebPreview | 网页预览（H5） | [web-preview.md](./web-preview.md) |
| MicSelector | 麦克风选择 | [mic-selector.md](./mic-selector.md) |
| VoiceSelector | 音色选择 | [voice-selector.md](./voice-selector.md) |
| EditorSlashMenu | 斜杠命令菜单 | [slash-menu.md](./slash-menu.md) |

### 反馈与基础

| 组件 | 说明 | 文档 |
|------|------|------|
| Loader | 轻量加载（pulse / spin / dots） | [loader.md](./loader.md) |
| Loading | 18 种 AI 加载特效 | [loading.md](./loading.md) |
| Actions | 操作按钮组 | [actions.md](./actions.md) |
| Avatar | 头像 / 头像组 | [avatar.md](./avatar.md) |
| Primitive | Button / Dialog / Select / Icon 等 | [primitive.md](./primitive.md) |

### 其他

| 文档 | 说明 |
|------|------|
| [composables.md](./composables.md) | 组合式函数 |
| 插件 `readme.md` / `components.md` | 安装配置与组件用法（插件市场） |

---

## 最小对话页

```vue
<template>
  <view class="chat-page">
    <AiConversation>
      <AiConversationContent>
        <AiMessage v-for="msg in messages" :key="msg.id" :from="msg.from">
          <AiMessageContent>
            <AiMessageResponse :content="msg.content" />
          </AiMessageContent>
        </AiMessage>
      </AiConversationContent>
      <AiConversationScrollButton />
    </AiConversation>

    <AiPromptFormComposer
      :status="status"
      placeholder="输入消息…"
      @submit="onSubmit"
    />
  </view>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import {
  AiConversation,
  AiConversationContent,
  AiConversationScrollButton,
  AiMessage,
  AiMessageContent,
  AiMessageResponse,
  AiPromptFormComposer,
} from '@/uni_modules/aiko-ai-elements/components'
import type { PromptFormMessage } from '@/uni_modules/aiko-ai-elements/components'

const messages = ref<{ id: string; from: 'user' | 'assistant'; content: string }[]>([])
const status = ref<'idle' | 'streaming'>('idle')

function onSubmit(message: PromptFormMessage) {
  if (!message.text?.trim()) return
  messages.value.push({ id: String(Date.now()), from: 'user', content: message.text })
}
</script>

<style lang="scss" scoped>
.chat-page {
  display: flex;
  flex-direction: column;
  height: 100vh;
  background: $ai-bg-secondary;
}
</style>
```

## 选用建议

| 场景 | 推荐组件 |
|------|----------|
| 对话主界面 | Conversation + Message + PromptInput |
| 推理 / 工具 | Reasoning、Tool、Confirmation、Plan |
| 代码展示 | CodeBlock、CodeDiff、Snippet、Terminal |
| 内联等待 | AiLoader |
| 全屏 / 特效等待 | AiLoading |
| 多媒体回复 | Image、Attachments |
| 工程产物 | FileTree、Commit、TestResults |

## 设计约定

- 尺寸单位优先 `rpx`
- 主题变量前缀 `$ai-*` / CSS `--ai-*`
- 暗色模式：根节点加 `.ai-dark` 或使用 `useTheme().toggleDark()`
