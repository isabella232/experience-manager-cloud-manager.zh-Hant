---
title: 代碼質量測試
description: 瞭解管道的代碼質量測試如何工作以及它如何提高部署質量。
exl-id: 6a574858-a30e-4768-bafc-8fe79f928294
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '2863'
ht-degree: 3%

---


# 代碼質量測試 {#code-quality-testing}

瞭解管道的代碼質量測試如何工作以及它如何提高部署質量。

## 簡介 {#introduction}

在管道執行期間，將捕獲多個度量，並將其與業務所有者定義的關鍵績效指標(KPI)或與Adobe Managed Services設定的標準進行比較。

這些報告採用三級評級系統。

## 三層評級 {#three-tiered-ratings}

有三道門正在鋪設中：

* 代碼質量
* 效能測試
* 安全測試

對於每個門，都有一個三層結構來處理由門確定的問題。

* **關鍵**  — 這些問題導致管道立即失效。
* **重要**  — 這些問題導致管道進入暫停狀態。 部署經理、項目經理或業務所有者可以覆蓋問題，在這種情況下，管道將繼續，或者他們可以接受問題，在這種情況下，管道將因失敗而停止。 重要故障的覆蓋受 [超時。](/help/using/code-deployment.md#timeouts)
* **資訊**  — 這些問題純粹是為了提供資訊而提供的，對管道執行沒有影響。

>[!NOTE]
>
>在僅代碼質量管線中，不能覆蓋代碼質量門中的重要故障，因為代碼質量測試步驟是管線中的最後一步。

## 代碼質量測試 {#code-quality-testing-step}

此步驟評估應用程式碼的質量，這是僅代碼質量管道的主要目的，並在所有非生產和生產管道的生成步驟後立即執行。 請參閱文檔 [配置非生產管道](/help/using/non-production-pipelines.md) 來瞭解更多資訊。

代碼質量測試掃描原始碼以確保它滿足某些質量標準。 這通過SonarQube分析、使用OakPAL的內容包級別檢查和使用Dispatcher Optimization Tool的調度器驗證的組合來實現。

有100多個規則將通用Java規則和特定AEM規則組合在一起。 某些特AEM定規則是根據工程部門的最AEM佳做法建立的，稱為 [自定義代碼質量規則。](/help/using/custom-code-quality-rules.md)

>[!TIP]
>
>您可以下載規則的完整清單 [使用此連結。](/help/assets/CodeQuality-rules-latest-AMS.xlsx)

代碼質量測試的結果以本表概述的等級形式提供。

| 名稱 | 定義 | 類別 | 故障閾值 |
|--- |--- |--- |--- |
| 安全等級 | A =無漏洞<br/>B =至少1個次要漏洞<br/>C =至少1個主要漏洞<br/>D =至少1個嚴重漏洞<br/>E =至少1個阻止程式漏洞 | 關鍵 | &lt; B |
| 可靠性評級 | A =無錯誤<br/>B =至少1個次要錯誤 <br/>C =至少1個主要錯誤<br/>D =至少1個嚴重錯誤<br/>E =至少1個阻止程式錯誤 | 重要 | &lt; C |
| 可維護性評級 | 由代碼氣味的未清補救成本定義，該成本佔已進入應用程式的時間的百分比<br/><ul><li>A = &lt;=5%</li><li>B = 6-10%</li><li>C = 11-20%</li><li>D = 21-50%</li><li>E = >50%</li></ul> | 重要 | &lt; A |
| 適用範圍 | 由單位test行覆蓋和條件覆蓋的混合使用公式定義： <br/>`Coverage = (CT + CF + LC) / (2 * B + EL)`  <ul><li>`CT` =已評估為 `true` 運行設備test時至少一次</li><li>`CF` =已評估為 `false` 運行設備test時至少一次</li><li>`LC` =覆蓋行=行到覆蓋 — 未覆蓋行</li><li>`B` =條件總數</li><li>`EL` =可執行行（行到封面）總數</li></ul> | 重要 | &lt; 50% |
| 跳過的設備Test | 跳過的設備test數 | 資訊 | > 1 |
| 未解決問題 | 總體問題類型 — 漏洞、錯誤和代碼氣味 | 資訊 | > 0 |
| 重複行 | 定義為重複塊中涉及的行數。 在以下情況下，代碼塊被視為重複。<br>非Java項目：<ul><li>至少應有100個連續和重複的令牌。</li><li>這些令牌至少應該分佈在以下幾個方面： </li><li>COBOL的30行代碼 </li><li>ABAP的20行代碼 </li><li>10行代碼供其他語言使用</li></ul>Java項目：<ul></li><li> 不管令牌和行數多少，至少應有10個連續重複的語句。</li></ul>在檢測重複項時，將忽略縮進和字串文字中的差異。 | 資訊 | > 1% |
| Cloud Service相容性 | 確定的Cloud Service相容性問題數 | 資訊 | > 0 |

>[!NOTE]
>
>請參閱 [SonarQube的度量定義](https://docs.sonarqube.org/latest/user-guide/metric-definitions/) 的子菜單。

>[!NOTE]
>
>瞭解有關由執行的自定義代碼質量規則的詳細資訊 [!UICONTROL Cloud Manager]，請參閱文檔 [自定義代碼質量規則。](custom-code-quality-rules.md)

### 處理誤報 {#dealing-with-false-positives}

質量掃描過程不完善，有時會錯誤地識別實際上沒有問題的問題。 這被稱為誤報。

在這些情況下，可以使用標準Java對原始碼進行注釋 `@SuppressWarnings` 注釋，將規則ID指定為注釋屬性。 例如，一個常見的誤報是，用於檢測硬編碼密碼的SonarQube規則在如何識別硬編碼密碼方面具有攻擊性。

以下代碼在項目中相當常AEM見，該項目具有連接到某些外部服務的代碼。

```java
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

SonarQube隨後將引發阻止程式漏洞。 但是，在查看代碼後，您會發現這不是漏洞，並且可以使用相應的規則ID對代碼進行注釋。

```java
@SuppressWarnings("squid:S2068")
@Property(label = "Service Password")
private static final String PROP_SERVICE_PASSWORD = "password";
```

但是，如果代碼是這樣的：

```java
@Property(label = "Service Password", value = "mysecretpassword")
private static final String PROP_SERVICE_PASSWORD = "password";
```

然後，正確的解決方案是刪除硬編碼密碼。

>[!NOTE]
>
>雖然這是最好的做法 `@SuppressWarnings` 注釋盡可能特定（即僅注釋導致問題的特定語句或塊），可以在類級別進行注釋。

## 安全測試 {#security-testing}

[!UICONTROL Cloud Manager] 在部署後AEM對登台環境運行現有安全健康檢查，並通過UI報告狀態。 從環境中的所AEM有實例聚合結果。

這些相同的運行狀況檢查可以通過Web控制台或操作儀表板隨時執行。

如果任何實例報告給定運行狀況檢查的失敗，則整個環境將不通過該運行狀況檢查。 與代碼質量和效能測試一樣，這些運行狀況檢查按類別組織，並使用三層門控系統進行報告。 唯一的區別是在安全測試中沒有閾值。 所有運行狀況檢查都通過或失敗。

下表列出了運行狀況檢查。

| 名稱 | 運行狀況檢查實施 | 類別 |
|---|---|---|
| 反序列化防火牆連接API就緒性處於可接受狀態。 | [還原序列化防火牆附加 API 整備](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html#security) | 關鍵 |
| 反序列化防火牆功能正常。 | [還原序列化防火牆已作用](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html#security) | 關鍵 |
| 已載入反序列化防火牆。 | [還原序列化防火牆已載入](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/mitigating-serialization-issues.html#security) | 關鍵 |
| `AuthorizableNodeName` 實現不會在節點名稱/路徑中公開可授權ID。 | [可授權節點名稱產生](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#security) | 關鍵 |
| 預設密碼已更改。 | [預設登入帳戶](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html#users-and-groups-in-aem) | 關鍵 |
| Sling預設GETservlet受DOS攻擊的保護。 | Sling Get Servlet | 關鍵 |
| Sling Java指令碼處理程式已正確配置。 | Sling Java 指令碼處理常式 | 關鍵 |
| Sling JSP指令碼處理程式已正確配置。 | Sling JSP指令碼處理程式 | 關鍵 |
| SSL配置正確。 | SSL 設定 | 關鍵 |
| 找不到明顯不安全的用戶配置檔案策略。 | 使用者設定檔預設存取 | 關鍵 |
| 配置Sling引用過濾器以防止CSRF攻擊。 | [Sling 查閱者篩選](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#security) | 重要 |
| Adobe花崗岩HTML庫管理器已正確配置。 | CQ HTML 文件庫管理員組態 | 重要 |
| 已禁用CRXDE支援包。 | CRXDE 支援 | 重要 |
| 已禁用Sling DavEx捆綁包和Servlet。 | DavEx 健康狀態檢查 | 重要 |
| 未安裝示例內容。 | 範例內容封裝 | 重要 |
| WCM請求篩選器和WCM調試篩選器都被禁用。 | [WCM 篩選設定](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/osgi-configuration-settings.html#configuring) | 重要 |
| Sling WebDAV捆綁包和Servlet已正確配置。 | WebDAV 健康狀態檢查 | 重要 |
| Web伺服器已配置為防止點擊劫持。 | Web 伺服器組態 | 重要 |
| 複製未使用 `admin` 。 | 複寫及傳輸使用者 | 資訊 |

## 效能測試 {#performance-testing}

### AEM Sites {#aem-sites}

Cloud Manager對AEM Sites程式執行效能測試。 效能test通過旋轉虛擬用戶（容器）來運行大約30分鐘，虛擬用戶（容器）模擬實際用戶訪問臨時環境中的頁面以模擬流量。 這些頁是使用Crawler找到的。

#### 虛擬用戶 {#virtual-users}

由Cloud Manager啟動的虛擬用戶或容器數由用戶定義的KPI（響應時間和頁面視圖/分鐘）驅動， **業務所有者** 角色 [建立或編輯程式。](/help/getting-started/program-setup.md) 根據定義的KPI，最多將分解10個模擬實際用戶的容器。 選擇用於測試的頁被拆分並分配給每個虛擬用戶。

#### 爬網程式 {#crawler}

在30分鐘test期開始之前，Cloud Manager將使用由客戶成功工程師配置的一組或多個種子URL來爬網登台環境。 從這些URL開始，檢查每個頁面的HTML，並以寬度優先的方式遍歷連結。

* 預設情況下，此搜索過程最多限制為5000頁。
* 通過設定 [環境變數](/help/getting-started/build-environment.md#environment-variables) `MAX_PAGES`。
   * 允許的值為 `2000` - `7000`。
* 來自Crawler的請求的固定超時為10秒。

#### 測試頁集 {#page-sets}

頁面由三個頁面集選擇。 Cloud Manager使用跨生產和登台環AEM境實例的訪問日誌來確定以下儲存桶。

* **熱門即時頁面**  — 選擇此選項可確保測試即時客戶訪問的最熱門頁面。 Cloud Manager將讀取訪問日誌，並確定即時客戶訪問量最大的25個頁面，以生成頂級清單 `Popular Live Pages`。 這些交集在轉移環境中也存在，然後在轉移環境上爬網。

* **其他即時頁**  — 選擇此選項可確保對位於前25個熱門活動頁面之外的頁面進行測試，這些頁面可能不受歡迎，但對test很重要。 與常用即時頁類似，這些頁面從訪問日誌中提取，並且必須也存在於暫存環境中。

* **新建頁面**  — 選擇此選項可以test新頁，這些新頁可能只部署到暫存，尚未部署到生產，但必須進行測試。

##### 所選頁集間通信的分佈 {#distribution-of-traffic}

您可以在 **測試** 頁籤 [管道配置。](/help/using/production-pipelines.md) 流量分配基於所選集數。 即，如果全部選擇這三個，則總頁面視圖的33%將放到每個集。 如果選擇了兩個，則每個集將佔50%。 如果選擇了一個，則100%的流量將轉到該集。

讓我們考慮一下這個例子。

* 熱門即時頁面和新頁面集之間有50/50的分割。
* 不使用其他即時頁面。
* 新頁面集包含3000頁。
* 每分鐘頁面視圖KPI設定為200。

在30分鐘test期：

* 熱門直播頁面集中的25頁，每頁將點擊120次： `((200 * 0.5) / 25) * 30 = 120`
* 新頁面集中的3000頁每頁將點擊一次： `((200 * 0.5) / 3000) * 30 = 1`

#### 測試和報告 {#testing-reporting}

Cloud Manager在臨時發佈伺服器上以未經過身份驗證的用戶身份請求頁面，執行AEM Sites程式的效能測試，test30分鐘。 它測量虛擬用戶生成的度量（響應時間、錯誤率、每分鐘視圖等） 以及所有實例的各種系統級度量（CPU、記憶體、網路資料）。

下表總結了使用三層門控系統的效能test矩陣。

| 量度 | 類別 | 故障閾值 |
|---|---|---|
| 頁面請求錯誤率 | 關鍵 | >= 2% |
| CPU利用率 | 關鍵 | >= 80% |
| 磁碟IO等待時間 | 關鍵 | >= 50% |
| 第95個百分位響應時間 | 重要 | >=方案級KPI |
| 峰值響應時間 | 重要 | >= 18秒 |
| 每分鐘頁面視圖 | 重要 | &lt;計畫級KPI |
| 磁碟頻寬利用率 | 重要 | >= 90% |
| 網路頻寬利用率 | 重要 | >= 90% |
| 每分鐘請求數 | 資訊 | >= 6000 |

請參閱一節 [已驗證的效能測試](#authenticated-performance-testing) 有關使用基本身份驗證進行站點和資產效能測試的詳細資訊。

>[!NOTE]
>
>作者和發佈實例都在test期間受到監視。 如果未獲取某個實例的任何度量，則該度量將報告為未知，並且相應的步驟將失敗。

#### 已驗證的效能測試 {#authenticated-performance-testing}

如有必要，具有經過身份驗證的站點的AMS客戶可以指定Cloud Manager在站點效能測試期間用於訪問該網站的用戶名和密碼。

用戶名和口令被指定為具有名稱的管線變數 `CM_PERF_TEST_BASIC_USERNAME` 和 `CM_PERF_TEST_BASIC_PASSWORD`。

用戶名應儲存在 `string` 變數和口令應儲存在 `secretString` 變數。 如果同時指定了這兩個身份驗證，則效能testCrawler和test虛擬用戶的每個請求都將包含這些身份驗證作為HTTP Basic身份驗證。

要使用Cloud Manager CLI設定這些變數，請運行：

```shell
$ aio cloudmanager:set-pipeline-variables <pipeline id> --variable CM_PERF_TEST_BASIC_USERNAME <username> --secret CM_PERF_TEST_BASIC_PASSWORD <password>
```

請參閱 [修補用戶管道變數](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#operation/patchPipelineVariables) API文檔，以瞭解如何使用API。

### AEM Assets {#aem-assets}

Cloud Manager通過在30分鐘的test期內反複上載資產來執行AEM Assets程式的效能測試。

#### 入職要求 {#onboarding-requirement}

對於資產效能測試，您的客戶成功工程師將建立 `cloudmanager` 在將作者登錄到登台環境期間使用用戶和密碼。 效能test步驟需要調用用戶 `cloudmanager` 以及CSE設定的關聯密碼。 不應從作者實例中刪除此內容，也不應更改其權限。 這樣做可能會使資產效能測試失敗。

#### 用於測試的映像和資產 {#assets-for-testing}

客戶可以上傳自己的資產進行測試。 這可以通過 **管道設定** 或 **編輯** 的上界。 支援常用影像格式，如JPEG、PNG、GIF和BMP以及Photoshop、Illustrator和Postscript檔案。

如果未上載任何映像，Cloud Manager將使用預設映像和PDF文檔進行測試。

#### 用於測試的資產分配 {#distribution-of-assets}

在中設定了每分鐘上載的每種類型的資產數量分佈 **管道設定** 或 **編輯** 的上界。

例如，如果使用70/30剝離，並且每分鐘上載10個資產，每分鐘將上載7個影像和3個文檔。

#### 測試和報告 {#testing-and-reporting}

Cloud Manager將在作者實例上使用CSE設定的用戶名和密碼建立資料夾。 然後，使用開源庫將資源上載到資料夾。 由「資產」測試步驟運行的test使用 [開啟源庫。](https://github.com/adobe/toughday2) 每個資產的處理時間以及各種系統級度量都在30分鐘的測試持續時間內進行測量。 此功能可上載影像和PDF文檔。

>[!TIP]
>
>請參閱文檔 [配置生產管道](/help/using/production-pipelines.md) 來瞭解更多資訊。 請參閱文檔 [程式設定](/help/getting-started/program-setup.md) 瞭解如何設定程式和定義KPI。

### 效能測試結果圖 {#performance-testing-results-graphs}

中提供了許多度量 **效能Test對話框**

![度量清單](/help/assets/understand_test-results-screen1.png)

可以擴展度量面板以顯示圖形、提供到下載的連結或兩者。

![度量擴展為圖形](/help/assets/screen_shot_2018-09-05at83933pm.png)

此功能可用於以下度量。

* **CPU利用率** -test期間的CPU利用率圖

* **磁碟I/O等待時間**  — 磁碟I/O等待時間的圖表，在test期間

* **頁錯誤率** -test期間每分鐘的頁錯誤圖
   * CSV檔案列出在test期間出錯的頁

* **磁碟頻寬利用率**  — 磁碟頻寬在test期間的利用率圖

* **網路頻寬利用率**  — 網路頻寬在test期間的利用率圖

* **峰值響應時間** -test期間每分鐘的峰值響應時間圖

* **第95個百分位響應時間**  — 在test期間，每分鐘第95百分點響應時間的圖表
   * 一個CSV檔案，列出其第95百分點響應時間超過定義的KPI的頁

## 內容包掃描優化 {#content-package-scanning-optimization}

作為質量分析流程的一部分，Cloud Manager會對Maven構建生成的內容包進行分析。 Cloud Manager提供優化功能以加速此過程，當觀察到某些打包約束時，此功能非常有效。 最重要的是，對輸出單個內容包的項目執行的優化，通常稱為「全部」包，其中包含由生成生成的許多其他內容包，這些內容包被標籤為已跳過。 當Cloud Manager檢測到此方案，而不是解包「全部」包時，將直接掃描各個內容包並根據相關性對其進行排序。 例如，請考慮以下生成輸出。

* `all/myco-all-1.0.0-SNAPSHOT.zip` （內容包）
* `ui.apps/myco-ui.apps-1.0.0-SNAPSHOT.zip` （跳過的內容包）
* `ui.content/myco-ui.content-1.0.0-SNAPSHOT.zip` （跳過的內容包）

如果只有內部項 `myco-all-1.0.0-SNAPSHOT.zip` 是兩個跳過的內容包，然後掃描兩個嵌入的包，而不是「全部」內容包。

對於生成數十個嵌入式軟體包的項目，顯示此優化後每執行管道可節省10分鐘。

當「全部」內容包包含跳過的內容包和OSGi包的組合時，可能會出現特殊情況。 例如，如果 `myco-all-1.0.0-SNAPSHOT.zip` 其中包含了之前提到的兩個嵌入式軟體包以及一個或多個OSGi包，然後僅使用OSGi包構建一個新的、最小的內容包。 此包始終被命名 `cloudmanager-synthetic-jar-package` 包裝的束被放入 `/apps/cloudmanager-synthetic-installer/install`。

>[!NOTE]
>
>* 此優化不會影響部署到的包AEM。
>* 由於嵌入式內容包和跳過的內容包之間的匹配基於檔案名，因此如果多個跳過的內容包具有相同的檔案名或在嵌入時更改了檔案名，則無法執行此優化。

