---
title: 了解測試結果
seo-title: 了解測試結果
description: 在Cloud Manager中執行管道時，進一步了解三層門
seo-description: 請參照本頁面，了解在Cloud Manager中執行管道、程式碼掃描、效能和安全性測試，以驗證您的程式時的三層入口。
uuid: 93caa01f-0df2-4a6f-81dc-23dfee24dc93
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 83299ed8-4b7a-4b1c-bd56-1bfc7e7318d4
feature: CI-CD管線，測試結果
exl-id: 6a574858-a30e-4768-bafc-8fe79f928294
source-git-commit: 5111a918b8063ab576ef587dc3c8d66ad976fc1a
workflow-type: tm+mt
source-wordcount: '2722'
ht-degree: 3%

---

# 了解測試結果 {#understand-your-test-results}

>[!NOTE]
>若要了解Cloud Manager支援的Cloud Services管道測試結果和測試，請參閱[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en#using-cloud-manager)。

在管道執行期間，會擷取許多量度，並與業務擁有者定義的關鍵績效指標(KPI)，或Adobe Managed Services設定的標準進行比較。

這些資料是使用三層門控系統（如本節所定義）來報告的。

## 管線運行時的三層門{#three-tier-gates-while-running-a-pipeline}

有三扇門正在鋪設：

* 程式碼品質
* 效能測試
* 安全性測試

對於每個門，門所標識的問題都有三層結構。

* **關鍵**  — 這些是閘道所識別的問題，會造成管道立即失敗。
* **重要**  — 這些是閘道所識別的問題，導致管道進入暫停狀態。部署經理、項目經理或業務負責人可以覆蓋問題，在這種情況下，管道將繼續，或者他們可以接受問題，在這種情況下，管道會因故障而停止。 重要失敗的覆寫受[逾時](deploying-code.md#timeouts)的約束。
* **Info**  — 這些是閘道所識別的問題，僅供參考，對管道執行沒有影響。

>[!NOTE]
>
>在僅代碼質量管道中，代碼質量測試澆口中的重要故障無法被覆蓋，因為代碼質量測試步驟是管道中的最後一步。

## 代碼質量測試{#code-quality-testing}

此步驟會評估應用程式程式碼的品質。 這是僅限程式碼品質管道的核心目標，會在所有非生產和生產管道的建立步驟後立即執行。 請參閱[設定CI-CD管道](/help/using/configuring-pipeline.md)以深入了解不同類型的管道。

### 了解代碼質量測試{#understanding-code-quality-testing}

在程式碼品質測試中，會掃描原始碼，以確保其符合特定品質標準。 目前，這是透過SonarQube、使用OakPAL的內容套件層級檢查，以及使用Dispatcher最佳化工具進行Dispatcher驗證而實作。 有100多個規則結合一般Java規則和AEM專用規則。 有些AEM專用規則是根據AEM Engineering的最佳實務建立，並稱為[自訂程式碼品質規則](/help/using/custom-code-quality-rules.md)。

>[!NOTE]
>您可以在此處[下載規則完整清單。](/help/using/assets/CodeQuality-rules-latest-AMS.xlsx)

此步驟的結果以&#x200B;*Rating*&#x200B;傳送。 下表匯總了各種測試標準的評等：

| 名稱 | 定義 | 類別 | 失敗閾值 |
|--- |--- |--- |--- |
| 安全性評等 | A = 0漏洞<br/>B =至少1個次要漏洞<br/> C =至少1個主要漏洞<br/>D =至少1個關鍵漏洞<br/>E =至少1個封鎖程式漏洞 | 關鍵 | &lt; B |
| 可靠性等級 | A = 0錯誤<br/>B =至少1個次要錯誤<br/>C =至少1個主要錯誤<br/>D =至少1個嚴重錯誤<br/>E =至少1個封鎖程式錯誤 | 重要 | &lt; C=&quot;&quot;> |
| 維修性等級 | 代碼氣味的未補償成本是：<br/><ul><li>&lt;> </li><li>6%到10%的評等是a B </li><li>11%到20%的評等是C </li><li>21%到50%的評等是D</li><li>超過50%的是E</li></ul> | 重要 | &lt; A |
| 適用範圍 | 使用以下公式的單元測試線覆蓋和條件覆蓋的組合：<br/>`Coverage = (CT + CF + LC)/(2*B + EL)` <br/>其中：CT =運行單元測試時至少被評估為「true」的條件<br/>CF =運行單元測試時被評估為「false」的條件<br/>LC =覆蓋行= linestocover - uncoveredlines <br/><br/> B =條件總數<br/>EL =可執行行總數(linestocover) | 重要 | &lt; 50% |
| 已跳過的單元測試 | 已跳過的單元測試數。 | 資訊 | > 1 |
| 未結問題 | 整體問題類型 — 弱點、錯誤和程式碼氣味 | 資訊 | > 0 |
| 重複行 | 重複塊中涉及的行數。 <br/>若要將程式碼區塊視為重複：  <br/><ul><li>**非Java專案：**</li><li>至少應有100個連續和重複的代號。</li><li>這些代號至少應散布在： </li><li>COBOL的30行代碼 </li><li>ABAP的20行代碼 </li><li>10行代碼以供其他語言使用</li><li>**Java項目：**</li><li> 無論代號和行的數量多寡，至少應有10個連續且重複的陳述式。</li></ul> <br/>在檢測重複時，會忽略縮排和字串文字的差異。 | 資訊 | > 1% |
| Cloud Service相容性 | 已識別的Cloud Service相容性問題數。 | 資訊 | > 0 |


>[!NOTE]
>
>如需詳細定義，請參閱[量度定義](https://docs.sonarqube.org/display/SONAR/Metric+Definitions) 。

>[!NOTE]
>
>若要進一步了解[!UICONTROL Cloud Manager]執行的自訂程式碼品質規則，請參閱[自訂程式碼品質規則](custom-code-quality-rules.md)。

### 處理誤判{#dealing-with-false-positives}

質量掃描過程不完美，有時會錯誤地識別實際上沒有問題的問題。 這稱為「誤判」。

在這些情況下，可以用標準Java `@SuppressWarnings`注釋對原始碼進行注釋，該標準Java 注釋指定規則ID作為注釋屬性。 例如，一個常見問題是，用於檢測硬編碼密碼的SonarQube規則對於硬編碼密碼的識別方式可能具有攻擊性。

若要查看特定範例，此程式碼在AEM專案中很常見，其程式碼可連線至某些外部服務：

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube隨後會引發Blocker漏洞。 檢閱程式碼後，您即可識別這不是漏洞，並可以使用適當的規則ID加以註解。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但另一方面，如果程式碼是：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

那麼正確的解決方案就是刪除硬式編碼的密碼。

>[!NOTE]
>
>盡可能使`@SuppressWarnings`注釋特定（即僅注釋引起此問題的特定語句或塊）是最佳做法，但可以在類級別注釋。

## 安全測試{#security-testing}

[!UICONTROL Cloud Manager] 在部署後執 ***行現有的AEM*** 安全性健康檢查階段，並透過UI報告狀態。結果會從環境中的所有AEM例項匯總。

這些相同的運行狀況檢查可以隨時通過Web控制台或操作儀表板執行。

如果&#x200B;**Instances**&#x200B;中的任何一個報告了給定運行狀況檢查的失敗，則整個&#x200B;**Environment**&#x200B;將失敗該運行狀況檢查。 和代碼質量和效能測試一樣，這些運行狀況檢查按類別組織，並使用三層選通系統報告。 唯一的區別在於，在安全性測試中沒有閾值。 所有健康檢查都只是通過或失敗。

下表列出了當前檢查：

| **名稱** | **運行狀況檢查實施** | **類別** |
|---|---|---|
| 反序列化防火牆附加API就緒處於可接受的狀態 | [還原序列化防火牆附加 API 整備](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html?lang=en#security) | 關鍵 |
| 反序列化防火牆功能正常 | [還原序列化防火牆已作用](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html?lang=en#security) | 關鍵 |
| 已載入反序列化防火牆 | [還原序列化防火牆已載入](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html?lang=en#security) | 關鍵 |
| 可授權NodeName實作不會公開節點名稱/路徑中可授權的ID。 | [可授權節點名稱產生](https://experienceleague.adobe.com/docs/experience-manager-64/administering/security/security-checklist.html?lang=en#security) | 關鍵 |
| 已更改預設密碼 | [預設登入帳戶](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=en#users-and-groups-in-aem) | 關鍵 |
| Sling預設GETServlet受DOS攻擊保護。 | Sling Get Servlet | 關鍵 |
| Sling Java指令碼處理常式已適當設定 | Sling Java 指令碼處理常式 | 關鍵 |
| Sling JSP指令碼處理程式已正確配置 | Sling JSP指令碼處理常式 | 關鍵 |
| SSL已正確設定 | SSL 設定 | 關鍵 |
| 未找到明顯不安全的用戶配置檔案策略 | 使用者設定檔預設存取 | 關鍵 |
| 已設定Sling反向連結篩選器，以防止CSRF攻擊 | [Sling 查閱者篩選](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=en#security) | 重要 |
| AdobeGranite HTML程式庫管理員已適當設定 | CQ HTML 文件庫管理員組態 | 重要 |
| CRXDE支援套件組合已停用 | CRXDE 支援 | 重要 |
| Sling DavEx套件組合和Servlet已停用 | DavEx 健康狀態檢查 | 重要 |
| 未安裝範例內容 | 範例內容封裝 | 重要 |
| WCM請求篩選器和WCM除錯篩選器皆已停用 | [WCM 篩選設定](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html?lang=en#configuring) | 重要 |
| 正確配置了Sling WebDAV捆綁包和Servlet | WebDAV 健康狀態檢查 | 重要 |
| Web伺服器配置為防止點擊劫持 | Web 伺服器組態 | 重要 |
| 復寫未使用「管理員」用戶 | 複寫及傳輸使用者 | 資訊 |

## 效能測試{#performance-testing}

### AEM Sites {#aem-sites}

Cloud Manager會對AEM Sites程式執行效能測試。 通過旋轉虛擬用戶（容器）來模擬實際用戶訪問Stage環境中的頁面並模擬流量，運行效能測試約30分鐘。 這些頁面使用Crawler找到。

1. **虛擬使用者**

   由Cloud Manager分解的虛擬使用者或容器數量，是由業務擁有者角色中的使用者所定義的KPI（回應時間和頁面檢視/分鐘）所驅動，而[會建立或編輯方案](setting-up-program.md)。 根據已定義的KPI，最多將分解10個模擬實際使用者的容器。 選擇用於測試的頁被拆分並分配給每個虛擬。

1. **Crawler**

   在30分鐘測試期間開始前，Cloud Manager將使用客戶成功工程師所設定的一組一或多個種子URL對Stage環境進行編目。 從這些URL開始，會檢查每個頁面的HTML，並以寬度優先的方式遍歷連結。 此編目程式最多只能有5000個頁面。 來自Crawler的請求具有10秒的固定超時。

1. **測試頁面集**

   頁面由三個頁面集選取。 Cloud Manager會使用AEM例項在生產與預備期間的存取記錄，以判斷下列三個貯體：

   * *熱門即時頁面*:選取此選項，以確保測試即時客戶存取的最受歡迎頁面。Cloud Manager會讀取存取記錄，並決定即時客戶最常存取的前25個頁面，以產生前`Popular Live Pages`的清單。 然後，在Stage環境中對Stage中也存在的這些交集進行爬網。

   * *其他即時頁面*:選取此選項，可確定落在前25個熱門即時頁面以外、雖然不受歡迎，但對測試而言很重要的頁面，會經過測試。與「熱門」即時頁麵類似，這些頁面會從存取記錄中擷取，且也必須存在於「階段」中。

   * *新頁面*:選取此選項可測試可能僅部署至「預備」而尚未部署至「生產」，但必須測試的新頁面。

      **所選頁面集的流量分佈**

      在管道配置的「測試」（「插入連結」）頁簽中，可以選擇從一組到全部三組的任意位置。 流量的分配是根據選取的集數，即如果選取了全部三個集，則會將總頁面檢視的33%放入每個集；若選取兩個，則50%會分配給每個集；如果選取一個，則100%的流量會進入該集。

      例如，假設「熱門即時頁面」和「新頁面」集（在此範例中，未使用其他即時頁面）之間有50%到50%的分割，而「新頁面」集包含3000個頁面。 每分鐘頁面檢視次數KPI設為200。 在30分鐘的測試期間：

      * 「熱門即時頁面」集中的25頁每頁都會點擊120次 — ((200 * 0.5)/ 25)* 30 = 120

      * 「新頁面」集中的3000個頁面將各點擊一次 — ((200 * 0.5)/ 3000)* 30 = 1

#### 測試和報告{#testing-reporting}

Cloud Manager會在預備發佈伺服器上要求頁面（依預設為未驗證的使用者）達30分鐘的測試期間，並測量（虛擬）使用者產生的量度（回應時間、錯誤率、每分鐘檢視次數等），以執行AEM Sites程式的效能測試 針對每個頁面，以及所有執行個體的各種系統層級量度（CPU、記憶體、網路資料）。\
下表總結了使用三層門控系統的效能測試度量：

下表匯總了使用三層選通系統的效能測試矩陣：

| **量度** | **類別** | **失敗閾值** |
|---|---|---|
| 頁面請求錯誤率% | 關鍵 | >= 2% |
| CPU利用率 | 關鍵 | >= 80% |
| 磁碟IO等待時間 | 關鍵 | >= 50% |
| 95個百分位數的回應時間 | 重要 | >=方案層級KPI |
| 峰值響應時間 | 重要 | >= 18秒 |
| 每分鐘頁面檢視次數 | 重要 | &lt; Program-level=&quot;&quot; KPI=&quot;&quot;> |
| 磁碟頻寬利用率 | 重要 | >= 90% |
| 網路頻寬利用率 | 重要 | >= 90% |
| 每分鐘請求數 | 資訊 | >= 6000 |

如需使用基本驗證來測試網站和資產效能的詳細資訊，請參閱以下的&#x200B;**驗證效能測試**&#x200B;一節。

>[!NOTE]
>在測試期間，會針對「發佈」和「作者」監控每個例項。 如果未取得某個例項的任何量度，該量度便會報告為未知，而對應的步驟將會失敗。

#### 驗證的效能測試{#authenticated-performance-testing}

此功能為Sites選用功能。
擁有已驗證網站的AMS客戶可指定使用者名稱和密碼，Cloud Manager將在Sites效能測試期間用來存取該網站。
用戶名和密碼被指定為名稱為`CM_PERF_TEST_BASIC_USERNAME`和`CM_PERF_TEST_BASIC_PASSWORD`的管道變數。
雖然並非嚴格必要，但建議將字串變數類型用於使用者名稱，並將secretString變數類型用於密碼。 如果同時指定了這兩項，則效能測試Crawler和測試虛擬用戶的每個請求都將包含這些憑據作為HTTP Basic身份驗證。

要使用Cloud Manager CLI設定這些變數，請運行：

```shell
$ aio cloudmanager:set-pipeline-variables <pipeline id> --variable CM_PERF_TEST_BASIC_USERNAME <username> --secret CM_PERF_TEST_BASIC_PASSWORD <password>
```

請參閱[變數](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchPipelineVariables)以了解如何使用API。

### AEM Assets {#aem-assets}

Cloud Manager會在30分鐘的測試期間內重複上傳資產，以執行AEM Assets程式的效能測試。

1. **入門要求**

   若是資產效能測試，您的客戶成功工程師將在製作環境上線期間建立`cloudmanager`使用者（和密碼）。 效能測試步驟需要名為`cloudmanager`的用戶以及由CSE設定的相關密碼。 這不應從「作者」中移除，也不應變更為權限。 這麼做很可能會失敗Assets效能測試。

1. **用於測試的影像和資產**

   客戶可上傳自己的資產以進行測試。 可從「管線設定」(Pipeline Setup)或「編輯」(Edit)螢幕執行此操作。 支援JPEG、PNG、GIF和BMP等常見影像格式，以及Photoshop、Illustrator和Postscript檔案。 不過，如果未上傳任何影像，Cloud Manager將使用預設影像和PDF檔案進行測試。

1. **用於測試的資產分配**

   每分鐘上傳多少個類型的資產會在「管道設定」或「編輯」畫面中設定。
例如，如下圖所示，如果使用70/30拆分。 每分鐘上傳10個資產，每分鐘上傳7個影像，以及3個檔案。

1. **測試和報告**

   Cloud Manager將使用CSE在上述步驟#1（入門需求）中設定的使用者名稱和密碼，在製作執行個體上建立資料夾，並使用開放原始碼的程式庫在資料夾中上傳資產。 由「資產」測試步驟執行的測試是使用此[開放原始碼程式庫](https://github.com/adobe/toughday2)寫入。 每個資產的處理時間以及各種系統層級量度都會在30分鐘的測試期間測量。 此功能可上傳影像和PDF檔案。

   >[!NOTE]
   >您可以從[配置CI/CD管道](configuring-pipeline.md)了解有關配置效能測試的更多資訊。 請參閱[設定您的程式](setting-up-program.md)，了解如何設定您的程式和定義您的KPI。

### 效能測試結果圖{#performance-testing-results-graphs}

「效能測試結果」對話方塊中已新增圖形和下載選項。

當您開啟「效能測試」對話方塊時，量度面板可展開以顯示圖形、提供下載連結或兩者皆可。

對於[!UICONTROL Cloud Manager] 2018.7.0版，此功能適用於下列量度：

* **CPU利用率**
   * 測試期間的CPU利用率圖表。

* **磁碟I/O等待時間**
   * 測試期間的磁碟I/O等待時間圖。

* **頁面錯誤率**
   * 測試期間每分鐘的頁面錯誤圖表。
   * 列出測試期間產生錯誤之頁面的CSV檔案。

* **磁碟頻寬利用率**
   * 測試期間磁碟頻寬利用率的圖表。

* **網路頻寬利用率**
   * 測試期間的網路頻寬利用率圖表。

* **峰值響應時間**
   * 測試期間每分鐘的峰值回應時間圖表。

* **第95個百分位數的回應時間**
   * 在測試期間，每分鐘第95個百分位數回應時間的圖表。
   * 一個CSV檔案，列出第95個百分位數的回應時間超過定義的KPI的頁面。

以下影像顯示效能測試圖：

![](assets/understand_test-results-screen1.png)

![](assets/screen_shot_2018-09-05at83933pm.png)
