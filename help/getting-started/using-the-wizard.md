---
title: 使用「新建項目」嚮導
description: 按照此頁瞭解如何使用嚮導建立應用程AEM序項目
exl-id: 9d7c6f4c-9379-471c-8dad-772a7099da54
source-git-commit: cb791a4f148ba394687b5e824b75fe1386d83c18
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# 使用「新建項目」嚮導 {#using-the-wizard}

當您作為新客戶加入Cloud Manager時，將為您提供一個空git儲存庫。 為幫助您入門，Cloud Manger提供了一個嚮導，以根據 [項AEM目原型](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype) 作為起點。

按照以下步驟使AEM用嚮導建立項目。

1. 登錄到Cloud Manager(位於 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com) 並選擇相應的組織。

1. 如果你還沒有， [建立程式。](program-setup.md) 程式建立後，Cloud Manager將認識到尚未設定儲存庫，並會在 **概述** 的上界。

   ![建立項目CTA](/help/assets/image2018-10-3_14-29-44.png)

1. 按一下 **建立** 以啟動嚮導並提供重要值。

   * **標題**  — 這是項目的標題，預設設定為項目群名稱。
   * **新建分支名稱**  — 這是您的Git儲存庫的初始分支，預設情況下 `main`。

   ![項目值](/help/assets/screen_shot_2018-10-08at55825am.png)

1. 對話框有一個抽屜，可通過向下按一下手柄開啟。 該對話框以擴展形式顯示項目原型的所有配AEM置參數。 這些參數具有根據 **標題** 已提供，不需要修改。 此處將向您解釋這些資訊。

   ![詳細原型參數](/help/assets/screen_shot_2018-10-08at60032am.png)

1. 按一下 **建立** 使用原型建立啟動程式項目並提交到命名的git分支。

你現在有個基本項目！ 現在，您可以設定管道。

## 現有或遷移客戶 {#existing-migrating}

如果您是當前的Adobe Managed Services(AMS)客戶或要遷移到的內部客戶AEM，則您可能已經擁有git或其他版本控制系統中的項目代碼。

在這種情況下，您會將項目導入到Cloud Manager Git儲存庫。
