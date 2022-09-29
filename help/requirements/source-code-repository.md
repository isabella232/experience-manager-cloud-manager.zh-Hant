---
title: 原始程式碼存放庫
description: 了解為您在 Cloud Manager 中擁有的每個方案佈建的 Git 存放庫。
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: ht
source-wordcount: '264'
ht-degree: 100%

---


# 原始程式碼存放庫 {#source-code-repository}

了解為您在 Cloud Manager 中擁有的每個方案佈建的 Git 存放庫。

## Cloud Manager 存放庫 {#cloud-manager-repository}

您的 [!UICONTROL AEM Managed Services] 訂閱包括由 Adobe 佈建和管理的原始程式碼存放庫。每個方案都分配有一個唯一的 Git 存放庫，在此將儲存和保護您的相關程式碼。

依照最佳做法的要求，您應該一直使用 Cloud Manager 的 Git 存放庫，該存放庫會是空白的，沒有設定任何分支或範例專案。為了使用 Cloud Manager 的 Git 存放庫，您將獲得一個私人的存取權杖，讓您能夠使用任何 Git 用戶端來建立分支、儲存和擷取您的程式碼、製作認可歷史記錄的清單等。

如需有關如何在 Git 中設定分支的詳細資訊，請參閱[設定版本分支。](/help/getting-started/configuring-branches.md)

如需有關如何將 Cloud Manager 的 Git 存放庫和 CI/CD 管道一起使用的詳細資訊，請參閱文件：[設定生產管道](/help/using/production-pipelines.md)和[設定非生產管道](/help/using/non-production-pipelines.md)，以深入了解。

## 內部部署存放庫 {#on-premise-repository}

您可能有一個現有的 Git 存放庫並希望繼續使用它，在這種情況下，您可以將 Git 的功能用於多個遠端存放庫。日常開發將繼續在您的 Git 存放庫中進行。當版本分支已就緒，可部署到生產環境時，您可以將最新的程式碼推送到 Cloud Manager 的 Git 存放庫並觸發 Cloud Manager CI/CD 管道。

若要檢視 Git 命令，請參閱 GitHub 網站上的 [Git 速查表](https://education.github.com/git-cheat-sheet-education.pdf)。
