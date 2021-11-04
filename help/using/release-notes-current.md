---
title: 2021.11.0 版發行說明
description: 請詳閱本頁以取得Cloud Manager版本2021.11.0的資訊
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 0395fd4263ae37bce49c698e8e72ad7b08af046a
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 3%

---

# 2021.10.0 版發行說明 {#release-notes-for}

以下章節概述的一般發行說明 [!UICONTROL Cloud Manager] 2021.11.0版。

>[!NOTE]
>請參閱 [最新發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) 若要查看AEM as a Cloud Service中Cloud Manager的最新發行說明，請參閱

## 發行日期 {#release-date}

的發行日期 [!UICONTROL Cloud Manager] 2021.11.0版是2021年11月4日。
下一版預計於2021年12月9日發行。

## 新增功能 {#whats-new}

* Git提交ID現在會顯示在管道執行詳細資訊中，以便更輕鬆追蹤已建置的程式碼。

* 此 `x-request-id` 回應標題現在會顯示在 [www.adobe.io](https://www.adobe.io/). 提交客戶服務問題以進行疑難排解時，此標題相當實用。

* 身為使用者，我看到管道為零的管道卡為我提供適當的指引。

* 現在提供新的管道頁面，其中提供暫留時顯示的狀態彈出視窗，以便您輕鬆檢視詳細資訊摘要。 可檢視管道執行及其相關聯的詳細資訊。

* 「編輯管道API」現在支援設定Dispatcher失效和排清路徑。

* 「編輯管道API」現在支援變更部署階段所使用的環境。

* 已針對大型封裝導入OakPal掃描程式的最佳化。

* 品質問題CSV檔案現在會包含每個品質問題的時間戳記。

* UI中將不再顯示「環境」頁面中的「管理」按鈕。

## 錯誤修正 {#bug-fixes}

* 某些非正統的組建設定會導致管道的Maven工件快取中儲存不必要的檔案，導致在啟動和停止組建容器時產生多餘的網路I/O。

* 如果部署階段不存在，管道PATCHAPI就會失敗。

* 此 `ClientlibProxyResourceCheck` 當有具有共同基本路徑的用戶端程式庫時，品質規則會產生誤判問題。

* 達到最大儲存庫數時，錯誤訊息未指定錯誤的原因。

* 在少數情況下，管道由於某些回應代碼的重試處理不當而失敗。
