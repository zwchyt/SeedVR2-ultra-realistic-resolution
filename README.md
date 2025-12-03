## SeedVR2超真实分辨率图像极限放大工作流（中文｜English）

**一个专为“极限放大任意图像”打造的一键式超高倍率无损放大工作流**  
A one-click extreme image upscale workflow using `SeedVR2 + smart tiling` (supports 7x+ magnification with almost no quality loss).

功能 | Features
| 功能                  | 说明                                      |
|-----------------------|-------------------------------------------|
| 智能瓦片分割（TTP Toolset） | 自动将大图切成 1024×1024 瓦片，完美避免显存爆炸       |
| SeedVR2 3B 真实超分      | 单张图像极限放大（支持 7 倍以上，细节自然电影感）     |
| 智能尺寸计算与重组       | 自动计算瓦片大小、重采样、精确重组原图比例            |
| rgthree Image Comparer | 实时滑动对比原图 vs 极限放大结果                  |
| 一键保存与显存友好       | 全程显存峰值仅 ≈12GB（RTX 4090）                  |

### 所需模型（与 Z-Image 工作流完全共享，无需额外下载）

| 节点              | 文件名                            | 放置路径                       |
|-------------------|-----------------------------------|--------------------------------|
| SeedVR2 DiT       | `seedvr2_ema_3b_fp16.safetensors` | `models/diffusion_models/`     |
| SeedVR2 VAE       | `ema_vae_fp16.safetensors`        | `models/vae/`                  |

### 必装自定义节点（已在上方 Z-Image 章节列出，无需重复安装）
- comfyui_ttp_toolset（提供瓦片分割与重组节点，必装）
- comfyui_essentials（提供高级尺寸调整，必装）
- rgthree-comfy（对比器，必装）
- SeedVR2 Video Upscaler（核心超分，必装）

**新增节点安装**：打开 ComfyUI Manager → 搜索并安装：
- comfyui_ttp_toolset
- comfyui_essentials

### 使用方法 | How to Use

1. 将本仓库中的 `extreme-upscale.json`（或 `图像极限放大.json`）拖入 ComfyUI 界面
2. 在 **Load Image** 节点上传您想放大的任意图像（支持超大图）
3. 点击 **Queue Prompt**，全程自动完成
4. 生成结果自动保存到 `ComfyUI/output/`，并可通过滑动条实时对比

### 推荐参数（已预设，可微调）
- 瓦片大小：1024×1024（平衡速度与质量）
- 放大倍率：7 倍（可改更高，显存会略增）
- SeedVR2 分辨率：1024（固定瓦片分辨率）
- 颜色校正：none（保持原图色调）

### 示例效果 | Samples

工作流演示  
![图像极限放大 完整工作流](samples/Z-image.png)  

| 原图                  | 极限放大后（7 倍放大示例）                  |
|-----------------------|---------------------------------------|
| ![原图示例](samples/Z-image.png) | ![7倍放大结果](samples/X-image.png) |

> 可轻松将 512×512 小图放大到 3584×3584 以上，细节清晰无糊  
> 支持风景、人像、插画等所有类型图像

更多放大案例持续更新 → [查看 samples 文件夹](samples/)
