---
title: 與Git Cloud Manager整合Adobe
description: 一個視訊系列，可逐步介紹客戶管理的（內部部署）git儲存庫與Adobe雲管理器的設定和整合。
seo-title: 與Git Cloud Manager整合Adobe
seo-description: 一個視訊系列，可逐步介紹客戶管理的（內部部署）git儲存庫與Adobe雲管理器的設定和整合。
feature: Git儲存庫
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 5%

---


# 與Git Cloud Manager整合Adobe

Adobe雲管理器隨附單一Git儲存庫，用來使用雲端管理器的CI/CD管道部署程式碼。 客戶可以立即使用Cloud Manager的git儲存庫。 客戶還可以選擇將內部部署或&#x200B;**customer-managed** git儲存庫與Cloud Manager整合。

## Git整合概觀

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

本影片系列探討在將客戶管理的Git儲存庫與Cloud Manager整合時的幾個使用案例，包括：

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支開發](#feature-development)
* [生產部署](#production-deployment)
* [同步發行標籤](#sync-tags)

如需完整概觀，請參閱[Cloud Manager使用指南](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)。 視訊系列具備Git和來源控制管理的基本知識。 如需Git的詳細資訊，請參閱[下方的其他資源。](#additional-resources)

>[!NOTE]
>
> 此系列影片中概述的步驟和命名慣例代表使用客戶管理的Git儲存庫和Cloud Manager的一些最佳實務。 預計所說明的慣例和工作流程將適用於個別開發團隊。

## 初始同步{#initial-sync}

將客戶管理的Git儲存庫與Cloud Manager的Git儲存庫同步的第一步。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略{#branching-strategy}

設定基本的分支策略，以利用Cloud Manager的[生產和非生產管道](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html)。

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支開發{#feature-development}

使用功能分支隔離客戶管理的Git儲存庫中的程式碼變更，並與Cloud Manager的Git儲存庫同步，以便使用非生產管道進行程式碼品質和驗證測試。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生產部署{#production-deployment}

在客戶管理的git儲存庫中準備生產版本的程式碼，並與Cloud Manager的git儲存庫同步，以便部署至存放和生產環境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步發行標籤{#sync-tags}

將Cloud Manager Git儲存庫中的釋放標籤同步到客戶管理的git儲存庫中，以便能夠查看哪些代碼已部署到存放和生產環境。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他資源 {#additional-resources}

* [Cloud Manager 文件](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)
* [GitHub資源](https://try.github.io)
* [Atlassian GitTutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)