# Release 資訊

## v1.2.3 — 2026-10-12

本版為發行檔精簡更新：發行檔移除建置除錯資訊，檔案更精簡。功能與介面與 v1.2.2 相同，沒有行為改變。

### 主要更新

- 發行檔精簡，移除建置除錯資訊。
- 介面、圖示與轉檔功能不變。

### 下載資產

- `PhotoConverterSetup-v1.2.3.exe`：Windows x64 安裝版（建議一般使用者使用）
- `PhotoConverter-Portable-x64-v1.2.3.zip`：Windows x64 免安裝版
- `SHA256.txt`：安裝版／ZIP／解壓後 EXE 的 SHA-256
- `RELEASE-MANIFEST.json`：版本、日期與資產資訊

### 已驗證範圍

- 核心測試 21/21 通過。
- Portable UI Automation 通過：視窗移動、縮放、最大化／還原、關閉、轉檔、再次掃描排除成品、單一執行個體與 Facebook 按鈕。
- Setup UI Automation 通過：移動、縮放、最小化／還原、最大化／還原與關閉。

## v1.2.2 — 2026-09-08

本版強化批次轉檔安全性與 Windows 使用體驗：已轉好的圖片不會在下一次掃描時再次被轉檔；並統一更新主程式、視窗、工作列、安裝程式與捷徑圖示。安裝程式也修正桌面／開始功能表捷徑可能只有圖示、卻沒有正確啟動目標的問題。

### 主要更新

- 輸出回來源資料夾時統一加上 `_converted`，重新掃描會辨識並排除已完成的成品。
- 原始圖片已移至資源回收筒、資料夾只剩成品時，也不會把成品再次加入待轉清單。
- 換用 256／128／64／48／32／16px 的全彩 PNG 壓縮 ICO，主程式、視窗、工作列、Alt+Tab、Setup 與捷徑使用相同圖示。
- 安裝程式改用 Windows 原生 Shell Link 建立捷徑，完整寫入 `TargetPath`、`WorkingDirectory` 與 `IconLocation`。
- Setup 建置加入隔離捷徑讀回測試，若捷徑無法啟動主程式就直接中止建置。
- 保留較矮螢幕的視窗工作區防護，最小化、最大化、還原、拖曳、縮放與關閉均已重新驗證。

### 下載資產

- `PhotoConverterSetup-v1.2.2.exe`：Windows x64 安裝版（建議一般使用者使用）
- `PhotoConverter-Portable-x64-v1.2.2.zip`：Windows x64 免安裝版
- `SHA256.txt`：安裝版／ZIP／解壓後 EXE 的 SHA-256
- `RELEASE-MANIFEST.json`：版本、日期與資產資訊

### 已驗證範圍

- 核心測試 21/21 通過，包含「已轉成品不會再次掃描」與「原圖回收後只剩成品也不會再次掃描」。
- Portable UI Automation 通過：視窗移動、四邊／四角縮放、最大化／還原、關閉、WebP 轉檔、再次掃描排除成品、單一執行個體與 Facebook 按鈕。
- Setup UI Automation 通過：移動、縮放、最小化／還原、最大化／還原與關閉。
- 實際安裝後已驗證桌面／開始功能表捷徑、解除安裝登錄資訊與安裝檔雜湊。

### 使用需求與限制

- 支援 Windows 10/11 x64；目前未提供 ARM64 版本。
- 輸入：HEIC、HEIF、JPG、JPEG、PNG、WebP、BMP、TIF、TIFF、GIF、AVIF、ICO。
- 輸出：JPG、PNG、WebP、AVIF、TIFF、BMP、GIF、ICO、PDF。
- HEIC/HEIF 解碼依賴 Windows HEIF codec 與實際照片編碼；不保證所有手機或設備產生的檔案都能解碼。
- GIF 只輸出第一張靜態畫面，不保留動畫。
- PDF 模式會輸出 `ConvertedImages.pdf`；同名檔案已存在時整批略過，且不會回收原始圖片。
- 安裝程式尚未申請數位簽章，Windows SmartScreen 可能顯示安全提醒。

## v1.2.1 — 2026-09-01

修正兩個 v1.2.0 遺留問題：

- **主視窗在較矮螢幕上開啟時，視窗上緣（含最小化／最大化／關閉鈕）會被推到螢幕外**，導致完全無法縮放、最小化、最大化或關閉視窗。原因是預設視窗高度 900px，在工作區高度小於 900px 的螢幕（例如 1536×864）上置中顯示時沒有自動縮小。現在開窗前會偵測目前螢幕工作區大小，超過就自動縮小再置中，確保視窗永遠完整落在可視範圍內。
- **應用程式圖示畫質很差（鋸齒、色階很少）**。原因是圖示產生腳本用了 `.NET` 的 `Bitmap.GetHicon()`，這個 API 不論來源圖片多精細，內部一律轉成 32×32、16 色的舊式圖示格式。已改用手動組出的「PNG 壓縮 ICO」格式，6 種尺寸（256～16px）皆為全彩並保留透明度。

### 下載資產

- `PhotoConverterSetup-v1.2.1.exe`：Windows x64 安裝版（建議一般使用者使用）
- `PhotoConverter-Portable-x64-v1.2.1.zip`：Windows x64 免安裝版
- `SHA256.txt`：安裝版／ZIP／解壓後 EXE 的 SHA-256
- `RELEASE-MANIFEST.json`：版本與資產資訊

已安裝 v1.2.0 的使用者，直接下載並重新執行 Setup 安裝版即可就地更新，設定與診斷紀錄不受影響。

### 已驗證範圍

- 用 Win32 API 直接量測視窗座標確認修復前後差異：修復前視窗頂端 `Top=-42`（超出螢幕），修復後 `Top=0, Bottom=816`，完整落在螢幕工作區內。
- 圖示重新產生後為 6 種尺寸的全彩 PNG 壓縮 ICO（256/128/64/48/32/16px），32 bits/pixel 含 alpha 透明度。
- 其餘功能與 v1.2.0 相同：19/19 單元測試通過，安裝／解除安裝流程已於隔離環境驗證。

## v1.2.0 — 2026-08-31

新增 **Setup 安裝版**，跟免安裝版並列提供，一般使用者建議改用安裝版（開始功能表／桌面捷徑、可從「新增或移除程式」解除安裝，不需要系統管理員權限）。同時新增診斷錯誤紀錄機制：程式崩潰、單一檔案轉檔逾時（3 分鐘）、轉檔到一半被強制中止，都會記錄到 `%LocalAppData%\TSY\PhotoConverter\Logs\bug.log`，方便回報問題時附上。

### 下載資產

- `PhotoConverterSetup-v1.2.0.exe`：Windows x64 安裝版（建議一般使用者使用）
- `PhotoConverter-Portable-x64-v1.2.0.zip`：Windows x64 免安裝版
- `SHA256.txt`：安裝版／ZIP／解壓後 EXE 的 SHA-256
- `RELEASE-MANIFEST.json`：版本與資產資訊

安裝程式尚未申請數位簽章憑證，執行時若出現「Windows 已保護您的電腦」的藍色畫面，屬正常現象，點選「其他資訊」→「仍要執行」即可繼續安裝。安裝程式支援靜默安裝（`/S`、`/dir=`、`/nodesktop`）與靜默解除安裝（`/uninstall /S [/purge]`），適合批次部署。

### 已驗證範圍

- 安裝／解除安裝流程已在隔離測試環境完整驗證：安裝正確落地全部檔案並建立捷徑，解除安裝正確清空並移除捷徑。
- 診斷錯誤紀錄機制（崩潰記錄、逾時偵測、中斷偵測）已有對應單元測試覆蓋。
- 其餘轉檔核心功能與 v1.1.0 相同，見下方 v1.1.0 紀錄。

### 格式行為

- GIF 僅輸出單張靜態影像，不保留動畫。
- PDF 會將掃描到的圖片合併為 `ConvertedImages.pdf`；同名 PDF 已存在時不覆寫，PDF 模式也不回收原始圖片。

## v1.1.0 — 2026-08-31

PhotoConverter 現在可以批次處理 HEIC、HEIF、JPG、PNG、WebP 等常見圖片，並輸出 JPG、PNG、WebP、AVIF、TIFF、BMP、GIF、ICO 或合併 PDF。新增縮圖、自動轉正、metadata 控制、輸出預覽、容量估算，以及微光創作室 Facebook 入口。

### 下載資產

- `PhotoConverter-Portable-x64-v1.1.0.zip`：Windows x64 免安裝版
- `SHA256.txt`：ZIP 與解壓後 EXE 的 SHA-256
- `RELEASE-MANIFEST.json`：版本與資產資訊

本版沒有 Setup 安裝版。

### 已驗證範圍

- 八種影像輸出格式均完成產生與重新解碼測試。
- PDF 合併完成頁數驗證。
- 封裝後 Portable EXE 已完成 UI 啟動、WebP 轉檔、Facebook 按鈕與單一實例測試。
- 未取得所有手機與設備產生的 HEIC/HEIF 樣本，因此不宣稱全面相容。遇到特定 HEIC/HEIF 無法解碼時，請確認 Windows 已安裝 Microsoft HEIF Image Extensions。

### 格式行為

- GIF 僅輸出單張靜態影像，不保留動畫。
- PDF 會將掃描到的圖片合併為 `ConvertedImages.pdf`；同名 PDF 已存在時不覆寫，PDF 模式也不回收原始圖片。
