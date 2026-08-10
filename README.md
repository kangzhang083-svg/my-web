# 金融部门票据贴现利率看板

上海明智国际 · 金融票据部 · 铝锭大宗贸易

## 一键部署到 Vercel

### 方法一：Vercel CLI（推荐，可随时更新数据）

```bash
# 1. 安装 Vercel CLI（仅首次）
npm i -g vercel

# 2. 登录 Vercel（仅首次，用 GitHub/GitLab/邮箱）
vercel login

# 3. 部署
cd bill-rate-dashboard
vercel --prod
```

部署后获得永久网址，如 `https://bill-rate-dashboard.vercel.app`

### 方法二：Vercel Web 界面

1. 访问 [vercel.com/new](https://vercel.com/new)
2. 将 `bill-rate-dashboard` 文件夹拖拽到页面
3. 点击 Deploy

### 方法三：GitHub 自动部署

1. 将项目推送到 GitHub
2. 在 Vercel 中 Import 该仓库
3. 之后每次 `git push` 自动部署

---

## 更新数据

数据文件：`data.js`（独立于页面代码）

### 方式 1：本地更新后重新部署

```bash
# 1. 用最新 Excel 生成新的 data.js
#    （双击打开 index.html → 上传Excel → 点「下载更新后看板」）

# 2. 提取 data.js
#    从下载的 HTML 中复制 const EMBEDDED_DATA = [...]; 部分

# 3. 重新部署
vercel --prod
```

### 方式 2：浏览器上传（临时更新）

1. 访问看板网址
2. 点击「上传Excel报价文件」→ 选择最新报价表
3. 数据自动更新并缓存在浏览器本地
4. 点击「下载更新后看板」保存完整 HTML（可发给同事或上传钉钉）

> **注意**：方式 2 的更新仅存在于当前浏览器，刷新其他人的浏览器不会同步。永久更新请使用方式 1。

---

## 项目结构

```
bill-rate-dashboard/
├── index.html    # 主页面（HTML + CSS + JS）
├── data.js       # 报价数据（独立文件，方便更新）
├── vercel.json   # Vercel 部署配置
└── README.md     # 本文件
```

- `index.html`：完整的看板应用，通过 `<script src="data.js">` 加载数据
- `data.js`：仅包含 `const EMBEDDED_DATA = [...];` 一行，含全部历史报价记录
- 更新数据只需替换 `data.js` 文件内容

---

## 功能一览

| 功能 | 说明 |
|------|------|
| 双月日历 | 2018-2030 年范围，快捷日期按钮 |
| KPI 汇总卡 | 最低/最高/平均利率、银行数量、未报价数 |
| 筛选面板 | 地区、利率范围、最低额度、银行搜索 |
| 报价明细表 | 排序、利率回填、颜色标记 |
| 银行 TOP20 图 | 低→高排序横向柱状图 |
| 利率区间分布图 | 直方图 |
| 各地区平均利率图 | 柱状图 + 全市场均值线 |
| Excel 上传 | 支持 .xls/.xlsx |
| Excel 导出 | 筛选结果导出 |
| 下载更新后看板 | 生成最新数据的完整 HTML |
| 本地缓存 | 上传数据自动缓存，关闭浏览器不丢失 |
