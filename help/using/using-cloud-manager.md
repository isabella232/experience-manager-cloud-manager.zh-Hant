---
title: 使用Cloud Manager
seo-title: 使用Adobe AEM Cloud Manager
description: AEM Cloud Manager使用者介面說明
seo-description: Adobe AEM Cloud Manager使用者介面說明
page-status-flag: 從未啓動
uuid: cf44d35-75ed-44bb-9636-2de2bca5e458
contentOwner: jsyal
discoiquuid: c37566d-5d1b-4c44-abd7-b271 ea443 c1 a
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 使用Cloud Manager{#using-cloud-manager}

本節說明使用者介面(UI)， [!UICONTROL Cloud Manager] 並說明從設定程式到程式碼部署，以及品質檢查後的工作流程。

## 必備條件 {#prerequisites}

在您深入瞭解使用情況 [!UICONTROL Cloud Manager]之前，建議您執行下列章節：

* [使用[！UICOHTROL Cloud Manager]](understanding-concepts.md)
* [設定[！UICOHTROL Cloud Manager]](setting-configurations-for-cloud-manager.md)

## 開始使用 [!UICONTROL Cloud Manager]{#getting-started-with-cloud-manager}

設定一般組態後，您 [!UICONTROL Cloud Manager]就可以使用 [!UICONTROL Cloud Manager]。

1. 登入Adobe，您 [!UICONTROL Experience Cloud] 就會看到解決方案清單。

   ![](assets/screen_shot_2018-04-22at92951am.png)

1. 選取程式，然後按一下左上角圖示開啓 [!UICONTROL Cloud Manager]。

   ![](assets/screen_shot_2018-04-22at93346am.png)

## 設定程式 {#setting-up-program}

在登入後，商業擁有者將需要進行一些初始設定。這包括設定程式描述並定義將用於效能測試的KPI。或者，也可以上傳縮圖。

定義的KPI作為效能測試的基準，在每次管線執行時傳遞。

>[!NOTE]
>
>在測試上測量的KPI會在 **測試環境** 上執行。通常這些KPI會縮小，以符合舞台環境的功能。
>
>例如，使用者在生產環境中平均每分鐘檢視1000次頁面檢視，並在生產環境中有個 `dispatcher/publish` 伺服器，則每分鐘的頁面檢視次數應會增加到250次(假設他們的舞台環境只包含 `dispatcher/publish` 單一伺服器配對)。
>
>此外，許多使用者在生產環境前面都有CDN(Akamai、CloudFront)。由於 [!UICONTROL Cloud Manager] 直接對舞台環境進行測試，KPI應只反映傳遞CDN的流量，即快取錯誤。通常這會是總生產流量的相對小部分。

### 用來 [!UICONTROL Cloud Manager] 定義KPI {#using-cloud-manager-to-define-kpis}

請依照下列步驟來設定程式並定義KPI：

1. 按一下 **「設定程式** 」以開始設定程序 [!UICONTROL Cloud Manager]。
1. 隨即顯示 **「編輯計劃資訊** 」畫面。

   將縮圖上傳至您的程式。您也可以新增相關說明至程式，然後按「下一步 **」**。

1. 隨即顯示 **「設定使用者** 」畫面。

   您可以設定團隊角色和使用者。按一下 **「下一步**」。

1. 隨即顯示 **「設定一般業務KPI** 」畫面。

   您可以定義兩個KPI(每個部署的期望)：

   1. 您可以接受的第95個百分位數回應時間為何？

      1. 建議值-秒
   1. 尖峰載入下每分鐘有多少頁面檢視？

      1. 建議值-200pv/m


1. 按一下 **「送出** 」以完成設定精靈。

   您將會看到主畫面， [!UICONTROL Cloud Manager] 以進行 **部署**。

## 可用環境 {#available-environments}

「 **可用環境** 」列出 [!UICONTROL Cloud Manager] 所有受管理的AEM環境。

每個列出的環境都有相關的狀態。

## 設定管道 {#configuring-pipeline}

### 設定管線 {#setting-up-pipeline}

>[!CAUTION]
>
>無法設定管線，直到Git存放庫至少有一個分支為止。

在開始部署程式碼之前，您必須先設定您的管道設定 [!UICONTROL Cloud Manager]。

To learn more about pipeline configuration, see **Pipeline Overview** section in ** [Understanding Concepts before Using [!UICONTROL Cloud Manager]](understanding-concepts.md)**.

>[!NOTE]
>
>您可以在初次設定後變更管線設定。

### 設定管道設定，從 [!UICONTROL Cloud Manager]{#configuring-pipeline-settings-from-the-cloud-manager}

請遵循下列步驟 [!UICONTROL Cloud Manager] ，為您的管線設定Bahavor或偏好設定：

1. 存取 **「分支** 」標籤以設定應用程式分支。

   選取您要設定的git分支。

   >[!NOTE]
   >
   >在Git存放庫中找到的分支會連結至您的程式。

   ![](assets/screen_shot_2018-05-06at73604pm.png)

1. 存取 **「環境** 」索引標籤，選取 **「舞台(Stage)」** 和 **「生產(Production)」** 選項。

   您可以定義觸發，以啓動管線：

   * **手動** -某人必須手動按一下UI，才能啓動管線。
   現在您定義控制生產部署的參數。下列可用選項如下：

   * **使用上線核准**-必須由企業擁有者、專案經理或部署管理員手動核准部署 [!UICONTROL Cloud Manager] 。
   * **使用CSE監督** -參與實際啓動部署。
   ![](assets/screen_shot_2018-05-06at73715pm.png)

1. 存取「 **測試** 」標籤，定義您的程式的測試准則。

   現在，您可以設定效能測試參數。

   ![](assets/screen_shot_2018-05-06at73750pm.png)

## 部署程式碼 {#deploying-code}

設定您的管道(儲存庫、環境和測試環境)後，即可部署您的程式碼。

### 部署程式碼從 [!UICONTROL Cloud Manager]{#deploying-code-from-cloud-manager}

請依照下列步驟將程式碼部署至生產環境：

1. 按一下 **「部署**[!UICONTROL Cloud Manager] 」，開始部署程序。
1. 「 **舞台部署」** 畫面隨即顯示。

   按一下 **「建立** 」以開始處理程序。

1. 完整的建置程序會考量數個參數來檢查和部署您的程式碼。

   已勾選的下列參數如下：

   **階段部署**

   * 存放庫
   * 單元測試
   * 程式碼掃描
   * 部署至舞台環境
   **前制測試**

   * 安全性測試
   * 效能測試
   >[!NOTE]
   >
   >此外，您也可以檢視上述測試准則的記錄檔或檢視結果。

## 品質檢查結果 {#results-from-quality-checks}

管線中有三個閘門：程式碼品質、效能測試和安全性測試。

對於上述每個關卡，關卡識別的問題有三層式結構。

* **重要** -這些是閘道識別的問題，造成管線立即失敗。
* **重要** -這些是閘道識別的問題，會導致管線進入暫停狀態。部署管理員、專案經理或業務擁有者可以覆寫問題，在此情況下，管線會發展，或者他們可以接受問題，此時管線會停止發生。
* **資訊** -這些是依關卡識別的問題，僅供資訊用途使用，不影響管線執行。

### 程式碼掃描 {#code-scanning}

![](assets/screen_shot_2018-04-22at101443am.png)

### 效能測試 {#performance-testing}

*測試中的效能測試*[!UICONTROL Cloud Manager] 是使用30分鐘的測試實施。

在管線設定期間，部署管理員可決定導向至每個貯體的流量。從一個到全部三個區間都可以選擇。流量的分配是根據選取的區間數，亦即，如果所有三個項目都已選取，則每個儲存貯體都會放置33%的頁面檢視總數；如果選取兩個，則50%移至每個集合；如果選取了一個，則100%流量都會移至該設定。

例如，假設「熱門即時頁面」和「新頁面」設定之間有50%/50%的分割(在此範例中，「其他即時頁面」未使用)和「新頁面」集包含3000頁。每分鐘KPI的頁面檢視設為200。30分鐘測試期間：

* 「熱門即時頁面」設定中的每個25頁都會點擊240次- `((200 &#42; 0.5) / 25) &#42; 30 = 120`
* 「新頁面」設定中的每個3000頁都將被點擊一次- `((200 &#42; 0.5) / 3000) &#42; 30 = 1`

![](assets/image2018-3-14_16-23-56.png)

### 效能測試度量 {#performance-test-metrics}

在測試期間，會擷取許多度量，並與由業務擁有者定義的KPI或AMS設定的標準比較。

These are reports using the三層ging system as follows：

### 執行管道時的三層式關卡 {#three-tier-gates-while-running-a-pipeline}

管道中有三個閘道，作為程式碼品質、效能測試和安全性測試。

對於上述每個關卡，關卡識別問題有三層式結構：

* **重要**：這是閘道識別的問題，造成管線立即失敗。
* **重要**：這是閘道識別的問題，會導致管線進入暫停狀態。部署管理員、專案經理或業務擁有者可以覆寫問題，在此情況下，管線會發展，或者他們可以接受問題，此時管線會停止發生。
* **資訊**：這些是由門識別的問題，僅供資訊目的使用，不會影響管線執行。

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

### 安全性測試 {#security-testing}

[!UICONTROL Cloud Manager] 在部署後執行現有 *的AEM Security Heats檢查* 階段，並透過UI報告其狀態。結果會從環境中的所有AEM實例匯總。

如果有任何例項回報特定健康狀態檢查失敗，則整個環境會失敗，無法正常運作。如同「程式碼品質」和「效能測試」，這些健康狀態檢查會組織成類別並使用三層式定位系統報告。唯一的區別在於，安全測試不會有臨界值。所有健康檢查都只是通過或失敗。

目前的檢查包括：

| **Health Check** | **類別** |
|---|---|
| 還原序列化防火牆附加 API 整備 | 重要事項 |
| 還原序列化防火牆已作用 | 重要事項 |
| 還原序列化防火牆已載入 | 重要事項 |
| 可授權節點名稱產生 | 重要事項 |
| 預設登入帳戶 | 重要事項 |
| Sling Get Servlet | 重要事項 |
| CQ Dispatcher 組態 | 重要事項 |
| CQ HTML 文件庫管理員組態 | 重要事項 |
| Sling Java 指令碼處理常式 | 重要事項 |
| Sling Jsp 指令碼處理常式 | 重要事項 |
| Sling 查閱者篩選 | 重要事項 |
| SSL 設定 | 重要事項 |
| 使用者設定檔預設存取 | 重要事項 |
| CRXDE 支援 | 重要事項 |
| DavEx 健康狀態檢查 | 重要事項 |
| 範例內容封裝 | 重要事項 |
| WCM 篩選設定 | 重要事項 |
| WebDAV 健康狀態檢查 | 重要事項 |
| Web 伺服器組態 | 重要事項 |
| 複寫及傳輸使用者 | 資訊 |

### SonarquBE的品質檢查實作 {#quality-check-implementation-by-sonarqube}

作為管道的一部分，如上方所述，會掃描代碼。目前，此項目由SonarquBE實施。我們有93個規則，它們是一般Java規則和AEM特定規則的組合(包括來自Conkefed&#39;s現有規則集的部分規則)。以下列出這些規則的清單： [Sonarque規則](assets/sonarqube-rules.xlsx)

在這些規則中，會計算多種度量，其中有些度量會被用作品質關卡，再允許部署至舞台環境。

這些是目前的臨界值：

| 名稱 | 定義 | 類別 | 失敗臨界值 |
|--- |--- |--- |--- |
| 安全性分級 | A=0弱點 <br/>B=至少次要弱點<br/> C=至少個重大弱點 <br/>D=至少個重大弱點 <br/>E=至少個封鎖程式弱點 | 重要事項 | &lt; B |
| 可靠性分級 | A=錯誤 <br/>B=至少次要錯誤 <br/>C=至少個主要錯誤 <br/>D=至少個重要錯誤E=至少個封鎖程式錯誤 | 重要事項 | &lt; C |
| 維護能力分級 | 程式碼閃現的顯著修補成本為： <br/><ul><li>&lt;=5%的時間已進入應用程式，評分為A </li><li>到10%之間，評分為B </li><li>在11到20%之間評分為C </li><li>到50%之間，評分為D</li><li>超過50%是一個E</li></ul> | 重要事項 | &lt; A |
| 適用範圍 | 使用此公式混合涵蓋範圍和條件涵蓋範圍： <br/>`Coverage = (CT + CF + LC)/(2*B + EL)`<br/>其中：CT=在至少一次 <br/>CF=條件被評估為&#39;false&#39;後至少評估成&#39;false&#39;的條件：至少一次 <br/>LC=涵蓋行=行_ to_封面-未涵蓋的行 <br/><br/> B=可 <br/>執行行數總計(行_至_封面) | 重要事項 | &lt; 50% |
| 跳過的單元測試 | 跳過的單元測試數。 | 資訊 | &gt; 1 |
| 開放問題 | 整體問題類型-弱點、錯誤和程式碼精靈 | 資訊 | &gt; 1 |
| 複製的線條 | 重復區塊的相關行數。<br/>要將程式碼區塊視為重復的區塊： <ul><li> **非Java專案：**</li><li>應至少有100個連續和重復的Token。</li><li>這些Token至少應被發送至： </li><li>COBOLE的30行程式碼 </li><li>ABAP20行程式碼 </li><li>其他語言10行程式碼</li></ul><ul><li>**Java專案：**</li><li> 無論預付碼和行數為何，至少應有10個連續和重復的陳述式。</li></ul>在偵測重復時，忽略縮排以及字串字詞的差異。 | 資訊 | &gt; 1% |

### 虛假錯誤 {#false-positives}

品質的掃描程序不完美，有時會不正確地識別問題並不會造成問題。這稱為 *false正面* (雖然 *負面負面效果* 可能更具語義正確性)。在這些情況下，來源程式碼可加上標準Java `@SuppressWarnings` 備注，以指定規則ID做為註解屬性。例如，一個常見的問題是Sonarque規則用來偵測硬式編碼密碼對於它的硬式編碼密碼而言是非常自由的。

若要查看特定範例，此程式碼在AEM專案中會相當常見，因為AEM專案具有連線至某些外部服務的程式碼：

```java
@Property(label = "Service Password")
private static final String SERVICE_PASSWORD = "password";
```

SonarQue會將此弱點提升為封鎖程式弱點。在此情況下，客戶可識別此弱點並將其加入適當的規則ID：

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String SERVICE_PASSWORD = "password";
```

但另一方面，如果程式碼實際上是如此：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String SERVICE_PASSWORD = "password";
```

然後，客戶應將Sonarque的警告置於心臟，並移除硬式編碼密碼。但是，由於詞語實際上會觸發Sonarque規則，所以仍需要新增 `@SuppressWarnings` 附註 `password`。

>[!NOTE]
>
>建議盡可能將 `@SuppressWarnings` 註解設為特定，亦即僅註解特定陳述式或封鎖造成問題的特定陳述式或區塊，以便在類別層級加上註解。

