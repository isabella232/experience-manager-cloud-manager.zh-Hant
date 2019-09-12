---
title: 瞭解您的測試結果
seo-title: 瞭解您的測試結果
description: 'null'
seo-description: 在執行管道、程式碼掃描、效能和安全性測試(在Cloud Manager中驗證程式)時，請遵循此頁面來瞭解三層式閘門。
uuid: 93caa01f-0df2-4a6f-81dc-23dve24dc93
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 使用
discoiquuid: 83299ed8-4b7a-4b1c-bd56-1bc7 e7318 d4
translation-type: tm+mt
source-git-commit: 26014cfabfee6226033ba2fc1167d8f5509e17c6

---


# 瞭解您的測試結果 {#understand-your-test-results}

**在「管道」** 程序中，會擷取許多度量，並與業務擁有者定義的關鍵績效指標(KPI)或Adobe Managed Services設定的標準比較。

這會使用本節中定義的三層式定位系統來報告。

## 執行管道時的三層式關卡 {#three-tier-gates-while-running-a-pipeline}

管線中有三個閘門：

* 程式碼品質
* 效能測試
* 安全性測試

對於上述每個關卡，關卡識別的問題有三層式結構。

* **重要** -這些是閘道識別的問題，造成管線立即失敗。
* **重要** -這些是閘道識別的問題，會導致管線進入暫停狀態。部署管理員、專案經理或業務擁有者可以覆寫問題，在此情況下，管線會發展，或者他們可以接受問題，此時管線會停止發生。
* **資訊** -這些是依關卡識別的問題，僅供資訊用途使用，不影響管線執行。

>[!NOTE]
>
>在「僅限程式碼品質的管道」中，「程式碼品質測試」門中的重要失敗無法被覆寫，因為「程式碼品質測試」步驟是管線中最後一個步驟。

## 程式碼品質測試 {#code-quality-testing}

作為管道的一部分掃描原始碼，以確保部署符合特定品質標準。目前，這是由Sonarque的組合以及使用OAKCAR的內容套件層級檢查所實施。有超過100種規則結合了一般Java規則和AEM專用規則。下表總結測試准則的分級：

| 名稱 | 定義 | 類別 | 失敗臨界值 |
|--- |--- |--- |--- |
| 安全性分級 | A=0弱點 <br/>B=至少次要弱點<br/> C=至少個重大弱點 <br/>D=至少個重大弱點 <br/>E=至少個封鎖程式弱點 | 重要事項 | &lt; B |
| 可靠性分級 | A=錯誤 <br/>B=至少次要錯誤 <br/>C=至少個主要錯誤 <br/>D=至少個重要錯誤E=至少個封鎖程式錯誤 | 重要事項 | &lt; C |
| 維護能力分級 | 程式碼閃現的顯著修補成本為： <br/><ul><li>&lt;=5%的時間已進入應用程式，評分為A </li><li>到10%之間，評分為B </li><li>在11到20%之間評分為C </li><li>到50%之間，評分為D</li><li>超過50%是一個E</li></ul> | 重要事項 | &lt; A |
| 適用範圍 | 使用此公式組合單元測試列涵蓋範圍和條件涵蓋範圍： <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`<br/>其中：CT=條件，在執行單元測試中至少評估過一次'true'時至少一次，執行單元測試 <br/>CF=條件在執行單元測試 <br/>LC=已涵蓋行=行_ to_封面- uncover_ line <br/><br/> B=總可執行行數 <br/>總計EL=總可執行行數(line_ to_ cover) | 重要事項 | &lt; 50% |
| 跳過的單元測試 | 跳過的單元測試數。 | 資訊 | &gt; 1 |
| 開放問題 | 整體問題類型-弱點、錯誤和程式碼精靈 | 資訊 | &gt; 1 |
| 複製的線條 | 重復區塊的相關行數。<br/>要將程式碼區塊視為重復的區塊： <br/><ul><li>**非Java專案：**</li><li>應至少有100個連續和重復的Token。</li><li>這些Token至少應被發送至： </li><li>COBOLE的30行程式碼 </li><li>ABAP20行程式碼 </li><li>其他語言10行程式碼</li><li>**Java專案：**</li><li> 無論預付碼和行數為何，至少應有10個連續和重復的陳述式。</li></ul> <br/>在偵測重復時，忽略縮排以及字串字詞的差異。 | 資訊 | &gt; 1% |


>[!NOTE]
>
>如需詳細定義，請參閱 [度量定義](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) 。

您可以在此處 [下載規則清單](/help/using/assets/CodeQuality-Rules-new.xlsx)

>[!NOTE]
>
>若要進一步瞭解自訂代碼品質規則， [!UICONTROL Cloud Manager]請參閱 [自訂代碼品質規則](custom-code-quality-rules.md)。

### 處理虛假問題 {#dealing-with-false-positives}

品質的掃描程序不完美，有時會不正確地識別問題並不會造成問題。這稱為「false正面」。

在這些情況下，來源程式碼可加上標準Java `@SuppressWarnings` 備注，以指定規則ID做為註解屬性。例如，一個常見問題是，Sonarque規則可偵測硬式編碼密碼，對於如何識別硬式編碼密碼很有可能。

若要查看特定範例，此程式碼在AEM專案中會相當常見，因為AEM專案具有連線至某些外部服務的程式碼：

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQue接著會增加封鎖程式弱點。檢視程式碼後，您可識別此弱點並可使用適當的規則ID予以註解。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但另一方面，如果程式碼實際上是如此：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然後正確的解決方案就是移除硬式編碼密碼。

>[!NOTE]
>
>雖然這是最好讓 `@SuppressWarnings` 註解盡可能具體的作法，不過，例如僅註解特定陳述式或封鎖造成問題的特定陳述式或區塊，以便在類別層級中註解。

## 安全性測試 {#security-testing}

[!UICONTROL Cloud Manager] 在部署後執行現有 ***的AEM Security Heats檢查*** 階段，並透過UI報告狀態。結果會從環境中的所有AEM實例匯總。

如果有任何 **「例項** 」回報特定健康狀態檢查失敗， **則整個環境** 會失敗，無法正常運作。如同「程式碼品質」和「效能測試」，這些健康狀態檢查會組織成類別並使用三層式定位系統報告。唯一的區別在於，安全測試不會有臨界值。所有健康檢查都只是通過或失敗。

下表列出目前檢查：

| **名稱** | **Health Check Implementation** | **類別** |
|---|---|---|
| 還原序列化防火牆附加API就緒狀態已可接受 | 還原序列化防火牆附加 API 整備 | 重要事項 |
| 還原序列化防火牆功能 | 還原序列化防火牆已作用 | 重要事項 |
| 還原序列化防火牆已載入 | 還原序列化防火牆已載入 | 重要事項 |
| AuthorizableNodeName實作不會在節點名稱/路徑中公開可授權ID。 | 可授權節點名稱產生 | 重要事項 |
| 預設密碼已變更 | 預設登入帳戶 | 重要事項 |
| Sling default GET servlet受DOS攻擊保護。 | Sling Get Servlet | 重要事項 |
| Dispatcher已正確篩選請求 | CQ Dispatcher 組態 | 重要事項 |
| 已適當設定Sling Java Script Handler | Sling Java 指令碼處理常式 | 重要事項 |
| 已適當設定Sling JSP Script Handler | Sling JSP Script Handler | 重要事項 |
| SSL設定正確 | SSL 設定 | 重要事項 |
| 找不到明顯不安全的使用者個人資料政策 | 使用者設定檔預設存取 | 重要事項 |
| Sling Referrer Filter is configured in order to防止CSRF攻擊 | Sling 查閱者篩選 | 重要事項 |
| 已適當設定Adobe Granite HTML Library Manager | CQ HTML 文件庫管理員組態 | 重要事項 |
| 已停用CRXDE支援套裝 | CRXDE 支援 | 重要事項 |
| 停用Sling DavEx搭售和servlet | DavEx 健康狀態檢查 | 重要事項 |
| 未安裝範例內容 | 範例內容封裝 | 重要事項 |
| WCM Request Filter和WCM Debug Filter都已停用 | WCM 篩選設定 | 重要事項 |
| 適當設定Sling WebDAV套裝和servlet | WebDAV 健康狀態檢查 | 重要事項 |
| Web伺服器設定為防止clickjacking | Web 伺服器組態 | 重要事項 |
| Replication is not using the'admin'user | 複寫及傳輸使用者 | 資訊 |

## 效能測試 {#performance-testing}

*效能測試* 是 [!UICONTROL Cloud Manager] 使用30分鐘測試實施。

在管線設定期間，部署管理員可決定導向至每個貯體的流量。

您可以從 [設定您的CI/CD管線，進一步瞭解貯體控制項](configuring-pipeline.md)。

>[!NOTE]
>
>若要設定程式並定義KPI，請參閱 [設定您的程式](setting-up-program.md)。

下表總結使用三層式定位系統的效能測試矩陣：

| **量度** | **類別** | **失敗臨界值** |
|---|---|---|
| 頁面請求錯誤率% | 重要事項 | &gt;= 2% |
| CPU使用率 | 重要事項 | &gt;= 80% |
| Disk IO等候時間 | 重要事項 | &gt;= 50% |
| 95個百分點回應時間 | 重要事項 | &gt;=方案層級KPI |
| 峰值回應時間 | 重要事項 | &gt;=18秒 |
| 每分鐘頁面檢視次數 | 重要事項 | &lt; Program-level KPI |
| 磁碟頻寬使用率 | 重要事項 | &gt;= 90% |
| 網路頻寬使用率 | 重要事項 | &gt;= 90% |
| 每分鐘要求 | 資訊 | &lt; 6000 |

### 效能測試結果圖表 {#performance-testing-results-graphs}

新增圖形和下載選項至「效能測試結果」對話方塊。

當您開啓「效能測試」對話方塊時，量度面板可以展開以顯示圖形、提供下載連結或兩者。

[!UICONTROL Cloud Manager] 針對2018.7.0版，此功能適用於下列度量：

* **CPU使用率**
   * 測試期間的CPU使用量圖表。

* **磁碟I/等候時間**
   * 測試期間的Disk I/O等候時間圖表。

* **頁面錯誤率**
   * 測試期間內每分鐘的頁面錯誤圖表。
   * 在測試期間產生錯誤的CSV檔案清單頁面。

* **磁碟頻寬使用率**
   * 測試期間的磁碟頻寬使用率圖表。

* **網路頻寬使用率**
   * 測試期間的網路頻寬使用率圖表。

* **峰值回應時間**
   * 測試期間每分鐘的峰值回應時間圖表。

* **第95個百分點的回應時間**
   * 測試期間內每分鐘的第95個百分位數回應時間圖表。
   * 列出第95個百分位數回應時間超過定義KPI的CSV檔案頁面。

下列影像會顯示效能測試圖表：

![](assets/understand_test-results-screen1.png)

![](assets/screen_shot_2018-09-05at83933pm.png)

