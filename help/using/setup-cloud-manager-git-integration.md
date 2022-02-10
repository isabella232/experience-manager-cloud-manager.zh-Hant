---
title: Git與Adobe雲管理器整合
description: 一個視頻系列，它介紹客戶管理的（內部部署的）git儲存庫與Adobe雲管理器的設定和整合。
seo-title: Git Integration with Adobe Cloud Manager
seo-description: A video series that walks through the set up and integration of a customer-managed (on-premise) git repository with Adobe Cloud Manager.
feature: Git Repositories
exl-id: e517f8a4-23f0-4486-8278-91396dba76ec
source-git-commit: 71d44c7e3673ca62fcd2203ecc0bc4ed9fa22002
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 4%

---

# Git與Adobe雲管理器整合

AdobeCloud Manager配置了單個Git儲存庫，用於使用Cloud Manager的CI/CD管道部署代碼。 客戶可以使用Cloud Manager的Git儲存庫。 客戶還可以選擇整合內部或 **客戶管理** git儲存庫（帶Cloud Manager）。

## Git整合概述

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

此視頻系列探討了在將客戶管理的Git儲存庫與Cloud Manager整合時的幾個使用案例，包括：

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支開發](#feature-development)
* [生產部署](#production-deployment)
* [同步釋放標籤](#sync-tags)

有關完整概述，請查看 [《 Cloud Manager使用手冊》。](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hant) 該視頻系列假設了Git和原始碼管理的基本知識。 查看 [其他資源](#additional-resources) 的子菜單。

>[!NOTE]
>
> 此視頻系列中概述的步驟和命名約定代表了一些與客戶管理的Git儲存庫和Cloud Manager協作的最佳做法。 預計所描述的公約和工作流將適用於個別發展小組。

## 初始同步 {#initial-sync}

將客戶管理的Git儲存庫與Cloud Manager的Git儲存庫同步的第一步。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

設定基本的分支策略以利用Cloud Manager [生產](configuring-production-pipelines.md) 和 [非生產管道。](configuring-non-production-pipelines.md)

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支開發 {#feature-development}

使用功能分支隔離客戶管理的Git儲存庫中的代碼更改，並與Cloud Manager的Git儲存庫同步，以便使用非生產流水線進行代碼質量和驗證測試。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生產部署 {#production-deployment}

在客戶管理的git儲存庫中為生產版本準備代碼，並與Cloud Manager的git儲存庫同步，以便部署到舞台和生產環境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步釋放標籤 {#sync-tags}

將Cloud Manager Git儲存庫中的發行標籤同步到客戶管理的git儲存庫中，以便查看已部署到存放和生產環境的代碼。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他資源 {#additional-resources}

* [Cloud Manager 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)
* [GitHub資源](https://try.github.io)
* [阿特拉西安·吉特Tutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git作弊表](https://education.github.com/git-cheat-sheet-education.pdf)
