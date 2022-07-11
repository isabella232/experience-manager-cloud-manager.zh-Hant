---
title: 配置分支
description: 瞭解如何以git設定第一個分支以及CI/CD管道如何使用它來部署應用程式碼。
exl-id: ff2ae28f-902e-4fb2-aeb1-3636cb5cd9bb
source-git-commit: 4c051cd1696f8a00d0278131c9521ad4dcb956a3
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# 配置分支 {#configuring-branches}

瞭解如何以git設定第一個分支以及CI/CD管道如何使用它來部署應用程式碼。

## 以Git設定第一個分支 {#setting-up-your-first-branch-in-git}

單個Git儲存庫（最初為空） [已設定](/help/requirements/environment-provisioning.md) 針對Cloud Manager中載入的每個程式。 此儲存庫可以包含您的開發過程所需的任意多個分支，但必須至少有一個分支由CI/CD管道使用，以將應用程式碼部署到存放和生產。 最佳做法是 `main` 作為此分支的名稱。 方便地，這是Git客戶端在設定新項目時的預設行為。

例如，在設定新項目時，將運行一組類似於以下命令的命令。

```shell
$ git init
Initialized empty Git repository in /Users/myname/workspace/new-project/.git/
... steps which add Maven build files and source code ...
$ git add pom.xml core/pom.xml core/src ui.apps/pom.xml ui.apps/src
$ git commit -m "initial commit"
 19 files changed, 777 insertions(+)
 create mode 100644 core/pom.xml
 create mode 100644 pom.xml
 create mode 100644 ui.apps/pom.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/config.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/definition/.content.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/filter.xml
 create mode 100644 ui.apps/src/main/content/META-INF/vault/nodetypes.cnd
 create mode 100644 ui.apps/src/main/content/META-INF/vault/properties.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/apps/my-aem-project/install/.vltignore
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/policies/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/policies/_rep_policy.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/template-types/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/template-types/_rep_policy.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/templates/.content.xml
 create mode 100644 ui.apps/src/main/content/jcr_root/conf/my-aem-project/settings/wcm/templates/_rep_policy.xml
```

>[!NOTE]
>
>它不需要使用命令行客戶端。 有多種圖形Git客戶端可用作獨立應用程式或整合開發環境(IDE)的一部分，如Eclipse或IntelliJ。 只要客戶端應用程式支援使用HTTPS的git，它就應與 [!UICONTROL Cloud Manager]。

## 推入您的第一個分支 {#pushing-your-first-branch}

提交至少一個修訂版本後，可以添加 [!UICONTROL Cloud Manager] 將儲存庫作為遠程資料庫，然後將提交推送到它。

```shell
$ git remote add adobe <url>
$ git push adobe master
Counting objects: 36, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (27/27), done.
Writing objects: 100% (36/36), 7.31 KiB | 1.83 MiB/s, done.
Total 36 (delta 6), reused 0 (delta 0)
To <url>
 * [new branch]      main -> main
```

>[!NOTE]
>
>您的客戶成功工程部門將在以下期間向您提供特定URL和您的憑據 [!UICONTROL Cloud Manager] 開始登機。

## 其他分支 {#additional-branches}

單 `main` 分支可以滿足非常簡單的項目，但在大多數情況下，需要更複雜的分支策略。 許多客戶遵循的流程是，日常開發活動在名為 `develop` 並將開發分支合併到 `main` 分支時進行部署。

>[!TIP]
>
>要查看常用git命令，請參見 [Git作弊表](https://github.github.com/training-kit/downloads/github-git-cheat-sheet)。
