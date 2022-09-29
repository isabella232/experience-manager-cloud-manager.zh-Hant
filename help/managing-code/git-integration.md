---
title: Git 和 Adobe Cloud Manager 整合
description: 本影片系列會逐步介紹客戶管理的 (內部部署) Git 存放庫與 Adob​​e Cloud Manager 的設定和整合。
exl-id: e517f8a4-23f0-4486-8278-91396dba76ec
source-git-commit: 91e909273bf2b21d7f6413731923011915079e45
workflow-type: ht
source-wordcount: '347'
ht-degree: 100%

---


# Git 和 Adobe Cloud Manager 整合

Adobe Cloud Manager 佈建了一個 Git 存放庫，用於使用 Cloud Manager 的 CI/CD 管道部署程式碼。您可以直接使用 Cloud Manager 的 Git 存放庫，也可以選擇將內部部署或客戶管理的 Git 存放庫和 Cloud Manager 整合。

## Git 整合總覽

>[!VIDEO](https://video.tv.adobe.com/v/28710/)

本影片系列會介紹幾個有關整合客戶管理的 Git 存放庫與 Adob&#x200B;&#x200B;e Cloud Manager 的使用案例。

* [初始同步](#initial-sync)
* [基本分支策略](#branching-strategy)
* [功能分支開發](#feature-development)
* [生產部署](#production-deployment)
* [同步版本標記](#sync-tags)

本影片系列會假定您具備 Git 和原始程式碼控制管理的基本知識。如需有關 Git 的更多詳細資訊，請參閱[下列附加資源](#additional-resources)。

本影片系列中概述的步驟和命名慣例代表使用客戶管理的 Git 存放庫和 Cloud Manager 的一些最佳做法。預計所描述的慣例和工作流程將適用於個別開發團隊。

如需 Cloud Manager 的完整總覽，請查看文件：[Cloud Manager 簡介。](/help/introduction.md)

## 初始同步 {#initial-sync}

將客戶管理的 Git 存放庫和 Cloud Manager 的 Git 存放庫同步處理的第一步。

>[!VIDEO](https://video.tv.adobe.com/v/28711/?quality=12)

## 基本分支策略 {#branching-strategy}

設定基本分支策略以利用 Cloud Manager 的[生產](/help/using/production-pipelines.md)和[非生產管道。](/help/using/non-production-pipelines.md)

>[!VIDEO](https://video.tv.adobe.com/v/28712/?quality=12)

## 功能分支開發 {#feature-development}

使用功能分支隔離客戶管理的 Git 存放庫中的程式碼變更並和 Cloud Manager 的 Git 存放庫同步，以便使用非生產管道進行程式碼品質和驗證測試。

>[!VIDEO](https://video.tv.adobe.com/v/28723/?quality=12)

## 生產部署 {#production-deployment}

在客戶管理的 Git 存放庫中為生產版本準備程式碼，並與 Cloud Manager 的 Git 存放庫同步，以便部署到中繼和生產環境。

>[!VIDEO](https://video.tv.adobe.com/v/28724/?quality=12)

## 同步版本標記 {#sync-tags}

將 Cloud Manager Git 存放庫中的版本標記同步到客戶管理的 Git 存放庫中，以便提供有關已將哪些程式碼部署到中繼和生產環境的可見度。

>[!VIDEO](https://video.tv.adobe.com/v/28725/?quality=12)

## 其他資源 {#additional-resources}

* [Cloud Manager 簡介](/help/introduction.md)
* [GitHub 資源](https://try.github.io)
* [Atlassian Git 教學課程](https://www.atlassian.com/git/tutorials/what-is-version-control)
* [Git 速查表](https://education.github.com/git-cheat-sheet-education.pdf)
