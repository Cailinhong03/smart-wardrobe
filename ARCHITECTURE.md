# 智能电子衣橱架构设计

## 1. 技术栈选择及原因

### 推荐技术栈
1. **前端**：HTML5 + CSS3 (Tailwind CSS) + JavaScript  
2. **数据存储**：localStorage (本地存储)  
3. **PWA**：manifest.json + service-worker.js  
4. **开发工具**：Visual Studio Code (免费、轻量)  

### 选择理由

#### 1. **前端技术**  
- **HTML5**：网页的基础结构，语法简单，容易上手，是所有前端开发的起点。  
- **Tailwind CSS**：通过CDN引入即可使用，无需安装配置，提供了大量预定义的样式类，零基础用户可以通过组合类名快速构建美观的界面，避免了复杂的CSS语法学习。  
- **JavaScript**：实现交互逻辑，如表单提交、数据存储、API调用等，是前端开发的核心语言，语法相对直观。  

#### 2. **数据存储**  
- **localStorage**：浏览器内置的本地存储功能，无需服务器，数据存储在用户本地设备，适合自用项目。操作简单，通过`localStorage.setItem()`和`localStorage.getItem()`即可实现数据的存取。  

#### 3. **PWA技术**  
- **manifest.json**：定义应用的名称、图标、显示方式等，使应用可以添加到主屏幕。  
- **service-worker.js**：实现离线缓存功能，支持离线访问，提升用户体验。  

#### 4. **开发工具**  
- **Visual Studio Code**：免费、轻量、功能强大的代码编辑器，支持语法高亮、代码提示等功能，适合初学者使用。  

### 技术栈优势
- **低门槛**：所有技术都可以通过浏览器直接运行，无需配置复杂的开发环境。  
- **易学习**：HTML、CSS、JavaScript是前端基础，学习资源丰富，Tailwind CSS进一步降低了样式开发的难度。  
- **功能满足**：足以实现电子衣橱的核心功能，如衣物管理、穿搭推荐、天气集成等。  
- **扩展性**：后续可根据需求逐步学习更高级的技术，如React、Node.js等。  

## 2. 项目目录结构

```
smart-wardrobe/
├── index.html          # 主页面
├── manifest.json       # PWA配置文件
├── service-worker.js   # Service Worker文件
├── assets/             # 静态资源
│   └── icons/          # 图标
├── README.md           # 项目说明
├── PRD.md              # 产品需求文档
└── ARCHITECTURE.md     # 架构设计文档
```

## 3. 核心模块说明

### 3.1 用户信息模块
- **功能**：管理用户身高、体重、身材类型、风格偏好、舞蹈课信息
- **实现**：使用localStorage存储用户信息，提供表单输入和验证
- **关键函数**：
  - `saveUserInfo()`：保存用户信息到本地存储
  - `loadUserInfo()`：从本地存储加载用户信息

### 3.2 衣物管理模块
- **功能**：添加、编辑、删除衣物，衣物分类管理
- **实现**：使用localStorage存储衣物数据，支持手动输入
- **关键函数**：
  - `addClothing()`：添加新衣物
  - `getClothingByCategory()`：按分类获取衣物

### 3.3 穿搭推荐模块
- **功能**：根据天气、场合、用户偏好生成穿搭推荐
- **实现**：基于简单的规则引擎，结合天气数据和用户偏好生成推荐
- **关键函数**：
  - `generateOutfit()`：生成穿搭推荐
  - `getWeeklyOutfits()`：生成一周穿搭计划

### 3.4 天气集成模块
- **功能**：获取天气信息
- **实现**：模拟天气数据，后续可集成OpenWeatherMap API
- **关键函数**：
  - `loadWeather()`：加载天气信息

### 3.5 界面渲染模块
- **功能**：渲染页面内容，处理用户交互
- **实现**：使用原生JavaScript操作DOM，Tailwind CSS美化界面
- **关键函数**：
  - `renderClothing()`：渲染衣物列表
  - `renderOutfits()`：渲染穿搭推荐

## 4. 数据模型设计

### 4.1 用户信息模型
```javascript
{
  id: "user1",
  height: 165,           // 身高(cm)
  weight: 50,            // 体重(kg)
  bodyType: "hourglass", // 身材类型：pear, apple, h, hourglass
  stylePreferences: ["casual", "sporty"], // 风格偏好
  location: "北京市",     // 地理位置
  danceClass: {           // 舞蹈课计划
    type: "jazz",      // 舞蹈类型：ballet, jazz, hiphop, latin
    day: "Wednesday",
    time: "evening",
    isWorkday: true
  },
  commute: {             // 通勤方式
    byBike: false,
    hasGym: true
  }
}
```

### 4.2 衣物模型
```javascript
{
  id: "clothing1",
  name: "白色T恤",
  type: "top",           // 类型：top, pants, skirt, shoes, accessory, hat
  color: "white",
  style: "casual",       // 风格：casual, sporty, retro, minimal, street, elegant, oldMoney, american, korean
  season: ["spring", "summer"], // 适用季节
  occasions: ["daily", "shopping"], // 适用场合
  image: "base64编码或本地路径",
  lastWorn: "2026-04-20", // 上次穿着日期
  frequency: 5           // 穿着频率
}
```

### 4.3 穿搭模型
```javascript
{
  id: "outfit1",
  date: "2026-04-21",
  weather: {
    condition: "sunny",
    temperature: 22
  },
  clothingItems: [       // 穿搭包含的衣物
    "clothing1",         // 衣物ID
    "clothing2",
    "clothing3"
  ],
  occasion: "daily",     // 适用场合
  style: "casual",       // 穿搭风格
  notes: "适合日常出行"   // 穿搭说明
}
```

## 5. 代码规范

### 5.1 HTML规范
- 使用语义化标签（header, nav, main, section, footer）
- 保持缩进一致（2或4个空格）
- 为所有图片添加alt属性
- 使用小写标签和属性名

### 5.2 CSS规范
- 使用Tailwind CSS类名，减少自定义CSS
- 自定义样式放在style标签中，使用BEM命名规范
- 保持选择器简洁，避免过度嵌套

### 5.3 JavaScript规范
- 使用ES6+语法（let, const, arrow functions）
- 采用模块化设计，将功能划分为不同的函数
- 函数和变量命名使用驼峰命名法
- 添加适当的注释，解释复杂逻辑
- 使用try-catch处理可能的错误

### 5.4 代码组织
- 按功能模块组织代码
- 保持文件结构清晰
- 避免重复代码，提取公共函数
- 定期清理无用代码

## 6. 实施建议

### 6.1 开发步骤
1. **搭建基础结构**：创建HTML文件，引入Tailwind CSS
2. **实现用户信息模块**：设计表单，实现数据存储
3. **实现衣物管理模块**：添加衣物功能，分类管理
4. **集成天气API**：获取天气数据
5. **实现穿搭推荐**：基于规则生成推荐
6. **美化界面**：优化UI设计，实现响应式布局
7. **测试与调试**：确保功能正常运行

### 6.2 学习资源
- **HTML/CSS基础**：W3Schools, MDN Web Docs
- **JavaScript基础**：JavaScript.info, MDN Web Docs
- **Tailwind CSS**：官方文档
- **PWA**：Google PWA文档

### 6.3 注意事项
- 由于是本地存储，清除浏览器数据会导致数据丢失
- 天气API有调用次数限制，注意合理使用
- 图片上传功能可能需要处理文件大小限制
- 确保代码兼容主流浏览器

这套轻量架构设计适合0基础用户，使用简单的技术栈，无需复杂的开发环境，同时能够实现PRD中描述的核心功能。通过模块化设计和清晰的代码规范，用户可以逐步学习和扩展功能。