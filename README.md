# NTN-OCUDU

## 流程圖

<img width="1046" height="2766" alt="mermaid-diagram (2)" src="https://github.com/user-attachments/assets/551ef100-d8f7-4fdc-80e7-f46bdcd2335d" />

參考 https://docs.ocudu.org/tutorials/ntn/

### 1. 前置準備

- 運行 Ubuntu 22.04.1 LTS 的 PC
- OCUDU（26.04 或更高版本），建置時支援 ZeroMQ
- 支援 NTN 的 Amarisoft UE（2023-12-15 或更高版本）
- Open5GS 5G 核心網
- 使用 Docker 和 Docker Compose 來運行 Open5GS 核心
- ZeroMQ

### 2. 安裝 ZeroMQ 及編譯套件

ZeroMQ 為一套通訊函式庫，可在程式之間傳送資料。在這個流程中，ZeroMQ 負責在 gNB、模擬器和 UE 之間傳遞數位形式的無線電訊號樣本，讓這些元件能透過軟體介面進行通訊。

安裝 ZeroMQ 開發套件：

```bash
sudo apt-get install libzmq3-dev
