---
title: Cloud Manager資料庫
description: 瞭解如何訪問、建立和編輯Cloud Manager程式的儲存庫。
exl-id: 384b197d-f7a7-4022-9b16-9d83ab788966
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Cloud Manager資料庫 {#cloud-manager-repos}

儲存庫是使用git管理代碼的位置。 瞭解如何為Cloud Manager程式建立儲存庫。

## 訪問儲存庫 {#accessing-repos}

您可以通過Cloud Manager的自助服務訪問和管理您的Git儲存庫。

要訪問儲存庫，請使用 **訪問回購資訊** 按鈕，其中最突出的是管道卡。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) 並選擇相應的組織和程式。

1. 導航到 **管線** 卡 **計畫概述** 頁面，你將看到 **訪問回購資訊** 選項訪問和管理git儲存庫 [已配置此管道。](/help/using/production-pipelines.md)

   ![訪問回購資訊按鈕](/help/assets/access-repo1.png)

1. 如果切換到 **非生產** 管道頁籤， **訪問回購資訊** 選項 [為管道配置。](/help/using/non-production-pipelines.md)

   ![非生產管道](/help/assets/access-repo-nonprod.png)

1. 按一下 **訪問回購資訊** 按鈕，開啟顯示的對話框：

   * Git儲存庫的URL
   * 使用者名稱
   * 密碼
   * 執行Git命令以本地克隆儲存庫

   ![儲存庫資訊對話框](/help/assets/access-repo-create.png)

使用提供的資訊在本地克隆儲存庫，以便開始本地開發。

>[!NOTE]
>
>的 **訪問回購資訊** 選項對中的用戶可見 **開發人員** 或 **部署管理器** 角色。

## 添加儲存庫 {#add-repos}

按照以下步驟在Cloud Manager中添加儲存庫：

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) 並選擇相應的組織和程式。

1. 從 **計畫概述** ，按一下 **儲存庫** 頁籤並導航至 **儲存庫** 的子菜單。

1. 按一下 **添加儲存庫** 的子菜單。

   >[!NOTE]
   >
   >您必須 **部署管理器** 或 **業務所有者** 角色以添加儲存庫。

   ![添加儲存庫](/help/assets/create-repo2.png)

1. 根據請求輸入名稱和說明，然後按一下 **保存**。

   ![回購協定詳細資訊](/help/assets/repo-1.png)

1. 選擇 **保存**。

將顯示新建立的回購。

![已建立新回購](/help/assets/create-repo3.png)

在雲管理器中建立的儲存庫可供您選擇 [建立管道。](/help/overview/ci-cd-pipelines.md)

## 查看和編輯儲存庫 {#edit-repos}

按照以下步驟編輯和查看Cloud Manager中的儲存庫：

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com) 並選擇相應的組織和程式。

1. 從 **計畫概述** ，按一下 **儲存庫** 頁籤並導航至 **儲存庫** 的子菜單。 在此，您可以查看現有儲存庫的詳細資訊。

1. 選擇儲存庫，然後按一下表最右側的省略號按鈕 **複製儲存庫URL**。 **查看和更新** 或 **刪除** 儲存庫。

![編輯回購](/help/assets/create-repo3.png)

## Git子模組支援 {#git-submodule-support}

Git子模組可用於在生成時合併多個分支在Git儲存庫中的內容。

當Cloud Manager的生成進程執行時，在克隆了為管道配置的儲存庫並簽出了已配置的分支後，如果分支包含 `.gitmodules` 檔案，執行命令。

```
$ git submodule update --init
```

這會將每個子模組檢出到相應的目錄中。 這種技術是 [使用多個源Git儲存庫](/help/managing-code/multiple-git-repos.md) 對於那些願意使用git子模組且不想管理外部合併進程的組織。

例如，假設有三個儲存庫，每個儲存庫都包含一個名為 `main`。 在「主」儲存庫中，即在管道中配置的儲存庫 `main` 分支具有 `pom.xml` 聲明其他兩個儲存庫中包含的項目的檔案：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
   
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
   
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
   
</project>
```

然後，您將為另外兩個儲存庫添加子模組：

```shell
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

這將導致 `.gitmodules` 檔案如下所示：

```text
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

有關git子模組的詳細資訊，請參閱 [Git參考手冊](https://git-scm.com/book/en/v2/Git-Tools-Submodules)。

### 限制 {#limitations}

使用git子模組時，請注意：

* Git URL必須與上述語法完全相同。
* 出於安全原因，請勿在這些URL中嵌入憑據。
* 只支援分支根上的子模組。
* 將Git子模組引用儲存到特定的Git提交。
   * 因此，當對子模組儲存庫進行更改時，需要更新引用的提交，例如，使用 `git submodule update --remote`。
* 除非有其他必要，強烈建議使用「淺」子模組。
   * 要執行此操作，請運行 `git config -f .gitmodules submodule.<submodule path>.shallow true` 每個子模組。
