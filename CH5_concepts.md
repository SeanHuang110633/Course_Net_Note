# Cat6、Cat7、Cat8


| 類別 (Category) | 最大傳輸速率                         | 頻寬 (MHz)         | 最大距離   | 主要應用             | 備註                        |
| ------------- | ------------------------------ | ---------------- | ------ | ---------------- | ------------------------- |
| **Cat6**      | 1 Gbps（最遠 100m）10 Gbps（最遠 55m） | 250 MHz          | 100 公尺 | 一般企業、家用網路        | 成本低、常用於一般區域網路             |
| **Cat7**      | 10 Gbps（最遠 100m）               | 600 MHz          | 100 公尺 | 伺服器機房、資料中心       | 使用 **屏蔽雙絞線 (STP)**，抗干擾能力強 |
| **Cat8**      | 25~40 Gbps（最遠 30m）             | 2000 MHz (2 GHz) | 30 公尺  | **資料中心、高速伺服器連線** | 為高頻寬、高速短距離連線設計            |

📘 **延伸說明：**

- 「100BASE-XX」中的 “BASE” 表示 **Baseband（基頻傳輸）**，  
    而 “XX” 則代表**傳輸介質種類**（例如 TX 代表雙絞線、FX 代表光纖）。


# 802.1x Port-Based Access Control

### 🔴 問題（The Problem）

- 在沒有安全機制的情況下，任何人只要進入建築、插上網線（例如 RJ-45 port），  
    就能直接連上企業內部網路，**完全繞過防火牆（Firewall）**。
- 這樣攻擊者就能入侵或竊取內部資料。
- 802.1X 是一種「連線前先驗身分」的網路安全機制，  讓企業能防止未授權設備透過實體網線進入內部網路

---
### 🔵 解決方案（Solution）

➡ **802.1X Port-Based Access Control**  
讓交換機（Switch）在每個實體埠（port）上都具備「身份驗證」功能。  
設備插上網線後，**必須先通過驗證（Authenticate）**，才能被允許上網。

---

### ⚙️ 運作角色與流程

圖中三個主要角色如下：

|角色|名稱|功能|
|---|---|---|
|**Supplicant (Peer)**|用戶端（例如筆電）|發起連線，提交身份驗證資訊（帳號密碼或憑證）|
|**Authenticator**|交換機（Switch）|負責「攔截」所有流量，並向中央伺服器請求驗證|
|**Authentication Server**|通常是 RADIUS 伺服器|驗證用戶身份（比對帳密、憑證），授權或拒絕通訊|

🧩 驗證流程：

1. 使用者插上網線 → Supplicant 向交換機要求連線。
2. 交換機（Authenticator）阻擋流量，轉而詢問中央認證伺服器。
3. 認證伺服器（Authentication Server）查詢資料庫驗證。
4. 通過後，交換機開啟該埠口 → 用戶可正常上網。

### 💡簡單比喻：

想像每個網路插孔都是一個「門」，802.1X 就像在每扇門前加裝門禁卡讀取器。  
沒有通過驗證的人，就算插上線也進不去公司內網。

# 中間人攻擊（Man-in-the-Middle Attack, MITM）
這四張圖解釋的是「**中間人攻擊（Man-in-the-Middle Attack, MITM）**」中常見的手法之一 —— **ARP Spoofing / ARP Poisoning（ARP 欺騙）**。以下是步驟說明與概念解析 👇

---

### 🧩 1️⃣ 正常情況（圖1）

- **ARP Cache（ARP快取）**：主機會記錄 IP ↔ MAC（EUI-48） 的對應表，用來決定封包要發送到哪個網卡。
    
- **Victim（受害者）** 的 ARP 表中記錄：
    
    ```
    IP 1.2.3.4  →  MAC AA-BB-CC-DD-EE（Router）
    ```
    
    所以它知道要傳資料給路由器（預設閘道）。
    

---

### 🧩 2️⃣ 攻擊發生（圖2）

- 攻擊者假裝自己是 Router，發送假的 ARP Reply：
    
    ```
    IP 1.2.3.4 is at MAC FF-FF-FF-DD-DD-DD
    ```
    
- **Victim 的 ARP Cache 被污染（Poisoned）**，以為：
    
    ```
    IP 1.2.3.4  →  MAC FF-FF-FF-DD-DD-DD（攻擊者）
    ```
    

---

### 🧩 3️⃣ 攻擊進行中（圖3）

- Victim 想發封包給 Router（IP 1.2.3.4），但因為 ARP Cache 錯誤，  
    → 封包實際被送到 **攻擊者（Attacker）**。
    

---

### 🧩 4️⃣ 攻擊結果（圖4）

- 攻擊者取得封包後，可以選擇：
    
    - 偷看（Eavesdrop）
    - 修改封包再轉發（真正的 MITM）
    - 或直接丟棄（Denial of Service）
        
- 結果：  
    Victim 以為資料送到 Router，實際上是先經過攻擊者。
    

---

### ⚙️ 關鍵概念整理

|名稱|說明|
|---|---|
|**ARP（Address Resolution Protocol）**|負責將 IP 轉換成 MAC 地址，讓乙太網路能定位目標主機。|
|**ARP Cache Poisoning**|攻擊者用偽造的 ARP 回應修改受害者的 ARP 表。|
|**MITM 攻擊**|攻擊者夾在雙方之間竊聽或篡改資料。|

### 🧠 防禦方式

1. 啟用 **Dynamic ARP Inspection（DAI）**  
    → 僅允許合法的 IP-MAC 對應通過。
2. 使用 **靜態 ARP 表**（Static ARP）  
    → 不讓主機隨意更新 ARP 對應。
3. 透過 **加密協定（HTTPS, SSH, VPN）**  
    → 即使流量被攔截，也無法輕易解讀。
