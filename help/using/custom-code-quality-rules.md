---
title: 自訂程式碼品質規則
seo-title: Custom Code Quality Rules
description: 請詳閱本頁，了解Cloud Manager執行的自訂程式碼品質規則。
seo-description: Follow this page to learn about the custom code quality rules executed by Adobe Experience Manager Cloud Manager.
uuid: a7feb465-1982-46be-9e57-e67b59849579
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: d2338c74-3278-49e6-a186-6ef62362509f
feature: Code Quality Rules
exl-id: 7d118225-5826-434e-8869-01ee186e0754
source-git-commit: 0bc3e775ef2432cdb8d3bd5470953c07c6628148
workflow-type: tm+mt
source-wordcount: '3625'
ht-degree: 4%

---

# 自訂程式碼品質規則 {#custom-code-quality-rules}

>[!NOTE]
>若要了解AEMas a Cloud Service中Cloud Manager的自訂程式碼品質規則，請參閱 [此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/custom-code-quality-rules.html?lang=en#using-cloud-manager).

本頁說明由Cloud Manager根據AEM Engineering最佳實務建立而執行的自訂程式碼品質規則。

>[!NOTE]
>此處提供的程式碼範例僅供說明之用。 請參閱 [概念](https://docs.sonarqube.org/7.4/user-guide/concepts/) 了解聲納庫比的概念和質量規則。

## SonarQube規則 {#sonarqube-rules}

以下章節重點說明SonarQube規則：

### 不要使用潛在的危險功能 {#do-not-use-potentially-dangerous-functions}

**金鑰**:CQRules:CWE-676

**類型**:漏洞

**嚴重性**:主要

**自**:2018.4.0版

方法 ***Thread.stop()*** 和 ***Thread.interrupt()*** 可產生難以重制的問題，在某些情況下，還可能產生安全漏洞。它們的使用應受到嚴密監控和驗證。總的來說，傳遞資訊是實現類似目標的更安全的方式。

#### 不相容代碼 {#non-compliant-code}

```java
public class DontDoThis implements Runnable {
  private Thread thread;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    thread.stop();  // UNSAFE!
  }
 
  public void run() {
    while (true) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

#### 相容代碼 {#compliant-code}

```java
public class DoThis implements Runnable {
  private Thread thread;
  private boolean keepGoing = true;
 
  public void start() {
    thread = new Thread(this);
    thread.start();
  }
 
  public void stop() {
    keepGoing = false;
  }
 
  public void run() {
    while (this.keepGoing) {
        somethingWhichTakesAWhileToDo();
    }
  }
}
```

### 請勿使用可能受外部控制的格式字串 {#do-not-use-format-strings-which-may-be-externally-controlled}

**金鑰**:CQRules:CWE-134

**類型**:漏洞

**嚴重性**:主要

**自**:2018.4.0版

使用來自外部源的格式字串（如請求參數或用戶生成的內容）可以生成，使應用程式暴露於拒絕服務攻擊。 在某些情況下，格式字串可能受外部控制，但僅允許來自受信任的源。

#### 不相容代碼 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP要求應一律有通訊端和連線逾時 {#http-requests-should-always-have-socket-and-connect-timeouts}

**金鑰**:CQRules:ConnectionTimeoutMechanism

**類型**:錯誤

**嚴重性**:關鍵

**自**:2018.6.0版

從AEM應用程式內執行HTTP要求時，請務必確保已設定正確逾時，以避免不必要的執行緒耗用。 很可惜，Java的預設HTTP用戶端(java.net.HttpUrlConnection)和常用的Apache HTTP元件用戶端的預設行為永遠不會逾時，因此必須明確設定逾時。 此外，作為最佳實務，這些逾時不應超過60秒。

#### 不相容代碼 {#non-compliant-code-2}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void dontDoThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  HttpClient httpClient = builder.build();

  // do something with the client
}

public void dontDoThisEither() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

#### 相容代碼 {#compliant-code-1}

```java
@Reference
private HttpClientBuilderFactory httpClientBuilderFactory;
 
public void doThis() {
  HttpClientBuilder builder = httpClientBuilderFactory.newBuilder();
  RequestConfig requestConfig = RequestConfig.custom()
    .setConnectTimeout(5000)
    .setSocketTimeout(5000)
    .build();
  builder.setDefaultRequestConfig(requestConfig);
 
  HttpClient httpClient = builder.build();
   
  // do something with the client
}

public void orDoThis() {
  URL url = new URL("http://www.google.com");
  URLConnection urlConnection = url.openConnection();
  urlConnection.setConnectTimeout(5000);
  urlConnection.setReadTimeout(5000);
 
  BufferedReader in = new BufferedReader(new InputStreamReader(
    urlConnection.getInputStream()));
 
  String inputLine;
  while ((inputLine = in.readLine()) != null) {
    logger.info(inputLine);
  }
 
  in.close();
}
```

### ResourceResolver物件應一律關閉 {#resourceresolver-objects-should-always-be-closed}

**金鑰**:CQRules:CQBP-72

**類型**:代碼氣味

**嚴重性**:主要

**自**:2018.4.0版

從ResourceResolverFactory獲取的ResourceResolver對象使用系統資源。 雖然在不再使用ResourceResolver時已有可回收這些資源的措施，但通過調用close()方法來顯式關閉任何已開啟的ResourceResolver對象會更有效。

一個相對常見的誤解是，使用現有JCR會話建立的ResourceResolver對象不應顯式關閉，或者這樣將關閉基礎的JCR會話。 但情況並非如此 — 無論ResourceResolver如何開啟，只要不再使用，就應關閉。 由於ResourceResolver實現了Closeable介面，因此也可以使用try-with-resources語法，而不是顯式調用close()。

#### 不相容代碼 {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 相容代碼 {#compliant-code-2}

```java
public void doThis(Session session) throws Exception {
  ResourceResolver resolver = null;
  try {
    resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
    // do something with the resolver
  } finally {
    if (resolver != null) {
      resolver.close();
    }
  }
}

public void orDoThis(Session session) throws Exception {
  try (ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object) session))){
    // do something with the resolver
  }
}
```

### 請勿使用Sling servlet路徑來註冊servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

**金鑰**:CQRules:CQBP-75

**類型**:代碼氣味

**嚴重性**:主要

**自**:2018.4.0版

如 [Sling檔案](http://sling.apache.org/documentation/the-sling-engine/servlets.html)不建議依路徑系結servlet。 路徑綁定的servlet無法使用標準JCR訪問控制，因此需要額外的安全嚴格性。 建議您不要使用路徑限制的servlet，而是在存放庫中建立節點，並依資源類型註冊servlet。

#### 不相容代碼 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕獲的例外應記錄或拋出，但不能同時記錄或擲出 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**金鑰**:CQRules:CQBP-44—CatchAndOtherLogOrThow

**類型**:代碼氣味

**嚴重性**:次要

**自**:2018.4.0版

一般而言，例外只應記錄一次。 多次記錄例外可能會造成混淆，因為不清楚例外發生的次數。 導致此情況的最常見模式是記錄並擲回已捕捉的例外。

#### 不相容代碼 {#non-compliant-code-6}

```java
public void dontDoThis() throws Exception {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
    throw e;
  }
}
```

#### 相容代碼 {#compliant-code-3}

```java
public void doThis() {
  try {
    someOperation();
  } catch (Exception e) {
    logger.error("something went wrong", e);
  }
}

public void orDoThis() throws MyCustomException {
  try {
    someOperation();
  } catch (Exception e) {
    throw new MyCustomException(e);
  }
}
```

### 請避免後面緊接有log語句和throw語句 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**金鑰**:CQRules:CQBP-44—ConsellyLogAndThrow

**類型**:代碼氣味

**嚴重性**:次要

**自**:2018.4.0版

另一種常見的避免模式是記錄訊息，然後立即擲回例外狀況。 這通常表示異常消息將在日誌檔案中重複。

#### 不相容代碼 {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 相容代碼 {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### 處理GET或HEAD請求時，請避免登入資訊 {#avoid-logging-at-info-when-handling-get-or-head-requests}

**金鑰**:CQRules:CQBP-44—LogInfoInGetOrHeadRequests

**類型**:代碼氣味

**嚴重性**:次要

一般而言，INFO記錄層級應用來標定重要動作，且依預設，AEM會設定為在INFO層級或更高層級登入。 GET和HEAD方法只應是只讀操作，因此不構成重要行動。 響應GET或HEAD請求而以INFO級別記錄可能會產生顯著的日誌噪音，因此在日誌檔案中更難識別有用資訊。 處理GET或HEAD要求時的記錄應位於發生錯誤時的「警告」或「錯誤」層級，或位於「除錯」或「TRACE」層級（如果更深入的疑難排解資訊有幫助的話）。

>[!CAUTION]
>
>這不適用於每個請求的access.log類型記錄。

#### 不相容代碼 {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 相容代碼 {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### 請勿將Exception.getMessage()用作記錄陳述式的第一個參數 {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

**金鑰**:CQRules:CQBP-44—ExceptionGetMessageIsFirstLogParam

**類型**:代碼氣味

**嚴重性**:次要

**自**:2018.4.0版

記錄訊息應提供關於應用程式中發生例外狀況的內容資訊，此為最佳作法。 雖然上下文也可以通過使用堆棧跟蹤來確定，但通常日誌消息將更容易讀取和理解。 因此，在記錄例外時，將例外消息用作日誌消息是一種錯誤的做法，例外消息將包含出錯的內容，而日誌消息應用於告知日誌讀取器發生例外時應用程式正在執行什麼操作。 例外訊息仍會記錄；透過指定您自己的訊息，記錄將更容易理解。

#### 不相容代碼 {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 相容代碼 {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 登錄捕獲塊應處於「警告」或「錯誤」級別 {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**金鑰**:CQRules:CQBP-44—WrongLogLevelInCatchBlock

**類型**:代碼氣味

**嚴重性**:次要

**自**:2018.4.0版

如名稱所示，Java例外狀況應一律用於 *特殊* 情況。 因此，當捕獲到異常時，務必確保日誌消息記錄在適當的級別，即「警告」或「錯誤」。 這可確保這些訊息在記錄檔中正確顯示。

#### 不相容代碼 {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 相容代碼 {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不將堆棧跟蹤打印到控制台 {#do-not-print-stack-traces-to-the-console}

**金鑰**:CQRules:CQBP-44 - ExceptionPrintStackTrace

**類型**:代碼氣味

**嚴重性**:次要

**自**:2018.4.0版

如前所述，了解日誌消息時，上下文至關重要。 使用Exception.printStackTrace()導致 **僅限** 要輸出到標準錯誤流的堆棧跟蹤，從而丟失所有上下文。 此外，在諸如AEM的多線程應用程式中，如果使用此方法並行打印多個例外，則其堆棧跡線可能重疊，從而產生明顯的混淆。 只有記錄架構才應記錄例外。

#### 不相容代碼 {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 相容代碼 {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不輸出為標準輸出或標準錯誤 {#do-not-output-to-standard-output-or-standard-error}

**金鑰**:CQRules:CQBP-44—LogLevelConsolePrinters

**類型**:代碼氣味

**嚴重性**:次要

**自**:2018.4.0版

登入AEM的作業一律應透過記錄架構(SLF4J)完成。 直接輸出到標準輸出或標準錯誤流會丟失由日誌記錄框架提供的結構和上下文資訊，在某些情況下，可能會導致效能問題。

#### 不相容代碼 {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 相容代碼 {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 避免硬式編碼/apps和/libs路徑 {#avoid-hardcoded-apps-and-libs-paths}

**金鑰**:CQRules:CQBP-71

**類型**:代碼氣味

**嚴重性**:次要

**自**:2018.4.0版

一般而言，以/libs和/apps開頭的路徑不應以硬式編碼撰寫，因為它們參考的路徑最常儲存為相對於Sling搜尋路徑（預設為/libs、/apps）的路徑。 使用絕對路徑可能會引入細微缺陷，這些缺陷只會在項目生命週期的稍後出現。

#### 不相容代碼 {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 相容代碼 {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### Sling排程器不應使用 {#sonarqube-sling-scheduler}

**金鑰**:CQRules:AMSCORE-554

**類型**:代碼氣味/Cloud Service相容性

**嚴重性**:次要

**自**:2020.5.0版

Sling排程器不得用於需要保證執行的工作。 Sling排程作業可確保執行，且更適合叢集和非叢集環境。

請參閱 [Apache Sling事件和作業處理](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html) 以進一步了解在叢集環境中如何處理Sling作業。

### AEM已棄用的API不應使用 {#sonarqube-aem-deprecated}

**金鑰**:AMSCORE-553

**類型**:代碼氣味/Cloud Service相容性

**嚴重性**:次要

**自**:2020.5.0版

AEM API表面不斷修訂，以識別不建議使用且因此視為已過時的API。

在許多情況下，這些API會使用標準Java來取代 *@Deprecated* 注釋，因此，由 `squid:CallToDeprecatedMethod`.

不過，在AEM的內容中，API有時會遭到取代，但在其他內容中，API可能不會遭到取代。 此規則可識別此第二類。

## OakPAL內容規則 {#oakpal-rules}

請在OakPAL檢查下方找到由Cloud Manager執行。

>[!NOTE]
>
>OakPAL是AEM合作夥伴(2019年AEM Rockstar北美地區獲勝者)開發的架構，可使用獨立Oak存放庫驗證內容套件。

### 客戶不應實作或擴充@ProviderType註解的產品API {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

**金鑰**:CQBP-84

**類型**:錯誤

**嚴重性**:關鍵

**自**:2018.7.0版

AEM API包含Java介面和類別，這些介面和類別僅能由自訂程式碼使用，但不能實作。例如，介面 *com.day.cq.wcm.api.Page* 僅由 ***AEM實作***。

將新方法添加到這些介面時，這些附加方法不會影響使用這些介面的現有代碼，因此，在這些介面中添加新方法會被視為向後相容。但是，如果自訂程 ***式碼實作*** 其中一個介面，該自訂程式碼會給客戶帶來向後相容性風險。

僅打算由AEM實作的介面（和類）會加上註解 *org.osgi.annotation.versioning.ProviderType* (或者，在某些情況下，類似的舊式註解 *aQute.bnd.annotation.ProviderType*)。 此規則可識別由自訂程式碼實作這類介面（或擴充類別）的案例。

#### 不相容代碼 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### 客戶包不應在/libs下建立或修改節點 {#oakpal-customer-package}

**金鑰**:UnpandedPaths

**類型**:錯誤

**嚴重性**:封鎖程式

**自**:2019.6.0版

客戶應將AEM內容存放庫中的/libs內容樹狀結構視為唯讀，這是長期以來的最佳作法。 修改下的節點和屬性 */libs* 會造成重大和微幅更新的重大風險。 修改 */libs* 只能通過官方渠道進行Adobe。

### 套件不應包含重複的OSGi設定 {#oakpal-package-osgi}

**金鑰**:DuplicateOsgiConfigurations

**類型**:錯誤

**嚴重性**:主要

**自**:2019.6.0版

複雜專案中發生的常見問題是多次設定相同的OSGi元件。 這就產生了關於哪個配置可操作的模糊。 此規則「執行模式感知」，因為它只會識別在同一執行模式（或執行模式組合）中多次設定相同元件的問題。

#### 不相容代碼 {#non-compliant-code-osgi}

```
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 相容代碼 {#compliant-code-osgi}

```
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### 配置和安裝資料夾應僅包含OSGi節點 {#oakpal-config-install}

**金鑰**:ConfigAndInstallShouldOnlyContainOsgiNodes

**類型**:錯誤

**嚴重性**:主要

**自**:2019.6.0版

基於安全原因，包含 */config/和/install/* 只有AEM中的管理使用者才能閱讀，且應僅用於OSGi設定和OSGi套件組合。 將其他類型的內容置於包含這些區段的路徑之下，會導致應用程式行為，這會無意中在管理使用者和非管理使用者之間有所差異。

常見的問題是使用名為 `config` 在元件對話方塊內，或指定用於內嵌編輯的rtf編輯器設定時。 要解決此問題，應將違規節點重新命名為符合規範的名稱。 對於RTF編輯器設定，請使用 `configPath` 屬性 `cq:inplaceEditing` 節點，指定新位置。

#### 不相容代碼 {#non-compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 相容代碼 {#compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### 套件不應重疊 {#oakpal-no-overlap}

**金鑰**:封裝重疊

**類型**:錯誤

**嚴重性**:主要

**自**:2019.6.0版

類似於 *套件不應包含重複的OSGi設定* 這是複雜專案中常見的問題，其中同一個節點路徑是由多個不同的內容套件所寫入。 雖然可使用內容套件相依性來確保結果一致，但最好避免完全重疊。

### 預設編寫模式不應為傳統UI {#oakpal-default-authoring}

**金鑰**:ClassicUIAuthoringMode

**類型**:代碼氣味/Cloud Service相容性

**嚴重性**:次要

**自**:2020.5.0版

OSGi設定 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` 定義AEM中的預設製作模式。 由於AEM 6.4後即已棄用傳統UI，因此現在當將預設編寫模式設為傳統UI時，會引發問題。

### 具有對話方塊的元件應具有觸控式UI對話方塊 {#oakpal-components-dialogs}

**金鑰**:ComponentWithOnlyClassicUIDialog

**類型**:代碼氣味/Cloud Service相容性

**嚴重性**:次要

**自**:2020.5.0版

具有傳統UI對話方塊的AEM元件應一律具有對應的觸控式UI對話方塊，以提供最佳的製作體驗，並與不支援傳統UI的Cloud Service部署模型相容。 此規則會驗證下列情況：

* 具有傳統UI對話方塊的元件（即對話方塊子節點）必須具有對應的觸控式UI對話方塊(即 `cq:dialog` 子節點)。
* 具有傳統UI設計對話方塊的元件（即design_dialog節點）必須具有對應的觸控式UI設計對話方塊(即 `cq:design_dialog` 子節點)。
* 元件具有傳統UI對話方塊和傳統UI設計對話方塊，必須同時具有對應的觸控式UI對話方塊和對應的觸控式UI設計對話方塊。

AEM現代化工具檔案提供如何將元件從傳統UI轉換為觸控式UI的檔案和工具。 請參閱 [AEM現代化工具](https://opensource.adobe.com/aem-modernize-tools/pages/tools.html) 以取得更多詳細資訊。

### 套件不應混用可變和不可變內容 {#oakpal-packages-immutable}

**金鑰**:ImmutableMutableMixedPackage

**類型**:代碼氣味/Cloud Service相容性

**嚴重性**:次要

**自**:2020.5.0版

為了與Cloud Service部署模型相容，單個內容包必須包含儲存庫不可變區域(即 `/apps and /libs, although /libs` 不應由客戶代碼修改，並且會造成個別違規)或可變區域（即其他所有項目），但不能同時造成兩者。 例如，包含兩者的套件 `/apps/myco/components/text and /etc/clientlibs/myco` 與Cloud Service不相容，且會造成問題回報。

請參閱 [AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 以取得更多詳細資訊。

### 不應使用反向複製代理 {#oakpal-reverse-replication}

**金鑰**:反向複製

**類型**:代碼氣味/Cloud Service相容性

**嚴重性**:次要

**自**:2020.5.0版

Cloud Service部署中不支援反向復寫，如 [發行說明：移除復寫代理。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=en#replication-agents)

使用反向復寫的Adobe應聯絡其他解決方案的客戶。

### OakPAL — 啟用Proxy的用戶端程式庫中所包含的資源應位於名為「資源」的資料夾中 {#oakpal-resources-proxy}

**金鑰**:ClientlibProxyResource

**類型**:錯誤

**嚴重性**:次要

**自**:2021.2.0版

AEM用戶端程式庫可包含靜態資源，例如影像和字型。 如 [使用前置處理器](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html?lang=en#using-preprocessors)，使用代理用戶端程式庫時，這些靜態資源必須包含在名為「資源」的子資料夾中，才能在發佈執行個體上有效參考。

#### 不相容代碼 {#non-compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 相容代碼 {#compliant-proxy-enabled}

```
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### OakPAL — 使用Cloud Service不相容的工作流程程式 {#oakpal-usage-cloud-service}

**金鑰**:CloudServiceIncomplatedWorkflowProcess

**類型**:代碼氣味

**嚴重性**:封鎖程式

**自**:2021.2.0版

隨著移轉至AEM Cloud Service上的資產微服務進行資產處理，內部部署和AEM AMS版本中使用的數個工作流程程式，已變得不支援或不必要。 移轉工具位於 [aem-cloud-migration](https://github.com/adobe/aem-cloud-migration) 可在AEM Cloud Service移轉期間用來更新工作流程模型。

### OakPAL — 不建議使用靜態範本，改用可編輯的範本 {#oakpal-static-template}

**金鑰**:StaticTemplateUsage

**類型**:代碼氣味

**嚴重性**:次要

**自**:2021.2.0版

雖然靜態範本的使用在AEM專案中向來很常見，但強烈建議使用可編輯的範本，因為這些範本可提供最大的彈性，並支援靜態範本中未出現的其他功能。 如需詳細資訊，請參閱 [頁面範本 — 可編輯](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-editable.html?lang=en). 從靜態範本移轉至可編輯的範本，可透過 [AEM現代化工具](https://opensource.adobe.com/aem-modernize-tools/).

### OakPAL — 不建議使用舊版基礎元件 {#oakpal-usage-legacy}

**金鑰**:LegacyFoundationComponentUsage

**類型**:代碼氣味

**嚴重性**:次要

**自**:2021.2.0版

舊版基礎元件(即 `/libs/foundation`)已在數個AEM版本中遭到取代，改用WCM核心元件。 不鼓勵使用舊版基礎元件作為自訂元件的基礎（不論是透過覆蓋或繼承），且應轉換為對應的核心元件。 此轉換可由 [AEM現代化工具](https://opensource.adobe.com/aem-modernize-tools/).

### OakPAL — 僅使用支援的執行模式名稱和排序 {#oakpal-supported-runmodes}

**金鑰**:支援的運行模式

**類型**:代碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEM Cloud Service會針對執行模式名稱強制執行嚴格的命名原則，並針對這些執行模式執行嚴格的排序。 可在上找到支援的執行模式清單 [執行模式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#runmodes) 而任何偏離這一點的行為都會被認定為問題。

### OakPAL — 自訂搜尋索引定義節點必須是/oak:index的直接子節點 {#oakpal-custom-search}

**金鑰**:OakIndexLocation

**類型**:代碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEM Cloud Service要求自訂搜尋索引定義（即oak:QueryIndexDefinition類型的節點）是直接子節點 `/oak:index`. 其他位置的索引必須移動以與AEM Cloud Service相容。 有關搜索索引的更多資訊，請參見 [內容搜尋與索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en).

### OakPAL — 自訂搜尋索引定義節點必須有2版的compat {#oakpal-custom-search-compatVersion}

**金鑰**:IndexCompatVersion

**類型**:代碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEM Cloud Service要求自訂搜尋索引定義（即oak:QueryIndexDefinition類型的節點）必須將compatVersion屬性設為2。 AEM Cloud Service不支援任何其他值。 有關搜索索引的更多資訊，請參見 [內容搜尋與索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en).

### OakPAL — 自定義搜索索引定義節點的子節點類型必須為Nt:Unstructured {#oakpal-descendent-nodes}

**金鑰**:IndexDescendationNodeType

**類型**:代碼氣味

**嚴重性**:次要

**自**:2021.2.0版

當自訂搜尋索引定義節點具有無序的子節點時，可能會發生難以疑難排解的問題。 若要避免這些情況，建議 `oak:QueryIndexDefinition` 節點類型為nt:unstructured。

### OakPAL — 自訂搜尋索引定義節點必須包含具有子項的子節點，名為indexRules {#oakpal-custom-search-index}

**金鑰**:IndexRulesNode

**類型**:代碼氣味

**嚴重性**:次要

**自**:2021.2.0版

正確定義的自定義搜索索引定義節點必須包含名為indexRules的子節點，而該子節點又必須至少包含一個子節點。 如需詳細資訊，請參閱 [Oak檔案](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### OakPAL — 自訂搜尋索引定義節點必須遵循命名慣例 {#oakpal-custom-search-definitions}

**金鑰**:IndexName

**類型**:代碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEM Cloud Service要求自訂搜尋索引定義（即，類型的節點） `oak:QueryIndexDefinition`)，必須依照 [內容搜尋與索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use).

### OakPAL — 自訂搜尋索引定義節點必須使用索引類型lucene  {#oakpal-index-type-lucene}

**金鑰**:IndexType

**類型**:代碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEM Cloud Service要求自訂搜尋索引定義（即oak:QueryIndexDefinition類型的節點）具有將值設為的type屬性 **lucene**. 使用舊版索引類型建立索引之前，必須先更新。 請參閱 [內容搜尋與索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use) 以取得更多資訊。

### OakPAL — 自訂搜尋索引定義節點不得包含名為seed的屬性 {#oakpal-property-name-seed}

**金鑰**:IndexSeedProperty

**類型**:代碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEM Cloud Service禁止自訂搜尋索引定義（即，類型的節點） `oak:QueryIndexDefinition`)，從包含名為seed的屬性。 使用此屬性建立索引必須先更新，才能移轉至AEM Cloud Service。 請參閱 [內容搜尋與索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use) 以取得更多資訊。

### OakPAL — 自訂搜尋索引定義節點不得包含名為重新索引的屬性 {#oakpal-reindex-property}

**金鑰**:IndexReindexProperty

**類型**:代碼氣味

**嚴重性**:次要

**自**:2021.2.0版

AEM Cloud Service禁止自訂搜尋索引定義（即，類型的節點） `oak:QueryIndexDefinition`)，從包含名為reindex的屬性。 使用此屬性建立索引必須先更新，才能移轉至AEM Cloud Service。 請參閱 [內容搜尋與索引](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/operations/indexing.html?lang=en#how-to-use) 以取得更多資訊。

## Dispatcher最佳化工具 {#dispatcher-optimization-tool-rules}

以下章節反白標示Cloud Manager執行的DOT檢查：

* [DOT — 解析違規 — Dispatcher配置意外的Token](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unexpected-tokens)

* [DOT — 解析違規 — Dispatcher配置不匹配的引號](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unmatched-quote)

* [DOT — 解析違規 — Dispatcher配置缺少大括弧](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-brace)

* [DOT — 解析違規 — 調度程式配置大括弧](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-extra-brace)

* [DOT — 解析違規 — Dispatcher配置缺少強制屬性](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-mandatory-property)

* [DOT — 解析違規 — Dispatcher配置已廢止屬性](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-deprecated-property)

* [DOT — 解析違規 — 未找到Dispatcher配置](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-not-found)

* [DOT — 解析違規 — 未找到Httpd配置包含檔案](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---httpd-configuration-include-file-not-found)

* [DOT — 解析違規 — 調度程式配置常規](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-general)

* [DOT - Dispatcher發佈伺服器陣列快取應已啟用serveStaleOnError](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-servestaleonerror-enabled)

* [DOT - Dispatcher發佈伺服器陣列篩選器應包含來自6.x.x版AEM原型的預設拒絕規則](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-contain-the-default-deny-rules-from-the-6xx-version-of-the-aem-archetype)

* [DOT - Dispatcher發佈伺服器陣列快取狀態檔案層級屬性應為>= 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-statfileslevel-property-should-be--2)

* [DOT - Dispatcher發佈伺服器陣列gracePeriod屬性應為>= 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-graceperiod-property-should-be--2)

* [DOT — 每個Dispatcher伺服器陣列的名稱都應是唯一的](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---each-dispatcher-farm-should-have-a-unique-name)

* [DOT - Dispatcher發佈伺服器陣列快取應以允許清單方式設定其ignoreUrlParams規則](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-its-ignoreurlparams-rules-configured-in-an-allow-list-manner)

* [DOT - Dispatcher發佈伺服器陣列篩選器應以允許清單方式指定允許的Sling選取器](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-selectors-in-an-allow-list-manner)

* [DOT - Dispatcher發佈伺服器陣列篩選器應以允許清單方式指定允許的Sling尾碼模式](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-suffix-patterns-in-an-allow-list-manner)

* [DOT — 在具有根目錄路徑的VirtualHost Directory節中，不應使用「要求所有授予的」指令](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-require-all-granted-directive-should-not-be-used-in-a-virtualhost-directory-section-with-a-root-directory-path)
