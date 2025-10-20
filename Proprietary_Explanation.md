以下是你圖片中所有名詞的簡明版「名詞解釋」，皆對應課本章節與重點整理：

---

### 📘 Ch1 — 基礎與雲端

**1️⃣ Data communication vs. Telecommunication**

* **Data communication**：以**數位資料**為主，通常在**電腦與網路**間傳遞。
* **Telecommunication**：泛指任何形式的**遠距資訊傳輸**（包含語音、影像、數據）。
  👉 數據通訊是電信的一種應用，屬於**數位、封包化的通訊技術**。

**2️⃣ Data link vs. Route**

* **Data link**：在**單一網路（LAN/WAN）中兩裝置**間傳送資料（frame）。
* **Route**：是**跨多個網路**的封包路徑，由路由器（Layer 3）負責。
  👉 Data link = 單網；Route = 多網連接。 

**3️⃣ Single network vs. Internet**

* **Single network**：同一協定、同一標準下的網路（如一個以太網）。
* **Internet**：由多個異質網路透過**路由器連結**而成的「網際網路」。

**4️⃣ Frame vs. Packet**

* **Frame**：資料鏈結層的單位，傳送於單一網路。
* **Packet**：網際層的單位，用於跨網路傳遞。
  👉 Frame 在單一網路內傳輸，Packet 在路由之間傳輸。

---

### 📘 Ch2 — 網路標準

**5️⃣ Connection-oriented vs. Connectionless protocol**

* **Connection-oriented**（如 TCP）：需建立連線、順序傳遞、有確認（ACK），**可靠但負載重**。
* **Connectionless**（如 UDP、IP）：不建立連線、不確認，**快速但不保證可靠性**。

---

### 📘 Ch3 — 網路安全

**6️⃣ Virus vs. Worm**

* **Virus**：需附著在檔案或程式中，靠使用者執行而傳播。
* **Worm**：可自我複製、獨立傳播（如透過網路掃描）。
  👉 Worm 傳播速度更快、對網路影響更大。

**7️⃣ Kill chain（滲透攻擊鏈）**

* 攻擊過程分為：偵查 → 武器化 → 投送 → 利用 → 安裝 → 指揮控制 → 目的達成。
* 改善方式：在每一階段部署偵測與防禦（如封鎖釣魚郵件、阻擋惡意執行）。

---

### 📘 Ch4 — 管理與效能

**8️⃣ QoS vs. SLA**

* **QoS**（Quality of Service）：網路層面指標，包含 latency、jitter、throughput。
* **SLA**（Service Level Agreement）：對外合約，用 QoS 指標作為**服務保證條件**。
  👉 QoS 是**方法**，SLA 是**承諾**。

**9️⃣ Rated speed vs. Throughput**

* **Rated speed**：理論最大速率（標示值）。
* **Throughput**：實際傳輸速率（有效資料率）。
  👉 實際 throughput 通常僅 rated speed 的 40%～60%。

**🔟 Latency vs. Jitter**

* **Latency**：封包傳遞的延遲時間。
* **Jitter**：延遲時間的變化程度。
  👉 高 jitter 會造成影音卡頓、語音不穩。 

**11️⃣ Momentary traffic peaks vs. Congestion prevention**

* **Momentary peaks**：短暫的流量暴增（可用緩衝或暫存吸收）。
* **Congestion prevention**：防止長期壅塞，需使用流量控制、優先權排程、整形等技術。
  👉 目標是讓網路不超出容量極限。 

**12️⃣ SNMP 的意義與應用**

* **SNMP**（Simple Network Management Protocol）：用於監控與管理網路設備的標準協定。
* 可集中收集狀態（如流量、錯誤率）、設定閾值、發送警報。
  👉 是 Ethernet switch、router 常用的管理機制。 

---

### 📘 Ch5 — Ethernet

**13️⃣ Baseband vs. Broadband**

* **Baseband**：整條通道傳一組數位信號，屬**數位傳輸**（如 Ethernet）。
* **Broadband**：將頻寬分成多個頻道、可同時傳多訊號（如有線電視）。
  👉 Baseband 用於資料網，Broadband 用於多媒體。 

**14️⃣ Baseband Transmission vs. Broadband Transmission**

* **Baseband Transmission**：訊號不調變，直接以數位形式傳輸；範圍短、速率高。
* **Broadband Transmission**：需調變成類比信號、可同軸多頻；距離長、可多通道。
  👉 Ethernet 用 Baseband；Cable 用 Broadband。

### 📘 Ch5 Ethernet 802.3 LANs

**1️⃣ Baseband Channel vs. Broadband Channel**

* **Baseband Channel**：單一數位訊號通道，直接以電壓或光脈衝傳送 0/1（如 Ethernet LAN）。
* **Broadband Channel**：多頻通道，可同時傳送多個模擬訊號（如 Cable TV）。
  📍出處：

---

**2️⃣ Access Line vs. Trunk Line (p.22)**

* **Access Line**：用戶端接入交換設備的線路（如住家網路 → ISP）。
* **Trunk Line**：交換設備之間的高容量連線（Switch ↔ Switch）。
  📍出處：

---

**3️⃣ VLAN（Virtual LAN）**

* **定義**：由軟體設定的虛擬區域網路，非實體布線形成。
* **優點**：可減少廣播流量、提升安全性，讓同一物理網路可劃分多個邏輯網段。
  📍出處：

---

### 📘 Ch6 Wireless Networks I

**4️⃣ Service Band vs. Golden Band (Golden Zone)**

* **Service Band**：法規允許的特定無線頻段（如 2.4GHz、5GHz）。
* **Golden Zone**：約 500MHz～10GHz 的理想頻率區間，兼具良好傳播特性與足夠頻寬。
  👉 太高頻會有傳播問題，太低頻頻寬不足。
  📍出處：

---

**5️⃣ PSK mode vs. 802.1x mode (=1X, in 802.11i)**

* **PSK (Pre-Shared Key)**：共用密鑰方式，用於家庭或小型網路（WPA2-PSK）。
* **802.1X mode**：基於使用者身分驗證（EAP + RADIUS），用於企業級網路，安全性更高。
  📍出處：

---

### 📘 核心通訊概念（跨章節）

**6️⃣ Circuit Switching vs. Packet Switching**

* **Circuit Switching**：通訊前需建立固定通道（如電話網路）。
* **Packet Switching**：資料分割成封包獨立傳送（如網際網路）。
  👉 封包交換效率高，但延遲變化大。
  📍出處：Ch1、Ch2 網路架構概述部分。

---

**7️⃣ LAN Fiber vs. Carrier Fiber**

* **LAN Fiber**：用於企業內網，距離短（200–500m）、成本較低。
* **Carrier Fiber**：用於電信骨幹，支援長距離、高容量傳輸。
  📍出處：

---

**8️⃣ SDLC vs. SLC**

* **SDLC (Synchronous Data Link Control)**：IBM 所制定的同步資料鏈結協定，為 HDLC 前身。
* **SLC (Subscriber Loop Carrier)**：電信接入技術，用於將多條語音或資料線路集中傳輸。
  📍未於講義明列，但屬常見通訊系統名詞，補充於考試延伸題背景。

---

**9️⃣ ADSL vs. Cable (Ch10)**

* **ADSL**：利用電話線，速度不對稱（上傳慢，下行快）。
* **Cable**：使用同軸電纜，頻寬更高但共享，易受同區用戶影響。
  📍出處：Ch10 寬頻接入比較頁。

---

**🔟 Bit Rate vs. Baud Rate**

* **Bit Rate**：每秒傳輸的 bit 數（bps）。
* **Baud Rate**：每秒符號變化次數（symbols/s）。
  👉 若每符號代表多 bit，bit rate > baud rate。
  📍課本未明列，但屬通訊基本速率概念（補充於 modulation 章節）。




-
