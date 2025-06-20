# 智慧農場 IoT 澆水決策系統 

本專案模擬一套基於 **oneM2M 架構**的智慧農場 IoT 系統，結合 **App Inventor**、**Node-RED**、與 **Mobius (OM2M)**，根據「土壤濕度」與「降雨機率」進行自動澆水判斷與控制，實現智慧化節水農業管理。

## 系統架構
[App Inventor] → [Node-RED] → [Mobius: sensorData Container]
↓
Notification (Subscription)
↓
[Node-RED /monitor 接收]
↓
判斷澆水邏輯 → 上傳至 waterControl

- App 輸入：濕度與降雨機率
- Node-RED：資料接收、格式轉換、建立 ContentInstance
- OM2M：儲存資料並透過 Subscription 通知 Node-RED
- Node-RED：接收通知並執行澆水邏輯，將結果回寫至 `waterControl` container
- App：可根據結果呈現動畫/狀態顯示（可擴充）

##  系統元件說明

| 元件 | 功能 |
|------|------|
| **App Inventor** | 輸入感測資料，傳送至 Node-RED |
| **Node-RED** | 上傳感測資料至 OM2M、訂閱感測結果、執行澆水判斷 |
| **OM2M** | oneM2M 平台，用於儲存 `sensorData` 與 `waterControl` |

---
##  使用方式

###  啟動環境

- 啟動 OM2M 伺服器
- 啟動 Node-RED（預設埠號 http://localhost:1880）

###  App 操作流程

- 輸入土壤濕度與降雨機率（數字格式）
- 輸入 Node-RED 的 IP 位址，例如 `192.168.1.100`
- 點擊傳送，會呼叫 `http://<IP>:1880/sensorData`

###  Node-RED 流程

- 接收資料後上傳至 `/sensorData`
- 建立對該 Container 的訂閱（Subscription），PoA 為 `/monitor`
- 接收到 Notification 時執行澆水邏輯
- 將結果以 ContentInstance 上傳至 `/waterControl`

---

---

## 資源

- `SmartFarmApp.aia`：App Inventor 專案檔
- `SmartFarmFlow.json`：Node-RED Flow 匯出檔
- `screenshots/`：畫面截圖資料夾

---

##  製作資訊

- 專案名稱：智慧農場 IoT 自動澆水系統
- 報告人：蔡炘晏
- 所屬課程：成大資工 物聯網應用與實作 Lab4
- 製作年份：2025 春季學期


