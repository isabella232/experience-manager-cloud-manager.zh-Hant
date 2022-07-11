---
title: Git與Adobe雲管理器整合
description: 此視頻系列介紹了客戶管理的（內部部署的）Git儲存庫與Adobe雲管理器的設定和整合。
exl-id: e517f8a4-23f0-4486-8278-91396dba76ec
source-git-commit: 91e909273bf2b21d7f6413731923011915079e45
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# Git與Adobe雲管理器整合

AdobeCloud Manager配置了單個Git儲存庫，用於使用Cloud Manager的CI/CD管道部署代碼。 您可以現成使用Cloud Manager的Git儲存庫，也可以選擇將內部或客戶管理的Git儲存庫與Cloud Manager整合。

## Git整合概述

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

此視頻系列探討了將客戶管理的Git儲存庫與Cloud Manager整合的幾個使用案例。

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支開發](#feature-development)
* [生產部署](#production-deployment)
* [同步釋放標籤](#sync-tags)

此視頻系列假定了Git和原始碼管理的基本知識。 查看 [其他資源](#additional-resources) 的子菜單。

此視頻系列中概述的步驟和命名約定代表了一些與客戶管理的Git儲存庫和Cloud Manager協作的最佳做法。 預計所描述的公約和工作流將適用於個別發展小組。

有關雲管理器的完整概述，請查看文檔 [雲管理器簡介。](/help/introduction.md)

## 初始同步 {#initial-sync}

將客戶管理的Git儲存庫與Cloud Manager的Git儲存庫同步的第一步。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

設定基本的分支策略以利用Cloud Manager [生產](/help/using/production-pipelines.md) 和 [非生產管道。](/help/using/non-production-pipelines.md)

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支開發 {#feature-development}

使用功能分支隔離客戶管理的Git儲存庫中的代碼更改，並與Cloud Manager的Git儲存庫同步，以便使用非生產流水線進行代碼質量和驗證測試。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生產部署 {#production-deployment}

在客戶管理的git儲存庫中為生產版本準備代碼，並與Cloud Manager的git儲存庫同步，以便部署到暫存和生產環境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步釋放標籤 {#sync-tags}

將Cloud Manager Git儲存庫中的發行標籤同步到客戶管理的git儲存庫中，以便查看已部署到暫存和生產環境的代碼。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他資源 {#additional-resources}

* [Cloud Manager簡介](/help/introduction.md)
* [GitHub資源](https://try.github.io)
* [阿特拉西安·吉特Tutorials](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git作弊表](https://education.github.com/git-cheat-sheet-education.pdf)
