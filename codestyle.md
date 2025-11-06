# 前端代码风格指南

本文档概述了联系人管理器前端项目的编码风格和约定。

## 一般原则

- 编写干净、可读和可维护的代码
- 遵循现代JavaScript (ES6+)标准
- 使用有意义的变量和函数名称
- 为复杂逻辑添加注释
- 保持函数简短并专注于单一任务

## 格式规范

### 缩进
- 使用2个空格进行缩进
- 永远不要使用制表符

### 行长度
- 最大行长度：100个字符
- 适当换行以保持可读性

### 空白
- 使用空行分隔逻辑部分
- 逗号后添加一个空格
- 运算符周围添加空格
- 函数之间使用一个空行

### 命名约定
- **变量/函数**：camelCase
- **常量**：UPPER_SNAKE_CASE
- **类**：PascalCase
- **HTML元素**：kebab-case
- **CSS类**：kebab-case

## HTML指南

### 结构
- 使用语义化HTML元素（header, nav, main, section, article, footer）
- 保持清晰的层次结构
- 使用适当的缩进
- 包含doctype声明
- 为html标签添加lang属性

### 属性
- 属性值使用双引号
- 一致地排序属性：class, id, data-*, 然后是其他属性
- 使用data-*属性存储自定义数据

### HTML示例

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>联系人管理器</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header class="app-header">
    <h1>联系人管理器</h1>
    <nav class="main-nav">
      <ul>
        <li><a href="#" class="nav-link active">首页</a></li>
        <li><a href="#" class="nav-link">联系人</a></li>
      </ul>
    </nav>
  </header>
  
  <main class="content-area">
    <section class="contact-list">
      <!-- 联系人列表内容 -->
    </section>
  </main>
  
  <footer class="app-footer">
    <p>&copy; 2023 联系人管理器</p>
  </footer>
  
  <script src="app.js"></script>
</body>
</html>
```

## CSS指南

### 组织
- 使用一致的CSS属性顺序：
  1. 定位（position, top, right等）
  2. 显示和盒模型（display, margin, padding等）
  3. 排版（font, color, line-height等）
  4. 视觉效果（background, border, box-shadow等）
  5. 动画和过渡
- 将相关样式分组
- 使用注释分隔主要部分

### 命名
- 对复杂组件使用类似BEM的命名：`.block__element--modifier`
- 使用有意义、描述性的类名
- 避免使用通用类名如"container"或"box"

### 选择器
- 优先使用类选择器而非元素或ID选择器
- 保持选择器特异性低
- 尽可能避免嵌套选择器

### 值
- 使用rem或em作为字体大小单位
- 使用十六进制颜色代码（可能时使用简写）
- 使用flexbox或grid进行布局

### CSS示例

```css
/* 头部样式 */
.app-header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: #f5f7fa;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.app-header h1 {
  margin: 0;
  font-size: 1.5rem;
  color: #333;
}

/* 导航样式 */
.main-nav ul {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.main-nav li {
  margin-left: 1.5rem;
}

.nav-link {
  text-decoration: none;
  color: #666;
  transition: color 0.3s ease;
}

.nav-link:hover,
.nav-link.active {
  color: #667eea;
}
```

## JavaScript指南

### 变量和数据类型
- 使用`const`声明不改变的变量
- 使用`let`声明会改变的变量
- 避免使用`var`
- 使用描述性的变量名
- 对回调函数优先使用箭头函数

### 函数
- 对简短、简单的函数使用箭头函数
- 对较长的函数使用函数声明
- 保持函数在50行以内
- 尽早从函数返回
- 对可选值使用默认参数

### Promises和Async/Await
- 优先使用async/await而非.then()/.catch()
- 使用try/catch块处理错误
- 使用Promise.all()进行并行操作

### DOM操作
- 缓存多次访问的DOM元素
- 对动态内容使用事件委托
- 最小化直接DOM操作
- 使用data属性将数据传递给JavaScript

### API调用
- 在服务模块中集中API调用
- 处理加载和错误状态
- 使用async/await进行API调用
- 包含适当的错误处理

### JavaScript示例

```javascript
// 常量
const API_URL = 'http://localhost:5500';
const CONTACT_LIST_EL = document.getElementById('contact-list');

// DOM元素
const elements = {
  contactForm: document.getElementById('contact-form'),
  nameInput: document.getElementById('name'),
  phoneInput: document.getElementById('phone'),
  emailInput: document.getElementById('email'),
  contactList: document.getElementById('contact-list')
};

// API服务
const apiService = {
  async getContacts(userId) {
    try {
      const response = await fetch(`${API_URL}/contacts/${userId}`);
      if (!response.ok) throw new Error('获取联系人失败');
      return await response.json();
    } catch (error) {
      console.error('获取联系人错误:', error);
      throw error;
    }
  },
  
  async addContact(contactData) {
    try {
      const response = await fetch(`${API_URL}/contacts`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(contactData)
      });
      
      if (!response.ok) throw new Error('添加联系人失败');
      return await response.json();
    } catch (error) {
      console.error('添加联系人错误:', error);
      throw error;
    }
  }
};

```

## 代码检查和格式化工具

- 使用ESLint进行代码分析
- 使用Prettier进行代码格式化
- 配置编辑器在保存时自动格式化

## Git提交指南

- 编写清晰、简洁的提交消息
- 在提交消息中适当引用问题编号
- 保持提交专注于单一变更
