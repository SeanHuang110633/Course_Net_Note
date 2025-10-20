# Traffic Shaping
## 🚦 Traffic Shaping（流量整形）的概念

### 📘 定義

**Traffic Shaping** 是一種 **控制網路流量速率與分配頻寬** 的技術，  
目的是讓網路維持穩定、避免**擁塞（congestion）**。

換句話說，它在流量進入網路（Traffic Access Point）之前，  
**限制、延遲或過濾部分流量**，確保主幹傳輸線不會超載。

---
## 🧩 一、目的：Congestion Prevention（預防網路擁塞）

### ✅ 傳統方法：
- **Over provisioning**：提高頻寬（但成本高）
- **Priority & QoS Reservation**：依流量優先權分配資源
### 🚫 問題：
這些方法主要在「應對擁塞」；而 **Traffic Shaping 是「預防擁塞」**。

---
## 🧩 二、運作方式（對應第一張圖）

### 1️⃣ 限制進入流量

Traffic Shaping 透過 **limiting incoming traffic** 來控制負載。
- **Desirable Traffic（合適流量）** → **Permitted**（允許通過）
- **Undesirable Traffic（不理想流量）** →
    - **Filtered Out（直接過濾掉）**
    - 或 **限速（Limited / Slowed）**，讓它佔用的頻寬不超過一定比例。

🟦 這樣能：
- 避免傳輸線過載
- 減少整體網路成本（因為不必要流量被過濾）
---

## 🧩 三、細節（對應第二張圖）

Traffic Shaping 可根據流量的性質做區分：
### ✴ 類別 1：完全阻擋的流量

> **“Some traffic can be banned and simply filtered out.”**

例如：  
垃圾郵件、P2P下載、DDoS 攻擊流量  
→ 被防火牆或路由器直接丟棄（filtered out）。

---
### ✴ 類別 2：部分限制的流量

> **“Other traffic has both legitimate and illegitimate uses.”**
例如：

- 雲端備份服務（合法但佔頻寬）
- YouTube、BT下載（娛樂用但消耗資源）

→ 系統會 **允許通過但限速**（limited to a percentage of total traffic）  
確保不影響主要業務流量（如 VoIP、公司伺服器流量）。

---

## 🧠 總結重點表格：

|類型|處理方式|範例|
|---|---|---|
|合法流量（Desirable）|允許通過|Web、Mail、業務應用|
|不良流量（Undesirable）|過濾或限速|P2P、Spam、惡意請求|
|雙用途流量（Legit + Illegit）|限制比例、降低速率|雲端同步、串流影片|

---

## ✅ 結論一句話（考試可用）：

> **Traffic Shaping 是一種透過過濾或限速不必要流量來防止網路擁塞的技術。**  
> 它能在不影響重要業務的前提下，降低頻寬負擔並維持網路穩定性。


# SNMP

### 🧩 SNMP 的基本概念

- SNMP 是一種標準協定，用於**收集網路設備狀態資訊**與**發送控制命令**。
    
- 它透過一種「**Manager-Agent 架構**」運作：
    
    - **SNMP Manager（管理者）**：通常是網管伺服器，用來發送請求、收集資料、分析網路狀況。
        
    - **SNMP Agent（代理端）**：部署在網路設備上，負責回應管理者的請求並提供設備資訊。
        
- 通訊主要透過 **UDP port 161（管理訊息）與 162（trap 警告）** 傳輸。
    

---

### ⚙️ SNMP 的運作方式

1. **Manager 向 Agent 發出請求**（如 `GET` 或 `SET` 命令）。
    
2. **Agent 回傳對應資料**（如設備狀態、介面流量、錯誤次數等）。
    
3. 當發生異常時（例如流量突增、設備故障），**Agent 會主動發送 Trap 訊息**給 Manager。
    

---

### 📊 管理資訊結構：MIB（Management Information Base）

- SNMP 透過 **MIB 資料庫** 來組織所有可監控的資訊。
- 每個可監控項目都有唯一的 **OID（Object Identifier）**，例如：

# SDN & Centralized Firewall Management
+ 有一個SDN Controller統一下管理
+ 同理Firewall Policy Server統一下發規則
