# Release 資訊

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
