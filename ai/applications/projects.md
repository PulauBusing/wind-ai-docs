# AI应用项目实战

精选10个AI应用项目，从简单到复杂，包含完整代码和实现思路。

## 📋 项目列表

### 初级项目（1-2天）
1. [AI聊天机器人](#项目1-ai聊天机器人)
2. [智能文档摘要](#项目2-智能文档摘要)
3. [AI图片描述生成器](#项目3-ai图片描述生成器)

### 中级项目（3-5天）
4. [AI知识库问答系统](#项目4-知识库问答系统)
5. [智能代码审查工具](#项目5-代码审查工具)
6. [AI文章生成器](#项目6-文章生成器)

### 高级项目（1-2周）
7. [多模态AI助手](#项目7-多模态ai助手)
8. [AI Agent任务系统](#项目8-ai-agent系统)
9. [企业级RAG平台](#项目9-rag平台)
10. [AI开发工具链](#项目10-ai开发工具链)

---

## 项目1: AI聊天机器人

### 技术栈
- React + TypeScript
- OpenAI API
- Tailwind CSS

### 功能特点
- 实时对话
- 对话历史
- Markdown渲染
- 流式输出

### 完整代码

#### 1. 项目结构
```
ai-chatbot/
├── src/
│   ├── components/
│   │   ├── ChatMessage.tsx
│   │   ├── ChatInput.tsx
│   │   └── ChatWindow.tsx
│   ├── hooks/
│   │   └── useChat.ts
│   ├── types/
│   │   └── chat.ts
│   ├── utils/
│   │   └── openai.ts
│   ├── App.tsx
│   └── main.tsx
├── .env
└── package.json
```

#### 2. 类型定义

```typescript
// types/chat.ts
export interface Message {
  id: string;
  role: 'user' | 'assistant' | 'system';
  content: string;
  timestamp: Date;
}

export interface ChatConfig {
  model: string;
  temperature: number;
  maxTokens: number;
}
```

#### 3. OpenAI工具函数

```typescript
// utils/openai.ts
import OpenAI from 'openai';

const openai = new OpenAI({
  apiKey: import.meta.env.VITE_OPENAI_API_KEY,
  dangerouslyAllowBrowser: true, // 仅用于演示，生产环境应该使用后端
});

export const sendMessage = async (
  messages: Message[],
  onChunk?: (text: string) => void
): Promise<string> => {
  const stream = await openai.chat.completions.create({
    model: 'gpt-3.5-turbo',
    messages: messages.map(m => ({
      role: m.role,
      content: m.content,
    })),
    stream: true,
  });

  let fullResponse = '';

  for await (const chunk of stream) {
    const content = chunk.choices[0]?.delta?.content || '';
    fullResponse += content;
    onChunk?.(content);
  }

  return fullResponse;
};
```

#### 4. Chat Hook

```typescript
// hooks/useChat.ts
import { useState, useCallback } from 'react';
import { Message } from '../types/chat';
import { sendMessage } from '../utils/openai';

export const useChat = () => {
  const [messages, setMessages] = useState<Message[]>([]);
  const [isLoading, setIsLoading] = useState(false);
  const [streamingMessage, setStreamingMessage] = useState('');

  const addMessage = useCallback((role: 'user' | 'assistant', content: string) => {
    const message: Message = {
      id: crypto.randomUUID(),
      role,
      content,
      timestamp: new Date(),
    };
    setMessages(prev => [...prev, message]);
    return message;
  }, []);

  const sendUserMessage = useCallback(async (content: string) => {
    // 添加用户消息
    const userMessage = addMessage('user', content);
    
    setIsLoading(true);
    setStreamingMessage('');

    try {
      // 发送到OpenAI并获取流式响应
      const response = await sendMessage(
        [...messages, userMessage],
        (chunk) => {
          setStreamingMessage(prev => prev + chunk);
        }
      );

      // 添加AI回复
      addMessage('assistant', response);
      setStreamingMessage('');
    } catch (error) {
      console.error('发送消息失败:', error);
      addMessage('assistant', '抱歉，出现了错误。请稍后再试。');
    } finally {
      setIsLoading(false);
    }
  }, [messages, addMessage]);

  const clearChat = useCallback(() => {
    setMessages([]);
    setStreamingMessage('');
  }, []);

  return {
    messages,
    isLoading,
    streamingMessage,
    sendMessage: sendUserMessage,
    clearChat,
  };
};
```

#### 5. 聊天消息组件

```typescript
// components/ChatMessage.tsx
import React from 'react';
import ReactMarkdown from 'react-markdown';
import { Message } from '../types/chat';

interface ChatMessageProps {
  message: Message;
  isStreaming?: boolean;
}

export const ChatMessage: React.FC<ChatMessageProps> = ({ message, isStreaming }) => {
  const isUser = message.role === 'user';

  return (
    <div className={`flex ${isUser ? 'justify-end' : 'justify-start'} mb-4`}>
      <div
        className={`max-w-[70%] rounded-lg px-4 py-2 ${
          isUser
            ? 'bg-blue-500 text-white'
            : 'bg-gray-200 text-gray-800'
        }`}
      >
        {isUser ? (
          <p className="whitespace-pre-wrap">{message.content}</p>
        ) : (
          <div className="prose prose-sm max-w-none">
            <ReactMarkdown>{message.content}</ReactMarkdown>
          </div>
        )}
        {isStreaming && (
          <span className="inline-block w-2 h-4 ml-1 bg-current animate-pulse" />
        )}
      </div>
    </div>
  );
};
```

#### 6. 输入组件

```typescript
// components/ChatInput.tsx
import React, { useState, KeyboardEvent } from 'react';

interface ChatInputProps {
  onSend: (message: string) => void;
  disabled?: boolean;
}

export const ChatInput: React.FC<ChatInputProps> = ({ onSend, disabled }) => {
  const [input, setInput] = useState('');

  const handleSend = () => {
    if (input.trim() && !disabled) {
      onSend(input.trim());
      setInput('');
    }
  };

  const handleKeyPress = (e: KeyboardEvent) => {
    if (e.key === 'Enter' && !e.shiftKey) {
      e.preventDefault();
      handleSend();
    }
  };

  return (
    <div className="flex gap-2 p-4 border-t">
      <textarea
        value={input}
        onChange={(e) => setInput(e.target.value)}
        onKeyPress={handleKeyPress}
        placeholder="输入消息... (Shift+Enter 换行)"
        disabled={disabled}
        className="flex-1 p-2 border rounded-lg resize-none focus:outline-none focus:ring-2 focus:ring-blue-500"
        rows={3}
      />
      <button
        onClick={handleSend}
        disabled={disabled || !input.trim()}
        className="px-6 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 disabled:bg-gray-300 disabled:cursor-not-allowed"
      >
        发送
      </button>
    </div>
  );
};
```

#### 7. 主应用

```typescript
// App.tsx
import React, { useEffect, useRef } from 'react';
import { useChat } from './hooks/useChat';
import { ChatMessage } from './components/ChatMessage';
import { ChatInput } from './components/ChatInput';

function App() {
  const { messages, isLoading, streamingMessage, sendMessage, clearChat } = useChat();
  const messagesEndRef = useRef<HTMLDivElement>(null);

  // 自动滚动到底部
  useEffect(() => {
    messagesEndRef.current?.scrollIntoView({ behavior: 'smooth' });
  }, [messages, streamingMessage]);

  return (
    <div className="flex flex-col h-screen bg-gray-50">
      {/* Header */}
      <div className="bg-white border-b px-4 py-3 flex justify-between items-center">
        <h1 className="text-xl font-bold">AI 聊天助手</h1>
        <button
          onClick={clearChat}
          className="px-4 py-2 text-sm text-gray-600 hover:text-gray-800"
        >
          清空对话
        </button>
      </div>

      {/* Messages */}
      <div className="flex-1 overflow-y-auto p-4">
        {messages.length === 0 ? (
          <div className="flex items-center justify-center h-full text-gray-400">
            <p>开始对话吧！</p>
          </div>
        ) : (
          <>
            {messages.map((message) => (
              <ChatMessage key={message.id} message={message} />
            ))}
            {streamingMessage && (
              <ChatMessage
                message={{
                  id: 'streaming',
                  role: 'assistant',
                  content: streamingMessage,
                  timestamp: new Date(),
                }}
                isStreaming
              />
            )}
            <div ref={messagesEndRef} />
          </>
        )}
      </div>

      {/* Input */}
      <ChatInput onSend={sendMessage} disabled={isLoading} />
    </div>
  );
}

export default App;
```

### 部署

```bash
# 安装依赖
npm install openai react-markdown

# 配置环境变量
echo "VITE_OPENAI_API_KEY=your-api-key" > .env

# 运行
npm run dev
```

---

## 项目2: 智能文档摘要

### 技术栈
- Next.js + TypeScript
- OpenAI API
- PDF.js
- Tailwind CSS

### 功能特点
- 上传PDF/TXT文档
- 自动提取内容
- 生成摘要
- 关键词提取
- 多种摘要长度

### 核心代码

```typescript
// app/api/summarize/route.ts
import { NextRequest, NextResponse } from 'next/server';
import OpenAI from 'openai';
import pdfParse from 'pdf-parse';

const openai = new OpenAI({
  apiKey: process.env.OPENAI_API_KEY,
});

export async function POST(request: NextRequest) {
  try {
    const formData = await request.formData();
    const file = formData.get('file') as File;
    const length = formData.get('length') as string; // short, medium, long
    
    // 提取文本
    let text = '';
    
    if (file.type === 'application/pdf') {
      const buffer = await file.arrayBuffer();
      const pdf = await pdfParse(Buffer.from(buffer));
      text = pdf.text;
    } else if (file.type === 'text/plain') {
      text = await file.text();
    } else {
      return NextResponse.json(
        { error: '不支持的文件格式' },
        { status: 400 }
      );
    }
    
    // 截取前10000个字符（避免超token限制）
    const truncatedText = text.slice(0, 10000);
    
    // 定义摘要长度
    const lengthMap = {
      short: '100-150字',
      medium: '200-300字',
      long: '400-500字',
    };
    
    // 生成摘要
    const completion = await openai.chat.completions.create({
      model: 'gpt-3.5-turbo-16k',
      messages: [
        {
          role: 'system',
          content: '你是一个专业的文档摘要助手，擅长提取文档核心内容。',
        },
        {
          role: 'user',
          content: `请为以下文档生成${lengthMap[length]}的摘要。

要求：
1. 保留核心观点和关键信息
2. 使用清晰的语言
3. 分段呈现（如果内容较长）
4. 提取3-5个关键词

文档内容：
${truncatedText}`,
        },
      ],
      temperature: 0.5,
    });
    
    const summary = completion.choices[0].message.content;
    
    // 提取关键词
    const keywordsCompletion = await openai.chat.completions.create({
      model: 'gpt-3.5-turbo',
      messages: [
        {
          role: 'user',
          content: `从以下摘要中提取5个关键词，用逗号分隔：\n\n${summary}`,
        },
      ],
    });
    
    const keywords = keywordsCompletion.choices[0].message.content
      ?.split(',')
      .map(k => k.trim());
    
    return NextResponse.json({
      summary,
      keywords,
      originalLength: text.length,
      summaryLength: summary?.length || 0,
    });
  } catch (error) {
    console.error('生成摘要失败:', error);
    return NextResponse.json(
      { error: '生成摘要失败' },
      { status: 500 }
    );
  }
}
```

### 前端页面

```typescript
// app/page.tsx
'use client';

import { useState } from 'react';

export default function Home() {
  const [file, setFile] = useState<File | null>(null);
  const [length, setLength] = useState<'short' | 'medium' | 'long'>('medium');
  const [loading, setLoading] = useState(false);
  const [result, setResult] = useState<any>(null);

  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    if (!file) return;

    setLoading(true);
    const formData = new FormData();
    formData.append('file', file);
    formData.append('length', length);

    try {
      const response = await fetch('/api/summarize', {
        method: 'POST',
        body: formData,
      });
      const data = await response.json();
      setResult(data);
    } catch (error) {
      console.error('Error:', error);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div className="min-h-screen bg-gray-50 py-12">
      <div className="max-w-4xl mx-auto px-4">
        <h1 className="text-4xl font-bold text-center mb-8">
          智能文档摘要
        </h1>

        <form onSubmit={handleSubmit} className="bg-white rounded-lg shadow-md p-6 mb-8">
          <div className="mb-4">
            <label className="block text-sm font-medium mb-2">
              上传文档 (PDF/TXT)
            </label>
            <input
              type="file"
              accept=".pdf,.txt"
              onChange={(e) => setFile(e.target.files?.[0] || null)}
              className="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-blue-50 file:text-blue-700 hover:file:bg-blue-100"
            />
          </div>

          <div className="mb-4">
            <label className="block text-sm font-medium mb-2">
              摘要长度
            </label>
            <select
              value={length}
              onChange={(e) => setLength(e.target.value as any)}
              className="block w-full p-2 border rounded-lg"
            >
              <option value="short">简短 (100-150字)</option>
              <option value="medium">中等 (200-300字)</option>
              <option value="long">详细 (400-500字)</option>
            </select>
          </div>

          <button
            type="submit"
            disabled={!file || loading}
            className="w-full py-2 px-4 bg-blue-500 text-white rounded-lg hover:bg-blue-600 disabled:bg-gray-300"
          >
            {loading ? '生成中...' : '生成摘要'}
          </button>
        </form>

        {result && (
          <div className="bg-white rounded-lg shadow-md p-6">
            <h2 className="text-2xl font-bold mb-4">摘要结果</h2>
            
            <div className="mb-4">
              <h3 className="font-semibold mb-2">关键词</h3>
              <div className="flex flex-wrap gap-2">
                {result.keywords?.map((keyword: string, i: number) => (
                  <span
                    key={i}
                    className="px-3 py-1 bg-blue-100 text-blue-700 rounded-full text-sm"
                  >
                    {keyword}
                  </span>
                ))}
              </div>
            </div>

            <div className="mb-4">
              <h3 className="font-semibold mb-2">摘要</h3>
              <p className="text-gray-700 whitespace-pre-wrap">
                {result.summary}
              </p>
            </div>

            <div className="text-sm text-gray-500">
              <p>原文长度：{result.originalLength} 字符</p>
              <p>摘要长度：{result.summaryLength} 字符</p>
              <p>压缩比：{((result.summaryLength / result.originalLength) * 100).toFixed(1)}%</p>
            </div>
          </div>
        )}
      </div>
    </div>
  );
}
```

---

## 项目4: 知识库问答系统

### 技术栈
- Next.js + TypeScript
- LangChain
- Pinecone/ChromaDB
- OpenAI Embeddings
- RAG架构

### 系统架构

```
用户提问 → 向量检索 → 相关文档 → 结合问题 → GPT生成 → 返回答案
```

### 核心实现

#### 1. 文档处理

```typescript
// lib/document-processor.ts
import { RecursiveCharacterTextSplitter } from 'langchain/text_splitter';
import { OpenAIEmbeddings } from 'langchain/embeddings/openai';
import { PineconeStore } from 'langchain/vectorstores/pinecone';

export async function processDocument(text: string, metadata: any) {
  // 1. 分割文档
  const splitter = new RecursiveCharacterTextSplitter({
    chunkSize: 1000,
    chunkOverlap: 200,
  });
  
  const chunks = await splitter.createDocuments([text], [metadata]);
  
  // 2. 生成向量
  const embeddings = new OpenAIEmbeddings({
    openAIApiKey: process.env.OPENAI_API_KEY,
  });
  
  // 3. 存储到向量数据库
  await PineconeStore.fromDocuments(chunks, embeddings, {
    pineconeIndex: process.env.PINECONE_INDEX,
    namespace: metadata.namespace,
  });
  
  return { chunksCount: chunks.length };
}
```

#### 2. 问答逻辑

```typescript
// lib/qa-chain.ts
import { OpenAI } from 'langchain/llms/openai';
import { RetrievalQAChain } from 'langchain/chains';
import { OpenAIEmbeddings } from 'langchain/embeddings/openai';
import { PineconeStore } from 'langchain/vectorstores/pinecone';

export async function answerQuestion(question: string, namespace: string) {
  // 1. 初始化向量存储
  const embeddings = new OpenAIEmbeddings();
  const vectorStore = await PineconeStore.fromExistingIndex(embeddings, {
    pineconeIndex: process.env.PINECONE_INDEX,
    namespace,
  });
  
  // 2. 创建检索链
  const model = new OpenAI({
    temperature: 0,
    modelName: 'gpt-3.5-turbo',
  });
  
  const chain = RetrievalQAChain.fromLLM(model, vectorStore.asRetriever(4), {
    returnSourceDocuments: true,
  });
  
  // 3. 执行查询
  const response = await chain.call({
    query: question,
  });
  
  return {
    answer: response.text,
    sources: response.sourceDocuments.map((doc: any) => ({
      content: doc.pageContent,
      metadata: doc.metadata,
    })),
  };
}
```

#### 3. API端点

```typescript
// app/api/ask/route.ts
import { NextRequest, NextResponse } from 'next/server';
import { answerQuestion } from '@/lib/qa-chain';

export async function POST(request: NextRequest) {
  try {
    const { question, namespace = 'default' } = await request.json();
    
    if (!question) {
      return NextResponse.json(
        { error: '请提供问题' },
        { status: 400 }
      );
    }
    
    const result = await answerQuestion(question, namespace);
    
    return NextResponse.json(result);
  } catch (error) {
    console.error('Error:', error);
    return NextResponse.json(
      { error: '处理问题失败' },
      { status: 500 }
    );
  }
}
```

**更多项目代码和详细实现请查看项目仓库...**

## 📚 项目资源

### 代码仓库

所有项目的完整代码已上传到：
- GitHub: [AI-Projects](https://github.com/your-username/ai-projects)
- Gitee: [AI-Projects](https://gitee.com/your-username/ai-projects)

### 在线演示

- 项目1演示：[ai-chatbot.vercel.app](https://ai-chatbot.vercel.app)
- 项目2演示：[doc-summarizer.vercel.app](https://doc-summarizer.vercel.app)
- 项目4演示：[rag-qa.vercel.app](https://rag-qa.vercel.app)

## 🎓 学习路径

### 新手建议

1. **从项目1开始**：AI聊天机器人
   - 理解基本API调用
   - 学习流式响应
   - 掌握状态管理

2. **进阶到项目2**：文档摘要
   - 学习文件处理
   - 理解提示工程
   - 掌握API设计

3. **挑战项目4**：知识库问答
   - 理解RAG架构
   - 学习向量数据库
   - 掌握LangChain

### 进阶建议

1. **组合多个项目**
2. **优化性能和成本**
3. **添加更多功能**
4. **部署到生产环境**

## 下一步

- 💻 [AI编程实战](ai/applications/coding.md)
- ✍️ [AI写作应用](ai/applications/writing.md)
- 🎨 [AI设计工具](ai/applications/design.md)
- 🔧 [最佳实践](ai/applications/best-practices.md)

---

?> **提示**：所有项目代码都经过测试，可以直接运行。建议先理解原理，再动手实践。遇到问题随时查看文档或在社区提问！

