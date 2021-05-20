---
title: 使用精靈
description: 請參照本頁面，了解如何使用精靈建立AEM應用程式專案
feature: 快速入門
exl-id: 9d7c6f4c-9379-471c-8dad-772a7099da54
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 10%

---

# 使用嚮導{#using-wizard-to-create-an-aem-application-project}

當客戶上線至Cloud Manager時，會提供空白的Git存放庫。 目前的Adobe Managed Services(AMS)客戶(或要移轉至AMS的內部部署AEM客戶)通常已在git（或其他版本控制系統）中擁有其專案代碼，並將其專案匯入Cloud Manager Git存放庫。 但是，新客戶沒有現有項目。

為協助新客戶開始使用，Cloud Manger現在可以建立最簡化的AEM專案作為起點。 此程式以&#x200B;[**AEM專案原型**](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)為基礎。


請依照下列步驟，在Cloud Manager中建立AEM應用程式專案：

1. 一旦您登入Cloud Manager且基本程式設定完成後，如果儲存庫為空，「概述」畫面將會顯示特殊的動作卡呼叫。****

   ![](assets/image2018-10-3_14-29-44.png)

1. 按一下&#x200B;**建立以**&#x200B;開啟一個對話方塊，讓使用者提供AEM專案原型所需的參數。 在其預設形式中，對話框要求兩個值：

   * **標題**  — 依預設，此名稱會設為方 *案名稱*

   * **新分支名稱**  — 預設為主 *分支*

   ![](assets/screen_shot_2018-10-08at55825am.png)

   對話框具有抽屜，通過按一下手柄朝向對話框底部可開啟抽屜。 對話方塊會以展開的形式顯示原型的所有設定參數。 其中許多參數具有根據&#x200B;**Title**&#x200B;產生的預設值。

   ![](assets/screen_shot_2018-10-08at60032am.png)

   >[!NOTE]
   >
   >例如，如果&#x200B;**Title**&#x200B;為&#x200B;***We.Finance***，則Base Maven對象ID參數將生成為&#x200B;***com.wefinance***。 如有需要，可以變更這些值。
   >
   >
   >例如，您可以從產生的&#x200B;***值com.wefinance***&#x200B;變更為&#x200B;***net.wefinance***。

1. 按一下上一步中的&#x200B;**建立** ，使用原型建立起始專案並提交至指定的git分支。 完成此操作後，可以設定管道。
