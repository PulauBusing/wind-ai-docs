# Stable Diffusion 完全指南

Stable Diffusion是最强大的开源AI绘画工具，可以免费使用，支持本地部署，完全掌控你的创作。

## 📋 目录

- [什么是Stable Diffusion](#什么是stable-diffusion)
- [使用方式](#使用方式)
- [本地部署](#本地部署)
- [提示词技巧](#提示词技巧)
- [模型和LoRA](#模型和lora)
- [实战案例](#实战案例)
- [进阶技巧](#进阶技巧)

## 🎯 什么是Stable Diffusion

### 简介

**Stable Diffusion (SD)**是由Stability AI开发的开源文生图AI模型，是Midjourney的主要竞争对手。

**核心优势**：
- 🆓 **完全免费**：开源，无需付费
- 💻 **本地运行**：可在自己电脑运行
- 🔧 **高度可控**：精确控制生成过程
- 🎨 **模型丰富**：海量社区模型
- 🔓 **无审查**：内容限制少
- 🛠️ **可定制**：支持训练自己的模型

### SD vs Midjourney

| 特性 | Stable Diffusion | Midjourney |
|------|-----------------|------------|
| **价格** | 免费 | $10-60/月 |
| **使用方式** | 本地/在线 | 仅Discord |
| **学习曲线** | 较陡 | 简单 |
| **艺术性** | 取决于模型 | 很强 |
| **可控性** | 非常强 | 一般 |
| **速度** | 取决于硬件 | 快 |
| **模型选择** | 丰富 | 固定 |
| **商业使用** | ✅ | ✅ |

### 版本演进

```
SD 1.5  → SD 2.0/2.1 → SDXL 1.0 → SD 3.0

当前推荐：
- SD 1.5：兼容性好，模型多
- SDXL：质量高，细节好
```

## 🚀 使用方式

### 方式1：在线平台（最简单）

**免费平台**：

1. **Hugging Face Spaces**
   - 网址：https://huggingface.co/spaces
   - 搜索 "Stable Diffusion"
   - 免费，但可能排队

2. **DreamStudio**
   - 网址：https://beta.dreamstudio.ai
   - Stability AI官方
   - 新用户有免费额度

3. **Clipdrop**
   - 网址：https://clipdrop.co
   - 简单易用
   - 部分功能免费

**国内平台**：
- **文心一格**（百度）
- **通义万相**（阿里）
- **6pen**（国产SD平台）

### 方式2：Colab云端（免费GPU）

**优势**：
- ✅ 免费GPU
- ✅ 无需本地配置
- ✅ 运行速度快

**步骤**：

```python
# Google Colab笔记本
# 1. 安装依赖
!pip install diffusers transformers accelerate

# 2. 加载模型
from diffusers import StableDiffusionPipeline
import torch

model_id = "runwayml/stable-diffusion-v1-5"
pipe = StableDiffusionPipeline.from_pretrained(
    model_id,
    torch_dtype=torch.float16
)
pipe = pipe.to("cuda")

# 3. 生成图片
prompt = "a beautiful landscape, mountains, sunset, highly detailed"
image = pipe(prompt).images[0]
image.save("output.png")
```

### 方式3：本地部署（最强大）

**系统要求**：
- Windows 10/11, Linux, macOS
- NVIDIA显卡（推荐RTX 3060以上，6GB+显存）
- 16GB+ 内存
- 20GB+ 硬盘空间

**推荐工具**：
1. **Stable Diffusion WebUI** (最流行)
2. **ComfyUI** (节点式，专业)
3. **InvokeAI** (用户友好)

## 💻 本地部署教程

### 使用Stable Diffusion WebUI

**一键安装包（推荐）**：

**Windows**：
```bash
# 1. 下载安装包
https://github.com/AUTOMATIC1111/stable-diffusion-webui

# 2. 解压后运行
webui-user.bat

# 3. 等待自动安装依赖（首次较慢）

# 4. 浏览器打开
http://localhost:7860
```

**Linux/Mac**：
```bash
# 1. 克隆仓库
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
cd stable-diffusion-webui

# 2. 运行安装脚本
./webui.sh

# 3. 访问
http://localhost:7860
```

**手动安装**：

```bash
# 1. 安装Python 3.10.6
# 下载：https://www.python.org/

# 2. 安装Git
# 下载：https://git-scm.com/

# 3. 克隆WebUI
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git

# 4. 下载模型（放到 models/Stable-diffusion/ 目录）
# Hugging Face: https://huggingface.co/runwayml/stable-diffusion-v1-5
# Civitai: https://civitai.com/

# 5. 运行
cd stable-diffusion-webui
python launch.py
```

### WebUI界面介绍

```
┌─────────────────────────────────────────┐
│  [txt2img] [img2img] [Extras] [PNG Info]│
├─────────────────────────────────────────┤
│                                         │
│  提示词输入框                           │
│  ┌───────────────────────────────┐     │
│  │ a beautiful woman...          │     │
│  └───────────────────────────────┘     │
│                                         │
│  反向提示词                             │
│  ┌───────────────────────────────┐     │
│  │ ugly, bad quality...          │     │
│  └───────────────────────────────┘     │
│                                         │
│  参数设置：                             │
│  [采样方法▼] [步数] [CFG] [尺寸]       │
│                                         │
│  [生成] [中断]                         │
│                                         │
│  生成结果显示区                         │
│  ┌───────────────┐                     │
│  │               │                     │
│  │  生成的图片   │                     │
│  │               │                     │
│  └───────────────┘                     │
└─────────────────────────────────────────┘
```

### 基础设置

**推荐配置**：

```
采样方法：DPM++ 2M Karras（速度快，质量好）
采样步数：20-30（更高=更好但更慢）
CFG Scale：7-11（文本引导强度）
尺寸：512x512（SD1.5）或 1024x1024（SDXL）
```

## 📝 提示词技巧

### 基础结构

**正向提示词（Prompt）**：
```
画面内容 + 质量标签 + 风格标签 + 细节描述

示例：
beautiful anime girl, long silver hair, blue eyes, 
smiling, school uniform, cherry blossoms background,
masterpiece, best quality, highly detailed,
anime style, soft lighting, 8k
```

**反向提示词（Negative Prompt）**：
```
排除不想要的元素

常用：
ugly, bad quality, blurry, deformed, disfigured,
bad anatomy, extra limbs, watermark, text, signature,
low resolution, jpeg artifacts
```

### 权重控制

**强调**：
```
(keyword)           # 权重 x1.1
((keyword))         # 权重 x1.21
(keyword:1.5)       # 自定义权重
```

**减弱**：
```
[keyword]           # 权重 x0.9
[keyword:0.5]       # 自定义权重
```

**示例**：
```
(beautiful face:1.3), detailed eyes, [background:0.8]
```

### 提示词模板

**人物肖像**：
```
(masterpiece:1.2), best quality, ultra detailed,
portrait of a beautiful woman, [年龄] years old,
[发型], [发色], [眼睛颜色] eyes,
[表情], [服装描述],
[场景], [光线],
[艺术风格]

Negative:
ugly, bad anatomy, bad hands, deformed, blurry,
low quality, watermark, signature
```

**风景**：
```
(masterpiece:1.2), best quality, highly detailed,
beautiful landscape, [地点],
[天气], [时间],
[特殊元素],
professional photography, 8k, HDR

Negative:
low quality, blurry, overexposed, underexposed,
people, watermark
```

**二次元动漫**：
```
(masterpiece:1.2), best quality, highly detailed,
1girl/1boy, [年龄], [发型特征],
[服装风格], [动作/姿势],
[背景], anime style, [风格标签],
vibrant colors, detailed eyes

Negative:
3d, realistic, photo, ugly, bad anatomy,
bad hands, extra fingers, watermark
```

## 🎨 模型和LoRA

### 模型类型

**大模型（Checkpoint）**：

1. **SD 1.5系列**
   - **Anything V5**：二次元通用
   - **Realistic Vision**：写实人像
   - **DreamShaper**：梦幻风格
   - **MeinaMix**：动漫风格

2. **SDXL系列**
   - **SDXL Base**：官方基础
   - **Juggernaut XL**：通用高质量
   - **RealVisXL**：写实风格

**下载地址**：
- [Civitai](https://civitai.com/)（最大社区）
- [Hugging Face](https://huggingface.co/)
- [LiblibAI](https://www.liblib.ai/)（国内）

### LoRA（Low-Rank Adaptation）

**什么是LoRA**：
- 小型模型文件（几MB到几百MB）
- 用于特定风格或角色
- 可叠加使用

**使用方法**：
```
将LoRA文件放到：models/Lora/

在提示词中添加：
<lora:文件名:权重>

示例：
<lora:chinese_dress:0.8>
```

**推荐LoRA**：
- **Add Detail**：增加细节
- **Fashion Girl**：时尚女性
- **Concept Art**：概念设计
- **各种角色LoRA**

### VAE（变分自编码器）

**作用**：改善色彩和细节

**使用**：
```
Settings → Stable Diffusion → SD VAE
选择对应的VAE文件
```

## 💼 实战案例

### 案例1：生成动漫角色

**需求**：创建一个动漫少女角色

**设置**：
```
模型：Anything V5
采样器：DPM++ 2M Karras
步数：25
CFG：7
尺寸：512x768
```

**提示词**：
```
Prompt:
(masterpiece:1.2), best quality, highly detailed,
1girl, 18 years old, long flowing hair, silver hair,
blue eyes, detailed eyes, beautiful face,
school uniform, white shirt, blue skirt,
standing, slight smile, looking at viewer,
cherry blossom trees, spring, soft lighting,
anime style, vibrant colors

Negative:
nsfw, ugly, bad anatomy, bad hands, extra fingers,
deformed, disfigured, mutation, bad proportions,
low quality, blurry, watermark, text, signature
```

### 案例2：写实人像

**需求**：专业人像摄影

**设置**：
```
模型：Realistic Vision
采样器：DPM++ SDE Karras
步数：30
CFG：8
尺寸：512x768
```

**提示词**：
```
Prompt:
professional portrait photography,
beautiful young woman, 25 years old,
natural makeup, confident expression,
elegant business attire, modern office background,
soft studio lighting, shallow depth of field,
shot with Sony A7III, 85mm f/1.4,
8k, ultra detailed, photorealistic

Negative:
cartoon, anime, painting, illustration, 3d render,
ugly, deformed, bad anatomy, low quality, blurry,
watermark, text, signature, overexposed
```

### 案例3：风景摄影

**需求**：自然风光

**提示词**：
```
Prompt:
(masterpiece:1.2), best quality, highly detailed,
beautiful mountain landscape, snow-capped peaks,
pristine alpine lake reflecting mountains,
autumn colors, golden hour lighting,
dramatic clouds, sunset sky,
professional landscape photography,
national geographic style,
8k uhd, HDR, sharp focus

Negative:
people, humans, animals, buildings, urban,
low quality, blurry, overexposed, watermark
```

### 案例4：概念设计

**需求**：科幻场景

**提示词**：
```
Prompt:
(masterpiece:1.2), best quality, highly detailed,
futuristic cyberpunk city, neon lights,
flying cars, massive skyscrapers,
holographic advertisements, rain, night scene,
cinematic lighting, volumetric fog,
concept art style, trending on artstation,
ultra detailed, 8k

Negative:
low quality, blurry, simple, amateur,
watermark, text, signature
```

### 案例5：产品设计

**需求**：产品渲染图

**提示词**：
```
Prompt:
product photography, modern smartwatch,
sleek minimalist design, metallic finish,
floating on white background,
professional studio lighting, soft shadows,
8k, ultra detailed, commercial photography,
product visualization, clean, elegant

Negative:
blurry, low quality, cluttered background,
bad lighting, dirty, watermark
```

## 🔧 进阶技巧

### img2img（图生图）

**用途**：
- 修改现有图片
- 风格转换
- 局部重绘

**步骤**：
```
1. 切换到 img2img 标签
2. 上传参考图片
3. 设置 Denoising strength（0.3-0.7）
   - 低值：接近原图
   - 高值：变化大
4. 输入提示词
5. 生成
```

### ControlNet（精确控制）

**功能**：精确控制画面构图

**类型**：
- **Canny**：边缘检测
- **Depth**：深度图控制
- **OpenPose**：人物姿态
- **Scribble**：草图转图
- **Seg**：语义分割

**使用**：
```
1. 安装ControlNet扩展
2. 上传控制图
3. 选择控制类型
4. 调整权重
5. 生成
```

### Inpainting（局部重绘）

**用途**：修改图片局部区域

**步骤**：
```
1. 切换到 inpaint 标签
2. 上传图片
3. 用笔刷涂抹要修改的区域
4. 输入新的描述
5. 生成
```

### 批量生成

**X/Y/Z Plot**：
```
用于测试不同参数组合
例如：
X轴：不同采样器
Y轴：不同CFG值
批量生成对比
```

### 高清修复（Hires Fix）

**作用**：生成更高分辨率图片

**设置**：
```
1. 勾选 Hires. fix
2. 设置放大倍数（1.5-2x）
3. 选择放大算法
4. 设置 Denoising strength（0.4-0.6）
```

## 🎓 优化技巧

### 提高质量

**通用技巧**：
```
1. 使用质量标签：
   masterpiece, best quality, highly detailed,
   ultra detailed, 8k, professional

2. 详细描述：
   越详细，结果越可控

3. 合适的采样步数：
   20-30步通常足够

4. 调整CFG：
   7-11之间实验
```

### 提高速度

**优化方法**：
```
1. 降低分辨率先预览
2. 减少采样步数
3. 使用更快的采样器
4. 启用xFormers（省显存）
5. 使用半精度（--medvram）
```

### 显存优化

**低显存设置**：
```bash
# 4GB显存
webui-user.bat 添加：
--medvram --opt-split-attention

# 2GB显存
--lowvram --opt-split-attention
```

## 🛠️ 常用扩展

**必装扩展**：

1. **ControlNet**
   - 精确控制构图

2. **Additional Networks**
   - LoRA管理

3. **Dynamic Prompts**
   - 提示词模板

4. **Image Browser**
   - 图片浏览器

5. **Aspect Ratio Helper**
   - 比例助手

**安装方法**：
```
Extensions → Available → 搜索 → Install
或
Extensions → Install from URL → 粘贴GitHub链接
```

## 💡 实用技巧总结

### DO - 应该做的

1. **✅ 详细描述**
   - 具体描述想要的内容

2. **✅ 使用质量标签**
   - masterpiece, best quality等

3. **✅ 写好负面提示词**
   - 排除不想要的元素

4. **✅ 多次生成**
   - 批量生成选最佳

5. **✅ 保存参数**
   - 记录好的配置

### DON'T - 不应该做的

1. **❌ 过度复杂**
   - 提示词太长反而混乱

2. **❌ 忽略负面提示词**
   - 会出现很多瑕疵

3. **❌ CFG过高**
   - >15可能过拟合

4. **❌ 步数过多**
   - >50通常无意义

5. **❌ 期望一次完美**
   - 需要多次调整

### 提示词公式

**万能公式**：
```
[质量标签], [主体], [细节描述],
[风格], [光线], [构图], [渲染质量]

Negative:
[质量问题], [解剖问题], [风格冲突],
[技术问题], [水印文字]
```

## 📚 学习资源

### 社区网站

- **Civitai**：最大模型社区
  - https://civitai.com/
  - 海量模型和LoRA
  - 提示词参考

- **LiblibAI**：国内社区
  - https://www.liblib.ai/
  - 中文友好

- **HuggingFace**：模型仓库
  - https://huggingface.co/

### 学习资源

- **Reddit**: r/StableDiffusion
- **Discord**: Stable Diffusion社区
- **YouTube**: SD教程频道
- **B站**: SD中文教程

### 工具推荐

- **PromptHero**：提示词灵感
- **Lexica**：SD作品搜索
- **NovelAI Tag生成器**
- **AI绘画魔咒百科词典**

## ❓ 常见问题

### Q: 最低配置要求？

**A**:
- **最低**: GTX 1060 6GB
- **推荐**: RTX 3060 12GB
- **理想**: RTX 4070 12GB+

### Q: 生成速度慢怎么办？

**A**:
1. 降低分辨率
2. 减少采样步数
3. 使用更快的采样器
4. 升级显卡

### Q: 显存不足怎么办？

**A**:
```
启动参数添加：
--medvram  # 中显存优化
--lowvram  # 低显存优化
--xformers # 进一步优化
```

### Q: 如何生成NSFW内容？

**A**:
- 注意遵守当地法律
- 不分享不当内容
- 使用私密模式

### Q: 能商用吗？

**A**:
- SD开源，可商用
- 具体模型需查看许可
- 注意版权问题

## 🔗 相关工具

### AI绘画工具

- **Midjourney**：付费，质量高
- **DALL-E 3**：OpenAI出品
- **Leonardo.ai**：在线SD
- **文心一格**：国产免费

### 辅助工具

- **Upscayl**：AI图片放大
- **Remove.bg**：AI抠图
- **Photoshop SD插件**
- **Krita AI插件**

## 下一步

- 🎨 [Midjourney绘画](ai/tools/midjourney.md)
- 💬 [ChatGPT指南](ai/tools/chatgpt.md)
- 📝 [提示词工程](ai/fundamentals/prompt-engineering.md)
- 🛠️ [更多AI工具](ai/tools/README.md)

---

?> **核心建议**：Stable Diffusion学习曲线较陡，但掌握后非常强大。建议从在线平台开始，熟悉后再部署本地。多看优秀作品的提示词，多实践，慢慢就能生成理想的图片！
