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

本輪 iPhone 完整 14 項測試結果位於 `build/V01Review.xcresult`；iPad 2 項 UI 測試結果位於 `build/V01iPad.xcresult`。原始 xcresult 及 QA 截圖只留在本機，不提交：模擬器可能帶有既有帳號的系統提示。詳情頁測試使用明確標示的 DEBUG 模擬資料，不能當作實機偵測證據。

不需要 App Intents 的本專案會出現 Xcode「Metadata extraction skipped. No AppIntents.framework dependency found.」工具提示；編譯、連結及測試均通過。沒有用 npm／pip／Cargo 依賴，未執行不適用的 package audit。

須完成 `device-validation.md` 的實機項目，才能宣稱已驗證真實硬體偵測。App 尚未經 Apple Beta App Review 或 App Store Review。
