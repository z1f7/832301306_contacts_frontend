# 832301306_contacts_frontend
# 联系人管理系统

一个全栈联系人管理应用，使用Flask（后端）和HTML/CSS/JavaScript（前端）构建。该系统允许用户注册、登录并管理他们的联系人，具有添加、查看、编辑、删除和搜索联系人等功能。

## 功能特点

- 用户认证（注册、登录）
- 联系人管理（添加、查看、编辑、删除）
- 联系人搜索功能
- 响应式设计与现代UI
- 使用SQLite数据库进行数据持久化

## 项目结构

```
contact-manager/
├── README.md          # 项目文档
├── frontend/          # 前端文件
│   ├── README.md      # 前端文档
│   ├── contacts.html  # 主应用页面
│   └── xingkong.jpg   # 背景图片
└── backend/           # 后端文件
    ├── README.md      # 后端文档
    └── app.py         # Flask应用
```

## 开始使用

### 先决条件

- Python 3.7+
- pip（Python包管理器）

### 安装步骤

1. 克隆仓库：
   ```bash
   git clone <仓库URL>
   cd contact-manager
   ```

2. 设置后端：
   ```bash
   cd backend
   pip install flask flask-cors
   ```

3. 设置前端：
   - 前端无需额外安装

### 运行应用

1. 启动后端服务器：
   ```bash
   cd backend
   python app.py
   ```
   服务器将运行在 http://localhost:5500

2. 打开前端：
   - 在浏览器中打开 `frontend/contacts.html`
   - 或通过 http://localhost:5500 访问（后端会提供前端文件）

## API端点

### 认证
- `POST /register` - 注册新用户
- `POST /login` - 登录并获取用户ID

### 联系人
- `POST /contacts` - 添加新联系人
- `GET /contacts/<user_id>` - 获取用户的所有联系人
- `PUT /contacts/<contact_id>` - 更新联系人
- `DELETE /contacts/<contact_id>` - 删除联系人
- `GET /contacts/count/<user_id>` - 获取用户的联系人数量

