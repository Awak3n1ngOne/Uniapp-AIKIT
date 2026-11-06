# Image 图片组件

消息中的 AI 生成图片展示，含加载骨架、错误占位与点击预览。

## 引入

```ts
import { AiImage } from '@/uni_modules/aiko-ai-elements/components/image'
```

## AiImage

### Props

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `src` | `string` | 必填 | 图片地址 |
| `alt` | `string` | - | 替代文字（错误态展示） |
| `mode` | `string` | `'aspectFill'` | uni-app image 裁剪模式 |
| `width` | `string \| number` | - | 宽度（数字视为 rpx） |
| `height` | `string \| number` | - | 高度 |
| `radius` | `string \| number` | - | 圆角，如 `16`、`'50%'` |
| `preview` | `boolean` | `true` | 点击调用 `uni.previewImage` |
| `lazyLoad` | `boolean` | `true` | 懒加载 |

### Events

| 事件 | 说明 |
|------|------|
| `load` | 加载完成 |
| `error` | 加载失败 |
| `click` | 点击（在预览前触发） |

## 使用示例

```vue
<AiImage
  src="https://example.com/image.png"
  alt="示例图片"
  :width="560"
  :height="360"
  radius="16rpx"
  @load="onLoad"
/>
```

### 在消息中

```vue
<AiMessage from="assistant">
  <AiMessageContent>
    <AiImage :src="imageUrl" :width="480" :height="480" />
  </AiMessageContent>
</AiMessage>
```

### 关闭点击预览

```vue
<AiImage :src="url" :preview="false" @click="customHandler" />
```
