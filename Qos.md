這題主要根據 **Ch04_Network and Security Management.pdf** 說明。

---

## 🧩 一、QoS（Quality of Service，服務品質）

**定義：**
QoS 是一組用來**保證網路效能**的機制與指標，確保特定應用（如語音、影音、交易系統）在網路壅塞時仍能獲得穩定的服務。

課本中指出：

> QoS 是針對速度、延遲、抖動、可用性等網路表現提供「**可量化保證**」的機制。
> 若未達標準，網路服務提供者需承擔**懲罰性條款**（penalty）。

QoS 的常見指標包含：

* **Latency（延遲）**
* **Jitter（抖動）**
* **Throughput（吞吐量）**
* **Availability（可用性）**

---

## ⏱️ 二、Latency（延遲）

* 指**封包從來源傳到目的地的時間**。
* 單位通常是毫秒（ms）。
* 例如：50 ms latency 表示訊息往返需 0.05 秒。
* 延遲越高，互動應用（如語音、遊戲）會出現明顯延時。

---

## 🔄 三、Jitter（抖動）

* 定義：**封包延遲的變化量**，即「延遲不穩定度」。
* 高 jitter 表示每個封包到達時間差異大，導致語音或影像不連貫。
* 低 jitter 表示封包到達時間穩定，播放流暢。

課本原文：

> “Jitter is variability in latency. Makes voice and video seem ‘jittery’.”

🔹 **High jitter** → 影片卡頓、聲音斷續
🔹 **Low jitter** → 延遲穩定、品質良好

---

## 📊 四、Aggregate Throughput（總吞吐量）

* **Aggregate throughput** 是網路整體的**總資料傳輸速率**，即「全部使用者共享的總帶寬」。
* **Individual throughput** 則是個別使用者分到的實際速率。

課本舉例：

> 若 AP 標示 300 Mbps、實際 throughput 僅 50%，5 人同時上傳下載，
> 則每人約分得 30 Mbps。

---

## 📜 五、SLA（Service Level Agreement，服務等級協定）

**定義：**
SLA 是網路服務供應商（ISP）與客戶間簽訂的**正式合約**，明確列出：

* 最低效能標準（如：99.99% uptime、latency 不高於 50 ms）
* 檢測與報告方式
* 未達標時的罰則（penalty）

課本說明：

> “SLAs specify worst cases (minimum performance to be tolerated)… Penalties if worse than the specified performance.”

範例：

* latency ≤ 50 ms (99.99% 時間)
* jitter ≤ 2% variation
* availability ≥ 99.99%

---

## 🔗 六、QoS 與 SLA 的關聯性

| 項目      | 說明                                |
| ------- | --------------------------------- |
| **QoS** | 技術層面的「服務品質控制與量測」機制。確保流量分級（如語音優先）。 |
| **SLA** | 法律／合約層面的「服務品質保證」。用 QoS 的指標來定義。    |
| **關聯性** | SLA 是對外承諾，QoS 是達成 SLA 的技術手段。      |

📘簡言之：

> **QoS 是方法，SLA 是承諾。**
> QoS 實作（如流量管理、優先權排程）確保網路表現達到 SLA 規定的數值。

---

✅ **總結重點表**

| 名稱                   | 中文     | 意義                  | 檔案來源        |
| -------------------- | ------ | ------------------- | ----------- |
| QoS                  | 服務品質   | 控制延遲、抖動、速度與可用性的網路機制 | Ch04 p.9–14 |
| Latency              | 延遲     | 封包傳遞時間              | 同上          |
| Jitter               | 抖動     | 延遲不穩定程度             | 同上          |
| Aggregate Throughput | 總吞吐量   | 所有使用者共享的總資料速率       | 同上          |
| SLA                  | 服務等級協定 | 對 QoS 指標的合約式保證      | 同上          |
| QoS 與 SLA 關係         | —      | QoS 為實現 SLA 的技術依據   | 同上          |
