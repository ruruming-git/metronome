# 🎵 節拍器 Metronome

一個仿真木製節拍器，以純 HTML/CSS/JavaScript 製作，無需任何框架或套件。針對 iOS Safari 與 OLED 螢幕特別優化。

![preview](preview.png)

---

## 功能特色

### 核心功能
- **擺針動畫**：指針從底部軸心向上伸出，左右擺動，符合真實節拍器物理結構
- **BPM 範圍**：40 ~ 208 BPM（涵蓋 Grave 到 Prestissimo 所有古典速度標記）
- **節拍聲**：首拍強音（1800 Hz）、其他拍次音（1200 Hz），使用 Web Audio API 合成
- **速度名稱**：自動顯示對應義大利速度術語（Andante、Allegro 等）

### 互動方式
| 操作 | 功能 |
|------|------|
| **拖動配重塊** | 向下拖 → 加快，向上拖 → 變慢 |
| **BPM 滑桿** | 精細調整速度 |
| **Tap 按鈕** | 連續點擊 6 次取平均計算 BPM |
| **▶ 開始 / ⏹ 停止** | 啟動或停止節拍器 |
| 鍵盤 `Space` | 開始 / 停止 |
| 鍵盤 `↑` / `↓` | BPM ±1 |
| 鍵盤 `T` | Tap Tempo |

### 拍號選擇
支援 **4/4、3/4、2/4、6/8**，底部燈號顯示當前拍次，首拍以不同音色標示。

---

## iOS 優化

- **Wake Lock**：啟動節拍器後自動申請 `navigator.wakeLock`，防止螢幕自動熄滅；停止時釋放。切換 App 後返回自動重新申請。
- **AudioContext 解鎖**：iOS 要求用戶手勢才能啟動音訊，首次觸碰頁面即自動解鎖。
- **觸控拖曳**：配重塊拖動時呼叫 `preventDefault()` 阻止頁面滾動，支援 `touchcancel` 處理來電中斷。
- **安全區域**：使用 `env(safe-area-inset-*)` 支援 iPhone 瀏海（Dynamic Island）與底部 Home Indicator。
- **點擊目標**：所有按鈕符合 Apple HIG 44×44pt 最小可點擊尺寸。
- **小螢幕適配**：裝置高度 < 700px 時節拍器自動縮小（scale 0.8）。
- **viewport-fit=cover**：配合 `black-translucent` 狀態列讓畫面滿版。

---

## OLED 螢幕保護

- **純黑背景**（`#000000`）：OLED 黑色像素完全不發光，大幅降低耗電與燒屏風險。
- **次要元素極暗化**：標題、速度名稱、BPM 單位、拍號標籤等非核心文字使用接近黑色的深棕色（`#1a1408` ~ `#2a2218`），視覺上幾乎不可見但不影響使用。
- **主要元素保留金色**：BPM 數字、配重塊、滑桿、啟用按鈕、活躍節拍燈保持金色（`#c9a84c`），確保功能可辨識。
- **移除背景漸層光暈**：原本的 radial-gradient 背景光已移除。

---

## 在 GitHub Pages 上運行

### 步驟

1. **建立新的 GitHub Repository**（例如 `metronome`）

2. **上傳檔案**：
   ```
   metronome/
   ├── index.html      ← 將 metronome.html 重新命名為 index.html
   └── README.md
   ```

3. **啟用 GitHub Pages**：
   - 進入 Repository → **Settings** → **Pages**
   - Source 選擇 **Deploy from a branch**
   - Branch 選 **main**，資料夾選 **/ (root)**
   - 點擊 **Save**

4. **等待約 1~2 分鐘**，GitHub Actions 自動部署後，網址會顯示在 Pages 設定頁。

5. **存取網址**：
   ```
   https://<你的GitHub帳號>.github.io/<repository名稱>/
   ```

### 加到 iPhone 主畫面

1. 用 Safari 開啟上述網址
2. 點擊分享按鈕（底部中間的方框加箭頭圖示）
3. 選擇「**加入主畫面**」
4. 命名為「節拍器」，點擊「加入」

加入後以全螢幕 App 模式運行，狀態列為黑色，體驗接近原生 App。

---

## 技術規格

| 項目 | 內容 |
|------|------|
| 技術 | 純 HTML5 / CSS3 / Vanilla JavaScript |
| 依賴 | 無（零 npm 套件） |
| 字型 | Google Fonts（Playfair Display、Crimson Pro） |
| 音訊 | Web Audio API（OscillatorNode + GainNode） |
| 動畫 | CSS `@keyframes`（swing） |
| 圖形 | 內嵌 SVG（木紋節拍器琴體） |
| 螢幕鎖定 | Screen Wake Lock API |
| 瀏覽器支援 | iOS Safari 14.5+、Chrome 86+、Firefox 90+ |

---

## 檔案結構

```
index.html   — 所有功能整合於單一 HTML 檔案，包含 CSS 與 JavaScript
README.md    — 本說明文件
```

---

## 授權

MIT License — 自由使用、修改與分發。
