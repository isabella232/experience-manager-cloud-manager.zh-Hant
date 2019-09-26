---
title: 自訂代碼品質規則
seo-title: 自訂代碼品質規則
description: 請依本頁瞭解Cloud manager執行的自訂代碼品質規則。
seo-description: 請依照本頁瞭解Adobe Experience Manager Cloud manager執行的自訂代碼品質規則。
uuid: a7feb465-1982-46be-9e57-e67b59849579
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 使用
discoiquuid: d2338c74-3278-49e6-a186-6ef62362509f
translation-type: tm+mt
source-git-commit: 4881ff8be97451aa90c3430259ce13faef182e4f

---


# 自訂代碼品質規則 {#custom-code-quality-rules}

本頁說明由Cloud manager根據AEM工程的最佳實務建立的自訂程式碼品質規則。

>[!NOTE]
>
>此處提供的程式碼範例僅供說明之用。

## SonarQube Rules {#sonarqube-rules}

以下章節重點說明SonarQube規則：

### 不要使用潛在的危險功能 {#do-not-use-potentially-dangerous-functions}

**密鑰**:CQRules:CWE-676

**類型**:弱點

**嚴重性**:主修

**自**:2018.4.0版

方法 ***Thread.stop()*** 和 ***Thread.interrupt()*** 可產生難以重制的問題，在某些情況下，還可能產生安全漏洞。 Their usage should be tightly monitored and validated. In general, message passing is a safer way to accomplish similar goals.

#### 不符合程式碼 {#non-compliant-code}

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

**密鑰**:CQRules:CWE-134

**類型**:弱點

**嚴重性**:主修

**自**:2018.4.0版

使用來自外部源（如請求參數或用戶生成的內容）的格式字串可以使應用程式暴露於拒絕服務攻擊。 在某些情況下，格式字串可能受到外部控制，但僅允許來自受信任來源。

#### 不符合程式碼 {#non-compliant-code-1}

```java
protected void doPost(SlingHttpServletRequest request, SlingHttpServletResponse response) {
  String messageFormat = request.getParameter("messageFormat");
  request.getResource().getValueMap().put("some property", String.format(messageFormat, "some text");
  response.sendStatus(HttpServletResponse.SC_OK);
}
```

### HTTP請求應一律有通訊端和連線逾時 {#http-requests-should-always-have-socket-and-connect-timeouts}

**密鑰**:CQRules:ConnectionTimeoutMechanism

**類型**:錯誤

**嚴重性**:關鍵

**自**:2018.6.0版

當從AEM應用程式內部執行HTTP請求時，請務必確定已設定適當逾時，以避免不必要的執行緒耗用。 很遺憾，Java的預設HTTP客戶端(java.net.HttpUrlConnection)和常用的Apache HTTP Components客戶端的預設行為都是永不超時，因此必須明確設定超時。 此外，作為最佳實務，這些逾時秒數不應超過60秒。

#### 不符合程式碼 {#non-compliant-code-2}

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

### 客戶不應實作或擴充以@ProviderType註解的產品API {#product-apis-annotated-with-providertype-should-not-be-implemented-or-extended-by-customers}

**密鑰**:CQBP-84、CQBP-84-dependicies

**類型**:錯誤

**嚴重性**:關鍵

**自**:2018.7.0版

AEM API包含Java介面和類別，這些介面和類別僅能由自訂程式碼使用，但不能實作。 例如，介面 *com.day.cq.wcm.api.Page* 僅由 ***AEM實作***。

將新方法添加到這些介面時，這些附加方法不會影響使用這些介面的現有代碼，因此，在這些介面中添加新方法會被視為向後相容。 但是，如果自訂程 ***式碼實作*** 其中一個介面，該自訂程式碼會給客戶帶來向後相容性風險。

僅打算由AEM實施的介面（和類）會用 *org.osgi.annotation.versioning.ProviderType* (或者，在某些情況下，類似的舊式注釋 *aQute.bnd.annotation.ProviderType*)進行註解。 此規則可識別自訂程式碼實作（或擴充類別）此類介面的情況。

#### 不符合程式碼 {#non-compliant-code-3}

```java
import com.day.cq.wcm.api.Page;

public class DontDoThis implements Page {
// implementation here
}
```

### ResourceResolver對象應始終關閉 {#resourceresolver-objects-should-always-be-closed}

**密鑰**:CQRules:CQBP-72

**類型**:程式碼氣味

**嚴重性**:主修

**自**:2018.4.0版

從ResourceResolverFactory中獲取的ResourceResolver對象會佔用系統資源。 雖然在ResourceResolver不再使用時，有措施可回收這些資源，但通過調用close()方法明確關閉任何已開啟的ResourceResolver對象會更有效。

一個相對常見的誤解是，使用現有JCR會話建立的ResourceResolver對象不應顯式關閉，或者這樣做會關閉基礎的JCR會話。 不是這樣的——無論如何開啟資源解析器，都應在不再使用時關閉它。 由於ResourceResolver實施了可關閉介面，因此也可以使用try-with-resources語法，而不是顯式調用close()。

#### 不符合程式碼 {#non-compliant-code-4}

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

### 不要使用Sling servlet路徑來註冊servlet {#do-not-use-sling-servlet-paths-to-register-servlets}

**密鑰**:CQRules:CQBP-75

**類型**:程式碼氣味

**嚴重性**:主修

**自**:2018.4.0版

如 [Sling檔案所述](http://sling.apache.org/documentation/the-sling-engine/servlets.html)，不建議依路徑系結servlet。 路徑綁定的servlet不能使用標準JCR訪問控制，因此需要額外的安全性嚴格性。 建議您不要使用路徑綁定的servlet，而是在儲存庫中建立節點並按資源類型註冊servlet。

#### 不符合程式碼 {#non-compliant-code-5}

```java
@Component(property = {
  "sling.servlet.paths=/apps/myco/endpoint"
})
public class DontDoThis extends SlingAllMethodsServlet {
 // implementation
}
```

### 捕獲到的異常應記錄或拋出，但不應同時記錄或拋出 {#caught-exceptions-should-be-logged-or-thrown-but-not-both}

**密鑰**:CQRules:CQBP-44—CatchAndEitherLogOrThrow

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

一般而言，例外應只記錄一次。 多次記錄例外可能會造成混淆，因為不清楚發生例外的次數。 導致這種情況的最常見模式是記錄並拋出一個捕獲到的異常。

#### 不符合程式碼 {#non-compliant-code-6}

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

### 避免在日誌語句後面立即加上拋出語句 {#avoid-having-a-log-statement-immediately-followed-by-a-throw-statement}

**密鑰**:CQRules:CQBP-44—ConcentilueLogAndThrow

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

另一個避免的常見模式是記錄訊息，然後立即擲回例外。 這通常表示異常消息將在日誌檔案中重複。

#### 不符合程式碼 {#non-compliant-code-7}

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

### 在處理GET或HEAD請求時，避免登入INFO {#avoid-logging-at-info-when-handling-get-or-head-requests}

**密鑰**:CQRules:CQBP-44—LogInfoInGetOrHeadRequests

**類型**:程式碼氣味

**Severity**: Minor

In general, the INFO log level should be used to demarcate important actions and, by default, AEM is configured to log at the INFO level or above. GET和HEAD方法只能是只讀操作，因此不構成重要操作。 響應GET或HEAD請求在INFO級別登錄可能會產生明顯的日誌雜訊，從而更難識別日誌檔案中的有用資訊。 處理GET或HEAD請求時的記錄應位於發生錯誤時的WARN或ERROR級別，或位於DEBUG或TRACE級別（如果更深入的疑難排解資訊有幫助）。

>[!CAUTION]
>
>這不適用於每個請求的access.log類型記錄。

#### 不符合程式碼 {#non-compliant-code-8}

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

### 請勿將Exception.getMessage()用作記錄語句的第一個參數 {#do-not-use-exception-getmessage-as-the-first-parameter-of-a-logging-statement}

**密鑰**:CQRules:CQBP-44 - ExceptionGetMessageIsFirstLogParam

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

作為最佳做法，日誌消息應提供有關應用程式中發生異常的位置的上下文資訊。 雖然上下文也可以透過使用堆疊追蹤來判斷，但一般而言，記錄訊息會更容易讀取和瞭解。 因此，在記錄例外時，將例外消息用作日誌消息的做法是不好的——例外消息將包含出錯的內容，而日誌消息應用於告知日誌讀取器發生例外時應用程式正在執行什麼操作。 例外消息仍將記錄；指定您自己的訊息，讓記錄檔更容易理解。

#### 不符合程式碼 {#non-compliant-code-9}

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

### 登錄捕獲塊應處於WARN或ERROR級別 {#logging-in-catch-blocks-should-be-at-the-warn-or-error-level}

**密鑰**:CQRules:CQBP-44—WrongLogLevelInCatchBlock

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

如名稱所示，Java例外應一律用於例 *外情* 況。 因此，在捕獲到異常時，務必確保日誌消息記錄在適當的級別- WARN或ERROR。 這可確保這些消息在日誌中正確顯示。

#### 不符合程式碼 {#non-compliant-code-10}

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

**密鑰**:CQRules:CQBP-44 - ExceptionPrintStackTrace

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

如前所述，瞭解日誌消息時，上下文至關重要。 使用Exception.printStackTrace()只會 **將堆疊跟蹤輸出到** 標準錯誤流，從而丟失所有上下文。 此外，在像AEM這樣的多執行緒應用程式中，如果使用此方法並行列印多個例外，則其堆疊追蹤可能會重疊，造成嚴重混淆。 只應通過記錄框架記錄異常。

#### 不符合程式碼 {#non-compliant-code-11}

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

### 不輸出為「標準輸出」或「標準錯誤」 {#do-not-output-to-standard-output-or-standard-error}

**密鑰**:CQRules:CQBP-44—LogLevelConsolePrinters

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

登入AEM應一律透過登入架構(SLF4J)完成。 直接輸出到標準輸出或標準錯誤流會丟失記錄框架提供的結構和上下文資訊，在某些情況下可能導致效能問題。

#### 不符合程式碼 {#non-compliant-code-12}

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

**密鑰**:CQRules:CQBP-71

**類型**:程式碼氣味

**嚴重性**:次要

**自**:2018.4.0版

一般而言，以/libs和/apps開頭的路徑不應硬式編碼為它們所參照的路徑，最常儲存為相對於Sling搜尋路徑的路徑（依預設會設為/libs,/apps）。 使用絕對路徑可能會帶來細微的缺陷，這些缺陷只會在項目生命週期的後期出現。

#### 不符合程式碼 {#non-compliant-code-13}

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


## OakPAL內容規則 {#oakpal-rules}

Please find below the OakPAL checks executed by Cloud Manager.

>[!NOTE]
>OakPAL是由AEM合作夥伴（並獲2019年AEM Rockstar北美地區得獎者）開發的架構，可使用獨立的Oak儲存庫來驗證內容套件。

### 客戶包不應在/libs下建立或修改節點 {#oakpal-customer-package}

**密鑰**:UnbandedPaths

**類型**:錯誤

**嚴重性**:封鎖程式

**自**:2019.6.0版

AEM內容存放庫中的/libs內容樹狀結構應被客戶視為唯讀，這是一項長期以來的最佳做法。 在 */libs下修改節點和屬性* ，會對主要和次要更新造成重大風險。 Adobe僅 *能透過* 「官方」通道對/libs進行修改。

### 軟體包不應包含重複的OSGi配置 {#oakpal-package-osgi}

**密鑰**:DuplicateOsgiConfigurations

**類型**:錯誤

**嚴重性**:主修

**自**:2019.6.0版

在複雜項目上發生的常見問題是，同一個OSGi元件被多次配置。 這就產生了關於哪些配置可操作的模糊性。 此規則是「執行模式感知」，因為它只會識別在相同執行模式（或執行模式組合）中多次設定相同元件的問題。

#### 不符合代碼 {#non-compliant-code-osgi}

```+ apps
  + projectA
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
  + projectB
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

#### 相容代碼 {#compliant-code-osgi}

```+ apps
  + shared-config
    + config
      + com.day.cq.commons.impl.ExternalizerImpl
```

### 配置和安裝資料夾應僅包含OSGi節點 {#oakpal-config-install}

**密鑰**:ConfigAndInstallShouldOnlyContainOsgiNodes

**類型**:錯誤

**嚴重性**:主修

**自**:2019.6.0版

基於安全性原因，包含 */config/和/install/* ，路徑僅能由AEM的管理使用者閱讀，且僅能用於OSGi組態和OSGi組合。 將其他類型的內容置於包含這些區段的路徑下，會導致應用程式行為在管理使用者與非管理使用者之間無意間有所不同。

常見的問題是使用元件對話方塊 `config` 中命名的節點，或在指定用於內嵌編輯的豐富型文字編輯器組態時。 要解決此問題，應將違規節點更名為相容名稱。 對於富格文本編輯器配置，請使 `configPath` 用節點上的 `cq:inplaceEditing` 屬性指定新位置。

#### 不符合代碼 {#non-compliant-code-config-install}

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

### 包不應重疊 {#oakpal-no-overlap}

**密鑰**:PackageOverlaps

**類型**:錯誤

**嚴重性**:主修

**自**:2019.6.0版

與「包不 *應包含重複OSGi配置」類似* ，在由多個獨立內容包寫入相同節點路徑的複雜項目中，這是一個常見問題。 雖然使用內容封裝相依性可確保結果一致，但最好避免完全重疊。
