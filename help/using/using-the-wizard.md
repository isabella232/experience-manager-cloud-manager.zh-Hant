---
title: 使用精靈
description: 請依照本頁瞭解如何使用精靈建立應用程AEM式專案
feature: Getting Started
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 10%

---


# 使用嚮導{#using-wizard-to-create-an-aem-application-project}

當客戶已登入Cloud Manager時，他們會獲得一個空的git儲存庫。 目前的Adobe Managed Services(AMS)客戶(或遷移至AMS的內部部AEM署客戶)通常已擁有其專案程式碼（或其他版本控制系統），並將其專案匯入Cloud Manager Git儲存庫。 但是，新客戶沒有現有的專案。

為協助新客戶開始使用，Cloud Manger現在可以從最AEM小的專案開始。 此程式基於&#x200B;[**AEM Project Archetype**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。


請依照下列步驟，在Cloud Manager中建AEM立應用程式專案：

1. 一旦您登入Cloud Manager且基本程式設定完成後，如果儲存庫為空，「概述」畫面將會顯示特殊的動作卡呼叫。****

   ![](assets/image2018-10-3_14-29-44.png)

1. 按一下&#x200B;**建立以**&#x200B;開啟一個對話框，該對話框允許用戶提供項目原型所需AEM的參數。 在其預設形式中，對話框要求輸入兩個值：

   * **Title**  —— 依預設，此值會設為 *Program Name*

   * **新建分支名稱** -預設情況下，這是主 *檔案*

   ![](assets/screen_shot_2018-10-08at55825am.png)

   對話框中有一個抽屜，可通過按一下指向對話框底部的手柄來開啟該抽屜。 在其展開形式中，對話框顯示Archetype的所有配置參數。 其中許多參數具有根據&#x200B;**Title**&#x200B;生成的預設值。

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >例如，如果&#x200B;**Title**&#x200B;是&#x200B;***We.Finance***，則Base Maven Artifact Id參數會產生為&#x200B;***com.wefinance***。 如有需要，這些值可以變更。
   >
   >
   >例如，您可以將產生的&#x200B;***value com.wefinance***&#x200B;變更為&#x200B;***net.wefinance***。

1. 在前面的步驟中，按一下&#x200B;**Create**，通過使用原型建立啟動程式項目並提交到命名的git分支。 完成此操作後，可以設定管線。