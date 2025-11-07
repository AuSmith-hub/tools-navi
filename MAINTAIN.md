# 维护指南

本文档旨在帮助新维护者理解和维护部门工具导航系统。

## 各页面文件作用说明

### 1. 首页 (index.html)
- **功能**：部门选择入口页面
- **主要元素**：
  - 部门导航卡片展示
  - 部门选择处理函数 `selectDepartment(deptKey)`
- **交互逻辑**：
  - 点击部门卡片时调用 `selectDepartment()` 函数
  - 清除之前保存的部门信息
  - 跳转到工具列表页面并传递部门key参数

### 2. 工具列表页面 (views/tools.html)
- **功能**：显示指定部门的所有工具列表
- **主要元素**：
  - 顶部信息栏（包含返回按钮、页面标题等）
  - 工具列表容器
  - 回到顶部按钮
- **核心功能**：
  - 从URL参数或sessionStorage获取部门key
  - 加载配置文件获取数据文件路径
  - 加载对应部门的工具数据
  - 按类别渲染工具列表
  - 提供返回首页功能

### 3. 工具详情页面 (views/info.html)
- **功能**：显示工具的详细信息
- **主要元素**：
  - 顶部信息栏（包含返回按钮）
  - 面包屑导航
  - 工具详细信息展示区域
  - 底部返回按钮
- **核心功能**：
  - 从URL参数获取工具名称
  - 从sessionStorage获取部门key
  - 加载工具详细信息并展示
  - 提供返回工具列表功能

## 如何添加新内容

### 1. 添加新部门

#### 步骤1：创建部门数据文件
在 [data/](file:///c:/Dev/qoder/navi%20tool/data/) 目录下创建新的JSON文件，例如 `finance.json`：

```json
{
  "title": "财务部门工具导航",
  "description": "财务部门常用工具和资源导航",
  "items": [
    {
      "id": 1,
      "name": "财务系统",
      "url": "https://finance.example.com",
      "description": "财务报表和预算管理系统",
      "category": "财务管理",
      "icon": "💰"
    }
  ]
}
```

#### 步骤2：更新配置文件
修改 [data/config.json](file:///c:/Dev/qoder/navi%20tool/data/config.json) 文件，添加新部门的映射关系：

```json
{
  "departments": {
    "it": "data/it.json",
    "hr": "data/hr.json",
    "finance": "data/finance.json"
  },
  "titles": {
    "it": "IT部门工具导航",
    "hr": "HR部门工具导航",
    "finance": "财务部门工具导航"
  },
  "icons": {
    "it": "💻",
    "hr": "👥",
    "finance": "💰"
  },
  "descriptions": {
    "it": "技术开发、系统维护相关工具",
    "hr": "人力资源管理相关工具",
    "finance": "财务管理相关工具"
  }
}
```

### 2. 修改现有部门信息

部门信息现在完全从 [data/config.json](file:///c:/Dev/qoder/navi%20tool/data/config.json) 配置文件中读取，要修改部门信息，只需编辑该文件：

#### 修改部门标题
在 `titles` 对象中找到对应的部门key，修改其值：

```json
"titles": {
  "it": "IT部门工具导航",
  "hr": "人力资源部门工具导航"  // 修改后的标题
}
```

#### 修改部门图标
在 `icons` 对象中找到对应的部门key，修改其值：

```json
"icons": {
  "it": "💻",
  "hr": "😊"  // 修改后的图标
}
```

#### 修改部门描述
在 `descriptions` 对象中找到对应的部门key，修改其值：

```json
"descriptions": {
  "it": "技术开发、系统维护相关工具",
  "hr": "员工管理、招聘培训相关工具"  // 修改后的描述
}
```

#### 修改部门数据文件路径
在 `departments` 对象中找到对应的部门key，修改其值：

```json
"departments": {
  "it": "data/it.json",
  "hr": "data/hr_new.json"  // 修改后的数据文件路径
}
```

### 3. 为现有部门添加新工具

编辑对应部门的JSON文件（如 [data/it.json](file:///c:/Dev/qoder/navi%20tool/data/it.json)），在 `items` 数组中添加新的工具项：

```json
{
  "id": 5,
  "name": "新工具名称",
  "url": "https://newtool.example.com",
  "description": "工具描述信息",
  "category": "工具分类",
  "icon": "🌟"
}
```

### 4. 添加新工具分类

直接在工具数据文件中为工具指定新的分类名称即可，系统会自动按类别分组显示。

## 构建单页面应用版本

项目包含一个构建脚本 [build-single-page.js](file:///c:/Dev/qoder/navi%20tool/build-single-page.js)，可以将所有页面和数据合并成一个单独的HTML文件，适用于边缘节点的serverless计算函数部署。

### 构建步骤：

1. 确保系统已安装Node.js环境
2. 在项目根目录下运行构建命令：
   ```
   node build-single-page.js
   ```
   
   或者使用npm命令：
   ```
   npm run build
   ```

3. 构建完成后会生成 `single-page-app.html` 文件，该文件包含了所有页面和数据，可直接在浏览器中打开或部署到任何静态文件服务器

### 单页面应用特点：

1. 所有数据都嵌入在HTML文件中，无需额外的网络请求
2. 通过前端路由实现页面切换，无页面刷新
3. 适用于边缘计算环境部署
4. 文件体积小，加载速度快

## 注意事项

1. **路径引用**：所有资源引用均使用绝对路径，确保在GitHub Pages上正确加载
2. **安全性**：通过配置文件映射机制避免直接暴露数据文件路径
3. **状态保持**：使用sessionStorage保持部门信息，避免页面跳转时参数丢失
4. **响应式设计**：所有新增内容应遵循Bootstrap 5的响应式设计原则
5. **图标使用**：推荐使用Emoji作为图标，也可使用Font Awesome等图标库
6. **数据格式**：确保JSON文件格式正确，避免语法错误导致页面无法加载