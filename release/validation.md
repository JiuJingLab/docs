# v0.1 驗證紀錄

日期：2026-09-29。環境：Xcode 26.6（17F113）、iOS Simulator 26.5、iPhone 17 Pro、iPad Pro 13。

| 驗證 | 結果 |
|---|---|
| Simulator 編譯 | 通過 |
| XCTest 核心測試 | 9 項通過、0 失敗：名單載入、非攝影機服務判讀、網段邊界及輸入驗證、停止／清除、localhost 真實 TCP listener、取消回呼 |
| iPhone XCUITest | 5 項通過、0 失敗：同意／模式、隱私／指引、BLE 不支援狀態與重試、Wi-Fi 啟停與重試、模擬線索詳情／返回／清除 |
| iPad XCUITest | 2 項通過、0 失敗：同意／模式、模擬線索詳情／返回／清除 |
| App 圖示 | 修復 headless AppKit 產生全黑圖示；CoreGraphics 產圖、像素斷言及視覺檢查通過 |
| Release 測試資料隔離 | 已檢查 Release binary，不含 DEBUG fixture 啟動參數及識別字 |
| Release iOS archive（未簽署） | 通過；`build/V01Validated-unsigned.xcarchive` 僅供建置驗證，不能上傳或安裝 |
| 自動簽署 archive | 失敗：Xcode `No Accounts`，且無 `org.jiujinglab.ios` matching provisioning profile |
| TestFlight build | 尚未上傳，沒有可供測試的 TestFlight 連結 |
| 真實 iPhone BLE／LAN／權限 | 尚未執行；本機列出的 iPhone 為 unavailable |
| 報名資料 | 痛點 36 字、理念 251 字、21 欄；表格可開啟、複製按鈕有回饋及手動選取備援 |
| 影片／報名送出 | 劇本完成；未錄製影片、未上傳 YouTube、未正式送出報名 |

本輪 iPhone 完整 14 項測試結果位於 `build/V01Review.xcresult`；iPad 2 項 UI 測試結果位於 `build/V01iPad.xcresult`。原始 xcresult 及 QA 截圖只留在本機，不提交：模擬器可能帶有既有帳號的系統提示。詳情頁測試使用明確標示的 DEBUG 模擬資料，不能當作實機偵測證據。

不需要 App Intents 的本專案會出現 Xcode「Metadata extraction skipped. No AppIntents.framework dependency found.」工具提示；編譯、連結及測試均通過。沒有用 npm／pip／Cargo 依賴，未執行不適用的 package audit。

須完成 `device-validation.md` 的實機項目，才能宣稱已驗證真實硬體偵測。App 尚未經 Apple Beta App Review 或 App Store Review。

## 新 Logo 套用驗證

2026-09-30：App 圖示、首頁品牌標誌、README、填表頁與網頁圖示統一使用 `docs/brand/jiujing-logo.png`。已確認此檔與使用者提供的原始 Logo 素材逐位元組相同。App 圖示為 1024 × 1024，以相同 sRGB 底色補滿透明圓角且無透明通道；App 內 256 × 256 圖檔保留透明圓角。

- iPhone 17 Pro / iOS 26.5（JiuJing QA）編譯與測試通過：9 項核心測試、1 項同意／模式切換 UI 測試，0 失敗。
- 已檢視 App 圖示與首頁截圖，並更新 `docs/qa` 截圖；資產目錄與 HTML 圖片路徑檢查、`git diff --check` 通過。
- 結果：先前的 Logo 專項測試紀錄（本機）；最終 App 圖示補底修正後另執行 Simulator build 通過。本次未重跑 iPad、Release archive 或實機測試，未發佈至商店。

## TestFlight 發佈前驗證（2026-09-30）

以目前 Logo 與品牌素材重新執行：iPhone 17 Pro / iOS 26.5 的 9 項核心測試及 5 項 UI 測試全部通過（`build/TestFlightFinal.xcresult`）。版本 0.1.0、build 1 的 Release archive 已成功完成 Apple Development 簽署（`build/JiuJing.xcarchive`）。TestFlight 最終上傳與處理狀態以[獨立發佈文件](https://github.com/JiuJingLab/docs/blob/main/release/testflight.md)為準。

## v0.2 驗證（2026-09-30）

- iPhone 17 Pro／iOS 26.5 Simulator：13 項核心測試、8 項 UI 測試通過；1 項實體相機測試按預期跳過（`build/V02FinalTests.xcresult`）。
- 區網／BLE 各自覆蓋待確認、未命中、部分結果、失敗；大字深色模式、線索詳情、停止／重試／清除及紅外線指引均通過。
- iPad Pro 13 吋／iOS 26.5：13 項核心測試及 2 項 UI 測試通過，1 項實體相機測試跳過（`build/V02iPad.xcresult`）。
- iPhone 15／iOS 26.6.1：相機 session 啟動、2×、補光開關、前後切換及停止實機自動測試通過（`build/V02HardwareRetry.xcresult`）。未建立照片／影片輸出，未擷取環境畫面。第一次嘗試因 Developer Disk Image 掛載逾時而未執行，連線恢復後重試成功。
- Release `0.2.0 (2)` archive 簽署成功，版本／權限檢查通過；二進位不含 `ScanFixture` 或 `--ui-test` 模擬啟動參數。
- 已人工檢視 iPhone／iPad 模擬截圖；[v0.2 截圖](https://github.com/JiuJingLab/ios/tree/v0.2/docs/qa/v0.2)明確標示模擬資料。
- 尚未完成所有真實區網／BLE 受控設備、權限拒絕與網路切換案例；不能宣稱偵測無誤判或「無 bug」。
- TestFlight 狀態見 [發佈紀錄](testflight.md)。
