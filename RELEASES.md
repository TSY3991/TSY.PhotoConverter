# Release 資訊

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
