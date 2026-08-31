# TSY PhotoConverter 照片轉檔工具

PhotoConverter 是 Windows 10/11 x64 的免安裝批次圖片轉檔工具。可將常見圖片轉為 JPG、PNG、WebP、AVIF、TIFF、BMP、GIF、ICO，或將多張圖片合併成 PDF。

> 此公開 repo 僅提供正式版本資訊、授權聲明與 GitHub Releases 下載資產；原始碼不在此公開 repo 發布。

## 下載

- [下載最新版本](https://github.com/TSY3991/TSY.PhotoConverter/releases/latest)
- [微光工具箱說明頁](https://tsy3991.github.io/TSY.Microglow-Tools/tools/photo-converter/)
- [TSY 微光創作室 Facebook](https://www.facebook.com/TSY.Microglow)

目前正式版本：**v1.1.0**（2026-08-31）

本版只提供 `Portable x64` 免安裝 ZIP，沒有 Setup 安裝版。解壓縮後執行 `PhotoConverter.exe` 即可。

## 支援格式

- 輸入：HEIC、HEIF、JPG、JPEG、PNG、WebP、BMP、TIF、TIFF、GIF、AVIF、ICO
- 輸出：JPG、PNG、WebP、AVIF、TIFF、BMP、GIF、ICO、PDF

## 主要功能

- 批次掃描與子資料夾處理
- 自訂輸出資料夾並保留子資料夾結構
- 等比例縮小、自動轉正與 metadata 控制
- 抽樣估算輸出容量
- 多張圖片合併成單一 PDF
- 暫存寫入、重新解碼驗證、不覆寫既有檔案
- 成功驗證後才可選擇將原始圖片移至資源回收筒

## 使用限制

- 需要 Windows 10/11 x64。
- HEIC/HEIF 相容性會受照片編碼方式與 Windows HEIF codec 影響；無法保證所有手機或設備產生的檔案都能解碼。
- GIF 輸出為單張靜態影像，不保留動畫。
- PDF 模式會輸出 `ConvertedImages.pdf`；檔案已存在時整批略過，且不會回收原始圖片。
- 請先備份重要照片，再使用回收原始圖片功能。

## 完整性驗證

Release 會提供 `SHA256.txt` 與 `RELEASE-MANIFEST.json`。下載後可在 PowerShell 執行：

```powershell
Get-FileHash .\PhotoConverter-Portable-x64-v1.1.0.zip -Algorithm SHA256
```

## 授權

本軟體為保留權利軟體，詳見 [LICENSE.txt](LICENSE.txt)。第三方元件授權聲明隨 Portable ZIP 一併提供。
