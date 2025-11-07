# Cursor AI 编程实战指南

Cursor是一款AI原生的代码编辑器，基于VSCode构建，集成了强大的AI辅助编程能力。

## 📋 目录

- [简介](#简介)
- [安装配置](#安装配置)
- [核心功能](#核心功能)
- [使用技巧](#使用技巧)
- [实战案例](#实战案例)
- [快捷键](#快捷键)
- [高级功能](#高级功能)
- [常见问题](#常见问题)

## 🎯 简介

### 什么是Cursor

Cursor是新一代AI代码编辑器，将GPT-4等大模型深度集成到编程工作流中。

**核心特点**：
- 🤖 **AI原生设计**：从零打造的AI编程体验
- 💬 **对话式编程**：用自然语言编写代码
- 📝 **智能补全**：超越传统代码补全
- 🔍 **代码理解**：深度理解整个项目
- ✨ **一键重构**：AI辅助代码优化
- 🐛 **智能Debug**：自动发现和修复问题

### Cursor vs 传统编辑器

| 特性 | Cursor | VS Code + Copilot | VS Code |
|------|--------|-------------------|---------|
| AI对话 | ⭐⭐⭐⭐⭐ | ⭐⭐ | ❌ |
| 代码补全 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| 项目理解 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ❌ |
| 代码生成 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ❌ |
| 学习曲线 | 低 | 低 | 低 |
| 价格 | $20/月 | $10/月 | 免费 |

### 为什么选择Cursor

**适合人群**：
- ✅ 各水平的开发者
- ✅ 想提高编码效率
- ✅ 学习新技术/框架
- ✅ 重构遗留代码
- ✅ 快速原型开发

**优势**：
1. **效率翻倍**：减少重复代码编写
2. **降低门槛**：新手也能写出好代码
3. **学习助手**：边写边学
4. **减少错误**：AI帮助发现潜在问题
5. **无缝迁移**：兼容VS Code插件

## 🚀 安装配置

### 下载安装

**官网下载**：
```
https://cursor.sh
```

**支持平台**：
- Windows
- macOS
- Linux

**安装步骤**：
1. 下载对应平台的安装包
2. 运行安装程序
3. 首次启动会引导设置
4. 登录账号

### 账号注册

**方式**：
- Google账号登录
- GitHub账号登录
- 邮箱注册

**订阅计划**：
- ✅ **免费版**：每月2000次AI请求
- 💰 **Pro版**：$20/月，无限制使用

### 从VS Code迁移

**导入设置**：
```
Cursor会自动检测VS Code配置
可以一键导入：
- 快捷键配置
- 编辑器设置
- 已安装插件
```

**同步插件**：
1. File → Preferences → Extensions
2. 搜索并安装常用插件
3. Cursor兼容大部分VS Code插件

### 基础配置

**推荐设置**：

```json
{
  // AI功能
  "cursor.ai.enabled": true,
  "cursor.ai.model": "gpt-4",
  
  // 自动补全
  "cursor.autocomplete.enabled": true,
  "cursor.autocomplete.triggerDelay": 300,
  
  // 编辑器
  "editor.fontSize": 14,
  "editor.tabSize": 2,
  "editor.formatOnSave": true,
  
  // 主题
  "workbench.colorTheme": "One Dark Pro"
}
```

## 💡 核心功能

### 1. AI Chat（AI对话）

**快捷键**：`Cmd/Ctrl + L`

**功能**：在侧边栏打开AI对话窗口

**使用场景**：

**① 代码生成**：
```
你: 用TypeScript写一个防抖函数

AI: [生成完整代码]
```

**② 代码解释**：
```
选中代码 → Cmd+L
你: 解释这段代码

AI: 这段代码实现了...
```

**③ Bug修复**：
```
你: 这段代码报错了，帮我修复
[粘贴错误信息]

AI: 问题出在...，应该改成...
```

**④ 项目问答**：
```
你: 这个项目的登录逻辑在哪里？

AI: 登录逻辑主要在 src/auth/login.ts...
```

### 2. Cmd K（行内编辑）

**快捷键**：`Cmd/Ctrl + K`

**功能**：在当前光标位置进行AI编辑

**使用方式**：

**① 生成代码**：
```javascript
// 按Cmd+K，输入：创建一个用户类
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }
  // AI会继续生成...
}
```

**② 修改代码**：
```javascript
// 选中代码，按Cmd+K
// 输入：添加错误处理

// AI会在原代码基础上添加try-catch等
```

**③ 重构**：
```javascript
// 选中函数，按Cmd+K
// 输入：优化这个函数的性能

// AI会提供优化后的版本
```

### 3. Tab补全

**触发**：自动触发或按`Tab`接受建议

**特点**：
- 🚀 速度快
- 🎯 准确度高
- 🧠 理解上下文
- 📚 学习项目风格

**示例**：
```javascript
// 你输入：
function calculateTo

// AI自动补全：
function calculateTotal(items) {
  return items.reduce((sum, item) => sum + item.price, 0);
}
```

### 4. @符号功能

**用法**：在Chat中使用`@`引用

**可引用**：
- `@文件名` - 引用特定文件
- `@代码` - 引用选中的代码
- `@文档` - 引用文档
- `@Codebase` - 引用整个项目

**示例**：
```
@app.js 这个文件的路由配置有什么问题？

@users.ts 基于这个文件，创建一个管理员用户类
```

### 5. 代码搜索

**功能**：AI理解的代码搜索

**使用**：
```
Cmd+P → 输入查询

例如：
- "处理支付的函数"
- "用户认证相关"
- "数据库连接配置"
```

## 🎨 使用技巧

### 提示词技巧

**1. 具体明确**：

❌ 不好：
```
写个函数
```

✅ 好：
```
用TypeScript写一个函数，
功能：对数组进行去重
参数：number[]
返回：number[]
要求：保持原始顺序
```

**2. 提供上下文**：

```
这是一个React项目，使用TypeScript和Redux。
请创建一个异步action来获取用户列表。
```

**3. 分步骤**：

```
第1步：创建User接口
第2步：创建UserService类
第3步：实现CRUD方法
```

**4. 指定风格**：

```
按照函数式编程风格，
使用纯函数，避免副作用，
使用TypeScript类型定义
```

### 工作流程

**典型开发流程**：

```
1. 用AI Chat讨论需求
   "我要实现一个登录功能，需要哪些部分？"

2. 让AI生成代码框架
   "创建登录页面的基本结构"

3. 用Cmd+K细化实现
   选中函数 → "添加表单验证"

4. Tab补全填充细节
   自动补全样式、逻辑等

5. AI Chat优化代码
   "优化这段代码的性能"

6. Debug
   "这里为什么报错？"
```

### 快速原型

**30分钟开发Todo App**：

```
1. Chat: "用React和TypeScript创建Todo应用的基础结构"
   → 获得组件骨架

2. Cmd+K: "添加状态管理"
   → 添加useState

3. Tab: 自动补全事件处理函数

4. Cmd+K: "添加样式，使用Tailwind"
   → 美化界面

5. Chat: "添加localStorage持久化"
   → 完善功能
```

### 学习新技术

**场景**：学习新框架

```
你: 我想学习Next.js，从零开始

AI: 好的，我们先创建一个基础项目...

你: @app/page.tsx 解释这个文件的作用

AI: 这是Next.js 13的App Router...

你: 如何添加数据获取？

AI: 在Next.js中可以这样...
```

## 💼 实战案例

### 案例1：创建REST API

**任务**：用Node.js + Express创建用户管理API

**步骤**：

**① 初始化项目**
```
Chat输入：
创建Express项目结构，包含：
- src/routes
- src/controllers
- src/models
- TypeScript配置
```

**② 创建路由**
```
@routes/users.ts
创建用户路由，包含CRUD操作
```

**③ 实现控制器**
```
Cmd+K在controllers/userController.ts
实现getUserById方法，
包含错误处理和参数验证
```

**④ 添加数据库**
```
Chat:
集成Prisma ORM，
创建User模型，
包含name, email, password字段
```

**⑤ 测试**
```
Chat:
为userController编写单元测试
使用Jest和Supertest
```

### 案例2：前端组件开发

**任务**：React数据表格组件

**步骤**：

**① 创建组件**
```typescript
// 输入注释后按Tab
// AI生成完整组件

/**
 * 数据表格组件
 * 功能：
 * - 显示数据
 * - 排序
 * - 分页
 * - 搜索
 */
```

**② 添加功能**
```
选中组件 → Cmd+K
输入：添加列排序功能
```

**③ 优化性能**
```
Chat:
@DataTable.tsx
这个组件有性能问题吗？
如何优化？
```

**④ 添加样式**
```
Cmd+K:
使用Tailwind CSS美化表格
添加hover效果和响应式设计
```

### 案例3：重构遗留代码

**任务**：重构老项目代码

**步骤**：

**① 理解代码**
```
Chat:
@legacy.js
解释这个文件的功能
指出潜在问题
```

**② 现代化改造**
```
Chat:
将这个文件转换为TypeScript
使用ES6+语法
添加类型定义
```

**③ 提取函数**
```
选中大函数 → Cmd+K
拆分成多个小函数
提高可读性
```

**④ 添加测试**
```
Chat:
为重构后的代码编写测试
覆盖主要功能
```

### 案例4：Debug调试

**场景**：生产环境bug

**步骤**：

**① 分析错误**
```
Chat:
[粘贴错误堆栈]
这是什么错误？
可能的原因是什么？
```

**② 定位问题**
```
Chat:
@app.js
@utils.js
这两个文件中哪里可能导致这个错误？
```

**③ 修复建议**
```
选中问题代码 → Cmd+K
修复这个空指针异常
添加防御性检查
```

**④ 预防措施**
```
Chat:
如何预防类似问题？
添加错误边界
实现错误监控
```

### 案例5：代码审查

**任务**：审查Pull Request

**步骤**：

**① 整体评估**
```
Chat:
@new-feature.ts
评估这段代码的质量
指出潜在问题
```

**② 安全检查**
```
Chat:
检查安全漏洞：
- SQL注入
- XSS攻击
- 身份验证问题
```

**③ 性能分析**
```
Chat:
分析性能问题
给出优化建议
```

**④ 最佳实践**
```
Chat:
这段代码符合最佳实践吗？
如何改进？
```

## ⌨️ 快捷键大全

### 核心快捷键

| 功能 | Windows/Linux | macOS |
|------|--------------|-------|
| AI Chat | `Ctrl+L` | `Cmd+L` |
| 行内编辑 | `Ctrl+K` | `Cmd+K` |
| Tab补全 | `Tab` | `Tab` |
| 接受建议 | `Tab` | `Tab` |
| 拒绝建议 | `Esc` | `Esc` |
| 下一个建议 | `Alt+]` | `Opt+]` |
| 上一个建议 | `Alt+[` | `Opt+[` |

### 编辑快捷键

| 功能 | Windows/Linux | macOS |
|------|--------------|-------|
| 多光标 | `Ctrl+Alt+↓/↑` | `Cmd+Opt+↓/↑` |
| 复制行 | `Shift+Alt+↓/↑` | `Shift+Opt+↓/↑` |
| 删除行 | `Ctrl+Shift+K` | `Cmd+Shift+K` |
| 格式化 | `Shift+Alt+F` | `Shift+Opt+F` |
| 查找 | `Ctrl+F` | `Cmd+F` |
| 替换 | `Ctrl+H` | `Cmd+H` |

### 导航快捷键

| 功能 | Windows/Linux | macOS |
|------|--------------|-------|
| 命令面板 | `Ctrl+Shift+P` | `Cmd+Shift+P` |
| 快速打开 | `Ctrl+P` | `Cmd+P` |
| 转到定义 | `F12` | `F12` |
| 返回 | `Alt+←` | `Cmd+←` |
| 前进 | `Alt+→` | `Cmd+→` |
| 侧边栏 | `Ctrl+B` | `Cmd+B` |

## 🚀 高级功能

### Composer模式

**功能**：AI帮你完成整个功能

**使用**：
```
1. 打开Composer（Cmd+I）
2. 描述需求
3. AI生成完整实现
4. 预览和应用更改
```

**示例**：
```
需求：创建一个带认证的博客系统

AI会：
1. 创建文件结构
2. 实现认证系统
3. 创建文章CRUD
4. 添加评论功能
5. 配置路由
```

### 代码索引

**功能**：AI理解整个项目

**工作原理**：
```
Cursor会自动索引：
- 项目结构
- 代码关系
- 函数定义
- 类型定义
```

**好处**：
- 跨文件理解
- 智能跳转
- 准确引用
- 上下文感知

### 自定义规则

**功能**：让AI遵循你的编码规范

**配置**：创建`.cursorrules`文件

```
# .cursorrules 示例

## 代码风格
- 使用函数式编程
- 优先使用const
- 使用箭头函数

## TypeScript
- 严格模式
- 显式类型注解
- 避免any

## React
- 使用函数组件
- Hooks优于Class
- Props解构

## 命名
- 组件用PascalCase
- 函数用camelCase
- 常量用UPPER_CASE
```

### Codebase模式

**@Codebase**：引用整个项目

**使用场景**：
```
@Codebase 这个项目的架构是怎样的？

@Codebase 如何添加一个新的API端点？

@Codebase 哪里处理了用户权限？
```

## 💰 定价方案

### 免费版

**包含**：
- ✅ 基础AI功能
- ✅ 2000次请求/月
- ✅ GPT-3.5模型
- ✅ 所有编辑器功能

**限制**：
- ❌ 请求数量限制
- ❌ 无法使用GPT-4
- ❌ 较慢的响应速度

### Pro版（$20/月）

**包含**：
- ✅ 无限AI请求
- ✅ GPT-4访问
- ✅ 优先支持
- ✅ 更快响应
- ✅ 所有新功能

**适合**：
- 专业开发者
- 重度使用
- 团队协作

### 企业版

- 自定义模型
- 数据隐私保障
- 团队管理
- 技术支持

## ❓ 常见问题

### Q: Cursor安全吗？代码会泄露吗？

**A**: 
- ✅ 代码通过加密传输
- ✅ 不会用于训练模型
- ✅ 可以选择不发送敏感文件
- ✅ 企业版有更严格的隐私保障

**建议**：
- 不要发送敏感信息（密钥、密码）
- 使用`.cursorignore`排除敏感文件

### Q: 如何提高AI建议的准确性？

**A**:
1. **提供清晰的上下文**
2. **使用@引用相关文件**
3. **编写有意义的注释**
4. **使用.cursorrules定义规范**
5. **使用TypeScript类型**

### Q: 能完全替代人工编程吗？

**A**: 
❌ 不能完全替代，但能大幅提升效率

**AI擅长**：
- 生成模板代码
- 常见功能实现
- 代码重构
- Bug修复

**仍需人工**：
- 架构设计
- 复杂业务逻辑
- 性能优化
- 代码审查

### Q: 如何迁移VS Code配置？

**A**:
```
1. Cursor会自动检测VS Code
2. File → Import VS Code Settings
3. 选择要导入的内容
4. 点击导入
```

### Q: 支持哪些编程语言？

**A**: 支持所有主流语言：
- JavaScript/TypeScript
- Python
- Java/Kotlin
- C/C++/C#
- Go
- Rust
- PHP
- Ruby
- 等等...

### Q: 离线能用吗？

**A**:
- ✅ 编辑器功能可离线使用
- ❌ AI功能需要网络
- ✅ 代码补全有本地缓存

### Q: 和GitHub Copilot比怎么样？

**A**:

**Cursor优势**：
- 更强的AI对话
- 项目级理解
- Composer模式
- 原生AI体验

**Copilot优势**：
- 价格更低（$10/月）
- 更广泛的支持
- GitHub集成

**选择建议**：
- 重度AI使用 → Cursor
- VS Code忠实用户 → Copilot
- 预算有限 → Copilot

## 💡 最佳实践

### DO - 应该做的

1. **✅ 写清晰的注释**
   - AI能更好理解意图
   
2. **✅ 使用TypeScript**
   - 类型信息帮助AI生成准确代码
   
3. **✅ 分步骤**
   - 复杂功能拆分成小任务
   
4. **✅ 验证结果**
   - AI可能出错，要测试
   
5. **✅ 迭代优化**
   - 不满意就继续对话改进

### DON'T - 不应该做的

1. **❌ 盲目信任**
   - AI会出错，需要理解代码
   
2. **❌ 放弃思考**
   - AI是辅助，不能替代思维
   
3. **❌ 发送敏感信息**
   - 注意数据安全
   
4. **❌ 忽略警告**
   - 注意AI的提示和建议
   
5. **❌ 过度依赖**
   - 保持编程能力的提升

## 📚 学习资源

### 官方资源

- [Cursor官网](https://cursor.sh)
- [文档](https://cursor.sh/docs)
- [更新日志](https://changelog.cursor.sh)
- [Discord社区](https://discord.gg/cursor)

### 推荐教程

- YouTube: "Cursor AI Tutorial"
- Twitter: @cursor_ai
- Reddit: r/cursor

### 社区

- [GitHub Discussions](https://github.com/getcursor/cursor/discussions)
- Discord频道
- Twitter社区

## 🎓 进阶技巧

### 团队协作

**分享配置**：
```json
// .cursor/settings.json
{
  "rules": "team-rules.md",
  "style": "company-style-guide.md"
}
```

**统一规范**：
- 使用共享的.cursorrules
- 团队编码标准
- 项目特定配置

### 工作流集成

**Git集成**：
- AI生成commit message
- 代码审查辅助
- 冲突解决帮助

**CI/CD**：
- 生成测试用例
- 生成部署脚本
- 文档自动化

## 下一步

- 💬 [ChatGPT使用指南](ai/tools/chatgpt.md)
- 🎨 [Midjourney绘画](ai/tools/midjourney.md)
- 📝 [提示词工程](ai/fundamentals/prompt-engineering.md)
- 🔧 [更多开发工具](ai/tools/README.md)

---

?> **核心建议**：Cursor最大的价值在于将AI无缝集成到编程工作流中。不要怕尝试，多实践，找到最适合自己的使用方式。记住：AI是助手，你才是主导！

