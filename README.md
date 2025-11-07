# 部门工具导航系统

一个基于Bootstrap 5的静态网站，用于企业内部各部门工具导航。该系统支持多部门、多工具的分类展示，并可通过GitHub Pages进行静态部署。

## 项目架构

```
navi-tool/
├── index.html              # 首页 - 部门选择页面
├── views/
│   ├── tools.html          # 工具列表页面
│   └── info.html           # 工具详情页面
├── data/
│   ├── config.json         # 配置文件 - 部门映射关系
│   ├── it.json             # IT部门工具数据
│   └── hr.json             # HR部门工具数据
├── build-single-page.js    # 构建脚本 - 用于生成单页面应用
├── package.json            # Node.js 包配置文件
└── README.md               # 项目说明文档
```

## 功能特性

1. **多部门支持**：通过配置文件支持多个部门的工具导航
2. **数据驱动**：所有内容通过JSON文件驱动，便于维护
3. **响应式设计**：基于Bootstrap 5，适配各种设备屏幕
4. **静态部署**：支持GitHub Pages等静态网站托管服务
5. **安全访问**：通过key映射机制避免直接暴露文件路径
6. **状态保持**：使用sessionStorage保持页面间状态

## 页面说明

### 1. 首页 (index.html)
- 部门选择入口页面
- 展示所有可用部门的导航卡片
- 点击卡片跳转到对应部门的工具列表页面

### 2. 工具列表页面 (views/tools.html)
- 显示指定部门的所有工具
- 按类别分组展示工具
- 支持工具搜索和筛选
- 点击工具可查看详细信息

### 3. 工具详情页面 (views/info.html)
- 显示工具的详细信息
- 包含工具描述、访问链接等信息
- 提供返回上一级的导航功能

## 数据结构

### 配置文件 (data/config.json)
```json
{
  "departments": {
    "it": "data/it.json",
    "hr": "data/hr.json"
  },
  "titles": {
    "it": "IT部门工具导航",
    "hr": "HR部门工具导航"
  },
  "icons": {
    "it": "💻",
    "hr": "👥"
  },
  "descriptions": {
    "it": "技术开发、系统维护相关工具",
    "hr": "人力资源管理相关工具"
  }
}
```

### 工具数据文件 (data/it.json, data/hr.json)
```json
{
  "title": "部门名称",
  "description": "部门描述",
  "items": [
    {
      "id": 1,
      "name": "工具名称",
      "url": "https://example.com",
      "description": "工具描述",
      "category": "工具分类",
      "icon": "🔧"
    }
  ]
}
```

## 部署方式

### 1. 静态部署（GitHub Pages等）
1. 将所有文件推送到GitHub仓库
2. 在仓库设置中启用GitHub Pages
3. 选择根目录作为部署源
4. 访问生成的GitHub Pages URL即可使用

### 2. 单页面应用部署
1. 安装Node.js环境
2. 运行构建命令：
   ```bash
   npm run build
   ```
3. 生成的 `single-page-app.html` 文件即为单页面应用版本
4. 可直接在浏览器中打开或部署到任何静态文件服务器

## 维护指南

请查看 [MAINTAIN.md](file:///c:/Dev/qoder/navi%20tool/MAINTAIN.md) 文件了解如何添加新内容和维护系统。