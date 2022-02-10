---
title: 原始碼存放庫
seo-title: Source Code Repository for Adobe AEM Cloud Manager
description: 按照此頁瞭解為Cloud Manager中的每個程式設定的Git儲存庫。
seo-description: Follow this page to learn about the git repository that is provisioned for each program you have in Adobe AEM Cloud Manager.
uuid: 2c42775f-8703-43f7-bad2-7dc086ea9dd7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: f90f0f4c-c1ff-47f6-8d97-ff5018561bf2
feature: Provisioning
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 4f0e1d163001fd18cfa838256c813152d65c3b4c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# 原始碼存放庫 {#source-code-repository}

## Cloud Manager儲存庫 {#cloud-manager-repository}

您 [!UICONTROL AEM Managed Services] 訂閱將包括原始碼儲存庫，該儲存庫由Adobe設定和管理。 每個客戶的計畫都分配了一個唯一的 **Git儲存庫**，將儲存並保護您的關聯代碼。

作為最佳做法，您應始終使用Cloud Manager的Git儲存庫，該儲存庫為空，但沒有配置任何分支或示例項目。 要使用雲管理器的Git儲存庫，將為您提供 **私有訪問令牌** 它將允許您使用任何與Git相容的客戶端建立分支、儲存和檢索代碼、列出提交歷史記錄等。

有關如何以Git設定分支的詳細資訊，請參閱 [配置發行分支](configure-your-release-branches.md)。

有關如何使用雲管理器的詳細資訊 **Git儲存庫** 使用CI/CD管道，請參閱文檔 [配置生產管道](configuring-production-pipelines.md) 和 [配置非生產管道](configuring-non-production-pipelines.md) 來瞭解更多資訊。

## 內部部署儲存庫 {#on-premise-repository}

在某些情況下，您將擁有一個現有的Git儲存庫，並希望繼續使用它。 在這些情況下，您可以將Git支援的功能用於多個遠程儲存庫。 日常開發將繼續在您的Git儲存庫中進行。 當發佈分支準備好部署到生產環境中時，您會將最新代碼推送到Cloud Manager的Git儲存庫，並觸發Cloud Manager CI/CD管道。

>[!NOTE]
>
>要查看常用Git命令，請參閱 [Git作弊表](https://education.github.com/git-cheat-sheet-education.pdf)。
