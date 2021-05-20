---
title: 評估
seo-title: 評估
description: '此頁面是學習產品更新精靈中「評估」階段的起點。 '
seo-description: 此頁面是學習產品更新精靈中「評估」階段的起點。
uuid: 62d68e79-c2ba-4d8b-ba7d-33709014d5b6
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
discoiquuid: ebcc91a5-be9e-4684-8146-d88f4013d4d1
feature: 快速入門
exl-id: 1ffcbc21-dc36-435d-b83b-0209f81a15e7
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---

# 評估階段 {#evaluation}

產品更新嚮導的第一階段為&#x200B;**[!UICONTROL Evaluation]**階段。
您可以在此處透過直接從精靈存取的模式偵測器來評估升級複雜度。 在此步驟結束時，您將可以存取評估報表。

產生的報表可讓您偵測下列模式，以檢查製作執行個體以進行升級：

* 違反某些規則，並在受升級影響或覆寫的區域中執行。

* 使用AEM 6.x功能或在新AEM上不向後相容且可能在升級後中斷的API。

這是對升級至Adobe Experience Manager(AEM)6.5所涉發展努力的評估。

>[!NOTE]
>
>要了解有關模式檢測器的詳細資訊，請參閱[使用模式檢測器評估升級複雜性](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/pattern-detector.html)

## 運行求值器{#running-evaluator}

按照以下步驟生成評估報告：

1. 按一下&#x200B;**[!UICONTROL Run Evaluation]**。

   >[!NOTE]
   >
   >模式偵測器可在任何環境中執行。 不過，為了提高偵測率並避免業務關鍵例項發生任何速度緩慢，Cloud Manager會在製作例項的預備環境中執行。

   ![](assets/Run-Evaluation.png)

1. 精靈會通知您動作的狀態。 在生成評估報告時，您將注意到&#x200B;**正在進行**&#x200B;或&#x200B;**已完成**（如果適用）。

   產生報表後，您可以按一下&#x200B;**[!UICONTROL Download report]**&#x200B;以儲存副本。

   ![](assets/Evaluation-1.png)


   >[!NOTE]
   >
   >Cloud Manager中目前版本的產品更新精靈僅支援&#x200B;**評估**&#x200B;階段。 其他四個階段即&#x200B;**Remediation**、**Execution**、**Validation**&#x200B;和&#x200B;**Completion**&#x200B;即將推出。
