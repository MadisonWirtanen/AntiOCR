# AntiOCR

AntiOCR 是一个纯前端的图片文字抗识别工具，提供两类处理方式：

- **微信 GIF 模式**：将普通图片转换为 GIF，适合微信发送场景。
- **静态图片模式**：导出带文字结构扰动的 PNG / JPG，适用于需要静态文件的场景。

所有图片处理都在浏览器本地完成，图片本身不会上传到服务器。

## 在线使用

GitHub Pages：<https://madisonwirtanen.github.io/AntiOCR/>

## 功能

### 微信 GIF 模式

在部分微信客户端环境中，GIF 与普通静态图片的文字识别行为存在差异，因此可以优先尝试 GIF 模式。

提供两种生成方式：

- **兼容模式**：优先保持原图观感与微信中的正常显示。
- **四相模式**：使用多帧动态结构，作为兼容模式之外的补充方案。

> 平台的 OCR 策略可能随客户端版本、图片内容和服务端策略变化，本项目不能保证在所有环境中都阻止文字识别。

### 静态图片模式

当目标平台需要 PNG / JPG 等静态图片时，可以使用静态模式。

内置三档预设：

- **阅读优先**：优先保留文字可读性。
- **平衡**：兼顾可读性与抗识别效果，默认选项。
- **拦截优先**：使用更明显的结构扰动。

静态模式包含行级扰动、微断笔、伪轮廓、纹理干扰与前景区域检测，并支持进一步调整高级参数。

## 使用方法

1. 打开在线页面，或直接打开仓库中的 `index.html`。
2. 选择、拖入或粘贴一张 PNG、JPEG 或 WebP 图片。
3. 根据用途选择 **微信 GIF 模式** 或 **静态图片模式**。
4. 调整需要的模式、尺寸或强度参数。
5. 处理完成后下载生成的文件。

在微信场景下，建议直接发送下载得到的原始 GIF，不要截图或重新转换为静态图片。

## 本地资源与部署

页面使用的 GIF 编码依赖已经随仓库一同提供：

- `./assets/js/gif.js`
- `./assets/js/gif.worker.js`

页面与 Worker 均使用**相对路径**引用，因此部署在 GitHub Pages 子路径、自定义域名或其他静态站点目录时，不依赖固定域名或根路径。

只要保持以下目录结构即可：

```text
AntiOCR/
├── index.html
├── assets/
│   └── js/
│       ├── gif.js
│       └── gif.worker.js
├── README.md
├── THIRD_PARTY_NOTICES.md
└── LICENSE
```

## 隐私

图片的读取、处理和导出均在浏览器本地完成。项目运行时不需要把图片上传到第三方服务。

## 兼容性

建议使用较新的 Chrome、Edge、Firefox 或 Safari。GIF 生成依赖 Web Worker、Canvas、Blob 与 Typed Array 等现代浏览器能力。

## 限制

AntiOCR 的目标是降低 OCR 自动识别的稳定性，而不是提供绝对的文字隐藏或加密能力。

不同 OCR 引擎、平台版本、图片压缩方式以及二次转码都可能影响最终效果。对于敏感信息，请不要仅依赖图片抗 OCR 处理来实现保密。

## 第三方组件

GIF 编码使用 [gif.js.optimized](https://github.com/terikon/gif.js.optimized)，其许可信息见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md)。

## License

本项目采用 [MIT License](LICENSE) 开源。
