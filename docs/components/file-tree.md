# FileTree 文件树

可展开的文件 / 文件夹树，用于展示项目结构或智能体读写的文件。

## 引入

```ts
import {
  AiFileTree,
  AiFileTreeFolder,
  AiFileTreeFile,
} from '@/uni_modules/aiko-ai-elements/components'
```

## 组件列表

| 组件 | 说明 |
|------|------|
| `AiFileTree` | 根容器 |
| `AiFileTreeFolder` | 文件夹节点 |
| `AiFileTreeFile` | 文件节点 |

## AiFileTree

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `defaultExpanded` | `string[]` | `[]` | 默认展开的路径 |
| `selectedPath` | `string` | `''` | 当前选中路径 |

### Events

| 事件 | 载荷 | 说明 |
|------|------|------|
| `select` | `path: string` | 选中文件 / 文件夹 |
| `expandedChange` | `expanded` | 展开集合变化 |

## AiFileTreeFolder / AiFileTreeFile

| 属性 | 类型 | 说明 |
|------|------|------|
| `path` | `string` | 完整路径（必填） |
| `name` | `string` | 显示名（必填） |
| `icon` | `string` | 仅 File：Remix Icon 名，省略则按扩展名推断 |

插槽：`actions`（操作区）；File 另有 `icon`。

## 使用示例

```vue
<template>
  <AiFileTree :default-expanded="['/src']" @select="onSelect">
    <AiFileTreeFolder path="/src" name="src">
      <AiFileTreeFolder path="/src/components" name="components">
        <AiFileTreeFile path="/src/components/App.vue" name="App.vue" />
      </AiFileTreeFolder>
      <AiFileTreeFile path="/src/main.ts" name="main.ts" />
    </AiFileTreeFolder>
    <AiFileTreeFile path="/package.json" name="package.json" />
  </AiFileTree>
</template>

<script setup lang="ts">
import {
  AiFileTree,
  AiFileTreeFolder,
  AiFileTreeFile,
} from '@/uni_modules/aiko-ai-elements/components'

function onSelect(path: string) {
  console.log('selected', path)
}
</script>
```
