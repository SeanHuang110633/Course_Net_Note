# TCP/IP目的對照表

|**General Purpose (Core Layer)**|**Layer**|**Specific Layer Purpose**|
|---|---|---|
|Application–application communication|Application (5)|Application–application interworking|
|Transmission of a packet across an internet|Transport (4)|Host–host (process-to-process) communication|
||Internet (3)|Packet delivery across an internet|
|Transmission of a frame across a single network (LAN or WAN)|Data Link (2)|Frame delivery across a network|
||Physical (1)|Device–device connection|
# IOT

### 📘 IoT（Internet of Things，物聯網）重點說明：

**1️⃣ IoT 的應用範例 (Application Example of IoT)**  
物聯網涵蓋了多個領域的應用，如智慧家庭、智慧城市、工業自動化、健康照護、車聯網等。教材中並提到「Market Share of IoT Domains」，說明這些應用在市場中所佔的比例。

---

**2️⃣ IoT 的構成要素 (IoT Elements)**  
IoT 由多層次服務組成，包括：

- **Identity-related Service**：透過唯一識別（如感測器ID、RFID等）識別物件。
- **Information-Aggregation Service**：收集與整合感測資料。
- **Collaborative-Aware Service**：讓設備間協同運作並做出智慧決策。
- **Ubiquitous Service**：達成「隨時、隨地、隨物」的連接（Anytime, Anywhere）。
    

---

**3️⃣ IoT 的架構 (Various Types of IoT Architecture)**  
課本提到 IoT 架構有多種形式，從感測層、網路層到應用層，各層之間需透過標準化協定進行通訊，確保不同廠牌與技術之間能互通。

---

**4️⃣ 常見的 IoT 通訊協定 (Common Protocols for IoT)**  
IoT 使用的輕量級通訊協定包括：

- **MQTT (Message Queue Telemetry Transport)**：採取「發佈／訂閱」（publish/subscribe）架構，適合低頻寬與高延遲環境。
- **AMQP (Advanced Message Queueing Protocol)**：用於可靠的訊息傳遞，常見於企業級應用。
- **mDNS / DNS-SD (DNS Service Discovery)**：提供區域網路內設備自動發現服務。
