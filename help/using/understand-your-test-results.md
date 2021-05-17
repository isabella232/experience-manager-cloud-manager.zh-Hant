---
title: 了解測試結果
seo-title: 了解測試結果
description: 在Cloud Manager中執行管道時，進一步瞭解三層門
seo-description: 在Cloud Manager中執行管道、程式碼掃描、效能和安全性測試驗證您的程式時，請依照本頁瞭解三層閘道。
uuid: 93caa01f-0df2-4a6f-81dc-23dfee24dc93
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 83299ed8-4b7a-4b1c-bd56-1bfc7e7318d4
feature: CI-CD管道，測試結果
exl-id: 6a574858-a30e-4768-bafc-8fe79f928294
source-git-commit: df2f598f91201d362f54b17e4092ff6bd6a72cec
workflow-type: tm+mt
source-wordcount: '2722'
ht-degree: 3%

---

# 了解測試結果 {#understand-your-test-results}

>[!NOTE]
>要瞭解Cloud Manager針對Cloud Services管道支援的測試結果和測試，請參閱[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/overview-test-results.html?lang=en#using-cloud-manager)。

在管道執行期間，會擷取許多量度並與企業擁有者定義的關鍵績效指標(KPI)或Adobe Managed Services設定的標準進行比較。

這些是使用本節定義的三層式選通系統來報告。

## 運行管線{#three-tier-gates-while-running-a-pipeline}時的三層門

目前有三扇門正在醖釀之中：

* 程式碼品質
* 效能測試
* 安全性測試

對於每個門，門都有三層結構來解決由門所識別的問題。

* **Critical**  —— 這些是由門確定的導致管道立即故障的問題。
* **重要** -這些是閘道識別的問題，導致管線進入暫停狀態。部署經理、專案經理或業務負責人可以覆寫問題（在這種情況下，管道會繼續），或者接受問題（在這種情況下，管道會因故障而停止）。 重要失敗的覆寫受[逾時](deploying-code.md#timeouts)的限制。
* **Info**  —— 這些是由門所標識的問題，這些問題僅供參考，對管線執行沒有影響。

>[!NOTE]
>
>在僅代碼質量管道中，不能改寫代碼質量測試門中的重要故障，因為代碼質量測試步驟是管道中的最後一步。

## 程式碼品質測試{#code-quality-testing}

此步驟會評估您的應用程式碼的品質。 它是僅限程式碼品質管道的核心目標，並會立即在所有非生產及生產管道的建立步驟後執行。 請參閱[配置CI-CD管線](/help/using/configuring-pipeline.md)以進一步瞭解不同類型的管線。

### 瞭解代碼質量測試{#understanding-code-quality-testing}

在「程式碼品質測試」中，會掃描原始碼，以確保其符合特定品質標準。 目前，這是透過SonarQube、使用OakPAL的內容封裝層級檢查以及使用Dispatcher Optimization Tool的Dispatcher驗證來實作的。 有超過100種規則結合一般Java規則和AEM特定規則。 有些特定AEM規則是根據工程部門的最佳實踐AEM而建立，稱為[自訂代碼品質規則](/help/using/custom-code-quality-rules.md)。

>[!NOTE]
>您可以下載規則的完整清單[這裡](/help/using/assets/CodeQuality-rules-AMS.xlsx)。

此步驟的結果以&#x200B;*Rating*&#x200B;的形式提供。 下表摘要了各種測試標準的評分：

| 名稱 | 定義 | 類別 | 故障閾值 |
|--- |--- |--- |--- |
| 安全性分級 | A = 0漏洞<br/>B =至少1個小漏洞<br/> C =至少1個主漏洞<br/>D =至少1個嚴重漏洞<br/>E =至少1個攔截器漏洞 | 重要 | &lt; B |
| 可靠性分級 | A = 0錯誤<br/>B =至少1次錯誤<br/>C =至少1次主要錯誤<br/>D =至少1次重大錯誤<br/>E =至少1次攔截器錯誤 | 重要 | &lt; C=&quot;&quot;> |
| 可維護性評級 | 代碼氣味的未付補救成本是：<br/><ul><li>&lt;> </li><li>6%到10%的評分是B </li><li>11%到20%的評分是C </li><li>21%到50%的評分是D</li><li>超過50%的項目是E</li></ul> | 重要 | &lt; A |
| 適用範圍 | 單位測試線覆蓋率與條件覆蓋率的混合使用公式：<br/>`Coverage = (CT + CF + LC)/(2*B + EL)` <br/>其中：CT =運行單元測試時評估為「true」的條件，運行單元測試時，評估為「false」的條件，運行單元測試時，評估為「false」的條件至少一次，運行單元測試時，LC =覆蓋行= lines_to_cover - ouncated_lines <br/><br/> B =條件總數<br/>EL =可執行行總數(lines_to_cover)<br/><br/> | 重要 | &lt; 50% |
| 跳過的設備測試 | 跳過的單元測試數。 | 資訊 | > 1 |
| 未結問題 | 整體問題類型——弱點、錯誤和程式碼氣味 | 資訊 | > 0 |
| 複製行 | 重複塊中涉及的行數。 <br/>對於要視為複製的代碼塊：  <br/><ul><li>**非Java專案：**</li><li>至少應有100個連續和重複的Token。</li><li>這些預付碼應至少分散於： </li><li>COBOL的30行代碼 </li><li>ABAP的20行代碼 </li><li>10行其他語言的程式碼</li><li>**Java專案：**</li><li> 不論預付碼和行數為何，至少應有10個連續和重複的陳述式。</li></ul> <br/>在檢測重複時，會忽略縮排和字串文字的差異。 | 資訊 | > 1% |
| Cloud Service相容性 | 已識別的Cloud Service相容性問題數。 | 資訊 | > 0 |


>[!NOTE]
>
>請參閱[量度定義](https://docs.sonarqube.org/display/SONAR/Metric+Definitions)以取得更詳細的定義。

>[!NOTE]
>
>若要進一步瞭解[!UICONTROL Cloud Manager]執行的自訂代碼品質規則，請參閱[自訂代碼品質規則](custom-code-quality-rules.md)。

### 處理誤報{#dealing-with-false-positives}

品質掃描程式不完善，有時會錯誤地識別實際上沒有問題的問題。 這稱為「假陽性」。

在這些情況下，原始碼可以用標準Java `@SuppressWarnings`注釋加以注釋，該標準Java 注釋指定規則ID作為注釋屬性。 例如，一個常見問題是，用於檢測硬編碼密碼的SonarQube規則對於如何識別硬編碼密碼具有攻擊性。

若要檢視特定範例，此程式碼在專案中相當常見，AEM專案中有程式碼可連接至某些外部服務：

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube隨後會提出一個「攔截器漏洞」。 在檢閱程式碼後，您會發現此程式碼不是弱點，並可使用適當的規則ID加以註解。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但是，另一方面，如果代碼是：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然後，正確的解決方案是移除硬式編碼密碼。

>[!NOTE]
>
>儘管最佳做法是盡可能使`@SuppressWarnings`注釋具體，即僅注釋導致問題的特定語句或塊，但可以在類別級別注釋。

## 安全性測試{#security-testing}

[!UICONTROL Cloud Manager] 在部署後執 ***行AEM現有的Security Heath*** Checkson階段，並透過UI報告狀態。從環境中的所有實例AEM匯總結果。

這些相同的Health Checks可以隨時透過Web Console或Operations Dashboard執行。

如果&#x200B;**Instances**&#x200B;中的任何一個報告給定健康檢查的失敗，則整個&#x200B;**Environment**&#x200B;將失敗該健康檢查。 如同程式碼品質與效能測試，這些健康狀況檢查會組織成類別，並使用三層式選通系統來報告。 唯一的區別是，在安全測試中沒有閾值。 所有健康檢查都只是通過或失敗。

下表列出了當前檢查：

| **名稱** | **運行狀況檢查實施** | **類別** |
|---|---|---|
| 還原序列化防火牆附加API就緒性處於可接受的狀態 | [還原序列化防火牆附加 API 整備](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html?lang=en#security) | 重要 |
| 還原序列化防火牆功能正常 | [還原序列化防火牆已作用](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html?lang=en#security) | 重要 |
| 已載入還原序列化防火牆 | [還原序列化防火牆已載入](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html?lang=en#security) | 重要 |
| AuthorizableNodeName實作不會在節點名稱／路徑中公開可授權的ID。 | [可授權節點名稱產生](https://experienceleague.adobe.com/docs/experience-manager-64/administering/security/security-checklist.html?lang=en#security) | 重要 |
| 預設密碼已變更 | [預設登入帳戶](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=en#users-and-groups-in-aem) | 重要 |
| Sling defaultGETservlets is protected for DOS attacks. | Sling Get Servlet | 重要 |
| Sling Java Script Handler已正確設定 | Sling Java 指令碼處理常式 | 重要 |
| Sling JSP指令碼處理常式已正確設定 | Sling JSP指令碼處理常式 | 重要 |
| SSL已正確設定 | SSL 設定 | 重要 |
| 未發現明顯不安全的使用者設定檔原則 | 使用者設定檔預設存取 | 重要 |
| Sling Referrer Filter已設定，以防止CSRF攻擊 | [Sling 查閱者篩選](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=en#security) | 重要 |
| Adobe花崗岩HTML庫管理器已正確配置 | CQ HTML 文件庫管理員組態 | 重要 |
| 已禁用CRXDE支援包 | CRXDE 支援 | 重要 |
| Sling DavEx套裝和servlet已停用 | DavEx 健康狀態檢查 | 重要 |
| 未安裝範例內容 | 範例內容封裝 | 重要 |
| WCM請求篩選器和WCM除錯篩選器都已停用 | [WCM 篩選設定](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html?lang=en#configuring) | 重要 |
| Sling WebDAV搭售和servlet已正確設定 | WebDAV 健康狀態檢查 | 重要 |
| Web伺服器已設定為防止點按劫持 | Web 伺服器組態 | 重要 |
| 複製不使用「admin」用戶 | 複寫及傳輸使用者 | 資訊 |

## 效能測試{#performance-testing}

### AEM Sites {#aem-sites}

Cloud Manager會執行AEM Sites程式的效能測試。 效能測試通過啟動虛擬用戶（容器）來運行約30分鐘，虛擬用戶（容器）模擬實際用戶訪問舞台環境上的頁面並模擬流量。 這些頁是使用Crawler找到的。

1. **虛擬用戶**

   由Cloud Manager分解的虛擬用戶或容器數量由[建立或編輯程式](setting-up-program.md)時由用戶在「業務所有者」角色中定義的KPI（響應時間和頁面視圖／分鐘）驅動。 根據定義的KPI，最多可以紡出10個模擬實際使用者的容器。 選取進行測試的頁面會分割並指派給每個虛擬頁面。

1. **Crawler**

   在30分鐘測試期開始之前，Cloud Manager將使用客戶成功工程師所設定的一組或多個種子URL來編目Stage環境。 從這些URL開始，會檢查每個頁面的HTML，並以寬度優先的方式瀏覽連結。 此編目程式最多限制為5000頁。 來自Crawler的請求有10秒的固定逾時。

1. **測試頁面集**

   頁面由三個頁面集選取。 Cloud Manager使用Production和Stage中實例AEM的訪問日誌來確定以下三個儲存區：

   * *熱門即時頁面*:選取此選項可確保測試即時客戶存取的最受歡迎頁面。Cloud Manager會讀取存取記錄，並決定即時客戶最常存取的前25個頁面，以產生前`Popular Live Pages`的清單。 然後，在Stage環境上搜索這些也存在於Stage中的交集。

   * *其他即時頁面*:選取此選項，可確保測試位於前25個熱門即時頁面以外的頁面，這些頁面可能不受歡迎，但對測試而言很重要。與「熱門」即時頁麵類似，這些頁面會從存取記錄中擷取，而且也必須出現在「舞台(Stage)」上。

   * *新頁面*:此選項會選取來測試可能只部署至「舞台(Stage)」而尚未部署至「生產(Production)」但必須測試的新頁面。

      **所選頁面集間的流量分佈**

      在管線配置的「測試」(Testing)頁籤(「插入」(Insert)連結)中，可以從一組到三組中選擇任意組。 流量的分配是根據選擇的集數，即如果全部三個都被選中，則33%的頁面檢視會放入每個集；如果選取2個，則每組50%;如果選取其中一個，則100%的流量會移至該集合。

      例如，假設「熱門即時頁面」和「新頁面」集之間有50% - 50%的分割（在此範例中，不使用其他即時頁面），而「新頁面」集包含3000頁。 每分鐘頁面檢視次數KPI設定為200。 在30分鐘的測試期間：

      * 「熱門即時頁面」集中的25個頁面，每個頁面將被點擊120次-((200 * 0.5)/ 25)* 30 = 120

      * 「新頁面」集中的3000個頁面中，每個頁面都會點擊一次-((200 * 0.5)/ 3000)* 30 = 1

#### 測試和報告{#testing-reporting}

Cloud Manager會在舞台發佈伺服器上請求頁面（依預設為未驗證的使用者）30分鐘的測試時段，並測量（虛擬）使用者產生的量度（回應時間、錯誤率、每分鐘檢視次數等），以執行AEM Sites程式的效能測試 針對每個頁面以及所有例項的各種系統層級量度（CPU、記憶體、網路資料）。\
下表匯總了使用三層式選通系統的效能測試度量：

下表總結了使用三層門控系統的效能測試矩陣：

| **量度** | **類別** | **故障閾值** |
|---|---|---|
| 頁面請求錯誤率% | 重要 | >= 2% |
| CPU使用率 | 重要 | >= 80% |
| 磁碟IO等待時間 | 重要 | >= 50% |
| 95百分位數回應時間 | 重要 | >=方案層級KPI |
| 峰值響應時間 | 重要 | >= 18秒 |
| 每分鐘頁面檢視次數 | 重要 | &lt; Program-level=&quot;&quot; KPI=&quot;&quot;> |
| 磁碟頻寬利用率 | 重要 | >= 90% |
| 網路頻寬利用率 | 重要 | >= 90% |
| 每分鐘請求數 | 資訊 | >= 6000 |

有關使用基本身份驗證進行站點和資產效能測試的詳細資訊，請參閱下面的&#x200B;**已驗證的效能測試**&#x200B;一節。

>[!NOTE]
>在測試期間（針對「發佈」和「作者」），會監控每個例項。 如果未取得任何度量（即使是一個例項），該度量會報告為未知，而對應的步驟將會失敗。

#### 已驗證的效能測試{#authenticated-performance-testing}

此功能是Sites選用功能。
具有已驗證網站的AMS客戶可以指定Cloud Manager在Sites效能測試期間用來存取網站的使用者名稱和密碼。
用戶名和口令被指定為名稱為`CM_PERF_TEST_BASIC_USERNAME`和`CM_PERF_TEST_BASIC_PASSWORD`的管線變數。
雖然並非嚴格要求，但建議使用字串變數類型做為username，並建議使用secretString變數類型作為密碼。 如果同時指定了這兩者，則效能測試Crawler和測試虛擬用戶的每個請求都將包含這些憑據作為HTTP Basic身份驗證。

要使用Cloud Manager CLI設定這些變數，請運行：

```shell
$ aio cloudmanager:set-pipeline-variables <pipeline id> --variable CM_PERF_TEST_BASIC_USERNAME <username> --secret CM_PERF_TEST_BASIC_PASSWORD <password>
```

請參閱[Variables](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Variables/patchPipelineVariables)以瞭解如何使用API。

### AEM Assets {#aem-assets}

Cloud Manager會在30分鐘的測試期間內，重複上傳資產，以執行AEM Assets程式的效能測試。

1. **入門要求**

   對於資產效能測試，您的客戶成功工程師將在Author to Stage環境登錄期間建立`cloudmanager`用戶（和密碼）。 效能測試步驟需要名為`cloudmanager`的用戶以及由CSE設定的相關密碼。 這不應從「作者」移除，也不應變更為權限。 這樣做很可能會失敗「資產」效能測試。

1. **影像和資產以進行測試**

   客戶可以上傳自己的資產以進行測試。 這可從「管線設定」(Pipeline Setup)或「編輯」(Edit)螢幕中完成。 JPEG、PNG、GIF和BMP等常用影像格式以及Photoshop、Illustrator和Postscript檔案都受支援。 不過，如果未上傳影像，Cloud Manager會使用預設影像和PDF檔案進行測試。

1. **分發資產以進行測試**

   每分鐘上載的每種類型的資產數量分佈在「管線設定」或「編輯」螢幕中設定。
例如，如果使用70/30分割，如下圖所示。 每分鐘上傳10個資產，每分鐘上傳7個影像和3個檔案。

1. **測試和報告**

   Cloud Manager將使用CSE在上述步驟#1（入門要求）中設定的使用者名稱和密碼，在「作者」實例上建立資料夾，並使用開放原始碼的程式庫，在資料夾中上傳資產。 由「資產」測試步驟執行的測試是使用此[開放原始碼程式庫](https://github.com/adobe/toughday2)來編寫。 每個資產的處理時間以及各種系統層級度量都會在30分鐘的測試期間內測量。 此功能可上傳影像和PDF檔案。

   >[!NOTE]
   >您可以從[配置CI/CD Pipeline](configuring-pipeline.md)瞭解有關配置效能測試的更多資訊。 請參閱[設定您的計畫](setting-up-program.md)以瞭解如何設定您的計畫並定義您的KPI。

### 效能測試結果圖{#performance-testing-results-graphs}

新的圖形和下載選項已新增至「效能測試結果」對話方塊。

當您開啟「效能測試」對話方塊時，量度面板可以展開以顯示圖形、提供下載連結或兩者。

對於[!UICONTROL Cloud Manager]版本2018.7.0，此功能適用於下列量度：

* **CPU使用率**
   * 測試期間的CPU使用率圖表。

* **磁碟I/O等待時間**
   * 測試期間磁碟I/O等待時間的圖表。

* **頁面錯誤率**
   * 測試時段內每分鐘的頁面錯誤圖表。
   * 列出測試期間產生錯誤的頁面的CSV檔案。

* **磁碟頻寬利用率**
   * 測試期間磁碟頻寬利用率的圖表。

* **網路頻寬利用率**
   * 測試期間的網路頻寬利用率圖。

* **峰值響應時間**
   * 測試時段內每分鐘的尖峰回應時間圖表。

* **第95個百分位數的回應時間**
   * 測試時段內每分鐘第95個百分位數回應時間的圖表。
   * 一個CSV檔案，列出第95個百分位元回應時間超過定義之KPI的頁面。

以下影像顯示效能測試圖：

![](assets/understand_test-results-screen1.png)

![](assets/screen_shot_2018-09-05at83933pm.png)
