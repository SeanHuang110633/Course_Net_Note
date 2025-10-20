# CH1
## TCP/IP

### 🧱 第1層：Physical Layer（實體層）

- **角色**：負責實際的**訊號傳輸**。
- **內容**：定義**傳輸媒介（如電纜、光纖）**、**接頭**與**訊號形式（電壓或光脈衝）**。
- **重點**：把 0、1 的位元透過物理媒介送出去。

---

### 🔗 第2層：Data Link Layer（資料鏈結層）

- **角色**：在**單一網路（local network）**中，傳送一個**Frame（影格）**。
- **內容**：包含**影格格式**、**交換器（Switch）與無線接取點（AP）運作**等。
- **重點**：確保資料能在**同一網段**中可靠傳送。

---

### 🌐 第3層：Internet Layer（網際層）

- **角色**：負責**跨網路傳遞封包（Packet）**。
- **內容**：包括**封包結構（IP header）**、**路由器運作（Router）**與**尋址機制（IP address）**。
- **重點**：讓資料能從**來源主機傳到目的主機**（跨網傳輸）。

---

### 🚚 第4層：Transport Layer（傳輸層）

- **角色**：提供端到端的傳輸服務，如**分段（Fragmentation）**與**重組**。
- **內容**：TCP（可靠，連線導向）、UDP（不可靠，非連線導向）。
- **重點**：確保資料能完整到達正確的應用程式。

---

### 💬 第5層：Application Layer（應用層）

- **角色**：**標準化應用程式之間的通訊方式**。
- **內容**：HTTP、FTP、DNS、SMTP 等協定。
- **重點**：提供使用者可直接使用的網路服務（例如網頁、郵件、檔案傳輸）。

---
### 🧩 總結表

|層級|名稱|功能重點|傳輸單位|
|---|---|---|---|
|5|應用層|定義應用間的通訊規範|Data (資料)|
|4|傳輸層|端到端傳輸控制（TCP/UDP）|Segment|
|3|網際層|封包跨網路傳輸（IP、Router）|Packet|
|2|資料鏈結層|同一網路內的傳輸（Switch、MAC）|Frame|
|1|實體層|實際訊號傳送（線纜、無線電波）|Bit|


## Streaming
### 🎬 一、什麼是 Streaming（串流傳輸）

**定義：**  
Streaming 是一種**邊下載邊播放（real-time playback）**的傳輸方式，資料不需全部下載完畢就能開始播放。

📘常見應用：

- YouTube、Netflix、Spotify、線上會議（Zoom、Teams）
    
- 即時影像、音訊、遊戲直播等
    

---

### ⚙️ 二、Streaming 的傳輸特性

|特性|說明|
|---|---|
|**即時性高**|使用者無法容忍延遲（Latency）太大。|
|**連續資料流**|資料是時間序列的影像或音訊封包。|
|**容錯性有限**|少量封包遺失比「延遲重傳」更可接受。|
|**以 UDP 為主**|多用 UDP（非連線導向），因 TCP 的重傳會造成延遲。|

---

### 🌐 三、要做到 Streaming，網路需要哪些配合？

Streaming 要能「順且不斷線」，**網路層與管理層**必須提供幾個關鍵條件👇

#### 1️⃣ **低 Latency（延遲低）**

- 資料封包從伺服器到用戶端的傳送時間要短。
    
- 若延遲太高，影片會「延遲啟動」或「語音不同步」。  
    📘在 Ch4 的 QoS 指標中列為首要參數【114-10 Ch04 L80-82】。
    

#### 2️⃣ **低 Jitter（抖動低）**

- 抖動是延遲時間的變化度。
    
- 高 jitter 會造成畫面卡頓、聲音斷續。  
    📘講義提到 jitter 是 “variability in latency”，影響影音連續性。
    

#### 3️⃣ **足夠 Throughput（吞吐量）**

- 傳輸速率必須大於影音播放速率（例如 1080p 影片約需 5 Mbps）。
    
- 若 throughput 不足，就會緩衝（buffering）。
    

#### 4️⃣ **QoS（Quality of Service） 支援**

- 網路設備要能**優先處理影音封包**。
    
- 例如設定 **Priority Queue** 或 **Traffic Shaping**，確保即時應用優先於一般資料傳輸。  
    📘Ch4 指出 QoS 可用於「流量整形與優先級排程」【114-10 Ch04 L54-73】。
    

#### 5️⃣ **Congestion Prevention（壅塞預防）**

- 要避免短時間的流量暴增導致封包延遲。
    
- 可透過流量監控與緩衝機制吸收瞬時尖峰。
    

---

### 🎯 總結一句話：

> **Streaming 是即時資料播放的傳輸方式，**  
> 要實現它，網路必須提供：
> 
> - 低延遲（Latency）
>     
> - 低抖動（Jitter）
>     
> - 穩定高吞吐量（Throughput）
>     
> - 並透過 QoS 機制確保影音封包的優先權。
>     

## Server Virtualization

### 🖥️ 一、Server Virtualization（伺服器虛擬化）的定義

> **Server Virtualization** 是指在一台**實體伺服器 (physical server)** 上，  
> 利用**虛擬化軟體（Hypervisor）**建立多個**虛擬伺服器（Virtual Machines, VMs）**的技術。

📘課本中提到：「虛擬化可讓多個虛擬伺服器共用同一硬體資源，提升資源使用效率並降低成本。」

---

### ⚙️ 二、運作原理

1️⃣ **Hypervisor（虛擬機監控程式）**

- 位於硬體與作業系統之間。
    
- 負責分配 CPU、記憶體、儲存空間等資源給不同的 VM。
    
- 常見例子：VMware ESXi、Microsoft Hyper-V、KVM、VirtualBox。
    

2️⃣ **Virtual Machines（虛擬機）**

- 每個 VM 都像一台獨立的電腦，能安裝自己的 OS 與應用程式。
    
- 彼此隔離，不會互相干擾。
    

---

## 🧩 三、主要優點（課本強調重點）

|優點|說明|
|---|---|
|**資源整合（Consolidation）**|多台伺服器整合在單一硬體上，節省成本。|
|**彈性部署（Flexibility）**|新系統可在幾分鐘內建立，不需額外硬體。|
|**容錯與備援（Fault Tolerance）**|一台 VM 故障不會影響其他 VM，可快速移轉。|
|**能耗降低（Energy Efficiency）**|伺服器集中化可減少耗電與散熱成本。|

📘出處：Ch1 中 Cloud Computing 與 Virtualization 的段落，說明虛擬化是雲端運算的基礎技術之一。

> “Server virtualization allows multiple virtual servers to run on one physical machine. This reduces cost and increases flexibility.”

---
### ☁️ 四、與雲端運算（Cloud Computing）的關係

- **虛擬化是雲端的基礎。**
    
- 雲端服務商（如 AWS、Azure、GCP）透過虛擬化技術，讓一台大型伺服器能同時服務數百名使用者。

- 提供 IaaS（Infrastructure as a Service）就是利用這種虛擬化環境動態分配運算資源。
    

📘講義強調：

> “Cloud computing builds on server virtualization to provide scalable and on-demand resources.”

**KVM** 是 Linux 原生的開源 Hypervisor，  
**VMware** 是公司；  
**ESXi** 是它的 Hypervisor；  
**vSphere** 是整個虛擬化平台（含 ESXi + vCenter）；  
**vCenter** 是集中管理與自動化的核心伺服器。

## New Client-Server Relationship in Cloud Era
**在雲端時代，新型 Client-Server 關係的核心在於：**

- 用戶端更輕量化（Thin Client）
    
- 伺服器集中於雲端（Cloud-based Server）
    
- 資料與應用經由網際網路提供（as-a-service）
    
- IT 維護與擴充改由雲端供應商負責

==This was Infrastructure and software as a product
This is Infrastructure and software as a service==

Cloud Concerns
Security : hackers & private
Stress on the Network : 需求

## 不同單一網路（single network）無法直接互相連線

**不同單一網路之間無法直接連線的原因**：  
> 1️⃣ 標準不同（Different Standards）  
> 2️⃣ 位址重疊（Overlapping Addresses）  
> 3️⃣ 連線標準不相容（Link uses only one standard）

📘 所以才需要「**Internet 層（Internet Layer）**」的出現，  
由 **Router** 透過 IP 協定來統一跨網溝通，  
形成真正的「網際網路（Internet）」。
