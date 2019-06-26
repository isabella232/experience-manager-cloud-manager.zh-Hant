---
title: 自訂代碼品質規則
seo-title: 自訂代碼品質規則
description: 請依照此頁面來瞭解Cloud Manager執行的自訂代碼品質規則。
seo-description: 請依照本頁面瞭解Adobe Experience Manager Cloud Manager執行的自訂代碼品質規則。
uuid: a feb465-1982-46be-7-e57-e67 b59849579
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 使用
discoiquuid: d2338c74-3278-49e6-a186-6ef62362509 f
translation-type: tm+mt
source-git-commit: 4881ff8be97451aa90c3430259ce13faef182e4f

---


# Custom Code Quality Rules {#custom-code-quality-rules}

此頁面說明Cloud Manager執行的自訂代碼品質規則，以根據AEM工程的最佳實務建立。

>[!NOTE]
>
>此處提供的程式碼範例僅用於說明用途。

## SonarQube Rules {#sonarqube-rules}

下節強調Sonarque規則：

### Do not use potentially dangerous functions {#do-not-use-potentially-dangerous-functions}

**索引鍵：CQR規則：CWE-676**

**類型**：弱點

**嚴重性**：主修

**** 因為：2018.4.0版

***執行緒. stop()*** 和 ***執行緒.中斷()*** 的方法可產生難以重制的問題，有時會造成安全性弱點。應密切監控其使用情況並加以驗證。一般而言，傳遞訊息是達成類似目標的安全方式。

#### Non-Compliant Code {#non-compliant-code}

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

#### Compliant Code {#compliant-code}

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

### Do not use format strings which may be externally controlled {#do-not-use-format-strings-which-may-be-externally-controlled}

**索引鍵：CQR規則：CWE-134**

**類型**：弱點

**嚴重性**：主修

**** 因為：2018.4.0版

使用外部來源的格式字串(此類請求參數或使用者產生的內容)可讓應用程式暴露於拒絕服務攻擊。在某些情況下，格式字串可能是外部控制，但僅允許來自受信任來源。

#### Non-Compliant Code {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text");
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP requests should always have socket and connect timeouts {#http-requests-should-always-have-socket-and-connect-timeouts}

**索引鍵：CQR規則：connectionTime機制**

**類型**：Bug

**嚴重性**：重要事項

**** 因為：2018.6.0版

在AEM應用程式內執行HTTP要求時，務必確定已設定適當逾時，以避免不必要的執行緒消耗。遺憾的是，Java的預設HTTP Client(VisitPurlConnection)和常用的Apache HTTP Components用戶端的預設行為不會逾時，因此必須明確設定逾時。此外，作為最佳實務，這些逾時不應超過60秒。

#### Non-Compliant Code {#non-compliant-code-2}

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

#### Compliant Code {#compliant-code-1}

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

### Product APIs annotated with @ProviderType should not be implemented or extended by customers {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

**索引鍵：CQBP-84、CQBP-84-相依性**

**類型**：Bug

**嚴重性**：重要事項

**** 因為：2018.7.0版

AEM API包含僅供自訂程式碼使用，但未實施的Java介面和類別。For example, the interface *com.day.cq.wcm.api.Page* is designed to be implemented by ***AEM only***.

將新方法新增至這些介面時，這些額外的方法不會影響使用這些介面的現有程式碼，因此，新增這些介面的新方法會視為向後相容。However, if custom code ***implements*** one of these interfaces, that custom code has introduced a backwards-compatibility risk for the customer.

Interfaces (and classes) which are only intended to be implemented by AEM are annotated with *org.osgi.annotation.versioning.ProviderType* (or, in some cases, a similar legacy annotation *aQute.bnd.annotation.ProviderType*). 此規則可識別自訂代碼的實施(或擴充類別)的案例。

#### Non-Compliant Code {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### ResourceResolver objects should always be closed {#resourceresolver-objects-should-always-be-closed}

**索引鍵：CQR規則：CQBP-72**

**類型**：程式碼氣味

**嚴重性**：主修

**** 因為：2018.4.0版

資源從ResourceSolverFactory取得的資源使用系統資源。雖然在不再使用ResourceSolver時仍有各項措施可用來重新命名這些資源，但呼叫close()方法以明確關閉任何開啓的resourceOver物件會更有效率。

相對常見的誤解是，使用現有JCR工作階段建立的ResourceSolver物件不應明確關閉，也不應關閉基礎JCR工作階段。不是如此-不論ResourceSolver如何開啓，在不再使用時，它應該會關閉。由於ResourceSolver實作可關閉介面，因此也可以使用試用資源語法，而非明確叫用關閉()。

#### Non-Compliant Code {#non-compliant-code-4}

```java
public void dontDoThis(Session session) throws Exception {
  ResourceResolver resolver = factory.getResourceResolver(Collections.singletonMap("user.jcr.session", (Object)session));
  // do some stuff with the resolver
}
```

#### Compliant Code {#compliant-code-2}

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

### Do not use Sling servlet paths to register servlets {#do-not-use-sling-servlet-paths-to-register-servlets}

**索引鍵：CQR規則：CQBP-75**

**類型**：程式碼氣味

**嚴重性**：主修

**** 因為：2018.4.0版

As described in the [Sling documentation](http://sling.apache.org/documentation/the-sling-engine/servlets.html), bindings servlets by paths is discouraged. 路徑系結的servlet無法使用標準JCR存取控制，因此需要額外的安全性防護。建議您不要使用路徑系結servlet，而是建議在儲存庫中建立節點，並依資源類型註冊servlet。

#### Non-Compliant Code {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### Caught Exceptions should be logged or thrown, but not both {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**索引鍵：CQR規則：CQBP-44—catcheIDTherlogorrow**

**類型**：程式碼氣味

**嚴重性**：次要

**** 因為：2018.4.0版

一般而言，應記錄一次例外狀況。記錄例外次數多次可能造成混淆，因為不清楚發生例外情況多少次。導致這個現象的最常見模式就是記錄並擲出一個畫面例外。

#### Non-Compliant Code {#non-compliant-code-6}

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

#### Compliant Code {#compliant-code-3}

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

### Avoid having a log statement immediately followed by a throw statement {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**索引鍵：CQR規則：CQBP-44—consectUvelyLoggandrop**

**類型**：程式碼氣味

**嚴重性**：次要

**** 因為：2018.4.0版

另一個避免的常見模式是記錄訊息，然後立即擲出例外狀況。這通常表示例外訊息會複製到記錄檔中。

#### Non-Compliant Code {#non-compliant-code-7}

```java
public void dontDoThis() throws Exception {
  logger.error("something went wrong");
  throw new RuntimeException("something went wrong");
}
```

#### Compliant Code {#compliant-code-4}

```java
public void doThis() throws Exception {
  throw new RuntimeException("something went wrong");
}
```

### Avoid logging at INFO when handling GET or HEAD requests {#avoid-logging-at-info-when-handling-get-or-head-requests}

**索引鍵：CQR規則：CQBP-44—loginfooting etorHeadRequests**

**類型**：程式碼氣味

**嚴重性**：次要

一般而言，應使用INFO記錄層級來校准重要動作，並依預設將AEM設定為在INFO層級或更高版本中記錄。GET和HEAD方法只能是唯讀操作，因此不構成重要動作。在INFO層級記錄以回應GET或HEAD請求很可能會產生顯著的記錄雜訊，因此難以識別記錄檔中有用的資訊。處理GET或HEAD請求時，應在出現錯誤或DEBUG或DEBUG層級的問題時(如果更深入的疑難排解資訊有更多用處)，在「警告」或「錯誤」層級上進行記錄。

>[!CAUTION]
>
>這不適用於每個請求的存取. log類型記錄。

#### Non-Compliant Code {#non-compliant-code-8}

```java
public void doGet() throws Exception {
  logger.info("handling a request from the user");
}
```

#### Compliant Code {#compliant-code-5}

```java
public void doGet() throws Exception {
  logger.debug("handling a request from the user.");
}
```

### Do not use Exception.getMessage() as the first parameter of a logging statement {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

**索引鍵：CQR規則：CQBP-44—ExcertionGetMessageIsFirstLogam**

**類型**：程式碼氣味

**嚴重性**：次要

**** 因為：2018.4.0版

作為最佳實務，記錄訊息應該提供有關應用程式中發生例外情形的相關資訊。雖然內容也可以透過堆疊追蹤來判斷，一般記錄訊息要更容易閱讀和瞭解。因此，當記錄例外時，使用例外訊息作為記錄訊息是很好的做法-例外訊息將會包含發生錯誤的訊息，而應使用記錄檔訊息來告知記錄檔，當發生例外狀況時，應用程式正在執行甚麼動作。例外訊息仍將記錄；透過指定您自己的訊息，即可更容易瞭解記錄。

#### Non-Compliant Code {#non-compliant-code-9}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error(e.getMessage(), e);
  }
}
```

#### Compliant Code {#compliant-code-6}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Logging in catch blocks should be at the WARN or ERROR level {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**索引鍵：CQR規則：CQBP-44—WRonGlogInincatBlock**

**類型**：程式碼氣味

**嚴重性**：次要

**** 因為：2018.4.0版

As the name suggests, Java exceptions should always be used in *exceptional* circumstances. 因此，當擷取例外時，務必確保記錄訊息已記錄在適當層級- WARN或ERROR。如此可確保這些訊息在記錄檔中正確顯示。

#### Non-Compliant Code {#non-compliant-code-10}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.debug(e.getMessage(), e);
  }
}
```

#### Compliant Code {#compliant-code-7}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Do not print stack traces to the console {#do-not-print-stack-traces-to-the-console}

**索引鍵：CQR規則：CQBP-44—ExcertionPrintTrackTrace**

**類型**：程式碼氣味

**嚴重性**：次要

**** 因為：2018.4.0版

如前所述，在瞭解記錄訊息時，上下文很重要。Using Exception.printStackTrace() causes **only** the stack trace to be output to the standard error stream thereby losing all context. 此外，在AEM(如AEM)的多執行緒應用程式中，如果同時使用此方法列印多個例外，其堆疊追蹤可能會重疊，造成嚴重混淆。例外情形應僅透過記錄架構登入。

#### Non-Compliant Code {#non-compliant-code-11}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    e.printStackTrace();
  }
}
```

#### Compliant Code {#compliant-code-8}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Do not output to Standard Output or Standard Error {#do-not-output-to-standard-output-or-standard-error}

**索引鍵：CQR規則：CQBP-44- LogishEnablePrinters**

**類型**：程式碼氣味

**嚴重性**：次要

**** 因為：2018.4.0版

登入AEM應一律透過記錄架構(SLF4J)完成。直接輸出至標準輸出或標準錯誤串流會遺失記錄架構提供的結構與內容資訊，有時可能會造成效能問題。

#### Non-Compliant Code {#non-compliant-code-12}

```java
public void dontDoThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    System.err.println("Unable to do something");
  }
}
```

#### Compliant Code {#compliant-code-9}

```java
public void doThis() {
  try {
    someMethodThrowingAnException();
  } catch (Exception e) {
    logger.error("Unable to do something", e);
  }
}
```

### Avoid Hardcoded /apps and /libs Paths {#avoid-hardcoded-apps-and-libs-paths}

**索引鍵：CQR規則：CQBP-71**

**類型**：程式碼氣味

**嚴重性**：次要

**** 因為：2018.4.0版

一般而言，以/libs和/apps開始的路徑不應被硬式編碼為他們參照的路徑，最常被儲存為相對於Sling搜尋路徑(預設為/libs)的路徑(預設為)。使用絕對路徑可能會帶來細微的瑕疵，只會出現在專案生命週期之後。

#### Non-Compliant Code {#non-compliant-code-13}

```java
public boolean dontDoThis(Resource resource) {
  return resource.isResourceType("/libs/foundation/components/text");
}
```

#### Compliant Code {#compliant-code-10}

```java
public void doThis(Resource resource) {
  return resource.isResourceType("foundation/components/text");
}
```


## OakPAL Content Rules {#oakpal-rules}

請尋找Cloud Manager執行的OAKCal檢查。

>[!NOTE]
>OAkCal是由AEM合作夥伴開發的架構(AEM Partner North America的得主)，可透過獨立的Oak儲存庫驗證內容套件。

### Customer Packages Should Not Create or Modify Nodes Under /libs {#oakpal-customer-package}

**索引鍵：BannetPath**

**類型**：Bug

**嚴重性**：封鎖程式

**** 因為：2019.6.0版

在AEM內容存放庫中，/libs內容樹狀目錄被客戶視為唯讀，這是長久以來的最佳做法。Modifying nodes and properties under */libs* creates significant risk for major and minor updates. */libs* 修改只能由Adobe透過正式管道進行。

### Packages Should Not Contain Duplicate OSGi Configurations {#oakpal-package-osgi}

**索引鍵：重復選項**

**類型**：Bug

**嚴重性**：主修

**** 因為：2019.6.0版

複雜專案發生的常見問題是相同OSGi元件設定多次。如此可讓您在哪個組態可操作時產生模糊化。此規則是「執行模式感知」，只會識別相同元件在相同執行模式中多次設定(或執行模式組合)的問題。

#### Non Compliant Code {#non-compliant-code-osgi}

```+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### Compliant Code {#compliant-code-osgi}

```+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### Config and Install Folders Should Only Contain OSGi Nodes {#oakpal-config-install}

**索引鍵：configAndInstallbodonlyContainosgiodes**

**類型**：Bug

**嚴重性**：主修

**** 因為：2019.6.0版

For security reasons, paths containing */config/ and /install/* are only readable by administrative users in AEM and should be used only for OSGi configuration and OSGi bundles. 將其他類型的內容放置在包含這些區段的路徑下，會導致應用程式行為在管理和非管理使用者之間有所差異。

A common problem is use of nodes named `config` within component dialogs or when specifying the rich text editor configuration for inline editing. 若要解決此問題，應重新命名為相符的名稱。For the rich text editor configuration make use of the `configPath` property on the `cq:inplaceEditing` node to specify the new location.

#### Non Compliant Code {#non-compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    + config [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

#### Compliant Code {#compliant-code-config-install}

```
+ cq:editConfig [cq:EditConfig]
  + cq:inplaceEditing [cq:InplaceEditConfig]
    ./configPath = inplaceEditingConfig (String)
    + inplaceEditingConfig [nt:unstructured]
      + rtePlugins [nt:unstructured]
```

### Packages Should Not Overlap {#oakpal-no-overlap}

**索引鍵：PackageAss**

**類型**：Bug

**嚴重性**：主修

**** 因為：2019.6.0版

Similar to the *Packages Should Not Contain Duplicate OSGi Configurations* this is a common problem on complex projects where the same node path is written to by multiple separate content packages. 雖然使用內容封裝相依性可確保一致的結果，但最好避免完全overlap。
