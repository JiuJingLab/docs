# TestFlight 發佈資料

版本 `0.2.0`，build `2`，Bundle ID `org.jiujinglab.ios`。2026-09-30 已成功上傳（`Upload succeeded`、`EXPORT SUCCEEDED`），Apple 已完成處理，並已加入 `v0.2 Internal QA`（1 位內部測試者、1 個建置）。v0.1 已完成 Apple 處理並提供內部測試。

## 仍需具備

- 已註冊 Bundle ID `org.jiujinglab.ios`，已建立「揪鏡 JiuJing」App 記錄（Apple ID `6817397936`）。
- Xcode 已登入，Release archive 簽署及 App Store Connect 上傳成功；不要將密碼／API 私鑰提交到 repo。
- 外部測試送審時仍需發佈者提供真實 Beta Review 聯絡姓名、電話及信箱。
- 依 `device-validation.md` 完成真實 BLE／區網／權限驗收。
- 外部 TestFlight 測試須經 Apple 的 Beta App Review；上傳成功不等於已可供外部測試。

## 可複製的 Beta 資料

| 欄位 | 內容 |
|---|---|
| 名稱 | 揪鏡 JiuJing |
| Beta App Description | 揪鏡是一款免費開源的隱私自我檢查工具。v0.2 可探索同一 Wi-Fi 的常見 TCP 端口與 Bonjour 服務，並掃描附近 BLE 廣播。顯示名稱、服務與訊號等可人工確認的線索，不會連線到藍牙裝置、不讀取其他設備的攝影機串流。新增清楚的結果總覽、待確認線索篩選，以及本機相機預覽、放大、補光及紅外線檢查指引；相機僅供人工觀察，不儲存、不上傳畫面，沒有自動 AI 判定。資料只在手機記憶體處理，不上傳、不保存紀錄。結果不能確認或排除偷拍設備。 |
| What to Test | 請使用自己有權測試的 Wi-Fi 與 BLE 設備。確認首次允許／拒絕權限、無 Wi-Fi、藍牙關閉、掃描進度、停止與重掃、背景停止、結果清除、端口及名稱命中理由。另外測試大型結果卡、待確認篩選、部分結果／失敗提示、深色與大字；相機首次允許／拒絕、預覽、放大、補光、前後鏡頭、離頁及背景停止、紅外線指引。請回報機型、iOS 版本、操作步驟與預期／實際結果；截圖前請隱藏裝置資訊。 |
| Review Notes | No account or login required. Use a physical iPhone or iPad. Select Wi-Fi or BLE, confirm permission to inspect the space/network, then tap Start. Local Network and Bluetooth permissions are requested only when scanning. LAN: IPv4 TCP connection checks on ports 80, 443, 554, 8554, 8000, 8080 and declared Bonjour services. BLE: passive advertisement discovery for 20 seconds; no pairing or peripheral connection. Optional Camera Assist uses AVFoundation for local preview, zoom (up to 4x when supported), torch and front/back switching after explicit user action and camera permission. It has no photo/video output, recording, image storage, upload or automated recognition. It stops on dismissal or backgrounding. The infrared guide is manual guidance, not a sensor or detector. No microphone/location access, cloud processing, tracking or analytics. Findings are heuristic clues, never a safety certification or proof of a camera. Simulator cannot validate BLE or local-network privacy. |
| Sign-in required | No |
| Feedback／Support URL | https://jiujinglab.github.io/docs/support/ |
| Privacy Policy URL | https://jiujinglab.github.io/docs/privacy/ |
| Beta Review contact | 由發佈者填寫真實姓名、電話、信箱 |

## 建置與上傳

開啟 `JiuJing.xcodeproj` → JiuJing target → Signing & Capabilities → 選擇正確 Team 和 Bundle ID。選 Any iOS Device，Product → Archive，Organizer → Distribute App → App Store Connect → Upload。或在終端使用：

```bash
DEVELOPMENT_TEAM=你的十碼TeamID BUNDLE_ID=org.jiujinglab.ios ./scripts/archive.sh
```

上傳前確認版本／build 尚未使用；重傳不同二進位須增加 `CURRENT_PROJECT_VERSION`。Archive 後使用 Organizer 驗證與上傳。完成後在 App Store Connect → TestFlight 確認 build、處理狀態與出口合規狀態，再填 Beta 資料並選擇測試群組。公開連結需外部測試設定及必要審查，不可憑空產生。

本 App 使用系統網路 API，未實作自訂加密；`ITSAppUsesNonExemptEncryption=false` 反映目前實作。若增加加密相關功能，需重新核對 Apple 出口合規問卷。

金源獎對原生 iOS 作品要求正式 App Store 上架網址；TestFlight 本身不滿足該項要求。

## v0.1 發佈紀錄（2026-09-30）

- 版本 `0.1.0 (1)`，Bundle ID `org.jiujinglab.ios`，Apple ID `6817397936`。
- iPhone Simulator 9 項核心測試及 5 項 UI 測試全部通過（`TestFlightFinal.xcresult`）。
- Release archive 簽署成功；Xcode 上傳回報 `Upload succeeded`、`EXPORT SUCCEEDED`。
- Apple 處理狀態為「完成」；`0.1.0 (1)` 已加入 `v0.1 Internal QA` 群組，帳號持有人狀態為「已邀請」。內部測試可透過 TestFlight 邀請安裝，外部測試與公開連結尚未開放。
- Beta 描述、行銷 URL、隱私政策 URL、審查備註及建置測試內容均已於 App Store Connect 儲存。
- 外部測試仍需真實審查聯絡資料及必要的 Apple Beta App Review。
- 原始碼含核定 Logo，已合併 [PR #3](https://github.com/JiuJingLab/ios/pull/3)。

[TestFlight 管理頁](https://appstoreconnect.apple.com/apps/6817397936/testflight)。公開隱私政策及支援頁均已部署至 GitHub Pages。

簽署 archive 後，可使用本 repo 的 `release/ExportOptions-TestFlight.plist` 搭配 `xcodebuild -exportArchive` 上傳；其中不含金鑰或密碼。此設定保留手動指定的 build number，重傳不同二進位請先增加 build number。

Apple 參考：[TestFlight overview](https://developer.apple.com/help/app-store-connect/test-a-beta-version/testflight-overview/)、[Upload builds](https://developer.apple.com/help/app-store-connect/manage-builds/upload-builds/)。

## v0.2 發佈紀錄（2026-09-30）

- 開發分支：`v0.2`；版本 `0.2.0 (2)`。
- iPhone Simulator：13 項核心測試與 8 項 UI 測試通過（`V02FinalTests.xcresult`），涵蓋深色／大字；1 項相機硬體案例在 Simulator 明確跳過。
- iPad Simulator：13 項核心測試及 2 項 UI 測試通過；實體相機案例明確跳過。
- iPhone 15／iOS 26.6.1：1 項相機硬體測試通過（`V02HardwareRetry.xcresult`），驗證啟動、2×、補光開關、前後切換及停止。未擷取環境影像。
- Release archive 簽署成功，版本與相機權限檢查通過；Release 不含 Debug 模擬資料。
- Xcode 上傳成功（2026-09-30 10:04 台北時間）；Apple 顯示 `Complete`，建置 `Ready to Test`。
- 已建立 `v0.2 Internal QA`，手動分發 `0.2.0 (2)`，帳號持有人已加入。建置頁確認 1 個群組、1 位測試者，What to Test 已儲存。
- [建置管理頁](https://appstoreconnect.apple.com/apps/6817397936/testflight/ios/0ff53bb7-61e6-4734-9d05-2d3f35144c2c)。外部公開測試尚未開放。
- 新版 Beta 描述已儲存；審查備註儲存時 Apple 回報另有欄位不合法；審查聯絡欄位目前空白，已請發佈者補齊。此問題不阻擋上述內部測試。
