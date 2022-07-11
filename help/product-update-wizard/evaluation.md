---
title: 評估階段
seo-title: Evaluation Phase
description: 瞭解產品更新嚮導的評估階段如何使用模式檢測器評估升級複雜性。
exl-id: 1ffcbc21-dc36-435d-b83b-0209f81a15e7
source-git-commit: ce2145da3b9e605e8a41bac28df520f14e255557
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# 評估階段 {#evaluation}

「產品更新」嚮導的第一階段是 **[!UICONTROL Evaluation]** 階段，該階段使用模式檢測器直接在嚮導中評估升級複雜性。 在此步驟結束時，您將有權訪問評估報告。

生成的報告允許您通過檢測以下模式來檢查作者實例的升級資格：

* 違反有關將受升級影響或覆蓋的區域的某些規則。

* 使用AEM6.x功能或與新版本不向後相容的API，並AEM且升級後可能中斷。

報告是對升級到Adobe Experience Manager(AEM6.5)的發展努力的評估。

>[!NOTE]
>
>要瞭解有關圖案檢測器的詳細資訊，請參閱文檔 [使用模式檢測器評估升級複雜性。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/pattern-detector.html?lang=en)

## 運行評估 {#running}

該圖案檢測器可在任何環境上運行。 但是，為了提高檢測率並避免業務關鍵型實例出現任何減速，Cloud Manager將在作者實例的暫存環境中運行它。

按照以下步驟生成評估報告。

1. 啟動嚮導，如文檔中所述 [產品更新嚮導。](/help/product-update-wizard/overview.md)

1. 按一下 **[!UICONTROL Run Evaluation]**。

   ![運行評估](/help/assets/Run-Evaluation.png)

1. 嚮導將通知您操作的狀態。 你會注意到 **正在進行** 或 **已完成** 在生成評估報告時適用。

1. 生成報告後，可按一下 **[!UICONTROL Download report]** 來保存副本。

   ![已建立報告](/help/assets/Evaluation-1.png)

Cloud Manager中當前版本的產品更新嚮導支援 **評估** 僅階段。 其他四個階段， **修正**。 **執行**。 **驗證**, **完成** 馬上就要來了。
