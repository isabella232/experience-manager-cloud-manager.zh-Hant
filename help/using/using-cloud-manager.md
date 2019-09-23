---
title: 使用Cloud Manager
seo-title: 使用Adobe AEM Cloud Manager
description: AEM Cloud manager使用者介面已說明
seo-description: Adobe AEM Cloud manager使用者介面已說明
page-status-flag: 從未激活
uuid: cef44d35-75ed-44bb-9636-2de2bca5e458
contentOwner: jsyal
discoiquuid: c37566d5-0d1b-4c44-abd7-b271ea443c1a
translation-type: tm+mt
source-git-commit: 4c1c6786db9b8972f9315bd2f12fc1752881492f

---


# 使用Cloud Manager{#using-cloud-manager}

本節說明的使用者介面(UI)，並說 [!UICONTROL Cloud Manager] 明從設定程式到程式碼部署的工作流程，接著是品質檢查。

## 必備條件 {#prerequisites}

在您瞭解使用的詳細資訊之 [!UICONTROL Cloud Manager]前，建議您先執行下列章節：

* [使用[!UICONTROL Cloud Manager]之前瞭解概念](understanding-concepts.md)
* [為[!UICONTROL Cloud Manager]設定常規配置](setting-configurations-for-cloud-manager.md)

## 開始使用 [!UICONTROL Cloud Manager]{#getting-started-with-cloud-manager}

在為設定常規配置後， [!UICONTROL Cloud Manager]您就可以使用 [!UICONTROL Cloud Manager]。

1. 登入Adobe，您 [!UICONTROL Experience Cloud] 就會看到解決方案清單。

   ![](assets/screen_shot_2018-04-22at92951am.png)

1. 選擇程式並按一下左上角表徵圖以開啟 [!UICONTROL Cloud Manager]。

   ![](assets/screen_shot_2018-04-22at93346am.png)

## 設定程式 {#setting-up-program}

上線後，企業負責人需要先設定程式。 這包括設定方案說明，以及定義將用於效能測試的KPI。 您也可以選擇上傳縮圖。

定義的KPI用作每次流水線執行時傳遞的效能測試基準。

>[!NOTE]
>
>定義的KPI是根據在舞台環境上執行的測 **試來測** 量。 通常，這些KPI會縮小以符合舞台環境的功能。
>
>例如，在生產環境中，平均每分鐘需要1000次頁面檢視，而在生產環境中有4個伺服器的使用者，應將此值調整為每分鐘250次頁面檢視(假設其階段環境僅包含單一伺服器 `dispatcher/publish``dispatcher/publish` 對)。
>
>此外，許多使用者在其製作環境前會有CDN(Akamai、CloudFront)。 由於 [!UICONTROL Cloud Manager] 直接針對階段環境進行測試，因此KPI應僅反映預期要透過CDN的流量，即快取未命中。 通常，這是生產流量總量中相對較小的子集。

### 使用 [!UICONTROL Cloud Manager] 定義KPI {#using-cloud-manager-to-define-kpis}

請依照下列步驟設定方案並定義KPI:

1. 按一下 **Setup Program** （設定程式）以在中啟動設定過程 [!UICONTROL Cloud Manager]。
1. 將顯 **示「編輯程式資訊** 」螢幕。

   將縮圖上傳至您的程式。 您也可以將相關說明新增至您的程式，然後按一下「下 **一步**」。

1. 將顯 **示「配置用戶** 」螢幕。

   您可以設定您的團隊角色和使用者。 按一 **下「下一步**」。

1. 此時將 **顯示「配置一般業務KPI** 」螢幕。

   您可以定義您的兩個KPI（每個部署的預期值）:

   1. 您可以接受的第95個百分位數回應時間是多少？

      1. 建議值- 3秒
   1. 在高峰負載下，每分鐘頁面檢視次數是多少？

      1. 建議值- 200 pv/m


1. 按一 **下提交** ，完成設定精靈。

   您將會看到變更為「部 [!UICONTROL Cloud Manager] 署」的 **主畫面**。

## 可用環境 {#available-environments}

The **Available Environments** in [!UICONTROL Cloud Manager] the Lists the all the managed AEM environments.

每個列出的環境都將具有與其關聯的狀態。

## 配置管線 {#configuring-pipeline}

### 設定管線 {#setting-up-pipeline}

>[!CAUTION]
>
>在git儲存庫至少有一個分支之前，無法設定管線。

開始部署代碼之前，必須從中配置管線設定 [!UICONTROL Cloud Manager]。

要瞭解有關管線配置的更多資訊，請參 **閱**使用[!UICONTROL Cloud Manager]**[](understanding-concepts.md)**中的「瞭解概念」一節。

>[!NOTE]
>
>可在初始設定後更改管線設定。

### 從中配置管線設定 [!UICONTROL Cloud Manager]{#configuring-pipeline-settings-from-the-cloud-manager}

請遵循下列中的步 [!UICONTROL Cloud Manager] 驟，為管線配置行為和首選項：

1. 訪問「 **Branch** 」（分支）頁籤以設定應用程式分支。

   選擇要設定的git分支。

   >[!NOTE]
   >
   >在Git儲存庫中找到的分支會連結至您的程式。

   ![](assets/screen_shot_2018-05-06at73604pm.png)

1. 存取「 **環境** 」標籤以選 **擇「舞台** 」 **和「生產** 」選項。

   可以定義將啟動管線的觸發器：

   * **手動** -必須有人在UI中手動按一下才能啟動管線。
   現在，您可以定義控制生產部署的參數。 三種可用選項如下：

   * **使用上線核准**-部署必須由業務擁有者、專案經理或部署經理透過 [!UICONTROL Cloud Manager] UI手動核准。
   * **使用CSE監督** -參與CSE以實際開始部署。
   ![](assets/screen_shot_2018-05-06at73715pm.png)

1. 存取「 **測試** 」標籤，以定義您方案的測試准則。

   現在，您可以設定效能測試參數。

   ![](assets/screen_shot_2018-05-06at73750pm.png)

## 部署程式碼 {#deploying-code}

配置了管線（儲存庫、環境和測試環境）後，您就可以部署代碼。

### 從部署程式 [!UICONTROL Cloud Manager] 碼 {#deploying-code-from-cloud-manager}

請依照下列步驟，將程式碼部署至生產環境：

1. 從中 **按一下** 「部 [!UICONTROL Cloud Manager] 署」以啟動部署過程。
1. 將顯 **示「舞台部署** 」螢幕。

   按一下 **Build** （生成）啟動進程。

1. 完整的建立程式會考慮數個參數，以檢查和部署您的程式碼。

   下列檢查的參數如下：

   **階段部署**

   * 存放庫
   * 單元測試
   * 程式碼掃描
   * 部署到舞台環境
   **預製測試**

   * 安全性測試
   * 效能測試
   >[!NOTE]
   >
   >此外，您也可以檢視上述測試准則的記錄檔或檢閱結果。

## 質量檢查的結果 {#results-from-quality-checks}

目前有三扇門正在醖釀之中：程式碼品質、效能測試和安全性測試。

對於每個門，門都有三層結構來解決由門所識別的問題。

* **Critical** —— 這些問題由門確定，導致管線立即出現故障。
* **重要** -這些是閘道識別的問題，導致管線進入暫停狀態。 部署經理、專案經理或業務負責人可以覆寫問題（在這種情況下，管道會繼續），或者接受問題（在這種情況下，管道會因故障而停止）。
* **Info** —— 這些問題由門確定，僅供參考，對管線執行沒有影響。

### 程式碼掃描 {#code-scanning}

![](assets/screen_shot_2018-04-22at101443am.png)

### 效能測試 {#performance-testing}

*中的效能測試* , [!UICONTROL Cloud Manager] 是使用30分鐘的測試來實作的。

在管線設定期間，部署管理員可決定要將多少流量導引至每個儲存貯體。 他們可以選擇從1到3個桶的任意位置。 流量的分配是根據選擇的時段數，即如果全部選擇三個時段，則33%的頁面檢視總數會放入每個時段；如果選取2個，則每組50%;如果選取其中一個，則100%的流量會移至該集合。

例如，假設「熱門即時頁面」和「新頁面」集（在此範例中，未使用其他即時頁面）之間有50%/50%的分割，而「新頁面」集包含3000個頁面。 每分鐘頁面檢視次數KPI設定為200。 在30分鐘的測試期間：

* 「熱門即時頁面」集的25個頁面中，每個頁面都會點擊240次- `((200 &#42; 0.5) / 25) &#42; 30 = 120`
* 「新頁面」集中的3000個頁面，每個頁面都會點擊一次- `((200 &#42; 0.5) / 3000) &#42; 30 = 1`

![](assets/image2018-3-14_16-23-56.png)

### 效能測試度量 {#performance-test-metrics}

在測試期間，會擷取許多量度，並與由業務擁有者定義的KPI或AMS設定的標準進行比較。

這些是使用三層式選通系統來報告的，如下所示：

### 運行管道時的三層門 {#three-tier-gates-while-running-a-pipeline}

程式碼品質、效能測試和安全性測試是管道中的三道門。

對於每個門，門所標識的問題都有三層結構：

* **重要**:這些是由澆口確定的問題，導致管線立即失效。
* **重要**:這些是由門所標識的導致管線進入暫停狀態的問題。 部署經理、專案經理或業務負責人可以覆寫問題（在這種情況下，管道會繼續），或者接受問題（在這種情況下，管道會因故障而停止）。
* **資訊**:這些是由門所標識的問題，這些問題僅供提供資訊之用，對管線執行沒有影響。

下表總結了使用三層門控系統的效能測試矩陣：

| **量度** | **類別** | **故障閾值** |
|---|---|---|
| 頁面請求錯誤率% | 關鍵 | &gt;= 2% |
| CPU使用率 | 關鍵 | &gt;= 80% |
| 磁碟IO等待時間 | 關鍵 | &gt;= 50% |
| 95百分位數回應時間 | 重要 | &gt;=方案層級KPI |
| 峰值響應時間 | 重要 | &gt;= 18秒 |
| 每分鐘頁面檢視次數 | 重要 | &lt;方案層級KPI |
| 磁碟頻寬利用率 | 重要 | &gt;= 90% |
| 網路頻寬利用率 | 重要 | &gt;= 90% |
| 每分鐘請求數 | 資訊 | &lt; 6000 |

### 安全性測試 {#security-testing}

[!UICONTROL Cloud Manager] 在部署後 *的舞台上執行現有的AEM Security Heath* Checks，並透過UI報告其狀態。 結果會從環境中的所有AEM例項匯總。

如果任一實例報告給定運行狀況檢查的失敗，則整個環境將失敗該運行狀況檢查。 如同程式碼品質與效能測試，這些健康狀況檢查會組織成類別，並使用三層式選通系統來報告。 唯一的區別是，在安全測試中沒有閾值。 所有健康檢查都只是通過或失敗。

當前檢查包括：

| **運行狀況檢查** | **類別** |
|---|---|
| 還原序列化防火牆附加 API 整備 | 關鍵 |
| 還原序列化防火牆已作用 | 關鍵 |
| 還原序列化防火牆已載入 | 關鍵 |
| 可授權節點名稱產生 | 關鍵 |
| 預設登入帳戶 | 關鍵 |
| Sling Get Servlet | 關鍵 |
| CQ Dispatcher 組態 | 關鍵 |
| CQ HTML 文件庫管理員組態 | 關鍵 |
| Sling Java 指令碼處理常式 | 關鍵 |
| Sling Jsp 指令碼處理常式 | 關鍵 |
| Sling 查閱者篩選 | 關鍵 |
| SSL 設定 | 關鍵 |
| 使用者設定檔預設存取 | 關鍵 |
| CRXDE 支援 | 重要 |
| DavEx 健康狀態檢查 | 重要 |
| 範例內容封裝 | 重要 |
| WCM 篩選設定 | 重要 |
| WebDAV 健康狀態檢查 | 重要 |
| Web 伺服器組態 | 重要 |
| 複寫及傳輸使用者 | 資訊 |

### SonarQube實現質量檢查 {#quality-check-implementation-by-sonarqube}

如上所述，作為管線的一部分，將掃描代碼。 目前，這是由SonarQube公司實施的。 我們有93個規則，是通用Java規則與AEM特定規則的組合（包括Cognifide現有規則集中的部分）。 這些規則的清單可在以下網址找到： [code-quality-rules.xlsx](/help/using/assets/code-quality-rules.xlsx)

從這些規則中，會計算各種度量，其中一些度量會在允許部署至舞台環境之前用作品質閘道。

以下是目前的臨界值：

| 名稱 | 定義 | 類別 | 故障閾值 |
|--- |--- |--- |--- |
| 安全性分級 | A = 0漏洞 <br/>B =至少1個小漏洞<br/> C =至少1個大漏洞 <br/>D =至少1個嚴重漏洞 <br/>E =至少1個攔截器漏洞 | 關鍵 | &lt; B |
| 可靠性分級 | A = 0錯誤 <br/>B =至少1個次要錯誤 <br/>C =至少1個主要錯誤 <br/>D =至少1個嚴重錯誤E =至少1個攔截器錯誤 | 重要 | &lt; C |
| 可維護性評級 | 代碼氣味的未付補救成本是： <br/><ul><li>&lt;=5%已進入應用程式的時間，評分為A </li><li>6%到10%的評分是B </li><li>11%到20%的評分是C </li><li>21%到50%的評分是D</li><li>超過50%的項目是E</li></ul> | 重要 | &lt; A |
| 適用範圍 | 使用此公式混合行覆蓋和條件覆蓋：其 <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`<br/>中：CT =已評估為「true」的條件，至少一次 <br/>CF =已評估為「false」的條件，至少一次 <br/>LC =覆蓋行= lines_to_cover - uncovered_lines <br/><br/> B =條件 <br/>EL =可執行行(lines_to_cover)的總數 | 重要 | &lt; 50% |
| 跳過的設備測試 | 跳過的單元測試數。 | 資訊 | &gt; 1 |
| 未結問題 | 整體問題類型——弱點、錯誤和程式碼氣味 | 資訊 | &gt; 1 |
| 複製行 | 重複塊中涉及的行數。 <br/>對於要視為複製的代碼塊： <ul><li> **非Java專案：**</li><li>至少應有100個連續和重複的Token。</li><li>這些預付碼應至少分散於： </li><li>COBOL的30行代碼 </li><li>ABAP的20行代碼 </li><li>10行其他語言的程式碼</li></ul><ul><li>**Java專案：**</li><li> 不論預付碼和行數為何，至少應有10個連續和重複的陳述式。</li></ul>在檢測重複時，會忽略縮排和字串文字的差異。 | 資訊 | &gt; 1% |

### 誤報 {#false-positives}

品質掃描程式不完善，有時會錯誤地識別實際上沒有問題的問題。 這稱為假 *陽性* (雖然 ** 假陰性可能在語義上更正)。 在這些情況下，原始碼可以用標準Java注釋加以注 `@SuppressWarnings` 釋，該標準Java注釋指定規則ID作為注釋屬性。 例如，一個常見問題是，用於檢測硬編碼密碼的SonarQube規則對於硬編碼密碼非常開明。

若要檢視特定範例，此程式碼在AEM專案中相當常見，該專案具有連接至某些外部服務的程式碼：

```java
@Property(label = "Service Password")
private static final String SERVICE_PASSWORD = "password";
```

SonarQube會將此列為「封鎖程式弱點」。 在這種情況下，客戶可以識別這並非弱點，並使用適當的規則ID加以註解：

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String SERVICE_PASSWORD = "password";
```

但是，另一方面，如果代碼是：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String SERVICE_PASSWORD = "password";
```

然後，客戶應當牢記SonarQube的警告，刪除硬編碼密碼。 不過，由於SonarQube規則實際上是由術語觸發 `@SuppressWarnings` 的，因此他們仍需要添加註釋 `password`。

>[!NOTE]
>
>最好使注釋盡可能具體 `@SuppressWarnings` ，即僅注釋導致問題的特定語句或塊，可在類別級別注釋。

