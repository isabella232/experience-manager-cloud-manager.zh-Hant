---
title: 設定您的計劃
seo-title: 設定您的計劃
description: 在登入後，商業擁有者將需要進行一些初始設定。
seo-description: '在登入後，商業擁有者必須進行一些初始設定Adobe AEM Cloud Manager。這包括設定程式描述並定義將用於效能測試的KPI。 '
uuid: 9ef 8743-f5 a-4744-86af-e2265567642 f
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 快速入門
discoiquuid: c2393540-e852-4f7 c-aafd-1427209065d2
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 設定您的計劃 {#setup-your-program}

在登入後，商業擁有者將需要完成本程式的一些初始設定。其中包括設定程式說明並定義關鍵績效指標(KPI)，以用於效能測試。或者，也可以上傳縮圖。此外，商業擁有者可在設定程式時設定環境布建。

定義的KPI作為效能測試的基準，在每次管線執行時傳遞。

>[!NOTE]
>
>在測試上測量的KPI會在 **測試環境** 上執行。通常這些KPI會縮小，以符合舞台環境的功能。
>
>例如，使用者在生產 **環境** 中平均每分鐘檢視1000次頁面檢視，並在生產環境中有個發送器/發佈伺服器，則每分鐘的頁面檢視次數應會縮放為250次(假設其階段環境只包含單一發送器/發佈伺服器配對)。
>
>此外，許多使用者在生產環境之前都有內容傳送網路(CDN)，例如Akamai或CloudFront。由於 [!UICONTROL Cloud Manager] 直接對舞台環境進行測試，KPI應只反映傳遞CDN的流量，即快取錯誤。通常這會是總生產流量的相對小部分。

## 使用 [!UICONTROL Cloud Manager] 來設定您的程式 {#using-cloud-manager-to-setup-your-program}

請依照下列步驟來設定程式並定義KPI：

1. 按一下 **「設定程式** 」以開始設定程序 [!UICONTROL Cloud Manager]。

   ![](assets/SetUpProgram1.png)

1. **「設定程式」** 畫面會顯示「編輯計劃資訊」。

1. 您會看到三個選項： **「一般」**、「 **KPI**」和「 **布建」** 索引標籤。

1. **在一般** 標籤中，將縮圖上傳至您的程式。您也可以新增相關說明至您的程式。

   ![](assets/Setup_Program-General.png)

1. 在 **KPI**下，您可以定義兩個KPI(每個部署的期望)。針對 **AEM Sites** 和 **AEM Assets定義個別KPI**。您將可以為您已授權的產品指定KPI。

   **AEM Sites**

   1. 您可以接受的第95個百分位數回應時間是甚麼？

      * 建議值-秒
   1. 尖峰載入下每分鐘有多少頁面檢視？

      * 建議值-每分鐘200次頁面檢視
   **AEM Assets**

   自首次發行以來，Cloud Manager就能夠執行AEM Sites程式的效能測試。在此版本中，也新增了功能，以執行AEM Assets程式的效能測試。資產效能測試是透過在30分鐘測試期間內重復上傳資產，並測量每個資產的處理時間以及各種系統層級量度來完成。
在計劃設定期間，會指定資產專屬KPI：

   * 第95個百分點的處理時間
   * 每分鐘上傳資產
   ![](assets/Setup_Program-KPIs.png)

1. 在 **Provisioning**(布建)底下，您可以檢視或編輯程式中生產和非生產環境的布建設設定。如果已開啓程式，則會開啓 ****自動縮放功能。

   >[!NOTE]
   >
   >* 自動調整功能僅適用於生產環境，而且可能無法用於所有客戶方案。
   >* 此發行不提供隨選縮放 [!UICONTROL Cloud Manager]。


   ![](assets/Setup_Program-Provisioning.png)

1. 按一下 **「儲存** 」以完成設定精靈。

   >[!NOTE]
   >
   >您隨時可以在初始計劃設定完成後編輯程式。請依照下列步驟進行詳細資訊。

## 編輯計劃

1. 導覽 **至Cloud Manager** 首頁畫面上的解決方案。

   ![](assets/SetUpProgram5.png)

1. 選取解決方案，按一下 **「編輯」** 以更新或修改程式，如下圖所示。

   ![](assets/SetUpProgram6.png)

1. 此時會顯示 **「編輯程式** 」畫面，可讓您更新或修改程式。

   ![](assets/Editing_Program-screen3.png)

## 後續步驟 {#the-next-steps}

如果您已設定 **「管道」**，下一次執行將會將您更新的設定納入考量。如果您尚未設定渠道，請依照步驟先設定渠道。

請參閱 [設定您的CI/CD管線](https://helpx.adobe.com/experience-manager/cloud-manager/using/configuring-pipeline.html) 以設定管線。
