# ChatGPT-Next-Web 项目规则总结

## 1. 当前项目使用的框架版本、依赖

### 主要框架
- **Next.js**: 版本 ^14.1.1 - 用于构建React应用的框架
- **React**: 版本 ^18.2.0 - 前端UI库
- **TypeScript**: 版本 5.2.2 - 类型安全的JavaScript超集

### 主要依赖
- **状态管理**: zustand (^4.3.8)
- **样式处理**: sass (^1.59.2)
- **Markdown渲染**: react-markdown (^8.0.7), remark-gfm (^3.0.1), rehype-highlight (^6.0.0)
- **HTTP请求**: axios (^1.7.5), fetch-event-source (^3.0.6)
- **工具库**: lodash-es (^4.17.21), nanoid (^5.0.3), zod (^3.24.1)
- **UI组件**: emoji-picker-react (^4.9.2), @hello-pangea/dnd (^16.5.0)

### 开发依赖
- **构建工具**: webpack (^5.88.1)
- **测试框架**: jest (^29.7.0), @testing-library/react (^16.1.0), @testing-library/jest-dom (^6.6.3)
- **代码质量工具**: eslint (^8.49.0), prettier (^3.0.2), husky (^8.0.0), lint-staged (^13.2.2)
- **桌面应用开发**: @tauri-apps/cli (1.5.11), @tauri-apps/api (^2.1.1)

## 2. 请不要使用某些 APIs

根据项目配置和代码分析，应避免使用以下APIs：

- **不安全的DOM操作**: 直接操作DOM可能导致XSS攻击，应使用React提供的安全方法
- **废弃的Web APIs**: 如document.execCommand()（项目中有使用但已被标记为废弃）
- **不稳定的实验性APIs**: 未经充分测试的浏览器实验性功能
- **特定平台APIs**: 在跨平台应用中应谨慎使用特定平台的API

## 3. 测试框架信息

### 测试技术栈
- **主要测试框架**: Jest (^29.7.0)
- **测试环境**: jsdom - 用于模拟浏览器环境
- **测试工具**: @testing-library/react, @testing-library/jest-dom
- **测试文件命名规范**: *.test.ts, *.test.tsx, *.test.js, *.test.jsx

### 测试配置
- **Jest配置文件**: jest.config.ts - 配置测试匹配模式、环境和模块映射
- **测试设置文件**: jest.setup.ts - 包含全局测试设置，如模拟fetch API
- **测试覆盖率工具**: v8 (coverageProvider)

### CI/CD测试集成
- **GitHub Actions**: 通过.github/workflows/test.yml配置自动测试
- **测试触发条件**: 主分支推送和拉取请求审核请求时
- **测试命令**: yarn test:ci

### 测试示例
项目包含多种类型的测试：
- **单元测试**: 如sum-module.test.ts中的简单函数测试
- **工具函数测试**: 如model-provider.test.ts和model-available.test.ts
- **功能测试**: 如vision-model-checker.test.ts测试模型识别功能

### 测试最佳实践
- **测试隔离**: 使用beforeEach和afterEach重置环境
- **环境变量处理**: 测试中正确处理和恢复环境变量
- **模拟外部依赖**: 使用jest.fn()模拟外部API调用
- **多场景测试**: 为同一功能测试多种输入和边界条件