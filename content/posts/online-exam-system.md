---
title: "全栈项目实战：在线考试系统 - SpringBoot + Vue 开发"
date: 2026-04-03T19:00:00+08:00
draft: false
tags:
  - 全栈开发
  - React
  - Node.js
  - MySQL
  - 项目实战
categories:
  - 技术分享
comments: true
---

## 项目简介

分享一个最近完成的全栈项目 - [在线学生考试系统](https://github.com/L5T2Y0/online-student-exam-system)。这是一个功能完整、安全可靠的在线考试平台，采用前后端分离架构，支持学生、教师、管理员三种角色。

项目最大的特点是**开箱即用**，内置了 27 道测试题目、5 份试卷、23 个测试账号，克隆下来就能直接运行体验！

## 核心功能

### 三种角色，各司其职

**学生端：**
- 用户注册登录
- 在线考试（倒计时、防作弊）
- 成绩查询
- 错题回顾
- 个人中心

**教师端：**
- 题库管理（增删改查）
- 试卷管理（手动/自动组卷）
- 批阅主观题
- 成绩统计与导出

**管理员端：**
- 用户管理（批量导入/导出）
- 系统权限控制
- 全局数据概览

## 技术栈

### 前端技术

- **React 18.2** - 现代化的前端框架
- **Ant Design 5.10** - 企业级 UI 组件库
- **React Router 6** - 路由管理
- **Axios** - HTTP 请求
- **Day.js** - 时间处理

### 后端技术

- **Node.js** - 运行环境（推荐 v18+）
- **Express 4.18** - Web 框架
- **Sequelize 6.32** - ORM 框架
- **MySQL** - 关系型数据库
- **JWT** - 身份认证

## 安全特性

作为一个考试系统，安全性至关重要。项目实现了多层安全防护：

### 1. 强制 JWT 密钥验证

```javascript
// 服务器启动时强制检查
if (!process.env.JWT_SECRET) {
  console.error('错误：未设置 JWT_SECRET');
  process.exit(1);
}
```

### 2. CORS 跨域白名单

只允许配置的前端地址访问 API，防止恶意请求。

### 3. 请求频率限制

```javascript
// 防暴力破解
登录接口：15分钟内最多 10 次尝试
全局接口：15分钟内最多 100 次请求
```

### 4. 输入安全

- XSS 输入清理
- 文件上传类型和大小验证
- 批量操作数量限制

### 5. 数据一致性

使用数据库事务保证数据操作的原子性。

## 项目亮点

### 1. 开箱即用的测试数据

运行一条命令即可初始化完整的测试环境：

```bash
npm run init
```

自动创建：
- 23 个测试用户（1 管理员 + 2 教师 + 20 学生）
- 27 道测试题目（涵盖 7 个科目）
- 5 份测试试卷（4 份已发布 + 1 份草稿）

### 2. 完善的权限控制

基于角色的访问控制（RBAC），不同角色看到不同的功能模块。

### 3. 自动组卷功能

教师可以设置题型、数量、难度，系统自动从题库中抽取题目组卷。

### 4. 实时考试监控

- 考试倒计时
- 自动提交
- 答题进度保存

## 快速开始

### 1. 克隆项目

```bash
git clone https://github.com/L5T2Y0/online-student-exam-system.git
cd online-student-exam-system
```

### 2. 安装依赖

```bash
npm install
cd client && npm install
```

### 3. 配置环境变量

生成 JWT 密钥：

```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

创建 `.env` 文件：

```env
DB_HOST=localhost
DB_PORT=3306
DB_NAME=online_exam
DB_USER=root
DB_PASSWORD=你的密码

JWT_SECRET=刚才生成的密钥

PORT=5000
ALLOWED_ORIGINS=http://localhost:3000
NODE_ENV=development
```

### 4. 初始化数据库

```bash
npm run init
```

### 5. 启动项目

```bash
npm run dev
```

访问 http://localhost:3000，使用测试账号登录：

- 管理员：admin / 123456
- 教师：teacher1 / 123456
- 学生：student1 / 123456

## 核心 API 设计

### 认证接口

```javascript
POST /api/auth/register  // 用户注册
POST /api/auth/login     // 用户登录
```

### 考试流程

```javascript
POST /api/exams/start           // 开始考试
PUT  /api/exams/:id/answer      // 保存答案
POST /api/exams/:id/submit      // 提交试卷
GET  /api/exams/my/list         // 我的考试列表
```

### 试卷管理

```javascript
GET  /api/papers                    // 获取试卷列表
POST /api/papers                    // 创建试卷
POST /api/papers/auto-generate      // 自动组卷
PUT  /api/papers/:id/publish        // 发布试卷
```

## 项目结构

```
online-exam-system/
├── client/                 # 前端 React 项目
│   ├── src/
│   │   ├── components/     # 公共组件
│   │   ├── pages/          # 页面视图
│   │   ├── contexts/       # 全局状态
│   │   └── utils/          # 工具函数
├── server/                 # 后端 Node.js 项目
│   ├── config/             # 配置文件
│   ├── models/             # 数据模型
│   ├── routes/             # API 路由
│   └── middleware/         # 中间件
├── database/               # 数据库脚本
│   ├── init.sql            # 表结构
│   ├── setup.js            # 初始化脚本
│   └── seed.js             # 测试数据
└── .env.example            # 环境变量模板
```

## 技术难点与解决方案

### 1. 考试防作弊

- 前端倒计时 + 后端时间验证
- 答题过程自动保存
- 超时自动提交

### 2. 并发控制

使用数据库事务和乐观锁，防止并发提交导致的数据不一致。

### 3. 性能优化

- 分页查询（最大 100 条/页）
- 数据库连接池
- 索引优化

## 未来规划

- [ ] 添加题目导入导出功能（Excel）
- [ ] 支持在线监考（WebRTC）
- [ ] 增加考试数据分析和可视化
- [ ] 支持多语言切换
- [ ] 移动端 App 开发

## 开源地址

项目地址：[https://github.com/L5T2Y0/online-student-exam-system](https://github.com/L5T2Y0/online-student-exam-system)

如果觉得有用，欢迎 Star ⭐ 支持！

## 总结

这个项目涵盖了全栈开发的方方面面：

- 前端：React 组件化开发、状态管理、路由控制
- 后端：RESTful API 设计、数据库设计、安全防护
- 部署：环境配置、数据初始化、项目部署

非常适合作为学习全栈开发的实战项目。代码完全开源，欢迎学习和交流！
