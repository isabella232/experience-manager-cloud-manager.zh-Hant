---
title: 2022.3.0 版發行說明
description: These are the release notes for Cloud Manager release 2022.3.0.
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 79b2729814af483844d095ed8d6db6cead2ceaf7
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 3%

---


# Release Notes for Cloud Manager Release 2022.3.0 {#release-notes}

[!UICONTROL Cloud Manager]

>[!NOTE]
>
>[](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager]The next release is planned for 7 April 2022.

## 新增功能 {#what-is-new}

* (Cloud Service only) Accessing the AEM Environment log can be done using the Developer role.
* (AMS): Outbounds HTTP requests from asset tests will now come from a Fixed IP range.


## 錯誤修正 {#bug-fixes}

* ****
* ********
* A subset of git repositories created manually had an incorrect name value which prevented the build artifact reuse feature from being effective. The names of those repositories have been changed and users will see the corrected name in the Cloud Manager API/UI.
* Build artifacts from non-production pipelines were inappropriately reused on production full stack pipelines.
* When adding or editing a code quality pipeline, the options to handle metric failures is no longer displayed.
* Some unexpected pipeline variable configurations could cause in the build step.
