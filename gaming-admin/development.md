# Next.js Admin 后台开发完整文档

## 🎯 项目概述

这是一个面向在线游戏平台的管理后台系统，采用现代化的技术栈构建，支持多语言、响应式设计和高效的状态管理。

## 🛠️ 技术栈

- 前端框架: Next.js 16+ (App Router)
- 开发语言: TypeScript 5+
- UI 组件库: shadcn/ui 3.8.4
- 样式方案: Tailwind CSS + CSS Modules
- 主题管理: next-themes 0.2.1
- 国际化: next-intl
- 状态管理: Zustand (推荐) 或 React Context
- HTTP 客户端: axios 或 fetch API
- 表单处理: React Hook Form + Zod
- 图标库: Lucide React
- 代码质量: ESLint + Prettier + Husky
- 包管理: pnpm

## 📱 三端架构

| Mobile App   | Admin Panel  | Server API    |
| ------------ | ------------ | ------------- |
| (Flutter)    | (Next.js)    | (Spring Boot) |
| • 用户界面   | • 管理界面   | • 业务逻辑    |
| • 移动端交互 | • 数据可视化 | • 数据持久化  |
| • 推送通知   | • 配置管理   | • 安全认证    |
| • 支付集成   | • 报表分析   | • 微服务      |

## **📁 目录结构详解**

### app/ - 应用核心

```text
app/
├── [locale]/                     # 多语言路由 (i18n)
│   ├── layout.tsx                # 本地化根布局
│   ├── page.tsx                  # 本地化首页
│   └── (routes)/                 # 路由组（不会出现在URL中）
```

#### **路由组设计理念**

- (admin) - 管理后台相关路由
- (auth) - 认证相关路由
- (game-categories) - 游戏分类路由组

### components/ - 组件架构

```text
components/
├── ui/                          # shadcn/ui 基础组件
│   ├── button.tsx
│   ├── card.tsx
│   ├── dialog.tsx
│   ├── form.tsx
│   ├── input.tsx
│   ├── table.tsx
│   ├── tabs.tsx
│   └── ...
├── forms/                       # 表单相关组件
│   ├── user-form.tsx
│   ├── lottery-form.tsx
│   └── ...
├── tables/                      # 表格相关组件
│   ├── data-table.tsx           # 通用数据表格
│   ├── user-table.tsx
│   ├── lottery-table.tsx
│   └── ...
├── charts/                      # 图表组件
│   ├── revenue-chart.tsx
│   ├── user-growth-chart.tsx
│   └── ...
├── layout/                      # 布局组件
│   ├── sidebar.tsx
│   ├── header.tsx
│   ├── breadcrumb.tsx
│   └── ...
├── dashboard/                   # 仪表板组件
│   ├── stats-card.tsx
│   ├── quick-actions.tsx
│   └── ...
└── game-management/             # 游戏管理特定组件
    ├── lottery/
    ├── live-casino/
    └── ...
```

### lib/ - 工具库

```text
lib/
├── api/                         # API 客户端
│   ├── client.ts               # axios 实例
│   ├── endpoints.ts            # API 端点定义
│   ├── users.ts               # 用户相关API
│   ├── lotteries.ts           # 彩票相关API
│   └── ...
├── utils/                      # 工具函数
│   ├── format.ts              # 格式化函数
│   ├── validation.ts          # 验证函数
│   ├── date.ts               # 日期处理
│   └── ...
├── constants/                  # 常量定义
│   ├── routes.ts              # 路由常量
│   ├── game-types.ts          # 游戏类型常量
│   └── ...
└── config/                     # 配置文件
    ├── site.ts                # 站点配置
    ├── theme.ts               # 主题配置
    └── ...
```

### stores/ - 状态管理

```text
stores/
├── auth.store.ts               # 认证状态
├── ui.store.ts                 # UI 状态 (侧边栏、主题等)
├── user.store.ts               # 用户相关状态
├── lottery.store.ts            # 彩票状态
└── ...
```

### hooks/ - 自定义Hooks

```text
hooks/
├── use-auth.ts                 # 认证相关hook
├── use-api.ts                  # API调用hook
├── use-debounce.ts             # 防抖hook
├── use-local-storage.ts        # localStorage hook
├── use-media-query.ts          # 媒体查询hook
├── use-game-management.ts      # 游戏管理hook
└── ...
```

### 🎮 游戏管理模块设计

#### **彩票模块 (Lotteries)**

```text
(lotteries)/
├── layout.tsx                  # 彩票管理布局
├── page.tsx                    # 彩票主页面
├── overview/                   # 概览
│   └── page.tsx
├── games/                      # 彩票游戏管理
│   ├── mark6/                  # 六合彩
│   │   ├── page.tsx
│   │   ├── settings/
│   │   ├── results/
│   │   └── statistics/
│   ├── 3d/
│   ├── ssc/
│   ├── double-color-ball/
│   └── quick-pick/
├── results/                    # 开奖结果管理
│   ├── page.tsx
│   ├── manual-entry/          # 手动录入
│   └── verification/          # 结果验证
├── settings/                   # 全局设置
│   ├── odds/                  # 赔率设置
│   ├── limits/                # 投注限制
│   └── schedules/             # 开奖时间表
├── reports/                   # 报表
│   ├── sales/
│   ├── payout/
│   └── ...
└── analytics/                 # 分析
    ├── trends/
    └── predictions/
```

#### 游戏分类管理

```text
├── (live-casino)/             # 真人娱乐
│   ├── games/                 # 游戏列表
│   ├── providers/             # 游戏提供商
│   ├── tables/               # 赌桌管理
│   └── live-streams/         # 直播流管理
├── (slots)/                   # 老虎机
│   ├── games/
│   ├── providers/
│   ├── themes/
│   └── jackpots/
├── (cards)/                   # 棋牌游戏
│   ├── poker/
│   ├── blackjack/
│   ├── baccarat/
│   └── ...
├── (sports)/                  # 体育博彩
│   ├── sports/
│   ├── matches/
│   ├── odds/
│   └── bet-settlement/
├── (esports)/                 # 电竞
│   ├── tournaments/
│   ├── matches/
│   └── live-betting/
└── (casual)/                  # 休闲游戏
    ├── fishing/              # 捕鱼游戏
    ├── arcade/               # 街机游戏
    ├── mini-games/           # 小游戏
    └── tournaments/          # 休闲游戏比赛
```

#### 🔐 安全与认证

##### 认证流程

```text
// middleware.ts
export function middleware(request: NextRequest) {
  // 1. 检查认证状态
  // 2. 验证权限
  // 3. 重定向未授权用户
  // 4. 记录访问日志
}

// 路由保护
export const protectedRoutes = [
  '/dashboard',
  '/users',
  '/lotteries',
  // ...
];

// 权限级别
export enum UserRole {
  SUPER_ADMIN = 'super_admin',
  ADMIN = 'admin',
  AGENT = 'agent',
  CUSTOMER = 'customer'
}

// 权限映射
export const routePermissions = {
  '/dashboard': [UserRole.SUPER_ADMIN, UserRole.ADMIN],
  '/users': [UserRole.SUPER_ADMIN],
  '/lotteries': [UserRole.SUPER_ADMIN, UserRole.ADMIN],
  // ...
};
```

#### API 安全

- JWT Token 认证
- API 限流
- CORS 配置
- 输入验证
- SQL 注入防护
- XSS 防护

## 🌐 国际化方案

### 文件结构

```text
messages/
├── en/
│   ├── common.json           # 通用词条
│   ├── navigation.json       # 导航词条
│   ├── dashboard.json       # 仪表板词条
│   ├── users.json           # 用户管理词条
│   ├── lotteries.json       # 彩票词条
│   ├── games.json           # 游戏词条
│   ├── errors.json          # 错误消息
│   └── success.json         # 成功消息
└── zh/
    └── [相同结构]
```

### 使用示例

```typescript
// 在组件中使用
import { useTranslations } from 'next-intl';

export function UserTable() {
  const t = useTranslations('users');

  return (
    <div>
      <h1>{t('title')}</h1>
      <p>{t('description')}</p>
    </div>
  );
}
```

## 📊 数据表格设计

### 通用 DataTable 组件

```typescript
// components/tables/data-table.tsx
interface DataTableProps<T> {
  data: T[]
  columns: ColumnDef<T>[]
  pagination?: PaginationState
  sorting?: SortingState
  onRowClick?: (row: T) => void
  actions?: TableAction[]
}

// 功能特性：
// 1. 分页
// 2. 排序
// 3. 筛选
// 4. 行选择
// 5. 批量操作
// 6. 导出功能
// 7. 自定义列渲染
```

## 🎨 UI/UX 设计规范

### 主题系统

```typescript
// lib/config/theme.ts
export const themeConfig = {
  colors: {
    primary: {
      50: '#eff6ff',
      500: '#3b82f6',
      900: '#1e3a8a',
    },
    // 游戏分类特定颜色
    lottery: '#4f46e5',
    sports: '#059669',
    casino: '#dc2626',
    // ...
  },
  spacing: {
    xs: '0.25rem',
    sm: '0.5rem',
    md: '1rem',
    lg: '1.5rem',
    xl: '2rem',
  },
  // ...
}
```

### 响应式断点

```css
// lib/config/breakpoints.ts
export const breakpoints = {
  xs: '320px',
  sm: '640px',
  md: '768px',
  lg: '1024px',
  xl: '1280px',
};
```

## 🚀 性能优化

### 优化策略

1. 代码分割 - 按路由懒加载
2. 图片优化 - 使用 next/image
3. 字体优化 - 字体子集和预加载
4. 缓存策略 - SWR/React Query
5. 包大小优化 - 按需引入

### 监控指标

- 首次内容绘制 (FCP)
- 最大内容绘制 (LCP)
- 首次输入延迟 (FID)
- 累积布局偏移 (CLS)

## 📈 数据分析与监控

### 仪表板指标

```typescript
interface DashboardMetrics {
  // 用户指标
  totalUsers: number
  activeUsers: number
  newRegistrations: number

  // 财务指标
  totalRevenue: number
  dailyRevenue: number
  payoutRatio: number

  // 游戏指标
  totalBets: number
  popularGames: GameStats[]
  conversionRate: number

  // 系统指标
  uptime: number
  activeSessions: number
  apiLatency: number
}
```

### 实时监控

- 游戏服务器状态
- 交易流水监控
- 异常行为检测
- 系统健康检查

## 🔧 开发工作流

### Git 提交规范

```text
feat: 新增功能
fix: 修复bug
docs: 文档更新
style: 代码格式
refactor: 代码重构
test: 测试相关
chore: 构建过程或辅助工具
```

### 代码检查

```json
// .eslintrc.json
{
  "extends": [
    "next/core-web-vitals",
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ],
  "rules": {
    "@typescript-eslint/no-unused-vars": "error",
    "@typescript-eslint/no-explicit-any": "warn"
  }
}
```

## 📱 移动端适配

### 响应式策略

1. 移动优先设计
2. 触控友好交互
3. 离线功能支持
4. 推送通知集成

### PWA 支持

```json
// next.config.js
const withPWA = require('next-pwa')({
  dest: 'public',
  disable: process.env.NODE_ENV === 'development',
});
```

## 🧪 测试策略

### 测试层级

```text
1. 单元测试 (Jest) - 组件/函数测试
2. 集成测试 - API/数据库集成
3. E2E 测试 (Cypress) - 用户流程测试
4. 性能测试 - 负载/压力测试
```

### 测试覆盖范围

- 核心业务逻辑
- 用户认证流程
- 支付交易流程
- 游戏操作流程
- 数据报表生成

## 📦 部署与 DevOps

### 环境配置

```text
.env.local          # 本地开发
.env.staging        # 测试环境
.env.production     # 生产环境
```

### 部署流程

- 开发 → 代码提交到 dev 分支
- 测试 → 自动部署到 staging
- 预发布 → 人工验证
- 生产 → 蓝绿部署/金丝雀发布

### 监控工具

- 错误监控: Sentry
- 性能监控: Datadog/New Relic
- 日志管理: ELK Stack
- 用户分析: Google Analytics/Mixpanel

## 🔄 API 集成规范

### RESTful API 设计

```typescript
// API 响应格式
interface ApiResponse<T> {
  success: boolean
  data?: T
  error?: {
    code: string
    message: string
    details?: unknown
  }
  meta?: {
    page: number
    limit: number
    total: number
  }
}

// 错误代码定义
export enum ErrorCode {
  UNAUTHORIZED = 'UNAUTHORIZED',
  FORBIDDEN = 'FORBIDDEN',
  VALIDATION_ERROR = 'VALIDATION_ERROR',
  NOT_FOUND = 'NOT_FOUND',
  INTERNAL_ERROR = 'INTERNAL_ERROR',
}
```

### WebSocket 实时更新

```typescript
// 实时事件类型
export enum GameEventType {
  LOTTERY_RESULT = 'lottery:result',
  LIVE_BET_UPDATE = 'bet:update',
  CHAT_MESSAGE = 'chat:message',
  SYSTEM_NOTIFICATION = 'system:notification',
}
```

## 📋 项目管理

### 开发里程碑

- 阶段一: 基础框架 + 用户管理
- 阶段二: 彩票模块 + 财务系统
- 阶段三: 游戏管理扩展
- 阶段四: 数据分析 + 移动优化

### 团队协作

- 设计系统: Figma + Storybook
- API 文档: Swagger/Postman
- 任务管理: Jira/Trello
- 文档协作: Confluence/Notion

## 🎯 最佳实践总结

### 代码质量

- 严格类型检查
- 组件单一职责
- 函数纯净性
- 错误边界处理

### 安全实践

- 最小权限原则
- 输入验证和清理
- 定期安全审计
- 数据加密传输

### 性能优化

- 图片懒加载
- 组件懒加载
- 状态管理优化
- CDN 静态资源

### 可维护性

- 清晰的目录结构
- 完整的文档
- 自动化测试
- 代码审查流程

> 最后更新: 2026年2月
> 版本: 1.0.0
> 维护团队: 技术开发部
