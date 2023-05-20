---
title: 計劃設定
description: 上線後，企業所有者將需要對方案進行一些初始設定。
exl-id: 795c7112-d564-4fbf-96a1-152a6c286bf2
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 100%

---


# 計劃設定 {#program-setup}

上線後，企業所有者完成方案的初始設定，包括設定方案說明並定義用於效能測試的關鍵績效指標 (KPI)。

## 使用 [!UICONTROL  的方案設定Cloud Manager] {#program-setup-cloud-manager}

依照下列步驟設定方案並定義 KPI。

1. 在 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) 登入 Cloud Manager 並選取適當的組織。

1. 按一下&#x200B;**設定方案**，即可開始設定流程。

   ![設定計劃](/help/assets/set-up-program/setup1.png)

1. 在&#x200B;**設定方案**&#x200B;對話框中，您可在以下三個索引標籤中輸入計劃資訊：

   * **一般**
   * **KPI**
   * **佈建**

1. 在&#x200B;**一般**&#x200B;索引標籤上，為您的方案新增說明，並可按一下&#x200B;**變更相片**，選擇上傳縮圖。

   ![「一般」索引標籤](/help/assets/Setup_Program-General.png)

1. 在 **KPI** 索引標籤上，定義您的 KPI。在此範例中，分別為 **AEM Sites** 和 **AEM Assets** 定義了單獨的 KPI。 您將能夠為已獲得授權的產品指定 KPI。

   * 請參閱 [KPI](#kpis) 一節，以取得有關如何在 Cloud Manager 中測量 KPI 的更多詳細資訊。

   ![定義 KPI](/help/assets/Setup_Program-KPIs.png)

1. 如果您的方案啟用了自動縮放，您可以在&#x200B;**佈建**&#x200B;索引標籤上為您的環境定義隨選縮放選項。

   * 自動縮放僅適用於生產環境，而且可能並未提供給所有客戶方案。

   ![佈建選項](/help/assets/Setup_Program-Provisioning.png)

1. 按一下&#x200B;**儲存**，即可完成設定精靈。

將建立您的方案。在方案就緒可供使用之前，可能需要幾分鐘的時間來佈建資源。

## 編輯方案 {#editing-program}

您可以在方案完成設定後進行編輯。請依照以下步驟編輯方案。

1. 在 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) 登入 Cloud Manager 並選取適當的組織。

1. 從 Cloud Manager 首頁畫面瀏覽至該方案。

1. 按一下&#x200B;**編輯方案**，從&#x200B;**概觀**&#x200B;頁面更新或修改您的方案。

   ![編輯方案選項](/help/assets/set-up-program/edit-program1.png)

1. 會顯示&#x200B;**編輯方案**&#x200B;對話框，讓您能夠更新方案。請參閱[使用 Cloud Manager 的方案設定](#program-setup-cloud-manager)一節，以取得有關可用欄位的詳細資訊。

   ![編輯方案對話框](/help/assets/set-up-program/edit-program-general.png)

1. 按一下&#x200B;**更新**&#x200B;以儲存變更。

請注意，變更會立即儲存到 Cloud Manager，但要一直到下一次管道執行時才會反映在您的環境中。

如果您尚未建立管道，請參閱文件：[設定生產管道](/help/using/production-pipelines.md)和[設定非生產管道。](/help/using/non-production-pipelines.md)

## 在方案之間切換 {#swithing-programs}

在處理一個方案時，您可以快速切換到另一個方案，而無需返回 Cloud Manager 概觀頁面。

使用動作列切換到另一個方案、編輯目前的方案或新增方案。

![計劃切換器](/help/assets/set-up-program/setup2.png)

## KPI {#kpis}

對網站 KPI 的測量會依據在中繼環境上執行的測試。通常，這些 KPI 會按比例縮小以適合中繼環境的功能。

例如，一個使用者若期望在其生產環境中每分鐘平均有 1000 次頁面檢視量，並在生產環境中有四個 Dispatcher/發佈伺服器，應該將其縮小至每分鐘 250 次頁面檢視量。這是假設他們的中繼環境僅包含一個單一 Dispatcher/發佈伺服器的配對。

資產效能測試會透過在 30 分鐘的測試期間重複上傳資產並測量每個資產的處理時間以及各種系統層級量度來完成。

您的生產環境前面可能有一個內容傳遞網路 (CDN)，例如 Akamai 或 CloudFront。由於直接針對中繼環境進行 [!UICONTROL Cloud Manager] 測試，因此 KPI 應僅反映預期會通過 CDN 的流量，也就是快取遺漏。通常，這將是總生產流量的一個相對較小的子集。

## 影片概觀 {#video}

>[!VIDEO](https://video.tv.adobe.com/v/26313/)
