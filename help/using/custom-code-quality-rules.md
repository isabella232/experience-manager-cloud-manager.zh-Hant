---
title: 自訂程式碼品質規則
description: 根據來自 AEM 工程團隊的最佳做法，了解 Cloud Manager 在程式碼品質測試過程中執行的自訂程式碼品質規則的詳細資訊。
exl-id: 7d118225-5826-434e-8869-01ee186e0754
source-git-commit: 1ba4ed6c311eeaff9c71313d265531f427ef2736
workflow-type: ht
source-wordcount: '3566'
ht-degree: 100%

---


# 自訂程式碼品質規則 {#custom-code-quality-rules}

根據來自 AEM 工程團隊的最佳做法，了解 Cloud Manager 在[程式碼品質測試過程](/help/using/code-quality-testing.md)中執行的自訂程式碼品質規則的詳細資訊。

>[!NOTE]
>
>在此提供的程式碼範例僅供說明用途。請參閱 [SonarQube 的概念文件說明](https://docs.sonarqube.org/latest/)以了解其中的概念和品質規則。

>[!NOTE]
>
>由於 Adobe 專屬資訊，完整的 SonarQube 規則無法下載。若要下載完整的規則清單，可[使用此連結。](/help/assets/CodeQuality-rules-latest-AMS.xlsx)繼續閱讀本文件以取得規則的說明和範例。

## SonarQube 規則 {#sonarqube-rules}

下節會詳細介紹由 Cloud Manager 執行的 SonarQube 規則。

### 請勿使用有潛在危險的功能 {#do-not-use-potentially-dangerous-functions}

* **索引碼**：CQRules:CWE-676
* **類型**：漏洞
* **嚴重度**：重大
* **始自**：2018.4.0 版本

方法 `Thread.stop()` 和 `Thread.interrupt()` 可能產生難以重現的問題，有時還可能產生安全性漏洞。它們的使用應受到嚴密監控和驗證。總的來說，傳遞資訊是實現類似目標的更安全的方式。

#### 不符合規範的程式碼 {#non-compliant-code}

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

#### 符合規範的程式碼 {#compliant-code}

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

### 請勿使用可能由外部控制的格式字串 {#do-not-use-format-strings-which-may-be-externally-controlled}

* **索引碼**：CQRules:CWE-134
* **類型**：漏洞
* **嚴重度**：重大
* **始自**：2018.4.0 版本

使用來自外部來源的格式字串 (例如請求參數或使用者產生的內容) 可能會讓應用程式遭受拒絕服務的攻擊。在某些情況下，格式字串可能會受到外部控制，但僅允許來自受信任的來源。

#### 不符合規範的程式碼 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text"));
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP 要求應該一定要有通訊端和連線逾時 {#http-requests-should-always-have-socket-and-connect-timeouts}

* **索引碼**：CQRules:ConnectionTimeoutMechanism
* **類型**：錯誤
* **嚴重度**：嚴重
* **始自**：2018.6.0 版本

從 AEM 應用計劃內部執行 HTTP 要求時，需確保設定適當的逾時以避免不必要的執行緒消耗，這點極為重要。不幸的是，Java™ 的預設 HTTP 用戶端 (`java.net.HttpUrlConnection`) 和常用的 Apache HTTP 元件用戶端的預設行為是永不逾時，因此必須明確設定逾時。依據最佳做法的要求，上述逾時不應超過 60 秒。

#### 不符合規範的程式碼 {#non-compliant-code-2}

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

#### 符合規範的程式碼 {#compliant-code-1}

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

### ResourceResolver 物件應該一直保持關閉 {#resourceresolver-objects-should-always-be-closed}

* **索引碼**：CQRules:CQBP-72
* **類型**：程式碼異味
* **嚴重度**：重大
* **始自**：2018.4.0 版本

`ResourceResolver` 物件 (獲自 `ResourceResolverFactory`) 會消耗系統資源。儘管現有一些措施可以在 `ResourceResolver` 不再使用時回收這些資源，但透過呼叫 `close()` 方法明確關閉任何開啟的 `ResourceResolver` 物件會更有效率。

一個常見的誤解是，不應明確關閉使用現有 JCR 工作階段建立的 `ResourceResolver` 物件，否則會關閉基本的 JCR 工作階段。情況並非如此。無論 `ResourceResolver` 如何開啟，不使用時都經將其關閉。由於 `ResourceResolver` 實作 `Closeable` 介面，也有可能使用 `try-with-resources` 語法而不是明確地叫用 `close()`。

#### 不符合規範的程式碼 {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### 符合規範的程式碼 {#compliant-code-2}

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

### 請勿使用 Sling Servlet 路徑來註冊 Servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

* **索引碼**：CQRules:CQBP-75
* **類型**：程式碼異味
* **嚴重度**：重大
* **始自**：2018.4.0 版本

如同在 [Sling 文件紀錄](https://sling.apache.org/documentation/the-sling-engine/servlets.html)中的說明，不建議按路徑繫結 servlet。路徑繫結的 servlet 不能使用標準的 JCR 存取控制，因此需要額外嚴格的安全性。建議不要使用路徑繫結的 servlet，而是在存放庫中建立節點並按資源類型註冊 servlet。

#### 不符合規範的程式碼 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 應將攔截到的例外狀況記錄或擲回，而非兩者。 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

* **索引碼**：CQRules:CQBP-44---CatchAndEitherLogOrThrow
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

一般而言，應該只記錄一次例外狀況。記錄多次例外狀況可能會導致混淆，因為會不清楚發生了多少次例外狀況。會導致這種情況的最常見模式是將攔截到的例外狀況記錄並擲回。

#### 不符合規範的程式碼 {#non-compliant-code-6}

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

#### 符合規範的程式碼 {#compliant-code-3}

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

### 避免 Log 陳述式後緊跟著 Throw 陳述式 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

* **索引碼**：CQRules:CQBP-44---ConsecutivelyLogAndThrow
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

另一個要避免的常見模式是記錄一則訊息後立即擲回例外狀況。此做法通常表示例外狀況訊息最終會在記錄檔案中重複。

#### 不符合規範的程式碼 {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### 符合規範的程式碼 {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### 處理 GET 或 HEAD 要求時避免在 INFO 上記錄 {#avoid-logging-at-info-when-handling-get-or-head-requests}

* **索引碼**：CQRules:CQBP-44---LogInfoInGetOrHeadRequests
* **類型**：程式碼異味
* **嚴重度**：輕微

一般而言，應該使用 INFO 紀錄層級來區分重要操作，並且預設情況下，會將 AEM 設定為在 INFO 或以上層級記錄。GET 和 HEAD 方法應僅能唯讀操作，因此不構成重要操作。在 INFO 層級記錄以回應 GET 或 HEAD 要求可能會產生大量記錄雜訊，而使得在記錄檔中識別有用資訊變得更加困難。在處理 GET 或 HEAD 要求時若出現錯誤，應該在 WARN 或 ERROR 層級進行記錄，或者若是更深入的疑難排解資訊會有幫助，則應在 DEBUG 或 TRACE 層級進行。

>[!NOTE]
>
>這不適用於每個請求的 access.log-type 記錄。

#### 不符合規範的程式碼 {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### 符合規範的程式碼 {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### 請勿使用 Exception.getMessage() 作為紀錄陳述式的第一個參數。 {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

* **索引碼**：CQRules:CQBP-44---ExceptionGetMessageIsFirstLogParam
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

依據最佳做法的要求，紀錄訊息應提供有關應用計劃中發生例外狀況的位置的內容相關資訊。雖然也可以透過使用堆疊追蹤來確定內容，但記錄訊息通常將更容易讀取和理解。因此，在記錄例外狀況時，將例外狀況的訊息當成記錄訊息來使用是不好的做法。例外狀況訊息會包含所發生的問題，而記錄訊息則應該用於告知記錄讀取程式例外狀況發生時應用程式正在做什麼。例外狀況訊息仍會記錄。透過指定您自己的訊息，更容易理解這些紀錄。

#### 不符合規範的程式碼 {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### 符合規範的程式碼 {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 登入 Catch 區塊應在 WARN 或 ERROR 層級 {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

* **索引碼**：CQRules:CQBP-44---WrongLogLevelInCatchBlock
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

顧名思義，在例外情況下，始終都應該使用 Java™ 例外狀況。因此，當攔截到例外狀況時，確保將紀錄訊息記錄在以下適當層級非常重要：WARN 或 ERROR。這可確保這些訊息正確地顯示在紀錄中。

#### 不符合規範的程式碼 {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### 符合規範的程式碼 {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不可將堆疊追踪列印到控制台 {#do-not-print-stack-traces-to-the-console}

* **索引碼**：CQRules:CQBP-44---ExceptionPrintStackTrace
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

在了解紀錄訊息時，內容極為重要。使用 `Exception.printStackTrace()` 只會導致堆疊追蹤輸出至標準錯誤串流，而遺失所有內容。此外，在像 AEM 這類多執行緒應用程式中，如果使用此方法同時列印多個例外狀況，它們的堆疊追踪可能會重疊，從而產生嚴重的混亂。僅能透過紀錄架構記錄例外狀況。

#### 不符合規範的程式碼 {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### 符合規範的程式碼 {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 不可輸出到標準輸出或標準錯誤 {#do-not-output-to-standard-output-or-standard-error}

* **索引碼**：CQRules:CQBP-44—LogLevelConsolePrinters
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

應該永遠都透過紀錄架構 SLF4J 完成登入 AEM。直接輸出到標準輸出或標準錯誤串流會遺失紀錄架構提供的結構和相關內容資訊，而且有時還可能導致效能問題。

#### 不符合規範的程式碼 {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### 符合規範的程式碼 {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### 避免硬式編碼 /應用計劃和 /libs 路徑 {#avoid-hardcoded-apps-and-libs-paths}

* **索引碼**：CQRules:CQBP-71
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2018.4.0 版本

一般而言，以 `/libs` 和 `/apps` 開頭的路徑不應為硬式編碼，因為它們引用的路徑最常儲存為和 Sling 搜尋路徑 (預設情況下會設定為 `/libs,/apps`) 相關的路徑。使用絕對路徑可能會引進難以察覺的缺陷，而且只會在專案生命週期的後期出現。

#### 不符合規範的程式碼 {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### 符合規範的程式碼 {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```

### 不應使用 Sling 排程器 {#sonarqube-sling-scheduler}

* **索引碼**：CQRules:AMSCORE-554
* **類型**：程式碼異味/雲端服務相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

請勿將 Sling 排程器用於要求保證執行的任務。Sling 已排程的作業可保證執行並更適合叢集和非叢集環境。

若要了解如何在叢集環境中處理 Sling 作業的詳細資訊，請參閱 [Apache Sling 事件和作業處理文件](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html)。

### 不應使用 AEM 已過時的 API {#sonarqube-aem-deprecated}

* **索引碼**：AMSCORE-553
* **類型**：程式碼異味/雲端服務相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

AEM API 表面經過不斷修正，以識別不鼓勵使用並因此被視為已過時的 API。

通常，會使用標準 Java™ *@Deprecated* 註解來取代這些 API，而且會由 `squid:CallToDeprecatedMethod` 進行識別。

但是，在某些情況下，API 在 AEM 的內容中會遭到取代，但在其他內容中卻可能不會。此規則會識別此第二分類。

## OakPAL 內容規則 {#oakpal-rules}

下節會詳細介紹由 Cloud Manager 執行的 OakPAL 檢查。

>[!NOTE]
>
>OakPAL 是一種架構，會使用獨立的 Oak 存放庫來驗證內容套件。它是由 AEM 合作夥伴開發出來的，並榮獲 2019 年 AEM Rockstar 北美獎。

### 客戶不應實作或擴展有 @ProviderType 註解的產品 API {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

* **索引碼**：CQBP-84
* **類型**：錯誤
* **嚴重度**：嚴重
* **始自**：2018.7.0 版本

AEM API 包含 Java™ 介面和類別，這些介面和類別僅能由自訂程式碼使用，但不能實作。例如，介面 `com.day.cq.wcm.api.Page` 僅由 AEM 實作。

將新方法新增到這些介面時，這些附加方法不會影響使用這些介面的現有程式碼，因此，在這些介面中新增新方法會被視為向後相容。但是，如果自訂程式碼實作其中一個介面，該自訂程式碼會給客戶帶來向後相容性風險。

只打算由 AEM 實作的介面和分類會使用 `org.osgi.annotation.versioning.ProviderType` 進行註解，或有時會使用類似的舊註解 `aQute.bnd.annotation.ProviderType`。此規則會識別實作此類介面或由自訂程式碼擴展的分類的情況。

#### 不符合規範的程式碼 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### 客戶套件不應在 /libs 下建立或修改節點 {#oakpal-customer-package}

* **索引碼**：BannedPath
* **類型**：錯誤
* **嚴重度**：阻斷因素
* **始自**：2019.6.0 版本

客戶應將 AEM 內容存放庫中的 `/libs` 內容樹視為唯讀，這是一個存在已久的最佳做法。修改 `/libs` 下的節點和屬性都會對大幅和小幅更新產生顯著風險。對 `/libs` 的修改應該只能由 Adobe 透過正式通道進行。

### 套件不應包含重複的 OSGi 設定 {#oakpal-package-osgi}

* **索引碼**：DuplicateOsgiConfigurations
* **類型**：錯誤
* **嚴重度**：重大
* **始自**：2019.6.0 版本

複雜專案中會出現的一個常見問題是多次設定同一個 OSGi 元件。這會產生模稜兩可的結果，無法確定哪個設定是可操作的。此規則為「執行模式感知」，因為它只會識別在同一執行模式或多個執行模式組合中多次設定相同元件的問題。

#### 不符合規範的程式碼 {#non-compliant-code-osgi}

```text
+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 符合規範的程式碼 {#compliant-code-osgi}

```text
+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### 設定和安裝檔案夾應只包含 OSGi 節點 {#oakpal-config-install}

* **索引碼碼**：ConfigAndInstallShouldOnlyContainOsgiNodes
* **類型**：錯誤
* **嚴重度**：重大
* **始自**：2019.6.0 版本

由於安全的理由，包含 `/config/` 和 `/install/` 的路徑只有 AEM 中的管理員使用者可讀取，並且僅能用於 OSGi 設定和 OSGi 套裝。將其他類型的內容放在包含這些區段的路徑下會導致應用計劃行為在管理員使用者和非管理員使用者之間無意間發生變化。

一個常見問題是在元件對話框中或在為內嵌編輯指定 RTF 文字編輯器設定時會使用名為 `config` 的節點。若要解決此問題，應將違規節點重新命名為合規名稱。對於 RTF 文字編輯器設定，請使用 `configPath` 屬性 (在 `cq:inplaceEditing` 節點上) 來指定新位置。

#### 不符合規範的程式碼 {#non-compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### 符合規範的程式碼 {#compliant-code-config-install}

```text
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### 套件不應重疊 {#oakpal-no-overlap}

* **索引碼**：PackageOverlaps
* **類型**：錯誤
* **嚴重度**：重大
* **始自**：2019.6.0 版本

類似[套件不應包含重複的 OSGi 設定規則，](#oakpal-package-osgi)這是複雜專案中常見的問題，這類專案會由多個單獨的內容套件寫入相同的節點路徑。雖然使用內容套件相依性可用於確保一致的結果，但最好還是完全避免重疊。

### 預設的撰寫模式不應該是 Classic UI {#oakpal-default-authoring}

* **索引碼**：ClassicUIAuthoringMode
* **類型**：程式碼異味/雲端服務相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

OSGi 設定 `com.day.cq.wcm.core.impl.AuthoringUIModeServiceImpl` 會定義 AEM 中的預設撰寫模式。由於從 AEM 6.4 起，Classic UI 就已被取代，若將預設的撰寫模式設定為 Classic UI，將會產生問題。

### 包含對話框的元件應該有 Touch UI 對話框 {#oakpal-components-dialogs}

* **索引碼**：ComponentWithOnlyClassicUIDialog
* **類型**：程式碼異味/雲端服務相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

有 Classic UI 對話框的 AEM 元件應該隨時有相對應的 Touch UI 對話框，既能提供最佳撰寫體驗，又能和不支援 Classic UI 的雲端服務部署模式相容。本規則可證實以下情境：

* 具有 Classic UI 對話框 (即 `dialog` 子節點) 的元件必須具有相對應的 Touch UI 對話框 (即 `cq:dialog` 子節點)。
* 具有 Classic UI 設計對話框 (即 `design_dialog` 節點) 的元件必須具有相對應的 Touch UI 對話框 (即 `cq:design_dialog` 子節點)。
* 同時具有 Classic UI 對話框以及 Classic UI 設計對話框的元件必須同時有相對應的 Touch UI 對話框以及相對應的 Touch UI 設計對話框。

AEM 現代化工具文件提供了有關如何將元件從 Classic UI 轉換為 Touch UI 的詳細資訊和工具。如需更多詳細資訊，請參閱 [AEM 現代化工具文件](https://opensource.adobe.com/aem-modernize-tools/)。

### 套件不應該混合可變和不可變的內容 {#oakpal-packages-immutable}

* **索引碼**：ImmutableMutableMixedPackage
* **類型**：程式碼異味/雲端服務相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

為了和雲端服務部署模式相容，個別內容套件必須包含存放庫不可變區域 (即 `/apps` 和 `/libs`) 或可變區域 (即不在 `/apps` 或 `/libs` 中的所有內容) 的內容，但不能同時包含兩者。例如，同時包含 `/apps/myco/components/text and /etc/clientlibs/myco` 的套件和雲端服務不相容，並會導致需通報的問題。

如需更多詳細資訊，請參閱 [AEM 專案結構文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html)。

>[!NOTE]
>
>此[客戶套件不應在 /libs 下建立或修改節點](#oakpal-customer-package)規則永遠適用。

### 不應使用反向複寫代理程式 {#oakpal-reverse-replication}

* **索引碼**：ReverseReplication
* **類型**：程式碼異味/雲端服務相容性
* **嚴重度**：輕微
* **始自**：2020.5.0 版本

雲端服務部署中不支援反向複寫，如下所述：[發行說明：移除複寫代理程式。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/aem-cloud-changes.html#replication-agents)

使用反向複寫的客戶應和 Adobe&#x200B; 聯絡，以獲取替代解決方案。

### 已啟用 Proxy 的用戶端資料庫中所包含的資源應位於名為資源的檔案夾中 {#oakpal-resources-proxy}

* **索引碼**：ClientlibProxyResource
* **類型**：錯誤
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

AEM 用戶端資料庫可能包含影像和字體之類的靜態資源如[使用用戶端資料庫文件](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html#using-preprocessors)中所述，使用透過 Proxy 的用戶端資料庫時，這些靜態資源必須包含在名為 `resources` 的子檔案夾中，以便在發佈執行個體上有效地引用。

#### 不符合規範的程式碼 {#non-compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + images
        + myimage.jpg
```

#### 符合規範的程式碼 {#compliant-proxy-enabled}

```text
+ apps
  + projectA
    + clientlib
      - allowProxy=true
      + resources
        + myimage.jpg
```

### 雲端服務的用法和工作流程不相容 {#oakpal-usage-cloud-service}

* **索引碼**：CloudServiceIncompatibleWorkflowProcess
* **類型**：程式碼異味
* **嚴重度**：阻斷因素
* **始自**：2021.2.0 版本

隨著在 AEM Cloud Service 上移動到資產微服務以進行資產處理，在 AEM 的內部部署和 AMS 版本中使用的多個工作流程已變得不受支援或不必要。

[AEM Assets as a Cloud Service GitHub 存放庫](https://github.com/adobe/aem-cloud-migration)中的遷移工具可在遷移至 AEM as a Cloud Service 期間用於更新工作流程模式。

### 不建議使用靜態範本而支援可編輯範本 {#oakpal-static-template}

* **索引碼**：StaticTemplateUsage
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

雖然靜態範本的使用歷來常見於 AEM 專案，但強烈建議使用可編輯範本，因為它們可提供最大的靈活度並支援靜態範本中不存在的附加功能。在以下連結中可找到更多資訊：[頁面範本 - 可編輯文件。](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/templates/page-templates-editable.html)

使用 [AEM 現代化工具](https://opensource.adobe.com/aem-modernize-tools/)可將從靜態範本到可編輯範本的遷移大幅自動化。

### 不建議使用舊版基礎元件 {#oakpal-usage-legacy}

* **索引碼**：LegacyFoundationComponentUsage
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版

舊版基礎元件 (即 `/libs/foundation` 下的元件) 已在多個 AEM 版本中被取代，以支持[核心元件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 不建議使用舊版基礎元件作為自訂元件的基礎 (無論是透過覆蓋還是繼承)，並應轉換為相對應的核心元件。

[AEM 現代化工具](https://opensource.adobe.com/aem-modernize-tools/)可有助於這種轉換。

### 僅應使用受支援的執行模式名稱和順序 {#oakpal-supported-runmodes}

* **索引碼**：SupportedRunmode
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

AEM Cloud Service 對執行模式名稱實施嚴格的命名原則，並對這些執行模式要求嚴格的排序。受支援的執行模式清單可在[部署到 AEM as a Cloud Service 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html#runmodes)中找到，任何與此的偏離都將被識別為問題。

### 自訂搜尋索引定義節點必須是 /oak:index 的直接子節點 {#oakpal-custom-search}

* **索引碼**：OakIndexLocation
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

AEM Cloud Service 要求自訂搜尋索引定義 (即類型 `oak:QueryIndexDefinition` 的節點) 是 `/oak:index` 的直接子節點。必須移動其他位置中的索引才能和 AEM Cloud Service 相容。有關搜尋索引的更多資訊可在以下連結中找到：[內容搜尋和索引文件。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html)

### 自訂搜尋索引定義節點的 compatVersion 必須為 2 {#oakpal-custom-search-compatVersion}

* **索引碼**：IndexCompatVersion
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

AEM Cloud Service 要求自訂搜尋索引定義 (即類型 `oak:QueryIndexDefinition` 的節點) 必須將 `compatVersion` 屬性設定為 `2`。AEM Cloud Service 並不支援任何其他值。有關搜尋索引的更多資訊可在以下連結中找到：[內容搜尋和索引文件。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html)

### 自訂搜尋索引定義節點的下階節點必須屬於 nt:unstructured 類型 {#oakpal-descendent-nodes}

* **索引碼**：IndexDescendantNodeType
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

當自訂搜尋索引定義節點具有無序子節點時，可能會出現難以解決的問題。若要避免出現這類節點，建議 `oak:QueryIndexDefinition` 節點的所有下階節點屬於 `nt:unstructured` 類型。

### 自訂搜尋索引定義節點必須包含名為 indexRules 並有子系的子節點 {#oakpal-custom-search-index}

* **索引碼**：IndexRulesNode
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

正確定義的自訂搜尋索引定義節點必須包含一個名為 `indexRules` 的子節點，而該子節點又必須至少有一個子系。在以下連結中可找到更多資訊：[Oak 文件。](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

### 自訂搜尋索引定義節點必須遵循命名慣例 {#oakpal-custom-search-definitions}

* **索引碼**：IndexName
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

AEM Cloud Service 要求自訂搜尋索引定義 (即 `oak:QueryIndexDefinition` 類型的節點) 必須按照以下說明的特定模式命名：[內容搜尋和索引。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use)

### 自訂搜尋索引定義節點必須使用索引類型 lucene  {#oakpal-index-type-lucene}

* **索引碼**：IndexType
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

AEM Cloud Service 要求自訂搜尋索引定義 (即類型 `oak:QueryIndexDefinition` 的節點) 必須具備 `type` 屬性，且值設定為 `lucene`。在遷移到 AEM Cloud Service 之前，必須更新使用舊式索引類型的索引。如需詳細資訊，請參閱[內容搜尋和索引文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use)。

### 自訂搜尋索引定義節點不得包含名為 seed 的屬性 {#oakpal-property-name-seed}

* **索引碼**：IndexSeedProperty
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

AEM Cloud Service 禁止自訂搜尋索引定義 (即 `oak:QueryIndexDefinition` 類型的節點) 包含名為 `seed` 的屬性。在遷移到 AEM Cloud Service 之前，必須更新使用此屬性的索引。如需詳細資訊，請參閱[內容搜尋和索引文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use)。

### 自訂搜尋索引定義節點不得包含名為 reindex 的屬性 {#oakpal-reindex-property}

* **索引碼**：IndexReindexProperty
* **類型**：程式碼異味
* **嚴重度**：輕微
* **始自**：2021.2.0 版本

AEM Cloud Service 禁止自訂搜尋索引定義 (即 `oak:QueryIndexDefinition` 類型的節點) 包含名為 `reindex` 的屬性。在遷移到 AEM Cloud Service 之前，必須更新使用此屬性的索引。如需詳細資訊，請參閱[內容搜尋和索引文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/operations/indexing.html#how-to-use)。

## Dispatcher 最佳化工具 {#dispatcher-optimization-tool-rules}

下節會包含由 Cloud Manager 執行的 Dispatcher 最佳化工具 (DOT) 檢查清單。請依照每個檢查的連結查看其 GitHub 定義和詳細資訊。

* [Dispatcher 設定非預期權杖](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unexpected-tokens)

* [Dispatcher 設定和引述不相符](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-unmatched-quote)

* [Dispatcher 設定遺漏大括弧](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-brace)

* [Dispatcher 設定額外大括弧](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-extra-brace)

* [Dispatcher 設定遺漏強制屬性](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-missing-mandatory-property)

* [Dispatcher 設定過時的屬性](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-deprecated-property)

* [未找到 Dispatcher 設定](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-not-found)

* [未找到 Httpd 設定包含檔案](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---httpd-configuration-include-file-not-found)

* [Dispatcher 設定一般](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---parsing-violation---dispatcher-configuration-general)

* [Dispatcher 發佈伺服器陣列快取應啟用 serveStaleOnError](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-servestaleonerror-enabled)

* [Dispatcher 發佈伺服器陣列篩選器應包含來自 AEM 原型 6.x.x 版本的預設否決規則](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-contain-the-default-deny-rules-from-the-6xx-version-of-the-aem-archetype)

* [Dispatcher 發佈伺服器陣列快取 statfileslevel 屬性應為 >= 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-statfileslevel-property-should-be--2)

* [Dispatcher 發佈伺服器陣列 gracePeriod 屬性應為 >= 2](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-graceperiod-property-should-be--2)

* [每個 Dispatcher 伺服器陣列都應該有唯一名稱](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---each-dispatcher-farm-should-have-a-unique-name)

* [Dispatcher 發佈伺服器陣列快取應以允許清單的方式設定其 ignoreUrlParams 規則](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-cache-should-have-its-ignoreurlparams-rules-configured-in-an-allow-list-manner)

* [Dispatcher 發佈伺服器陣列篩選器應以允許清單的方式指定允許的 Sling 選取器](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-selectors-in-an-allow-list-manner)

* [Dispatcher 發佈伺服器陣列篩選器應以允許清單的方式指定允許的 Sling 尾碼模式](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-dispatcher-publish-farm-filters-should-specify-the-allowed-sling-suffix-patterns-in-an-allow-list-manner)

* [請勿在具有根目錄路徑的 VirtualHost Directory 區段中使用「要求所有被授予」指令](https://github.com/adobe/aem-dispatcher-optimizer-tool/blob/main/docs/Rules.md#dot---the-require-all-granted-directive-should-not-be-used-in-a-virtualhost-directory-section-with-a-root-directory-path)
