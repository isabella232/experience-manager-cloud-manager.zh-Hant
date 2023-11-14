---
title: 在Cloud Manager中使用您自己的GitHub存放庫
description: 瞭解如何設定Cloud Manager以使用您自己的GitHub存放庫。
feature: Release Information
source-git-commit: 76a3dc6df41032488a3cfe11d0c72769562b96df
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 2%

---


# 在Cloud Manager中使用您自己的GitHub存放庫 {#byo-github}

透過設定Cloud Manager使用您自己的GitHub存放庫，您可以直接透過Cloud Manager在您的GitHub存放庫中驗證您的程式碼，而不需要以一致的方式將您的程式碼與Adobe存放庫同步。

>[!NOTE]
>
>此功能僅適用於[早期採用者計劃。](/help/release-notes/current.md#early-adoption)

## 設定 {#configuration}

設定包含兩個主要步驟：

1. [新增存放庫](#add-repo)
1. [私人存放庫所有權驗證](#validate-ownership)

### 新增存放庫 {#add-repo}

1. 在Cloud Manager中，從 **計畫總覽** 頁面，點選或按一下 **存放庫** 標籤以切換至 **存放庫** 頁面並按一下 **新增存放庫**.

1. 在 **新增存放庫** 對話方塊，選取 **私人存放庫** 作為存放庫型別。

1. 提供存放庫的詳細資料

   * **存放庫名稱**  — 表現式名稱
   * **存放庫URL**  — 存放庫的URL，結尾必須是 `.git`
   * **說明** （選用） — 視需要提供較長的存放庫說明

   ![新增自己的存放庫](/help/assets/repositories/add-own-github.png)

1. 點選或按一下&#x200B;**儲存**。

>[!TIP]
>
>如需有關在Cloud Manager中管理存放庫的詳細資訊，請參閱檔案 [Cloud Manager存放庫。](/help/managing-code/repositories.md)

### 私人存放庫所有權驗證 {#validate-ownership}

Cloud Manager現在知道您的GitHub存放庫，但仍需要存取它。 若要授與存取權，您必須安裝AdobeGitHub應用程式，並確認您擁有指定的存放庫。

1. 新增您自己的存放庫後， **私人存放庫所有權驗證** 對話方塊將會開啟。

   ![私人存放庫所有權驗證](/help/assets/repositories/private-repo-validate.png)

1. Cloud Manager會使用GitHub應用程式來安全地與您的存放庫互動。
   * 您GitHub組織的所有者必須安裝應用程式，位置位於 `https://github.com/apps/cloud-manager-for-aem-stage` 和授予存放庫的存取權。
   * 如需有關如何操作的詳細資訊，請參閱GitHub的檔案。

1. 若要增強安全性，您必須在存放庫的預設分支中建立機密檔案。 點選或按一下 **產生**.

1. 點選或按一下以確認產生機密檔案 **確認**.

   ![確認密碼產生](/help/assets/repositories/confirm-generation.png)

1. 返回 **私人存放庫所有權驗證** 視窗，Cloud Manager已產生的私人檔案的內容在 **機密檔案內容** 欄位。 複製該欄位中的內容。

   * 機密檔案的內容只會顯示一次。 如果您在關閉此視窗之前未複製內容，則需要重新產生密碼。

   ![複製密碼檔案內容](/help/assets/repositories/new-secret.png)

1. 在GitHub存放庫的預設分支中建立名為的新檔案 `.well-known/adobe/cloud-manager-challenge` 並將機密檔案內容貼入該檔案並儲存。

1. 安裝應用程式且存放庫中存在機密檔案後，您可以點選或按一下 **驗證** 在 **私人存放庫所有權驗證** 對話方塊。

您可以安裝應用程式，並依任何順序建立機密檔案。 不過，必須先完成這兩個步驟，然後才能進行驗證。

在驗證之前，存放庫將以紅色圖示列出，表示它尚未驗證且尚無法使用。

![未驗證的存放庫](/help/assets/repositories/unvalidated-repo.png)

請注意 **型別** 欄可輕鬆識別Adobe提供的存放庫(**Adobe**)和您自己的GitHub存放庫(**GitHub**)。

如果您需要在稍後日期返回存放庫以完成驗證，請在 **存放庫** 頁面，點選或按一下代表您剛剛新增的GitHub存放庫一列中的省略符號按鈕，然後選取 **所有權驗證** （從下拉式功能表）。

## 將您自己的GitHub存放庫與Cloud Manager搭配使用 {#using}

在Cloud Manager中驗證GitHub存放庫後，整合即完成，您可以透過Cloud Manager使用該存放庫。

1. 當您建立提取請求時，GitHub檢查會自動啟動。

   ![GitHub檢查](/help/assets/repositories/github-checks.png)

1. 對於每個提取請求， [完整棧疊計畫碼品質管道](/help/using/managing-pipelines.md) 將會自動建立。 此管道會在每次提取請求更新時啟動。

1. GitHub檢查會維持在執行狀態，直到程式碼品質檢查完成為止。 然後程式碼品質結果會傳播至GitHub檢查。

   ![GitHub程式碼品質檢查](/help/assets/repositories/github-code-quality.png)

當拉取請求關閉或合併時，建立的完整棧疊計畫碼品質管道會自動刪除。

## 限制 {#limitations}

當您透過Cloud Manager使用自己的GitHub存放庫時，請記住以下限制。

* 您不能使用GitHub存放庫作為您管理的管道的直接存放庫來源。
   * 此功能已在規劃中。
* 您可以使用Cloud Manager的GitHub檢查來暫停提取請求驗證。
   * 如果已在Cloud Manager中驗證GitHub存放庫，Cloud Manager一律會嘗試驗證為該存放庫建立的提取請求。
如果從您的GitHb組織移除AdobeGitHub應用程式，這將會移除所有存放庫的提取請求驗證功能。
