# 贡献指南

感谢你对本知识库的关注！我们欢迎任何形式的贡献。

## 贡献方式

你可以通过以下方式为项目做出贡献：

- 📝 改进文档内容
- 🐛 报告Bug或错误
- 💡 提出新功能建议
- 🌍 帮助翻译文档
- 🎨 优化样式和设计
- 📚 添加示例和教程

## 如何贡献

### 1. Fork项目

点击页面右上角的"Fork"按钮，将项目复制到你的GitHub账户。

### 2. 克隆仓库

```bash
git clone https://github.com/your-username/repo-name.git
cd repo-name
```

### 3. 创建分支

为你的更改创建一个新分支：

```bash
git checkout -b feature/your-feature-name
# 或
git checkout -b fix/your-bug-fix
```

分支命名规范：
- `feature/xxx`：新功能
- `fix/xxx`：Bug修复
- `docs/xxx`：文档更新
- `style/xxx`：样式调整
- `refactor/xxx`：代码重构

### 4. 进行更改

#### 文档编写规范

**Markdown格式**

```markdown
# 一级标题（每页只有一个）

## 二级标题

### 三级标题

段落之间空一行。

- 列表项1
- 列表项2

**粗体** 和 *斜体*
```

**代码块**

````markdown
```javascript
function hello() {
  console.log('Hello');
}
```
````

**链接和图片**

```markdown
[链接文本](path/to/page.md)
![图片描述](path/to/image.png)
```

#### 文件命名规范

- 使用小写字母
- 单词之间用连字符`-`分隔
- 使用英文命名
- 例如：`getting-started.md`

#### 提交规范

提交信息应该清晰描述改动内容：

```bash
# 格式
<type>: <subject>

# 示例
docs: 添加安装指南
fix: 修复侧边栏显示问题
feat: 添加搜索功能
style: 优化移动端样式
```

类型说明：
- `feat`：新功能
- `fix`：Bug修复
- `docs`：文档更新
- `style`：样式调整
- `refactor`：代码重构
- `test`：测试相关
- `chore`：构建或辅助工具变动

### 5. 提交更改

```bash
# 查看更改
git status

# 添加文件
git add .

# 提交
git commit -m "docs: 添加贡献指南"
```

### 6. 推送到远程

```bash
git push origin feature/your-feature-name
```

### 7. 创建Pull Request

1. 访问你的Fork仓库页面
2. 点击"Pull Request"按钮
3. 填写PR标题和描述
4. 等待审核

## Pull Request指南

### PR标题

清晰描述改动内容，例如：
- `docs: 完善安装文档`
- `fix: 修复图片路径错误`
- `feat: 添加暗黑模式`

### PR描述模板

```markdown
## 改动类型
- [ ] 文档更新
- [ ] Bug修复
- [ ] 新功能
- [ ] 样式优化
- [ ] 其他

## 改动说明
<!-- 详细描述你的更改 -->

## 相关Issue
<!-- 如果有相关Issue，请引用 -->
Closes #123

## 测试
<!-- 描述如何测试你的更改 -->

## 截图（如适用）
<!-- 添加截图说明视觉变化 -->

## 检查清单
- [ ] 代码遵循项目规范
- [ ] 已测试改动
- [ ] 已更新相关文档
- [ ] 提交信息清晰明确
```

### 代码审查

所有PR都需要经过审查：
- 至少一位维护者审核通过
- 通过所有检查
- 解决所有讨论和建议

## 报告Issue

### Bug报告

使用Bug报告模板：

```markdown
## Bug描述
<!-- 清晰简洁地描述Bug -->

## 复现步骤
1. 访问 '...'
2. 点击 '...'
3. 滚动到 '...'
4. 看到错误

## 期望行为
<!-- 描述你期望发生什么 -->

## 实际行为
<!-- 描述实际发生了什么 -->

## 截图
<!-- 如果适用，添加截图 -->

## 环境信息
- 浏览器：[如 Chrome 95]
- 操作系统：[如 Windows 10]
- Docsify版本：[如 4.12.0]

## 其他信息
<!-- 其他相关信息 -->
```

### 功能建议

```markdown
## 功能描述
<!-- 清晰简洁地描述建议的功能 -->

## 动机和背景
<!-- 说明为什么需要这个功能 -->

## 建议的实现方案
<!-- 如果有想法，描述如何实现 -->

## 替代方案
<!-- 描述你考虑过的其他方案 -->

## 其他信息
<!-- 其他相关信息 -->
```

## 文档规范

### 结构规范

```
docs/
├── guide/          # 指南（入门内容）
├── tutorial/       # 教程（详细步骤）
├── reference/      # 参考（API、配置）
└── other/         # 其他（FAQ、更新日志等）
```

### 写作规范

1. **语言简洁明了**
   - 使用简单直接的语言
   - 避免冗长的句子
   - 一个段落讲清一个要点

2. **结构清晰**
   - 使用合适的标题层级
   - 内容按逻辑顺序组织
   - 添加目录导航

3. **代码示例**
   - 提供完整可运行的示例
   - 添加必要的注释
   - 解释关键步骤

4. **图片使用**
   - 压缩图片大小
   - 使用描述性文件名
   - 添加alt文本

5. **链接**
   - 使用相对路径引用内部文档
   - 确保链接有效
   - 外部链接在新标签打开

### 中文写作规范

1. **标点符号**
   - 使用全角中文标点
   - 英文和数字使用半角
   - 中英文之间添加空格

2. **术语统一**
   - 保持术语翻译一致
   - 专有名词使用原文
   - 建立术语表

3. **格式规范**
   ```markdown
   正确：这是一个 Docsify 知识库。
   错误：这是一个Docsify知识库。
   
   正确：版本号为 1.0.0。
   错误：版本号为1.0.0。
   ```

## 开发环境

### 本地预览

```bash
# 全局安装docsify-cli
npm i docsify-cli -g

# 启动本地服务器
docsify serve .

# 访问 http://localhost:3000
```

### 推荐工具

- **编辑器**：VS Code、Typora
- **VS Code插件**：
  - Markdown All in One
  - markdownlint
  - Code Spell Checker
- **Git客户端**：GitHub Desktop、SourceTree

## 社区准则

### 行为准则

- 尊重所有参与者
- 接受建设性批评
- 专注于对项目最有利的事情
- 展现同理心

### 沟通方式

- 使用清晰、专业的语言
- 保持友好和耐心
- 及时响应反馈
- 公开透明地交流

## 获得帮助

如果你有任何疑问：

1. 查看[常见问题](reference/faq.md)
2. 搜索现有的[Issues](https://github.com/username/repo/issues)
3. 在[Discussions](https://github.com/username/repo/discussions)提问
4. 联系维护者

## 致谢

感谢所有为本项目做出贡献的人！

你的贡献让这个知识库变得更好！🎉

---

**记住**：没有贡献太小，每一个改进都很重要！

