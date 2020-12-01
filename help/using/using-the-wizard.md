---
title: 使用精靈
description: 請依照本頁瞭解如何使用精靈來建立AEM應用程式專案
translation-type: tm+mt
source-git-commit: 7146a41d64365c9de03d32f4fc4c33f9e366c244
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 9%

---


# 使用嚮導{#using-wizard-to-create-an-aem-application-project}

當客戶已登入Cloud Manager時，他們會獲得一個空的git儲存庫。 目前的Adobe Managed Services(AMS)客戶（或內部部署AEM客戶，如果要移轉至AMS），通常其專案程式碼已位於git（或其他版本控制系統）中，並將其專案匯入Cloud Manager Git儲存庫。 但是，新客戶沒有現有的專案。

為協助新客戶開始使用，Cloud Manger現在可以建立最少的AEM專案作為起點。 此程式基於&#x200B;[**AEM Project Archetype**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。


請依照下列步驟，在Cloud Manager中建立AEM應用程式專案：

1. 一旦您登入Cloud Manager且基本程式設定完成後，如果儲存庫為空，「概述」畫面將會顯示特殊的動作卡呼叫。****

   ![](assets/image2018-10-3_14-29-44.png)

1. 按一下「建立至&#x200B;**」開啟對話方塊，讓使用者提供AEM Project Archetype所需的參數。**&#x200B;在其預設形式中，對話框要求輸入兩個值：

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