# Vue App — 响应式管理面板

一个使用 Vue 3 + Vue Router + Vite 构建的纯前端响应式管理页面，配有仪表盘、任务清单和备忘录功能。

## 项目截图

| 页面 | 说明 |
|------|------|
| 📊 仪表盘 | 统计卡片、最近任务概览、快捷入口 |
| ✅ 任务清单 | 添加/删除任务、标记完成、按状态筛选 |
| 📝 备忘录 | 新建/删除笔记，网格布局展示 |
| ℹ️ 关于 | 项目信息和技术栈介绍 |

## 技术栈

- [Vue 3](https://vuejs.org/) — Composition API + `<script setup>`
- [Vue Router](https://router.vuejs.org/) — SPA 路由管理（懒加载）
- [Vite](https://vite.dev/) — 构建工具
- 纯 CSS — Flexbox + Grid 响应式布局，无第三方 UI 库

## 快速开始

```bash
# 进入项目目录
cd vue-app

# 安装依赖
npm install

# 启动开发服务器
npm run dev
```

启动后浏览器打开 `http://localhost:5173` 即可访问。

## 打包构建

```bash
npm run build
```

构建产物在 `dist/` 目录下。

## 项目结构

```
src/
├── main.js                 # 入口文件
├── App.vue                 # 主布局（侧边栏 + 内容区）
├── router/index.js         # 路由配置
├── assets/                 # 样式文件
└── views/
    ├── DashboardView.vue   # 仪表盘
    ├── TasksView.vue       # 任务清单
    ├── NotesView.vue       # 备忘录
    └── AboutView.vue       # 关于
```

## 特点

- 纯前端，无需后端和数据库
- 桌面端侧边栏导航，移动端自动折叠为汉堡菜单
- 热更新开发体验，修改代码后浏览器自动刷新
- 无外部 UI 依赖，纯 CSS 实现
