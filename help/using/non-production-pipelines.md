---
title: 配置非生產管道
description: 瞭解如何使用雲管理器建立和配置非生產管道以部署代碼。
exl-id: ccf4b4a2-6e29-4ede-821c-36318b568e5c
source-git-commit: 567a16a032bf80451b5e8ba4e3d842cb617a615f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---

# 配置非生產管道 {#configuring-non-production-pipelines}

瞭解如何使用雲管理器建立和配置非生產管道以部署代碼。 如果您首先想要更概念化地概述管道在Cloud Manager中的工作方式，請參閱文檔 [CI/CD管道。](/help/overview/ci-cd-pipelines.md)

## 概觀 {#overview}

使用 **管線** 平鋪 [!UICONTROL Cloud Manager]，也請參見Wiki頁。 **部署管理器** 可以建立兩種不同類型的管線。

* **生產管線**  — 生產管道是專門構建的管道，由一系列精心安排的步驟組成，從始至終將原始碼投入生產。
* **非生產管道**  — 非生產管道主要用於運行代碼質量掃描或將原始碼部署到開發環境中。

本文檔重點介紹非生產管道。 有關如何配置生產管線的詳細資訊，請參閱文檔 [配置生產管線。](/help/using/production-pipelines.md)

非生產管道有兩種類型：

* **代碼質量管道**  — 這些運行代碼質量掃描git分支中的代碼，並執行生成和代碼質量步驟。
* **部署管道**  — 除了執行生成和代碼質量步驟（如代碼質量管道）外，這些管道還將代碼部署到非生產環境。

>[!NOTE]
>
>在其關聯的Git儲存庫具有至少一個分支和 [程式設定](/help/getting-started/program-setup.md) 完成。 查看文檔 [Cloud Manager資料庫](/help/managing-code/repositories.md) 瞭解如何在雲管理器中添加和管理儲存庫。

## 視頻教程 {#video-tutorial}

此視頻提供了管道建立過程的概述，該過程在本文檔中進行了詳細介紹。

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

## 添加非生產管道 {#add-non-production-pipeline}

一旦您設定了程式並且使用Cloud Manager UI至少擁有一個環境，您就可以通過執行以下步驟來添加非生產管道。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) 並選擇相應的組織和程式。

1. 從Cloud Manager主螢幕訪問管道卡。 按一下 **添加** 選擇 **添加非生產管道**。

   ![添加非生產管道](/help/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. 在 **配置** 頁籤 **添加非生產管道** 對話框，選擇要建立的管線類型 **代碼質量管道** 或 **部署管道**。

   ![選擇管線類型](/help/assets/configure-pipelines/add-non-production-pipeline.png)

1. 提供管道的說明 **非生產管道名稱** 的子菜單。

1. 如果選擇添加 **部署管道**，從 **合格的部署環境** 下拉清單。

1. 提供管道應在其中檢索代碼的儲存庫。

   * **儲存庫**  — 此選項定義管道應從哪個git回購中檢索代碼。
   * **Git分支**  — 其選項定義管道中應從哪個分支檢索代碼。

1. 定義部署選項。

   1. 下 **部署觸發器**，定義激活管線的事件。

      * **手動**  — 使用此選項手動啟動管線。
      * **Git更改**  — 只要將提交添加到配置的git分支中，此選項就會啟動管道。 使用此選項，您仍可根據需要手動啟動管線。
   1. 對於部署管道，在 **重要度量故障行為**，定義在任何質量門中遇到重要故障時管線的行為。

      * **每次詢問**  — 這是預設設定，需要對任何重要故障進行手動干預。
      * **立即失敗**  — 如果選中此選項，則每當發生重要故障時，管線將被取消。 這實質上是模擬用戶手動拒絕每個故障。
      * **立即繼續**  — 如果選中此選項，則每當發生重要故障時，管線將自動繼續。 這實質上是模擬用戶手動批准每個故障。


1. 按一下 **保存** 保存管道。

## 後續步驟 {#the-next-steps}

配置管道後，需要部署代碼。 請參閱文檔 [代碼部署](/help/using/code-deployment.md) 的子菜單。
