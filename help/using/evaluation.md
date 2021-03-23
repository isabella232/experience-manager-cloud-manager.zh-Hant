---
title: 評估
seo-title: 評估
description: '本頁是「產品更新精靈」中學習「評估」階段的起點。 '
seo-description: 本頁是「產品更新精靈」中學習「評估」階段的起點。
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
feature: 快速入門
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---


# 評估階段{#evaluation}

「產品更新」嚮導的第一個階段是&#x200B;**[!UICONTROL Evaluation]**階段。
您可以在這裡使用模式偵測器，直接從精靈存取，以評估升級的複雜性。 在此步驟結束時，您將可存取評估報表。

產生的報表可讓您偵測下列模式，以檢查Author例項是否要升級：

* 違反特定規則，並在受升級影響或覆寫的區域執行。

* 使用AEM6.x功能或API，新功能不向後相容，且升級後AEM可能會中斷。

這是對升級至Adobe Experience Manager(AEM)6.5的發展努力的評估。

>[!NOTE]
>
>若要進一步瞭解圖樣偵測器，請參閱[使用圖樣偵測器評估升級複雜性](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/pattern-detector.html)

## 運行評估器{#running-evaluator}

請依照下列步驟產生評估報表：

1. 按一下&#x200B;**[!UICONTROL Run Evaluation]**。

   >[!NOTE]
   >
   >該圖案檢測器可在任何環境下運行。 但是，為了提高檢測率並避免關鍵業務實例出現任何慢速，Cloud Manager將在作者實例的測試環境中運行它。

   ![](assets/Run-Evaluation.png)

1. 嚮導會通知您操作的狀態。 當評估報告產生時，您會注意到&#x200B;**In progress**&#x200B;或&#x200B;**completed**。

   報告生成後，可以按一下&#x200B;**[!UICONTROL Download report]**&#x200B;保存副本。

   ![](assets/Evaluation-1.png)


   >[!NOTE]
   >
   >Cloud Manager中當前版本的產品更新嚮導僅支援&#x200B;**評估**&#x200B;階段。 其他四個階段即&#x200B;**補救**、**執行**、**驗證**&#x200B;和&#x200B;**完成**&#x200B;即將推出。
