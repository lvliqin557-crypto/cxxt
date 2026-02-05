# GitHub Pages 部署问题解决方案

## 问题 1: Tailwind CSS CDN 生产环境警告

### 问题描述
在 GitHub Pages 上部署时，浏览器控制台会显示警告：
```
cdn.tailwindcss.com should not be used in production
```

### 解决方案（推荐）

由于您的系统没有安装 Node.js/npm，有以下几种选择：

#### 方案 A: 使用在线构建工具（最简单）
1. 访问 https://tailwind.build/
2. 复制您的 HTML 中的 Tailwind 类名
3. 在线生成 CSS
4. 将生成的 CSS 保存为 `styles.css`
5. 在 HTML 中替换 CDN 引用：
   ```html
   <!-- 删除这行 -->
   <script src="https://cdn.tailwindcss.com?plugins=forms,typography,aspect-ratio"></script>
   
   <!-- 添加这行 -->
   <link rel="stylesheet" href="styles.css">
   ```

#### 方案 B: 使用预编译的 Tailwind CSS（推荐用于 GitHub Pages）
1. 下载预编译的 Tailwind CSS 文件：
   - 访问 https://cdn.tailwindcss.com/3.4.0/tailwind.min.css
   - 保存为 `tailwind.min.css`
2. 在 HTML 中替换：
   ```html
   <!-- 删除这行 -->
   <script src="https://cdn.tailwindcss.com?plugins=forms,typography,aspect-ratio"></script>
   
   <!-- 添加这行 -->
   <link rel="stylesheet" href="tailwind.min.css">
   ```

#### 方案 C: 安装 Node.js 后使用官方构建流程（最佳实践）
如果以后安装了 Node.js：
```bash
# 安装依赖
npm install

# 构建生产版本 CSS
npm run build-css

# 在 HTML 中使用
<link rel="stylesheet" href="output.css">
```

---

## 问题 2: JSON 文件加载错误

### 问题描述
```
SyntaxError: Unexpected end of JSON input
Attempting to load: ./香港大学.json
```

### 已修复
✅ 已在代码中添加了文件名映射表，将中文校名映射到对应的英文文件名：
- 香港大学 → HKU.json
- 香港中文大学 → CUHK.json
- 等等...

### 确保文件存在
请确保以下 JSON 文件存在于项目根目录：
- HKU.json (香港大学)
- CUHK.json (香港中文大学)
- HKUST.json (香港科技大学)
- PolyU.json (香港理工大学)
- CityU.json (香港城市大学)
- HKBU.json (香港浸会大学)
- Lingnan.json (岭南大学)
- EdUHK.json (香港教育大学)
- HKMU.json (香港都会大学)
- SYU.json (香港树仁大学)
- HSUHK.json (香港恒生大学)
- CHC.json (香港珠海学院)
- THEi.json (香港高等教育科技学院)
- HKUST-GZ.json (香港科技大学（广州）)
- CUHK-SZ.json (香港中文大学（深圳）)
- CityU-DG.json (香港城市大学（东莞）)
- UIC.json (北师香港浸会大学)
- NUS.json (新加坡国立大学)
- NTU.json (南洋理工大学)
- SMU.json (新加坡管理大学)
- SUTD.json (新加坡科技设计大学)
- SIT.json (新加坡理工大学)
- SUSS.json (新跃社科大学)
- UM.json (澳门大学)
- MUST.json (澳门科技大学)
- CityU-Macau.json (澳门城市大学)
- MPU.json (澳门理工大学)

---

## GitHub Pages 部署注意事项

### 文件结构
```
data/
├── index.html
├── HKU.json
├── CUHK.json
├── ... (其他 JSON 文件)
├── styles.css (可选，如果使用方案 A 或 B)
└── README.md
```

### 确保所有文件都提交到 Git
```bash
git add .
git commit -m "修复 JSON 文件加载和 Tailwind CSS 警告"
git push
```

### 测试本地运行
在推送到 GitHub 之前，建议使用本地服务器测试：
```bash
# 使用 Python
python -m http.server 8000

# 或使用 Node.js 的 http-server
npx http-server
```

然后访问 http://localhost:8000 测试功能是否正常。
