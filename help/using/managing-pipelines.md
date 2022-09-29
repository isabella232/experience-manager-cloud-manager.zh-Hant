---
title: 管理管道
description: 了解如何管理現有管道，包括將其編輯、執行和刪除。
exl-id: e36420d2-57c5-4375-99fb-dd47c1c8bffd
source-git-commit: 99325c28c379103db2ba4c19bb6d206849c6e126
workflow-type: ht
source-wordcount: '517'
ht-degree: 100%

---


# 管理管道 {#managing-pipelines}

了解如何管理現有管道，包括將其編輯、執行和刪除。

## 管道卡 {#pipeline-card}

此&#x200B;**管道**&#x200B;卡位於 Cloud Manager 中的&#x200B;**方案總覽**&#x200B;頁面上，可讓您總覽您所有的管道及其目前狀態。

![Cloud Manager 中的管道卡](/help/assets/configure-pipelines/pipelines-card.png)

按一下每個管道旁邊的省略符號按鈕，您就可以執行下列操作。

* [執行管道](#running-pipelines)
* [編輯管道](#editing-pipelines)
* [刪除管道](#deleting-pipelines)
* [檢視詳情](#view-details)

在管道清單底部，您有一般選項。

* **新增** - 至[可新增生產管道](/help/using/production-pipelines.md)或是[新增非生產管道](/help/using/non-production-pipelines.md)
* **顯示全部** - 將使用者帶到&#x200B;**管道**&#x200B;畫面，在更詳細的表格中檢視所有管道。
* **存取存放庫資訊** - 顯示要存取 Cloud Manager Git 存放庫所必需的資訊
* **了解更多** - 瀏覽至 CI/CD 管道文件資源。

## 執行管道 {#running-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 瀏覽至&#x200B;**管道**&#x200B;卡 (位於&#x200B;**方案總覽**&#x200B;頁面)，並按一下您執行的管道旁的省略符號按鈕，從選單中選取&#x200B;**執行**。

1. 此管道執行開始，並由&#x200B;**狀態**&#x200B;欄顯示。

您可以查看執行的詳細資訊，只要再按一下省略符號按鈕，並選取 **[檢視全部。](#view-details)**

依管道的類型而定，您也許可以取消執行，只要再按一下省略符號按鈕，並選取&#x200B;**取消**。

## 編輯管道 {#editing-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 瀏覽至&#x200B;**管道**&#x200B;卡 (位於&#x200B;**方案總覽**&#x200B;頁面)，並按一下您要編輯的管道旁的省略符號按鈕，然後從選單中選取&#x200B;**編輯**。

1. **編輯生產管道**&#x200B;或是&#x200B;**編輯非生產管道**&#x200B;對話框會隨即顯示，讓您可以對您在建立管道時輸入的詳細資訊進行編輯。

   * 如需有關管道可用的所有欄位和設定選項的詳細資訊，請參閱以下頁面。
      * [設定生產管道](/help/using/production-pipelines.md)
      * [設定非生產管道](/help/using/non-production-pipelines.md)

1. 按一下&#x200B;**更新**&#x200B;一次，您即完成編輯管道。

>[!NOTE]
>
>您無法編輯執行中的管道。

## 刪除管道 {#deleting-pipelines}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 瀏覽至&#x200B;**管道**&#x200B;卡 (位於&#x200B;**方案總覽**&#x200B;頁面)，並按一下您執行的管道旁的省略符號按鈕，從選單中選取&#x200B;**刪除**。

>[!NOTE]
>
>您無法刪除執行中的管道。

## 檢視詳情 {#view-details}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 瀏覽至&#x200B;**管道**&#x200B;卡 (位於&#x200B;**方案總覽**&#x200B;頁面)，並按一下您執行的管道旁的省略符號按鈕，從選單中選取&#x200B;**檢視詳情**。

1. 系統將會帶您前往執行中管道的詳細資訊頁面。

![管道詳情](/help/assets/configure-pipelines/pipeline-running-details.png)

從這裡您可以查看管道各個步驟的狀態，並擷取組建紀錄以進行診斷。 如需詳細資訊，請參閱文件：[程式碼部署](/help/using/code-deployment.md)。

>[!NOTE]
>
>您只能查看正在執行或已執行至少一次的管道的詳細資訊。
