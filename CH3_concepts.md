# Human break-in
+ Scanning Phase Port scanning by probing ◦
+ The Break-In  exploit 
+ After the Break-In  Download hacker tool kit (Backdoor, Trojan horse, keystroke logger, etc).

# 常見的驗證方式
在教材中，Digital Certificate Authentication 以「**信任鏈（Trust Chain）＋非對稱加密**」為核心，比密碼、Token 或生物辨識更能同時達到 **Authentication（身分驗證）**、**Integrity（完整性）**、**Confidentiality（機密性）** 三大安全目標。

|驗證方式|驗證依據|安全性|常見攻擊|優點|缺點|
|---|---|---|---|---|---|
|**Password**|使用者記憶的密碼|低|釣魚、暴力破解、重放|簡單、成本低|易被竊取或重複使用|
|**Token**|臨時產生的代碼|中|裝置被竊、截取|一次性、減少重放攻擊|須額外設備或應用|
|**Biometric**|身體特徵|高|偽造樣本、隱私洩漏|使用方便、安全性高|成本高、不可更改|
|**Digital Certificate**|公私鑰＋CA信任鏈|**最高**|憑證被盜或過期|防偽造、防竄改、具信任性|架設成本高、需管理PKI|

### 🔒 **為何 Digital Certificate Authentication 較安全**

- 不依賴使用者記憶或輸入，私鑰永不離開裝置。
- 憑證經 **CA 簽章** 驗證，能防止偽造身分（spoofing）。
- 結合 **加密與完整性驗證**，確保資料不可竄改。
- 可與其他方法（如密碼或生物特徵）組合成 **多因素驗證（MFA）**。

# Stateful Inspection Firewall
這張圖（出自 **Ch03《Network Security》p.3-63**）說明的是「通訊狀態（States in a Conversation）」概念，主要在解釋 **狀態檢查型防火牆（Stateful Inspection Firewall）** 如何根據「連線狀態」來判斷資料包是否安全。

---

## 🧩 內容說明

### 1. Connection-Opening Attempt（連線開啟階段）

- 屬於 **Risky State（高風險狀態）**。
- 這時雙方尚未建立信任，必須進行嚴格的 **身份驗證（authentication）**。
- 攻擊者最常在這階段嘗試滲透，例如 TCP SYN flood 或假冒連線請求。
- 因此這階段的封包通常會被防火牆仔細檢查，例如 SYN 封包。

---

### 2. Ongoing Communication（持續通訊階段）

- 屬於 **Less Risky State（低風險狀態）**。
- 一旦連線建立完成（例如 TCP 三向交握後），雙方已經驗證過身分，後續封包只需較輕量檢查。
- 防火牆會將此連線記錄到 **「連線狀態表（State Table）」**，之後的封包只要符合該狀態即可快速通過。
### 🔐 與安全防護的關聯

| 阶段                    | 狀態風險 | 防火牆策略         | 例子            |
| --------------------- | ---- | ------------- | ------------- |
| Connection Opening    | 高    | 嚴格驗證、限制連線請求數量 | TCP SYN 檢查    |
| Ongoing Communication | 低    | 根據狀態表快速放行     | TCP 資料封包（ACK） |

# Next-Generation Firewall（NGFW）

## 🔹 一、Stateful Packet Inspection (SPI) 的限制

### ✴ SPI 的三大限制：

1. **僅檢查 socket-level 資料（port/IP 層級）**  
    → 只能看傳輸層（TCP/UDP），無法深入了解封包內的應用層內容。
2. **無法辨識實際應用程式**  
    → 例如所有 HTTP 流量都走 port 80，但 SPI 無法分辨這是正常網頁、惡意程式、還是 VPN。
3. **無法分析連續的封包流（streams）問題**  
    → 無法跨多個封包重組分析應用層行為，像 SQL injection 或分段攻擊就偵測不到。

---

### ✅ 解決方案：**Next-Generation Firewall (NGFW)**

- **採用 Deep Inspection（深度檢測）**：
    
    - 檢查網際網路層與傳輸層所有欄位；
    - 能深入解析 **應用層內容**；
    - 可重新組裝多個封包的應用層訊息再判斷。

➡️ 結論：NGFW = 傳統防火牆 + 深度封包檢測（DPI）

---

## 🔹 二、NGFW 的主要功能（Features）

### 🔸 1. **Application Awareness（應用程式辨識）**

- 能辨識是哪個應用程式產生流量。
- 可依應用程式自訂防火牆規則（例如只允許公司 Slack、不允許 Line）。
- 甚至能辨識惡意應用（如木馬或 P2P 程式）。

---

### 🔸 2. **IDS（入侵偵測系統）功能**

- **偵測並記錄可疑流量**（但不一定阻擋）。
    
- 通知安全管理員（例如疑似攻擊）。
- 缺點：可能產生過多誤報（false alarms）。

---

### 🔸 3. **IPS（入侵防禦系統）功能**

- 是加強版 IDS。
- 若確認攻擊風險高，會**主動丟棄可疑封包（drop packets）**。

---

### 🔸 4. **Reputation Management（信譽管理）**

- 透過 **白名單 / 黑名單（whitelist / blacklist）**，  
    檢查來源是否為惡意或高風險站點。
- 可結合外部信譽資料庫，自動更新阻擋策略。
    

---

### 🔸 5. **NAT 與 VPN Traversal**

- 支援傳統防火牆的基本功能（NAT 轉址）。
- 能讓 **加密 VPN 流量通過**，但由於內容加密，**無法進行深度檢查**。

---

## 🔹 三、Wire-Speed Operation（線速運作）

### ✴ 問題：
- Deep Inspection 對每個封包都做詳細分析，**處理量非常大**。
- 若速度太慢，會造成封包延遲或封鎖瓶頸。
### ✴ 解決方法：

- **傳統防火牆**：使用一般 CPU（general-purpose computer），速度慢。
- **NGFW**：採用 **專用硬體（purpose-built hardware）**，  
    在硬體層直接處理檢測工作，速度可達「**線速（wire-speed）**」，  
    即能在不降低傳輸速率的情況下完成檢測。

---

## ✅ 總結一句話：

> **NGFW 是 SPI 的升級版，具備深度檢測、應用辨識、入侵防禦、信譽管理與硬體加速等功能，能在不影響速度的情況下，提供更精確與全面的安全防護。**

# Signature Detection & Behavioral Detection

## 🧩 一、Signature Detection（特徵碼偵測）

### 🔹 概念

- 利用**惡意程式特徵碼（signature）**偵測病毒。
    
- 每種惡意軟體都有獨特的 **位元組模式（byte pattern）**，防毒軟體會在資料或程式中搜尋這些特徵碼來判斷是否感染。
    

### 🔹 缺點

1. **惡意程式數量過多**：  
    當前有數以百萬計的病毒，無法為所有惡意程式維護完整特徵庫。
    
2. **惡意程式會變種（mutate）**：  
    許多病毒會改變自己的碼（self-modifying）或混淆結構，使簽章（signature）失效。
    
### 🔹 小結

> 優點：快速、準確率高（對已知病毒）。  
> 缺點：無法偵測**未知（zero-day）或變種病毒**。

---

## 🧩 二、Behavioral Detection（行為偵測）

### 🔹 概念

- 不靠特徵碼，而是分析程式**正在嘗試做什麼（attempting to do）**。
    
- 例如：試圖重設硬碟、修改系統設定、建立自啟動項、連線可疑伺服器等行為。
    

### 🔹 方式

1. **監控程式行為** — 若發現可疑動作，立即警告或封鎖。
    
2. **在 Sandbox（沙箱）中執行** —  
    把可疑程式放入受控的隔離環境執行，觀察行為而不危及主系統。
    
3. **必要時刪除程式** — 若行為明確惡意，系統會直接移除。
    

### 🔹 優點與缺點

|優點|缺點|
|---|---|
|能偵測未知或變種病毒|可能誤報正常程式|
|不依賴簽章資料庫|需要較高資源與分析時間|

---

## ✅ 總結比較

|偵測方式|偵測依據|能偵測未知病毒|是否需更新簽章|範例|
|---|---|---|---|---|
|**Signature Detection**|已知惡意程式的 byte pattern|❌ 否|✅ 是|傳統防毒引擎|
|**Behavioral Detection**|程式行為（例如修改系統、異常存取）|✅ 是|❌ 否|沙箱分析系統|

---

📘 **出處：**  
《114-9 Ch03 Network Security.pdf》p.3-77～3-78 (Antivirus Protection – Signature Detection & Behavioral Detection)
