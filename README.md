# TSV
# TSV 單字檔案載入與檢視工具 (TSV Word Viewer)

這是一個基於 Windows Forms (C#) 開發的桌面應用程式，主要功能是讀取結構化的 TSV（Tab-Separated Values）或 TXT 檔案，將內含的單字、音標、發音路徑與解釋進行解析，並優雅地顯示於介面的清單中。

<img width="1473" height="597" alt="image" src="https://github.com/user-attachments/assets/933da94e-9c57-474d-9acf-9fd51068b96f" />


---

## 🚀 功能特點

* **檔案自訂載入**：支援 2026 年主流的 `.tsv` 與 `.txt` 格式檔案，內建 `OpenFileDialog` 視窗方便引導使用者瀏覽電腦中的檔案。
* **高效能清單重繪**：採用 `ListView` 的 `BeginUpdate()` 與 `EndUpdate()` 機制，在載入大量單字資料時能防止畫面閃爍，確保介面流暢。
* **自訂強型別集合**：繼承 `Collection<WordItem>` 實作 `WordCollection` 類別，封裝了物件轉換邏輯（`LoadFromStringArray`），讓程式碼架構更易於維護與擴充。
* **防呆防誤觸機制**：關閉視窗時內建彈出式確認視窗（`MessageBox`），防止使用者因誤觸而意外關閉程式。
* **即時狀態提示**：下方狀態列（`tsslMessage`）會即時反饋當前系統狀態（如：「請開啟檔案」或「X 個單字已成功載入」）。

---

## 🛠 專案架構與核心類別

### 1. `frmTSVFile` (主要表單)
負責處理所有的 UI 互動（UI Logic），包含選單點擊、檔案讀取事件、以及將資料填入 `ListView`。

### 2. `WordCollection` (巢狀類別)
繼承自 `Collection<WordItem>`，負責管理記憶體中的單字清單。
* **`LoadFromStringArray(string[] lines)`**：負責將從檔案讀進來的每一行字串，逐一實例化為 `WordItem` 物件並存入集合。

### 3. `WordItem` (資料模型 - Model)
*(此類別定義於專案的其他檔案中)* 
預期包含以下屬性：
* `Word`：單字本身
* `Phonogram`：音標
* `SoundPath`：發音音檔路徑
* `Explain`：單字中文解釋

---

## ⚙️ 系統需求與環境

* **開發環境**：Visual Studio 2022 / 2025 或更新版本
* **目標框架**：.NET Framework 4.8+ 或 .NET 6.0/8.0/9.0 Windows Forms
* **依賴命名空間**：
  * `System.IO`（用於檔案讀取）
  * `System.Collections.ObjectModel`（用於強型別集合）
  * `System.Windows.Forms`（UI 控制項）

---

## 📝 檔案格式範例 (TSV)

請確保您載入的 `.tsv` 檔案是以 **Tab (標籤跳格鍵)** 作為分隔符號，格式範例：
```text
apple   /ˈæp.əl/   C:\audio\apple.mp3   蘋果
banana  /bəˈnɑː.nə/  C:\audio\banana.mp3  香蕉
