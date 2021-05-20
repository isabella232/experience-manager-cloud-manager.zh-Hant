---
title: 原始碼存放庫
seo-title: AdobeAEM Cloud Manager的原始碼存放庫
description: 請詳閱本頁，了解針對您在Cloud Manager中擁有的每個方案所布建的Git存放庫。
seo-description: 請詳閱本頁，了解針對您在Adobe AEM Cloud Manager中擁有的每個方案所布建的Git存放庫。
uuid: 2c42775f-8703-43f7-bad2-7dc086ea9dd7
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: requirements
discoiquuid: f90f0f4c-c1ff-47f6-8d97-ff5018561bf2
feature: 布建
exl-id: af551e33-3623-4fcd-8d25-4362d8871411
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 2%

---

# 原始碼存放庫 {#source-code-repository}

## Cloud Manager儲存庫{#cloud-manager-repository}

您的[!UICONTROL AEM Managed Services]訂閱將包含由Adobe布建和管理的原始碼儲存庫。 每個客戶的程式都會獲派單一且唯一的&#x200B;**Git存放庫**，以儲存您的關聯程式碼並加以保護。

您應一律使用Cloud Manager的Git存放庫，此存放庫會是空白狀態，且未設定任何分支或範例專案。 若要使用Cloud Manager的Git存放庫，系統會提供&#x200B;**私人存取權杖** ，讓您能使用任何與Git相容的用戶端來建立分支、儲存和擷取程式碼、列出提交歷史記錄等。

如需如何在Git中設定分支的詳細資訊，請參閱[設定發行分支](configure-your-release-branches.md)。

如需如何將Cloud Manager的&#x200B;**Git存放庫**&#x200B;與CI/CD管道搭配使用的詳細資訊，請參閱[設定CI/CD管道](configuring-pipeline.md)。

## 內部部署存放庫{#on-premise-repository}

某些情況下，您會擁有現有的Git存放庫，並想繼續使用。 在這些情況下，您可以針對多個遠端存放庫使用Git的支援功能。 您的Git存放庫會繼續進行日常開發。 當發行分支準備好部署至生產環境時，您會將最新程式碼推送至Cloud Manager的Git存放庫，並觸發Cloud Manager CI/CD管道。

>[!NOTE]
>
>若要檢視常見的Git命令，請參閱[ Git速查表](https://education.github.com/git-cheat-sheet-education.pdf)。
