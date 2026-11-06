# MicSelector 麦克风选择

麦克风设备列表选择器。

## 引入

```ts
import { AiMicSelector } from '@/uni_modules/aiko-ai-elements/components'
```

## AiMicSelector

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `devices` | `{ deviceId: string; label: string }[]` | `[]` | 设备列表 |
| `value` | `string` | `''` | 当前选中 deviceId |
| `defaultValue` | `string` | `''` | 初始选中 |

### Events

| 事件 | 载荷 |
|------|------|
| `value-change` | `deviceId: string` |

## 使用示例

```vue
<template>
  <AiMicSelector
    :devices="devices"
    default-value="default"
    @value-change="onChange"
  />
</template>

<script setup lang="ts">
import { AiMicSelector } from '@/uni_modules/aiko-ai-elements/components'

const devices = [
  { deviceId: 'default', label: '默认麦克风' },
  { deviceId: 'usb-1', label: '外接 USB 麦克风' },
]

function onChange(id: string) {
  console.log(id)
}
</script>
```
