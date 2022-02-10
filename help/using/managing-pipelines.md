---
title: 管理管道
description: 瞭解如何管理現有管道，包括編輯、運行和刪除這些管道。
index: true
source-git-commit: 099a4490e3a8578b9f3485fd1514d1e97db977ab
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# 管理管道 {#managing-pipelines}

瞭解如何管理現有管道，包括編輯、運行和刪除這些管道。

## 管道卡 {#pipeline-card}

的 **管線** 卡 **計畫概述** Cloud Manager中的頁面將概述所有管道及其當前狀態。

![雲管理器中的管道卡](/help/using/assets/configure-pipelines/pipelines-card.png)

通過按一下每條管線旁邊的省略號按鈕，您可以執行以下操作。

* [運行管線](#running-pipelines)
* [編輯管線](#editing-pipelines)
* [刪除管線](#deleting-pipelines)
* [檢視詳情](#view-details)

在管線清單的底部，有常規選項。

* **添加**  — 至 [添加新的生產管道](configuring-production-pipelines.md) 或 [添加新的非生產管道](configuring-non-production-pipelines.md)
* **全部顯示**  — 將用戶帶至 **管線** 的子菜單。
* **訪問回購資訊**  — 顯示訪問Cloud Manager Git儲存庫所需的資訊
* **瞭解更多資訊**  — 導航到CI/CD管道文檔資源。

## 運行管線 {#running-pipelines}

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **管線** 卡 **計畫概述** 並按一下所選管線旁邊的省略號按鈕 **運行** 的子菜單。

1. 管線運行開始，並由 **狀態** 的雙曲餘切值。

通過再次按一下省略號按鈕並選擇 **[查看詳細資訊。](#view-details)**

根據管線類型，您可以通過再次按一下省略號按鈕並選擇取消運行 **取消**。

## 編輯管線 {#editing-pipelines}

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **管線** 卡 **計畫概述** ，然後按一下要編輯的管道旁邊的省略號按鈕，然後選擇 **編輯** 的子菜單。

1. 的 **編輯生產管線** 或 **編輯非生產管線** 對話框，允許您編輯建立管線時輸入的相同詳細資訊。

   * 有關管道可用的所有欄位和配置選項的詳細資訊，請參閱以下頁。
      * [配置生產管線](configuring-production-pipelines.md)
      * [配置非生產管道](configuring-non-production-pipelines.md)

1. 按一下 **更新** 編輯完管線後。

>[!NOTE]
>
>無法編輯正在運行的管線。

## 刪除管線 {#deleting-pipelines}

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **管線** 卡 **計畫概述** 並按一下所選管線旁邊的省略號按鈕 **刪除** 的子菜單。

>[!NOTE]
>
>無法刪除正在運行的管道。

## 檢視詳情 {#view-details}

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **管線** 卡 **計畫概述** 並按一下所選管線旁邊的省略號按鈕 **查看詳細資訊** 的子菜單。

1. 您將被帶到正在運行的管道的詳細資訊頁面。

![管道詳細資訊](/help/using/assets/configure-pipelines/pipeline-running-details.png)

從此處，您可以查看管道的各個步驟的狀態，並檢索生成日誌以用於診斷目的。 查看文檔 [部署代碼](deploying-code.md) 的子菜單。

>[!NOTE]
>
>您只能查看正在運行或至少已運行一次的管道的詳細資訊。
