# CSS 現代與核心功能完整指南

本指南收錄了現代 CSS 中最關鍵的佈局、現代前沿特性、選擇器、動效、效能優化與開發便利性功能。每個項目均包含功能名稱、用途描述與具體的示範程式碼。

---

## 目錄
1. [佈局與幾何定位（Layout & Positioning）](#一佈局與幾何定位layout--positioning)
2. [現代前沿架構特性（Modern & Cutting-Edge Architecture）](#二現代前沿架構特性modern--cutting-edge-architecture)
3. [選擇器與偽類/偽元素（Selectors & Pseudo-elements）](#三選擇器與偽類偽元素selectors--pseudo-elements)
4. [視覺特效、圖形與遮罩（Visual Effects & Graphics）](#四視覺特效圖形與遮罩visual-effects--graphics)
5. [動畫與互動（Animations & Interactions）](#五動畫與互動animations--interactions)
6. [色彩、變數與數學運算（Colors, Variables & Math）](#六色彩變數與數學運算colors-variables--math)
7. [排版細節與無障礙（Typography & Accessibility）](#七排版細節與無障礙typography--accessibility)
8. [捲動控制與效能優化（Scroll Control & Performance）](#八捲動控制與效能優化scroll-control--performance)
9. [日常開發便利性助手（Quality of Life Helpers）](#九日常開發便利性助手quality-of-life-helpers)

---

## 一、佈局與幾何定位（Layout & Positioning）

### 1. Flexbox 一維佈局
* **描述**：負責單一行或單一列的空間分配、彈性伸縮與軸向對齊。
* **示範 code**：
```css
.flex-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
}

.flex-item {
  flex: 1 1 200px; /* grow, shrink, basis */
}
```

---

### 2. CSS Grid 二維網格系統
* **描述**：同時掌控水平列（columns）與垂直行（rows），能以極簡語法製作完全自適應的瀑布流卡片。
* **示範 code**：
```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
}
```

---

### 3. Subgrid 巢狀子網格
* **描述**：讓子元素直接繼承父級 Grid 的軌道定義，確保深層卡片的標題、內容與按鈕在視覺上維持跨卡片齊平。
* **示範 code**：
```css
.card {
  display: grid;
  grid-template-rows: subgrid;
  grid-row: span 3; /* 跨越標題、內文、底欄三行 */
}
```

---

### 4. CSS Anchor Positioning（錨點定位）
* **描述**：無需 JavaScript（如 Popper.js），直接將絕對定位元素依附錨定在另一個元素旁，並支援邊界自動調整。
* **示範 code**：
```css
/* 被錨定的目標元素 */
.anchor-button {
  anchor-name: --my-button;
}

/* 浮動提示框 */
.tooltip {
  position: absolute;
  position-anchor: --my-button;
  bottom: anchor(top);
  left: anchor(center);
  transform: translateX(-50%);
}
```

---

### 5. Multi-column Layout（多欄排版）
* **描述**：報章雜誌風格的多欄文字排列，內容會依欄數自動平流至下一欄。
* **示範 code**：
```css
.newspaper-article {
  column-count: 3;
  column-gap: 2rem;
  column-rule: 1px solid #e2e8f0;
}
```

---

### 6. Sticky Positioning（黏性定位）
* **描述**：在元素滾動到特定閾值時自動固定在視窗或容器邊緣，介於 relative 與 fixed 之間。
* **示範 code**：
```css
.table-header {
  position: sticky;
  top: 0;
  z-index: 10;
  background-color: #ffffff;
}
```

---

### 7. Logical Properties（邏輯屬性）與 Inset
* **描述**：使用邏輯流向（inline, block）取代固定方向（left/right, top/bottom），原生適應多語系與 RTL（從右至左）排版。
* **示範 code**：
```css
.modal-overlay {
  position: fixed;
  inset: 0; /* 同時設定 top, right, bottom, left 為 0 */
}

.box {
  margin-inline: auto; /* 水平居中 */
  padding-block: 2rem; /* 上下內距 */
}
```

---

## 二、現代前沿架構特性（Modern & Cutting-Edge Architecture）

### 8. Container Queries（容器查詢）
* **描述**：不再根據整個瀏覽器視窗寬度，而是依照「父容器本身寬度」動態調整元件樣式，達到真正獨立封裝的元件設計。
* **示範 code**：
```css
.card-wrapper {
  container-type: inline-size;
  container-name: card;
}

@container card (min-width: 450px) {
  .card-content {
    display: flex;
    flex-direction: row;
  }
}
```

---

### 9. Native CSS Nesting（原生巢狀）
* **描述**：無需依賴 Sass 或 Less 等預處理器，直接在標準 CSS 中巢狀撰寫子選擇器與狀態偽類。
* **示範 code**：
```css
.btn {
  background-color: #2563eb;
  color: white;

  &:hover {
    background-color: #1d4ed8;
  }

  &.btn-secondary {
    background-color: #64748b;
  }
}
```

---

### 10. Cascade Layers（@layer 層級控制）
* **描述**：顯式定義 CSS 樣式的覆蓋優先順序，徹底解決大型專案中權重（Specificity）失控與 `!important` 濫用問題。
* **示範 code**：
```css
@layer reset, base, components, utilities;

@layer components {
  .btn { background: red; } /* 優先權高於 base，無論選擇器權重多大 */
}

@layer base {
  button.btn { background: blue; }
}
```

---

### 11. View Transitions API（跨頁轉場）
* **描述**：在 SPA 切換視圖或 MPA 頁面跳轉時，由瀏覽器自動計算元素的前後狀態並執行平滑轉場動畫。
* **示範 code**：
```css
@view-transition {
  navigation: auto;
}

.header-title {
  view-transition-name: main-title;
}
```

---

### 12. Scoped Styles（@scope 作用域樣式）
* **描述**：限定樣式僅在特定 DOM 子樹內生效，甚至可定義排除特定子區域的下邊界（Donut Scope）。
* **示範 code**：
```css
/* 僅在 .card 內部生效，但排除 .card-body 內部的 .content */
@scope (.card) to (.card-body) {
  p {
    color: #475569;
  }
}
```

---

## 三、選擇器與偽類/偽元素（Selectors & Pseudo-elements）

### 13. `:has()`（父選擇器 / 關聯選擇器）
* **描述**：根據內部包含的子元素或子元素狀態，反向為父元素套用樣式。
* **示範 code**：
```css
/* 當表單內有驗證未通過的欄位時，讓整個表單邊框發紅 */
form:has(input:invalid) {
  border: 2px solid #ef4444;
}

/* 僅包含圖片的卡片 */
.card:has(> img:only-child) {
  padding: 0;
}
```

---

### 14. `:is()` 與 `:where()` 集合選擇器
* **描述**：將重複的選擇器列表簡寫。`:is()` 權重為列表最高者，而 `:where()` 的權重永遠為 0，適合用來寫預設樣式。
* **示範 code**：
```css
/* 簡化前：header a:hover, main a:hover, footer a:hover */
:is(header, main, footer) a:hover {
  text-decoration: underline;
}

/* 零權重重置樣式 */
:where(h1, h2, h3) {
  margin: 0;
}
```

---

### 15. `:focus-visible` 焦點控制
* **描述**：僅在使用者透過鍵盤（如 Tab 鍵）操作時顯示外框焦點，避免滑鼠點擊時產生礙眼的預設邊框。
* **示範 code**：
```css
button:focus {
  outline: none; /* 移除滑鼠點擊焦點 */
}

button:focus-visible {
  outline: 2px solid #2563eb;
  outline-offset: 2px;
}
```

---

### 16. `:user-valid` 與 `:user-invalid`
* **描述**：只有在使用者與欄位產生互動並失焦後才顯示驗證結果，改善頁面一載入就出現錯誤樣式的不好體驗。
* **示範 code**：
```css
input:user-invalid {
  border-color: #dc2626;
  background-color: #fef2f2;
}
```

---

### 17. `::backdrop` 與 Top Layer
* **描述**：專門為原生 `<dialog>` 或處於 Fullscreen 狀態的頂層元素設定全螢幕半透明背景。
* **示範 code**：
```css
dialog::backdrop {
  background-color: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(4px);
}
```

---

### 18. `::marker`
* **描述**：自訂清單項目符號（Bullet points）或數字的顏色、大小與內容。
* **示範 code**：
```css
ul li::marker {
  color: #2563eb;
  font-size: 1.2em;
}
```

---

## 四、視覺特效、圖形與遮罩（Visual Effects & Graphics）

### 19. `backdrop-filter`（背景濾鏡）
* **描述**：對元素後方的內容套用模糊或變色效果，製作毛玻璃質感（Glassmorphism）。
* **示範 code**：
```css
.glass-panel {
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(12px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.3);
}
```

---

### 20. `filter: drop-shadow()`
* **描述**：依據 PNG/SVG 實際透明輪廓投射真實陰影，而非像 `box-shadow` 只能投射出外層矩形陰影。
* **示範 code**：
```css
.logo-icon {
  filter: drop-shadow(0 4px 6px rgba(0, 0, 0, 0.3));
}
```

---

### 21. `clip-path`（路徑裁切）
* **描述**：透過多邊形、圓形或向量路徑將矩形元素裁切成特定形狀。
* **示範 code**：
```css
.hero-banner {
  /* 裁切出底部傾斜的視覺切角 */
  clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
}
```

---

### 22. `mask-image`（遮罩漸變）
* **描述**：使用漸層或圖案作為透明度遮罩，產生邊界淡出等遮蔽效果。
* **示範 code**：
```css
.fade-out-text {
  mask-image: linear-gradient(to bottom, black 60%, transparent 100%);
}
```

---

### 23. `shape-outside`（異形文字環繞）
* **描述**：讓文字環繞著非矩形的浮動幾何形狀排列。
* **示範 code**：
```css
.circle-avatar {
  float: left;
  width: 150px;
  height: 150px;
  border-radius: 50%;
  shape-outside: circle(50%);
}
```

---

### 24. `conic-gradient()`（圓錐漸層）
* **描述**：讓顏色沿中心軸旋轉漸變，常用於色相環、純 CSS 圓餅圖與雷達掃描動畫。
* **示範 code**：
```css
.pie-chart {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  background: conic-gradient(#2563eb 0% 70%, #e2e8f0 70% 100%);
}
```

---

## 五、動畫與互動（Animations & Interactions）

### 25. 滾動驅動動畫（Scroll-driven Animations）
* **描述**：無須 JS 監聽 `window.onscroll`，將動畫進度直接綁定到頁面滾動條或元素進入視窗的進度。
* **示範 code**：
```css
@keyframes progress {
  from { width: 0%; }
  to { width: 100%; }
}

.scroll-progress-bar {
  animation: progress auto linear;
  animation-timeline: scroll(root block);
}
```

---

### 26. 離散屬性動畫（`@starting-style` 與 `allow-discrete`）
* **描述**：讓 `display: none` 切換到 `display: block` 的進入過程也能直接觸發 CSS 平滑淡入過渡。
* **示範 code**：
```css
.dialog {
  display: block;
  opacity: 1;
  transition: opacity 0.3s ease, display 0.3s allow-discrete;

  @starting-style {
    opacity: 0;
  }
}
```

---

### 27. CSS Transitions & Keyframes
* **描述**：標準的屬性過渡與多階段影格動畫，實現介面微互動。
* **示範 code**：
```css
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

.animated-badge {
  animation: pulse 2s infinite ease-in-out;
}
```

---

### 28. `pointer-events: none`
* **描述**：讓元素對滑鼠與觸控事件透明，直接穿透至下方底層元素，常用於按鈕內的裝飾性 Icon。
* **示範 code**：
```css
.select-chevron-icon {
  position: absolute;
  pointer-events: none; /* 點擊圖示依然能觸發底下的 select 開啟 */
}
```

---

## 六、色彩、變數與數學運算（Colors, Variables & Math）

### 29. CSS Custom Properties（CSS 變數）
* **描述**：具備層疊與動態繼承特性的自訂變數，是主題切換與設計系統的核心。
* **示範 code**：
```css
:root {
  --primary: #3b82f6;
}

[data-theme="dark"] {
  --primary: #60a5fa;
}

.button {
  background-color: var(--primary);
}
```

---

### 30. Oklch 色彩空間
* **描述**：感知均勻的色彩空間，調整色相時亮度不會劇烈跳變，在螢幕上呈現更自然的漸層與主題色盤。
* **示範 code**：
```css
.vibrant-box {
  /* 亮度 (0-1), 色彩純度 (Chroma), 色相環 (0-360) */
  background-color: oklch(0.65 0.24 140);
}
```

---

### 31. `color-mix()` 與 `light-dark()`
* **描述**：純 CSS 原生混色與依據系統深淺主題自動切換色票。
* **示範 code**：
```css
.mixed-color {
  /* 在 sRGB 空間將 primary 與白色以 80:20 混合 */
  background-color: color-mix(in srgb, var(--primary) 80%, white);
}

.auto-theme-text {
  color: light-dark(#1e293b, #f8fafc);
}
```

---

### 32. 數學函式：`clamp()`、`min()`、`max()`
* **描述**：限制數值在上下限區間內動態計算，常用於免寫 media query 的流體字體大小（Fluid Typography）。
* **示範 code**：
```css
.fluid-heading {
  /* 最小 1.5rem，理想大小 3vw，最大 3rem */
  font-size: clamp(1.5rem, 3vw + 1rem, 3rem);
}
```

---

## 七、排版細節與無障礙（Typography & Accessibility）

### 33. `text-wrap: balance` 與 `pretty`
* **描述**：由瀏覽器排版引擎自動計算最合適的斷行長度，避免標題行末出現難看的「孤字」。
* **示範 code**：
```css
h1, h2 {
  text-wrap: balance; /* 平衡每行字數長度 */
}

p {
  text-wrap: pretty; /* 預防段落最後出現單獨孤字 */
}
```

---

### 34. 多行文字截斷（`-webkit-line-clamp`）
* **描述**：限制區塊內顯示的行數，超出部分自動以省略號（`...`）截斷。
* **示範 code**：
```css
.truncate-multiline {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

---

### 35. `font-variant-numeric: tabular-nums`
* **描述**：強制數字使用等寬排版，避免計時器或數據表格在數字跳動時產生左右微幅抖動。
* **示範 code**：
```css
.counter {
  font-variant-numeric: tabular-nums;
}
```

---

### 36. 首字下沉（`initial-letter`）
* **描述**：純 CSS 實現雜誌印刷風格的段落開頭大型下沉首字。
* **示範 code**：
```css
p:first-of-type::first-letter {
  initial-letter: 3 2; /* 佔 3 行高，下沉 2 行 */
  color: #1e3a8a;
}
```

---

### 37. `accent-color`
* **描述**：只需一行屬性，即可將原生 checkbox、radio、range 與 progress 改為指定的品牌色。
* **示範 code**：
```css
:root {
  accent-color: #10b981;
}
```

---

## 八、捲動控制與效能優化（Scroll Control & Performance）

### 38. Scroll Snap（滾動吸附）
* **描述**：無需 JS，以純 CSS 打造類似手機 App 的水平輪播與逐屏滑動吸附。
* **示範 code**：
```css
.slider {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
}

.slide {
  flex: 0 0 100%;
  scroll-snap-align: center;
}
```

---

### 39. `scroll-margin-top`
* **描述**：解決固定在頁面頂部的導覽列（Sticky / Fixed Header）遮擋網頁錨點跳轉目標的歷史問題。
* **示範 code**：
```css
section[id] {
  scroll-margin-top: 80px; /* 保留頂部導覽列的高度空間 */
}
```

---

### 40. `overscroll-behavior: contain`
* **描述**：防止彈窗（Modal）內容滾動到底部時，連帶觸發外層 body 滾動（滾動穿透）。
* **示範 code**：
```css
.modal-body {
  overflow-y: auto;
  overscroll-behavior: contain;
}
```

---

### 41. `content-visibility: auto`
* **描述**：類似虛擬捲軸，瀏覽器會跳過視窗外非可見元素的排版與繪製，長頁面的初次載入速度顯著提升。
* **示範 code**：
```css
.long-list-item {
  content-visibility: auto;
  contain-intrinsic-size: 0 350px; /* 提供未渲染時的預估佔位高度，防止卷軸抖動 */
}
```

---

## 九、日常開發便利性助手（Quality of Life Helpers）

### 42. 動態視窗單位（`dvh`, `svh`, `lvh`）
* **描述**：解決行動裝置上 `100vh` 會被 Safari / Chrome 動態工具列遮擋或縮放破版的問題。
* **示範 code**：
```css
.fullscreen-hero {
  min-height: 100dvh; /* 動態隨工具列伸長縮短的 100% 高度 */
}
```

---

### 43. 媒體查詢範圍語法（Range Media Queries）
* **描述**：使用直觀的比較運算子（`<`, `<=`, `>=`, `>`）取代繁瑣易混淆的 `min-width` 與 `max-width`。
* **示範 code**：
```css
@media (768px <= width <= 1024px) {
  .sidebar { display: none; }
}
```

---

### 44. `aspect-ratio`（寬高比固定）
* **描述**：免除利用 `padding-top` 百分比的舊時代 hack，直接指定元素或容器的長寬比，有效消除 CLS 版面抖動。
* **示範 code**：
```css
.video-container {
  aspect-ratio: 16 / 9;
  width: 100%;
}
```

---

### 45. `isolation: isolate`（隔離層疊上下文）
* **描述**：建立獨立的層疊上下文，將內部的 `z-index` 完全限制在元件內，防止元素內部層級意外污染或擊穿外層元件。
* **示範 code**：
```css
.component-card {
  isolation: isolate;
}
```

---

### 46. 安全區域邊界（`safe-area-inset-*`）
* **描述**：讓介面避開 iPhone 螢幕瀏海、動態島與底端 Home 導覽條。
* **示範 code**：
```css
.fixed-footer {
  padding-bottom: env(safe-area-inset-bottom, 16px);
}
```

---

### 47. 偏好感知查詢：`prefers-reduced-motion`
* **描述**：偵測使用者作業系統是否開啟「減少動態效果」，自動降級為淡入或關閉動畫以照顧眩暈症使用者。
* **示範 code**：
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```