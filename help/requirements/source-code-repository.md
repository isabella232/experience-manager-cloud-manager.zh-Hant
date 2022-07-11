---
title: 原始碼存放庫
description: 瞭解為您在Cloud Manager中擁有的每個程式設定的Git儲存庫。
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---


# 原始碼存放庫 {#source-code-repository}

瞭解為您在Cloud Manager中擁有的每個程式設定的Git儲存庫。

## Cloud Manager儲存庫 {#cloud-manager-repository}

您 [!UICONTROL AEM Managed Services] 訂閱包括原始碼儲存庫，該儲存庫由Adobe設定和管理。 每個程式都分配了一個唯一的git儲存庫，在該儲存庫中將儲存並保護您的關聯代碼。

作為最佳做法，您應始終使用Cloud Manager的git儲存庫，該儲存庫為空，但沒有配置任何分支或示例項目。 要使用雲管理器的Git儲存庫，您將獲得一個專用訪問令牌，該令牌使您能夠使用任何Git客戶端建立分支、儲存和檢索代碼、列出提交歷史記錄等。

有關如何以Git設定分支的詳細資訊，請參閱 [配置發行分支。](/help/getting-started/configuring-branches.md)

有關如何將Cloud Manager的git儲存庫與CI/CD管道一起使用的詳細資訊，請參閱文檔 [配置生產管道](/help/using/production-pipelines.md) 和 [配置非生產管道](/help/using/non-production-pipelines.md) 來瞭解更多資訊。

## 內部部署儲存庫 {#on-premise-repository}

您可能有一個現有的Git儲存庫，並且希望繼續使用它，在這種情況下，您可以將Git的功能用於多個遠程儲存庫。 日常開發將繼續在您的Git儲存庫中進行。 當發佈分支準備好部署到生產環境中時，您可以將最新代碼推送到Cloud Manager的git儲存庫，並觸發Cloud Manager CI/CD管道。

要查看常用git命令，請參見 [Git作弊表](https://education.github.com/git-cheat-sheet-education.pdf) 在GitHub網站上。
