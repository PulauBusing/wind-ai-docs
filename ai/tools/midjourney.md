# Midjourney AI绘画完全指南

Midjourney是目前最强大的AI绘画工具之一，能够根据文字描述生成惊艳的艺术作品。

## 📋 目录

- [快速入门](#快速入门)
- [提示词技巧](#提示词技巧)
- [参数详解](#参数详解)
- [风格指南](#风格指南)
- [实战案例](#实战案例)
- [进阶技巧](#进阶技巧)

## 🚀 快速入门

### 什么是Midjourney

**Midjourney**是一款基于Discord的AI绘画工具，通过文字描述生成高质量图像。

**特点**：
- 🎨 艺术性强，画面精美
- 🚀 生成速度快（约1分钟）
- 💡 创意性好，适合概念设计
- 🌍 支持多种艺术风格
- 👥 社区活跃，灵感丰富

### 注册和订阅

**步骤**：

1. **注册Discord**
   - 访问 https://discord.com
   - 注册账号（需要邮箱）

2. **加入Midjourney**
   - 访问 https://midjourney.com
   - 点击"Join the Beta"
   - 授权Discord

3. **选择订阅**
   - Basic: $10/月（200张图/月）
   - Standard: $30/月（不限量）
   - Pro: $60/月（隐私模式+更多）

### 基本使用

**生成图片流程**：

```
1. 进入Midjourney Discord服务器
2. 找到任一 #newbies 频道
3. 输入命令：/imagine prompt: [你的描述]
4. 等待生成（约1分钟）
5. 选择操作：U（放大）或V（变体）
```

**第一张图片**：

```
/imagine prompt: a cute orange cat sitting on a windowsill, sunset lighting, digital art
```

## 📝 提示词技巧

### 基础结构

**标准格式**：
```
主体 + 细节 + 风格 + 参数

例如：
a majestic dragon, flying over mountains, sunset sky, fantasy art, highly detailed --ar 16:9 --v 6
```

### 提示词组成

#### 1. 主体（Subject）

描述画面的核心内容

**示例**：
- a young woman
- a futuristic city
- a magical forest
- a cyberpunk street

#### 2. 细节描述（Details）

丰富画面内容

**角度视角**：
- close-up（特写）
- wide angle（广角）
- bird's eye view（鸟瞰）
- from behind（背后视角）

**光线**：
- golden hour lighting（黄金时刻）
- studio lighting（影棚打光）
- neon lights（霓虹灯）
- volumetric lighting（体积光）

**材质**：
- watercolor（水彩）
- oil painting（油画）
- 3D render（3D渲染）
- photograph（摄影）

#### 3. 艺术风格（Style）

**艺术流派**：
- impressionism（印象派）
- surrealism（超现实主义）
- art nouveau（新艺术）
- pop art（波普艺术）

**艺术家风格**：
- in the style of Van Gogh
- Studio Ghibli style
- Pixar style
- Artstation trending

**质量描述**：
- highly detailed
- 8k resolution
- ultra realistic
- masterpiece

### 提示词公式

**万能模板**：
```
[主体]，[动作/状态]，[环境]，[光线]，[风格]，[质量] --[参数]

示例：
a beautiful elven warrior, holding a glowing sword, in an enchanted forest, moonlight filtering through trees, fantasy art, highly detailed, 8k --ar 16:9 --v 6
```

**摄影模板**：
```
[主体]，[表情/姿势]，[服装]，[背景]，professional photography, [相机型号]，[镜头]，[光线] --ar 2:3

示例：
a fashion model, confident pose, elegant black dress, urban rooftop at sunset, professional photography, shot with Sony A7III, 85mm lens, golden hour lighting --ar 2:3 --v 6
```

**艺术作品模板**：
```
[主题]，[艺术风格]，[色彩]，[情绪]，by [艺术家]，[媒介] --ar [比例]

示例：
a lone tree on a hill, impressionist style, warm colors, peaceful atmosphere, in the style of Monet, oil painting --ar 4:3 --v 6
```

## ⚙️ 参数详解

### 常用参数

#### --ar（比例）

设置图片长宽比

```
--ar 1:1    (正方形，Instagram)
--ar 4:3    (标准照片)
--ar 16:9   (宽屏，电脑壁纸)
--ar 9:16   (竖屏，手机壁纸)
--ar 2:3    (人像摄影)
--ar 3:2    (风景摄影)
```

#### --v（版本）

选择Midjourney版本

```
--v 6       (最新版本，推荐)
--v 5.2     (上一代)
--v 5.1     (经典版)
--niji 5    (动漫风格专用)
```

#### --s（风格化程度）

控制艺术化程度（0-1000）

```
--s 0       (最真实，接近提示词)
--s 250     (适中，默认值)
--s 750     (艺术化)
--s 1000    (高度艺术化)
```

#### --c（混沌度）

控制变化程度（0-100）

```
--c 0       (准确，变化小)
--c 50      (适中)
--c 100     (变化大，惊喜多)
```

#### --q（质量）

渲染质量（0.25, 0.5, 1, 2）

```
--q 0.5     (快速，消耗少)
--q 1       (标准，推荐)
--q 2       (高质量，慢)
```

### 高级参数

#### --no（排除元素）

```
/imagine a beach scene --no people
(海滩场景，但不要人)

a forest landscape --no trees
(森林风景，但不要树😅)
```

#### --tile（平铺）

生成可平铺的图案

```
floral pattern --tile
(花卉图案，可平铺作为背景)
```

#### --iw（图片权重）

与图片上传结合使用（0-2）

```
/imagine [上传图片] city at night --iw 0.5
```

### 参数组合示例

```
/imagine a cyberpunk street, neon lights, rainy night, highly detailed --ar 16:9 --v 6 --s 750 --q 1

/imagine cute cartoon character --niji 5 --ar 1:1 --s 500

/imagine minimalist logo --v 6 --ar 1:1 --s 50 --no text
```

## 🎨 风格指南

### 艺术风格

**写实风格**：
```
photorealistic, ultra detailed, 8k, professional photography, DSLR
```

**油画风格**：
```
oil painting, brush strokes, impressionist, in the style of Monet
```

**水彩风格**：
```
watercolor, soft colors, dreamy, delicate, painted on paper
```

**插画风格**：
```
digital illustration, vibrant colors, stylized, concept art
```

**动漫风格**：
```
anime style, manga, Studio Ghibli, by Makoto Shinkai --niji 5
```

**赛博朋克**：
```
cyberpunk, neon lights, futuristic, dark atmosphere, blade runner style
```

**蒸汽朋克**：
```
steampunk, Victorian era, brass and copper, mechanical, gears and cogs
```

**魔幻风格**：
```
fantasy art, magical, mystical, enchanted, ethereal lighting
```

### 摄影风格

**人像摄影**：
```
portrait photography, 85mm lens, shallow depth of field, bokeh, professional lighting --ar 2:3
```

**风景摄影**：
```
landscape photography, wide angle, golden hour, dramatic sky, National Geographic style --ar 16:9
```

**微距摄影**：
```
macro photography, extreme close-up, detailed texture, shallow focus
```

**街头摄影**：
```
street photography, candid, urban, black and white, Leica style
```

### 艺术家风格

**引用艺术家**：
```
in the style of [艺术家名字]

示例：
- Van Gogh（梵高）
- Picasso（毕加索）
- Salvador Dalí（达利）
- Hayao Miyazaki（宫崎骏）
- Greg Rutkowski（概念艺术家）
```

## 💼 实战案例

### 案例1：角色设计

**任务**：设计游戏角色

**提示词**：
```
/imagine a female warrior character, long silver hair, wearing ornate armor, holding a magic staff, fantasy RPG style, detailed character design, front view, full body, white background, concept art, highly detailed --ar 2:3 --v 6
```

**优化技巧**：
1. 指定"front view"（正面视图）
2. "white background"（白色背景）
3. "full body"（全身）
4. 使用2:3比例适合角色展示

### 案例2：场景概念图

**任务**：科幻城市场景

**提示词**：
```
/imagine futuristic city skyline, flying cars, neon advertisements, cyberpunk aesthetic, rainy night, reflections on wet streets, volumetric fog, cinematic lighting, wide angle, highly detailed, 8k --ar 16:9 --v 6 --s 750
```

**关键要素**：
- 明确风格（cyberpunk）
- 环境氛围（rainy night）
- 光线效果（volumetric fog）
- 构图（wide angle）

### 案例3：产品设计

**任务**：科技产品渲染

**提示词**：
```
/imagine minimalist smartwatch, sleek design, metallic finish, floating in white space, studio lighting, professional product photography, high-end tech, clean background, 3D render, ultra realistic, 8k --ar 1:1 --v 6 --s 50
```

**要点**：
- 降低风格化（--s 50）
- 强调写实（ultra realistic）
- 产品摄影术语

### 案例4：艺术海报

**任务**：电影海报风格

**提示词**：
```
/imagine movie poster, a lone astronaut standing on an alien planet, two moons in the sky, dramatic lighting, epic scale, sci-fi adventure, cinematic composition, trending on artstation, highly detailed --ar 2:3 --v 6
```

### 案例5：Logo设计

**任务**：品牌Logo

**提示词**：
```
/imagine minimalist logo design, abstract mountain and sun symbol, modern, clean lines, professional, vector style, black and white, simple geometry --ar 1:1 --v 6 --s 50 --no text, letters
```

**注意**：
- 使用--no text排除文字
- 降低风格化保持简洁
- 正方形比例

## 🔧 进阶技巧

### 图片融合（Blend）

**命令**：/blend

```
上传2-5张图片
Midjourney会融合它们的特征
生成新图片
```

**用途**：
- 融合风格
- 组合元素
- 创意实验

### 图片作为参考

**Image Prompt**：

```
/imagine [上传图片URL] a futuristic version --iw 1.5
```

**权重说明**：
- --iw 0.5：轻微参考
- --iw 1.0：平衡参考（默认）
- --iw 2.0：强烈参考

### 种子值（Seed）

**用途**：复现相似结果

```
生成图片后，使用✉️表情获取seed值
复用：--seed [数字]

/imagine sunset beach --seed 12345
```

### Remix模式

**开启**：/settings → Remix mode

**作用**：在变体时修改提示词

```
原图：a red car
Remix：a blue car（保持构图，改颜色）
```

### 描述图片（Describe）

**命令**：/describe

```
上传图片
Midjourney生成4个描述
可用于学习提示词
```

## 💡 实用技巧总结

### DO - 应该做的

1. **✅ 具体描述**
   - 详细描述主体和细节
   
2. **✅ 使用专业术语**
   - 摄影、艺术术语提升质量
   
3. **✅ 指定风格**
   - 明确艺术风格或流派
   
4. **✅ 多次尝试**
   - 生成多张选最佳
   
5. **✅ 使用U和V**
   - U放大细节
   - V生成变体

### DON'T - 不应该做的

1. **❌ 过于简单**
   - "a cat"太模糊
   
2. **❌ 堆砌关键词**
   - 太多词反而混乱
   
3. **❌ 期望完美文字**
   - MJ不擅长生成文字
   
4. **❌ 违反政策**
   - 不生成暴力、成人内容
   
5. **❌ 完全依赖**
   - 需要后期处理和筛选

### 提升质量的秘诀

**3要素法则**：
```
1. 主体要明确
2. 风格要统一
3. 细节要丰富
```

**质量关键词**：
```
highly detailed, 8k, ultra realistic, masterpiece, trending on artstation, professional, cinematic lighting
```

### 快速生成套路

**速成公式**：
```
[具体主体] + [精确描述] + [风格关键词] + [质量词] + 合适参数

示例：
a dragon, perched on a mountain peak, breathing fire, fantasy art style, epic scene, highly detailed, dramatic lighting, 8k --ar 16:9 --v 6
```

## 💰 订阅建议

### Basic Plan（$10/月）

**适合**：
- 新手试用
- 偶尔使用
- 个人爱好

**限制**：
- 200张图/月
- 约3.3小时快速生成
- 作品公开

### Standard Plan（$30/月）

**适合**：
- 设计师
- 创作者
- 商业使用（基础）

**包含**：
- 15小时快速生成
- 无限慢速生成
- 可选私密模式

### Pro Plan（$60/月）

**适合**：
- 专业设计师
- 商业项目
- 大量使用

**包含**：
- 30小时快速生成
- 无限慢速生成
- 隐私模式（Stealth Mode）
- 最高优先级

## 🎯 常见问题

### Q: 生成的图片版权归谁？

**A**: 
- 付费用户：拥有商业使用权
- 免费试用：有限使用权
- 详见：https://midjourney.com/terms

### Q: 如何生成一致的角色？

**A**:
1. 使用相同的seed值
2. 使用image prompt作为参考
3. 详细描述角色特征
4. 使用--cref参数（角色参考）

### Q: 图片模糊怎么办？

**A**:
1. 使用U放大
2. 添加"highly detailed, 8k"
3. 使用--q 2提高质量
4. 后期使用AI放大工具

### Q: 文字总是错的？

**A**:
- Midjourney不擅长生成文字
- 建议后期用PS添加
- 或使用专门的文字生成工具

### Q: 如何学习好的提示词？

**A**:
1. 在社区频道查看他人作品
2. 使用/describe学习
3. 收集优秀提示词
4. 不断实验和迭代

## 📚 学习资源

### 官方资源

- [Midjourney官网](https://midjourney.com)
- [Discord社区](https://discord.gg/midjourney)
- [官方文档](https://docs.midjourney.com)
- [更新公告](https://midjourney.com/announcements)

### 社区资源

- [Midjourney Showcase](https://www.midjourney.com/showcase)
- Reddit: r/midjourney
- Twitter: #midjourney
- [Prompt数据库](https://prompthero.com/midjourney-prompts)

### 教程推荐

- YouTube: Midjourney教程
- B站：Midjourney中文教程
- 在线课程平台

## 🔗 相关工具

### 替代品

- **Stable Diffusion**：开源免费，可本地部署
- **DALL-E 3**：OpenAI的图像生成
- **Firefly**：Adobe的AI绘画
- **文心一格**：百度的AI绘画（国内）

### 辅助工具

- **PromptBase**：提示词市场
- **Promptomania**：提示词生成器
- **Upscayl**：AI图片放大
- **Remove.bg**：AI抠图

## 下一步

- 💬 [ChatGPT使用](ai/tools/chatgpt.md)
- 💻 [Cursor编程](ai/tools/cursor.md)
- 📝 [提示词工程](ai/fundamentals/prompt-engineering.md)
- 🎨 [Stable Diffusion](ai/tools/stable-diffusion.md)

---

?> **小贴士**：Midjourney的魅力在于创作的不确定性。同一个提示词可能生成完全不同的结果，这正是AI创作的乐趣所在。多实验，多尝试，享受创作过程！

