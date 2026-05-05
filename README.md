這是一個設計相當完整且具備實戰能力的 **後慈湖驗票系統 Turbo**。該系統採用了現代化的行動優先（Mobile-First）設計，結合了 QR Code 掃描、手動補票以及後台連動（Google Apps Script）功能。

以下是為你撰寫的 `README.md`，內容涵蓋了功能亮點、安裝方式、以及技術細節，這能幫助其他開發者或管理員快速上手。

---

# 🎟️ 後慈湖驗票系統 Turbo (Back Cihu Ticketing System)

這是一個專為後慈湖導覽設計的輕量化、高響應式 **前端驗票介面**。系統採用 `html5-qrcode` 庫，支援手機鏡頭掃描 QR Code 並即時與 Google Sheets 後端同步進場人數與票價分類。

## 🌟 功能亮點

*   **⚡ 極速掃描**：優化相機參數，支援 30 FPS 高幀率掃描與環境自動對焦。
*   **📱 行動裝置優化**：深色模式設計，減少陽光下操作的視覺疲勞，並具備觸覺回饋（振動）。
*   **🎫 雙模驗票**：
    *   **相機掃描**：自動解析 URL 中的 `id` 參數。
    *   **手動輸入**：應對掃描失敗或特殊票種的應急方案。
*   **📊 即時數據回報**：驗票成功後即時顯示票價結構（現金、悠遊卡、優待票等）及場內總人數。
*   **🔧 進園人數微調**：內建微調面板，可快速進行 `+1`, `-1`, `+5`, `-5` 的手動修正。

---

## 🛠️ 技術架構

*   **前端**: HTML5, CSS3 (Flex/Grid), Vanilla JavaScript.
*   **掃描庫**: [html5-qrcode](https://github.com/mebjas/html5-qrcode).
*   **後端連結**: Google Apps Script (GAS) API.
*   **字體**: Google Fonts - Noto Sans TC.

---

## 🚀 快速開始

### 1. 部署 API
確保你的 Google Apps Script 已經發佈為「Web App」，且權限設定為「Anyone」（任何人，包含匿名者）。

### 2. 設定程式碼
在 `index.html` 中，找到以下變數並替換為你的 GAS 部署網址：
```javascript
const API_URL = "YOUR_GAS_DEPLOYMENT_URL";
```

### 3. 本地測試
由於相機功能涉及隱私安全，請確保在以下環境中運行：
*   **HTTPS 環境** (生產環境必備)
*   **Localhost** (開發環境)

---

## 📡 API 通訊協議

### 驗票請求 (Verify)
*   **Method**: `POST`
*   **Body**: `JSON.stringify({ id: "票號", action: "verify" })`

### 人數微調 (Adjust)
*   **Method**: `POST`
*   **Body**: 
    ```json
    {
      "type": "IN",
      "delta": 5,
      "source": "驗票端微調",
      "note": "票號:XXXX"
    }
    ```

---

## 🎨 UI 設計規範
*   **主要色調**: `#00d2ff` (Turbo Blue)
*   **成功狀態**: `#2ecc71` (Success Green)
*   **錯誤狀態**: `#e74c3c` (Error Red)
*   **背景**: `#121212` (OLED Dark)

---

## ⚠️ 注意事項
1.  **瀏覽器相容性**: 建議使用 iOS Safari 11+ 或 Android Chrome。
2.  **相機權限**: 初次開啟需點擊「啟動相機」並授權瀏覽器存取。
3.  **網路穩定性**: 驗票過程依賴實時 API 回傳，網路環境較差時會顯示「網路異常」。

---

> **開發建議**: 若未來需要處理更複雜的離線需求，建議加入 **Service Worker** 將此網頁轉為 **PWA (Progressive Web App)**，以獲得類原生 App 的體驗。
```
