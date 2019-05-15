---
title: 設定您的版本分支
seo-title: 設定您的版本分支
description: 為AEM Cloud Manager設定Git中的發行分支
seo-description: 請依照此頁面瞭解如何在Git中配置您的版本分支。
uuid: d12a8b85-b7 fd-4b55-a05 a-a0 f874 ce598 c
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 快速入門
discoiquuid: 53807ea6-9464-429d-9322-85c9f405dff6
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 設定您的版本分支 {#configure-your-release-branches}

## 在Git中設定您的第一個分支 {#setting-up-your-first-branch-in-git}

Cloud Manager中會為每個計劃布建一個最初空白的 **Git存放庫** 。在開發程序之後，此儲存庫可包含任意數目(或少)分支，但必須至少有一個分支，才能用於CI/CD管線，將應用程式碼部署至舞台和生產環境。最佳實務是用作 `master` 此分支的名稱。方便的是，這是Git客戶設定新專案時的預設行為。

例如，設定新專案時，您將執行下列命令集：

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
>它不需要使用命令列用戶端。有多種圖形化Git用戶端可獨立使用，或做為整合開發環境(IDE)的一部分，例如Eclipse或IntelliJ。只要用戶端應用程式使用HTTPS支援Git，它就應該相容 [!UICONTROL Cloud Manager]。

## 推送您的第一個分支 {#pushing-your-first-branch}

在您至少收到一個修訂後，您可以將 [!UICONTROL Cloud Manager] 存放庫新增為 **遠端** ，然後將您的同意推送給它：

```shell
$ git remote add adobe <url>
$ git push adobe master
Counting objects: 36, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (27/27), done.
Writing objects: 100% (36/36), 7.31 KiB | 1.83 MiB/s, done.
Total 36 (delta 6), reused 0 (delta 0)
To <url>
 * [new branch]      master -> master
```

>[!NOTE]
>
>在上線期間 [!UICONTROL Cloud Manager] ，您的客戶成功工程將會提供特定URL以及您的認證。

## 其他分支 {#additional-branches}

`master` 單一分支可能會佔用非常簡單的專案，但在大多數情況下，需要更複雜的分支策略。許多客戶會遵循一個程序，此程序會在呼叫 `develop` 的分支上執行日常開發活動，而開發分支則會在該 `master` 分支進行部署時合併至分支中。

>[!NOTE]
>
>若要檢視常用的git命令，請參閱 [Git Cheat Sheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf)。

