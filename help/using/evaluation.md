---
title: 評估
seo-title: 評估
description: '此頁面是產品更新精靈中學習評估階段的起點。 '
seo-description: 此頁面是產品更新精靈中學習評估階段的起點。
uuid: 62d68e79-c2 ba-4d8 b-ba7 d-33709014d5 b6
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
discoiquuid: ebcc91a5-be9 e-4684-8146-d88 f4013 d4 d1
translation-type: tm+mt
source-git-commit: 9a1af88238a232c64d9f0229059c5001f314c736

---


# Evaluation Phase {#evaluation}

Once you click **[!UICONTROL Start Update]**, the first phase in Product Update wizard is the **[!UICONTROL Evaluation]** phase. 在這個階段中，您可以使用直接從精靈存取的圖樣檢測器來評估升級複雜性。在本步驟結束時，您將可存取評估報告。

產生的報表可讓您偵測「作者」執行個體，借由偵測下列模式來檢查：

* 違反某些規則，並在升級時會受到影響或覆寫。

* 使用AEM6.x功能或在新AEM上不會向後相容的API，而且在升級後可能會中斷。

這是評估升級至Adobe Experience Manager(AEM)6.5所涉及的開發成果。

>[!NOTE]
>To learn more about pattern detector, refer to [Assessing the Upgrade Complexity with the Pattern Detector](https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/pattern-detector.html)

## Running the Evaluator {#running-evaluator}

請遵循下列步驟執行評估工具：

1. Click on **[!UICONTROL Run Evaluation]** to run the pattern detector.

   >[!NOTE]
   >圖樣檢測器可在任何環境上執行。但是，若要提高偵測率並避免在業務關鍵性例項上發生任何慢動作，Cloud Manager將會在作者例項上執行測試環境。

   ![](assets/Run-Evaluation.png)

1. 精靈會通知您動作的狀態。You will notice **In progress** or **completed** as applicable when the evaluation report is being generated.

   Once the report is generated, you can click on **[!UICONTROL Download report]** to save a copy of the evaluation report.

   ![](assets/Evaluation-1.png)

   新增功能，您可以在狀態更新時檢視更新的脈衝通知。

   ![](assets/Evaluation-pulse-notification.png)

>[!NOTE]
>The other four phases succeeding **Evaluation** namely **Remediation**, **Execution**, **Validation**, and **Completion** are coming soon and are not available in the current release.
