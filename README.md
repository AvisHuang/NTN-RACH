# NTN-OCUDU 安裝與測試流程

本筆記參考 [OCUDU NTN 官方教學](https://docs.ocudu.org/tutorials/ntn/)。

## 流程圖

![NTN-OCUDU 流程圖](https://github.com/user-attachments/assets/551ef100-d8f7-4fdc-80e7-f46bdcd2335d) 

## 1. 前置準備

- 執行 Ubuntu 22.04.1 LTS 的 PC
- OCUDU 26.04 或更新版本，建置時須啟用 ZeroMQ
- 支援 NTN 的 Amarisoft UE（請確認版本符合[官方教學](https://docs.ocudu.org/tutorials/ntn/)的要求）
- Open5GS 5G 核心網
- Docker 和 Docker Compose，用來啟動 Open5GS
- ZeroMQ

## 2. 安裝 ZeroMQ 與編譯工具

ZeroMQ 是通訊函式庫，可讓 gNB、UE 和通道模擬器透過軟體交換無線訊號樣本，無須直接使用實體無線電設備。

```bash
sudo apt-get update
sudo apt-get install -y libzmq3-dev
```

OCUDU 的其他編譯相依套件，請參考[官方安裝文件](https://docs.ocudu.org/user_manual/installation/)。

## 3. 下載並建置 OCUDU

下載 OCUDU 原始碼，切換至符合 NTN 教學需求的版本，再使用 CMake 設定建置選項並編譯。

- **CMake**：檢查建置環境並產生編譯規則。
- **Make**：依照編譯規則，將原始碼編譯成 OCUDU 程式。

建置時須啟用 ZeroMQ。實際命令與選項請依照[官方安裝文件](https://docs.ocudu.org/user_manual/installation/)及 NTN 教學中的版本要求操作。

## 4. 建置 Amarisoft UE 的 ZeroMQ TRX 驅動

Amarisoft UE 需要 OCUDU 提供的 TRX 驅動，才能透過 ZeroMQ 與 OCUDU gNB 交換訊號樣本。

TRX 驅動負責連接 UE 與 ZeroMQ 介面；它本身不是衛星通道模擬器。請依照[官方 NTN 教學](https://docs.ocudu.org/tutorials/ntn/)提供的步驟編譯驅動，並設定 Amarisoft UE 載入該驅動。

## 5. 選擇衛星通道模擬方式

依照教學選擇並設定通道模擬方式。通道模擬器負責模擬衛星鏈路的傳播特性，例如傳輸延遲；ZeroMQ 則負責在軟體元件之間傳送訊號樣本。

## 6. 準備設定檔

準備並檢查以下設定檔：

- **gNB 設定檔**：NTN、無線參數、ZeroMQ 介面及核心網連線設定。
- **UE 設定檔**：無線參數、ZeroMQ 介面及用戶身分設定。
- **通道設定檔**：依所選的衛星通道模擬方式設定。

請確認 gNB 與 UE 的 ZeroMQ 位址及埠號能正確對接。UE 的用戶身分資料也必須與 Open5GS 中設定的訂閱資料相符。

## 7. 啟動 Open5GS

使用 Docker Compose 啟動 Open5GS，並確認核心網容器正常運作。UE 的訂閱資料及相關網路參數須與核心網設定相符。

## 8. 啟動通道模擬器

依照官方教學啟動通道模擬器，並確認它已連接預期的 ZeroMQ 端點且能正常傳送訊號樣本。

## 9. 啟動 gNB 與 UE

依照官方教學指定的順序啟動 OCUDU gNB 和 Amarisoft UE。查看終端機輸出，確認 gNB 已連上 Open5GS，且 UE 已找到小區並完成註冊。

## 10. 驗證 UE 網路連線

UE 註冊成功並取得 IP 位址後，設定所需路由，再使用 `ping` 和 `iperf` 測試連線與資料傳輸。
