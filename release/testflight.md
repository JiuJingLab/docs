# TestFlight 發佈資料

版本 0.1.0，build 1，預設 Bundle ID `org.jiujinglab.ios`。目前尚未上傳 TestFlight；必須以 App Store Connect 中實際出現且處理完成的 build 為準。

## 仍需具備

- 已註冊 Bundle ID `org.jiujinglab.ios`，已建立「揪鏡 JiuJing」App 記錄（Apple ID `6817397936`）。
- Xcode 登入該帳號，完成 Apple 端要求的必要合約；不要將密碼／API 私鑰提交到 repo。
- 外部測試送審時仍需發佈者提供真實 Beta Review 聯絡姓名、電話及信箱。
- 依 `device-validation.md` 完成真實 BLE／區網／權限驗收。
- 外部 TestFlight 測試須經 Apple 的 Beta App Review；上傳成功不等於已可供外部測試。

## 可複製的 Beta 資料

| 欄位 | 內容 |
|---|---|
| 名稱 | 揪鏡 JiuJing |
| Beta App Description | 揪鏡是一款免費開源的隱私自我檢查工具。v0.1 可探索同一 Wi-Fi 的常見 TCP 端口與 Bonjour 服務，並掃描附近 BLE 廣播。顯示名稱、服務與訊號等可人工確認的線索，不會連線到藍牙裝置、不存取攝影機影像。資料只在手機記憶體處理，不上傳、不保存紀錄。結果不能確認或排除偷拍設備。 |
| What to Test | 請使用自己有權測試的 Wi-Fi 與 BLE 設備。確認首次允許／拒絕權限、無 Wi-Fi、藍牙關閉、掃描進度、停止與重掃、背景停止、結果清除、端口及名稱命中理由。請回報機型、iOS 版本、操作步驟與預期／實際結果；截圖前請隱藏裝置資訊。 |
| Review Notes | No account or login required. Use a physical iPhone or iPad. Select Wi-Fi or BLE, confirm permission to inspect the space/network, then tap Start. Local Network and Bluetooth permissions are requested only when scanning. LAN: IPv4 TCP connection checks on ports 80, 443, 554, 8554, 8000, 8080 and declared Bonjour services. BLE: passive advertisement discovery for 20 seconds; no pairing or peripheral connection. No camera/microphone/location access, cloud processing, tracking or analytics. Findings are heuristic clues, never a safety certification or proof of a camera. Simulator cannot validate BLE or local-network privacy. |
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

## 本次發佈嘗試

已嘗試 Xcode 自動簽署，回報 `No Accounts: Add a new account in Accounts settings` 及缺少本 App 的 provisioning profile。App Store Connect 網頁已登入，但 Xcode 帳號仍未完成設定。本機既有其他 App 的 profile 不能替代此 App 的發佈設定。請在 Xcode 登入發佈用 Apple 帳號，再重試簽署與上傳。2026-09-29 重試仍回報相同錯誤；目前沒有已上傳建置。

[TestFlight 管理頁](https://appstoreconnect.apple.com/apps/6817397936/testflight)。公開隱私政策及支援頁均已部署至 GitHub Pages 並驗證 HTTP 200。

Apple 參考：[TestFlight overview](https://developer.apple.com/help/app-store-connect/test-a-beta-version/testflight-overview/)、[Upload builds](https://developer.apple.com/help/app-store-connect/manage-builds/upload-builds/)。
