# NTN-RACH

流程圖

<img width="1046" height="2766" alt="mermaid-diagram (2)" src="https://github.com/user-attachments/assets/551ef100-d8f7-4fdc-80e7-f46bdcd2335d" />


參考 https://docs.ocudu.org/tutorials/ntn/


1. 前置準備

運行 Ubuntu 22.04.1 LTS 的 PC

OCUDU（26.04 或更高版本）建置時支援 ZeroMQ

支援 NTN 的 Amarisoft UE（2023-12-15 或更高版本）

Open5GS 5G核心網

使用 Docker和 Docker Compose 來運行 Open5GS 核心

ZeroMQ

2. 安裝ZeroMQ及編譯套件
ZeroMQ為一套通訊函式庫，在程式之間傳送資料，把數位形式的無線電訊號樣本，在 gNB、模擬器和 UE 之間傳遞。

4. 下載OCUDU原始碼
5. CMAKE:檢查編譯套件產生編譯規則
6. MAKE：把原始碼編譯成OCUDU程式
7. 編譯Amarisoft UE所需的ZeroMQ TRX驅動
   Amarisoft UE用來模擬User，它搜尋基地台、讀取衛星資訊、嘗試註冊並傳送資料。
   TRX是使UE能透過ZeroMQ的形式收送訊號
9. 選擇衛星通道模擬方式 
10. 準備並設定gNB、UE、NTN設定檔
11. 用Docker Compose啟動Open5GS
12. 啟動通道模擬確認
13. 確認UE註冊並取得ip
14. 設定路由、使用ping iperf測試
