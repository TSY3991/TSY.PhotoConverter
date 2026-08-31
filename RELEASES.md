# Release 資訊

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
