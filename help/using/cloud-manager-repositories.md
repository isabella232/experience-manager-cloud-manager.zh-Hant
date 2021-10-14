---
title: Cloud Manager儲存庫
description: Cloud Manager儲存庫
exl-id: 384b197d-f7a7-4022-9b16-9d83ab788966
source-git-commit: 17f79fdc7278cae532485570a6e2b8700683ef0d
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Cloud Manager儲存庫 {#cloud-manager-repos}

在Cloud Manager中建立和可用的儲存庫可透過「儲存庫」頁面來檢視和管理。

## 添加和管理儲存庫 {#add-manage-repos}

請依照下列步驟，在Cloud Manager中檢視及管理存放庫：

1. 從&#x200B;**程式概述**&#x200B;頁，按一下&#x200B;**儲存庫**&#x200B;頁簽並導航到&#x200B;**儲存庫**&#x200B;頁。

1. 按一下&#x200B;**添加儲存庫**&#x200B;以啟動嚮導。

   >[!NOTE]
   >必須登錄部署管理員或業務所有者角色中的用戶才能添加儲存庫。

   ![](assets/create-repo2.png)


1. 按要求輸入名稱和說明，然後按一下&#x200B;**Save**。

   ![](assets/repo-1.png)

1. 選擇&#x200B;**保存**。 新建立的存放庫會顯示在表格中，如下所示。

   ![](assets/create-repo3.png)

   >[!NOTE]
   >在Cloud Manager中建立的儲存庫也可供您在新增或編輯管道步驟期間選取。

1. 您可以選擇儲存庫，然後按一下表格最右側的菜單選項，以&#x200B;**複製儲存庫URL**、**查看和更新**&#x200B;或&#x200B;**刪除**&#x200B;儲存庫，如下圖所示。

   ![](assets/create-repo3.png)



## Git子模組支援 {#git-submodule-support}

Git子模組可用來在建置時合併Git存放庫間多個分支的內容。 執行Cloud Manager的建置程式時，在為管道配置的存放庫複製並簽出已配置的分支後，如果根目錄中的分支包含`.gitmodules`檔案，則會執行命令。

```
$ git submodule update --init
```

這會將每個子模組簽入相應目錄。 對於熟悉使用Git子模組且不想管理外部合併程式的組織，此技術是使用多個來源Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/working-with-multiple-source-git-repositories.html)的替代方法。[

例如，假設有三個存放庫，每個存放庫都包含名為main的單一分支。 在「主要」存放庫（即管道中設定的存放庫）中，主分支有一個pom.xml檔案，聲明其他兩個存放庫中包含的專案：

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

然後，您將為其他兩個存放庫新增子模組：

```
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectA/ project-a
$ git submodule add -b main https://git.cloudmanager.adobe.com/ProgramName/projectB/ project-b
```

這會產生如下所示的`.gitmodules`檔案：

```
[submodule "project-a"]
    path = project-a
    url = https://git.cloudmanager.adobe.com/ProgramName/projectA/
    branch = main
[submodule "project-b"]
    path = project-b
    url = https://git.cloudmanager.adobe.com/ProgramName/projectB/
    branch = main
```

有關Git子模組的詳細資訊，請參閱[Git參考手冊](https://git-scm.com/book/en/v2/Git-Tools-Submodules)。

使用Git子模組時，請記住以下事項：

* Git URL必須完全使用上述語法。 基於安全考量，請勿在這些URL中內嵌憑證。
* 僅支援分支根的子模組。
* Git子模組參考會儲存至特定的Git提交。 因此，在對子模組儲存庫進行更改時，需要更新引用的提交，例如，使用`git submodule update --remote`。
* 除非另有必要，強烈建議使用「淺層」子模組。 要執行此操作，請對每個子模組運行`git config -f .gitmodules submodule.<submodule path>.shallow true`。
