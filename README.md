# 智能电子衣橱

## 项目简介

智能电子衣橱是一款帮助用户管理衣物、生成个性化穿搭推荐的应用，旨在减少用户做决定的时间，提高穿搭效率，同时传达高审美标准。

### 核心功能

- **用户信息管理**：身高体重输入、身材类型选择、个人风格偏好设置、舞蹈课信息管理
- **衣物管理**：添加衣物、分类管理、衣物展示
- **穿搭推荐**：一周穿搭计划、天气穿搭推荐、舞蹈课穿搭推荐
- **天气集成**：显示天气信息，提供天气预警
- **PWA支持**：可添加到手机主屏幕，支持离线访问

## 技术栈

- **前端**：HTML5, CSS3 (Tailwind CSS), JavaScript
- **PWA**：manifest.json, service-worker.js
- **第三方库**：
  - Tailwind CSS v3（用于样式）
  - Font Awesome（用于图标）

## 如何运行

### 方法一：直接在浏览器中打开

1. 找到 `index.html` 文件
2. 双击该文件，它会在您的默认浏览器中打开
3. 开始使用智能电子衣橱应用

### 方法二：使用本地服务器

如果您希望使用本地服务器运行，可以尝试以下方法：

1. **使用Python**（如果已安装）：
   ```bash
   cd smart-wardrobe
   python -m http.server 8000
   ```
   然后在浏览器中访问 `http://localhost:8000`

2. **使用Node.js**（如果已安装）：
   ```bash
   cd smart-wardrobe
   npx http-server -p 8000
   ```
   然后在浏览器中访问 `http://localhost:8000`

## 部署到GitHub Pages

1. 在GitHub上创建一个新仓库
2. 将项目文件推送到仓库
3. 在仓库设置中开启GitHub Pages
4. 获取部署后的URL

## 在手机上使用

1. 访问部署后的URL
2. **iOS设备**：点击分享按钮，选择"添加到主屏幕"
3. **Android设备**：点击三点菜单，选择"添加到主屏幕"
4. 现在您可以像使用原生应用一样随时打开智能电子衣橱

## 项目结构

```
smart-wardrobe/
├── index.html          # 主页面
├── manifest.json       # PWA配置文件
├── service-worker.js   # Service Worker文件
├── assets/             # 静态资源
│   └── icons/          # 图标
└── README.md           # 项目说明
```