---
title: Cloud Manager常見問題
description: 本文檔提供有關AMS客戶的Cloud Manager的最常見問題的答案。
exl-id: 52c1ca23-5b42-4eae-b63a-4b22ef1a5aee
source-git-commit: 6be659e02df0657ec7d3dbce8c18c44a327a36f4
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 0%

---


# Cloud Manager常見問題 {#cloud-manager-faqs}

本文檔提供有關AMS客戶的Cloud Manager的最常見問題的答案。

## 是否可以將Java 11與Cloud Manager生成一起使用？ {#java-11}

可以。 您需要添加 `maven-toolchains-plugin` 設定正確。

* 此過程已記錄 [給。](/help/getting-started/using-the-wizard.md)
* 有關示例，請參見 [wknd示例項目代碼。](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)

## 在從Java 8切換到Java 11後，我的生成失敗，並出現有關maven-scr插件的錯誤。 我能做什麼？ {#maven-src-plugin}

嘗AEM試將生成從Java 8切換到11時，Cloud Manager生成可能失敗。 如果遇到以下錯誤，則需要刪除 `maven-scr-plugin` 將所有OSGi注釋轉換為OSGi R6注釋。

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

有關如何刪除此插件的說明， [見。](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)

## 從Java 8切換到Java 11後，我的生成失敗，出現有關RequireJavaVersion的錯誤。 我能做什麼？ {#requirejavaversion}

對於Cloud Manager版本， `maven-enforcer-plugin` 可能失敗

```text
[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion
```

這是已知問題，因為Cloud Manager使用不同版本的Java運行maven命令而不是編譯代碼。 簡單省略 `requireJavaVersion` 從 `maven-enforcer-plugin` 配置。

## 代碼質量檢查失敗，我們的部署停滯。 有辦法繞過這張支票嗎？ {#deployment-stuck}

可以。 除安全評級之外的所有代碼質量故障都是非關鍵度量，因此，通過擴展結果UI中的項，可以將它們作為部署管道的一部分跳過。

具有 [部署經理、項目經理或業務所有者](/help/requirements/users-and-roles.md#role-definitions) 角色可以覆蓋問題，在這種情況下，管線將繼續，或者他們可以接受問題，在這種情況下，管線將因失敗而停止。

查看文檔 [運行管道時的三層門](/help/using/code-quality-testing.md#three-tier-gates-while-running-a-pipeline) 和 [配置非生產管道](/help/using/non-production-pipelines.md#understanding-the-flow) 的子菜單。

## 在Adobe Managed Services環境中，在效能test步驟中Cloud Manager部署失敗。 我們如何調試此項以傳遞關鍵指標？ {#debug-critical-metrics}

這個問題沒有一個答案。 但是，對於效能test步驟，您應牢記以下幾點：

* 此步驟是Web效能步驟，即使用Web瀏覽器載入頁面的時間。
* 結果.csv檔案中列出的URL將在test期間載入到Cloud Manager基礎架構中的Chrome瀏覽器中。
* 失敗的公用度量是錯誤率。
   * 要傳遞URL，主URL必須載入 `200` 狀態和小於 `20` 秒。
   * 超過的頁面載入 `20` 秒標籤為 `504` 錯誤。
* 如果您的站點需要用戶身份驗證，請參閱文檔 [瞭解您的Test結果](/help/using/code-quality-testing.md#authenticated-performance-testing) 配置test以驗證到您的站點。

請參閱文檔 [瞭解Test結果](/help/using/code-quality-testing.md) 的子菜單。

## 是否可以將SNAPSHOT用於Maven項目的版本？ {#snapshot}

可以。 對於開發人員部署， Git分支 `pom.xml` 檔案必須包含 `-SNAPSHOT` 在 `<version>` 值。

這允許在版本未更改時仍安裝後續部署。 在開發人員部署中，不會為maven內部版本添加或生成自動版本。

也可以將版本設定為 `-SNAPSHOT` 用於階段和生產構建或部署。 Cloud Manager會自動設定正確的版本號，並以Git為您建立標籤。 如果需要，可以稍後引用此標籤。

有關版本處理的詳細資訊包括 [記錄在此。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/project-version-handling.html)

## 軟體包和捆綁包版本控制如何用於轉移和生產部署？ {#staging-production}

在轉移和生產部署中，將生成自動版本 [如本文所述。](/help/managing-code/maven-project-version.md)

對於階段和生產部署中的自定義版本控制，請設定一個適當的三部分版本，如 `1.0.0`。 每次部署到生產環境時都增加版本。

Cloud Manager會自動將其版本添加到舞台和生產構建中並建立Git分支。 不需要特殊配置。 如果未按前面所述設定主版本，則部署仍將成功，並自動設定版本。

## 我的maven生成對Cloud Manager部署失敗，但是它在本地生成，沒有錯誤。 怎麼了？ {#maven-build-fail}

查看 [git資源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) 的子菜單。

## 無法使用aio命令設定變數。 我能做什麼？ {#set-variable}

在嘗試通過以下方式列出或設定管道變數時，可能會收到403錯誤： `aio` 的雙曲餘切值。

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

在這種情況下，需要將執行這些命令的用戶添加到 **部署管理器** 在Admin Console中。

請參閱 [API權限](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/) 的子菜單。
