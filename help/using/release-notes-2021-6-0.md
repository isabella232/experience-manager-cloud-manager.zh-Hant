---
title: 2021.6.0 版發行說明
description: 請詳閱本頁以取得Cloud Manager 2021.6.0版的資訊
feature: 發行資訊
source-git-commit: ee701dd2d0c3921455a0960cbb6ca9a3ec4793e7
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 4%

---

# 2021.6.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2021.6.0版的一般發行說明。

>[!NOTE]
>請參閱[最新發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) ，查看AEM as aCloud Service中Cloud Manager的最新發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2021.6.0版的發行日期為2021年6月10日。
下一版預計於2021年7月15日發行。

## 新增功能 {#whats-new}

* Assets和Sites測試現在會並行執行（若適用），因此可縮短管道執行總時間。 此功能將在未來數週內為客戶啟用。

* 現在，系統會在管道執行之間快取建置步驟期間下載的Maven相依性。 此功能將在未來數週內為客戶啟用。

* 專案建立期間和透過管理Git工作流程的預設推送命令中使用的預設分支名稱已變更為`main`。

* 重新整理UI中的編輯方案體驗。 請參閱[編輯程式](/help/using/setting-up-program.md#editing-program)以了解詳細資訊。

* 品質規則`ImmutableMutableMixCheck`已更新，將`/oak:index`節點分類為不可變。

* 品質規則`CQBP-84`和`CQBP-84--dependencies`已整合為單一規則。 作為此整合的一部分，對依賴項的掃描可以更準確地識別部署到AEM運行時的第三方依賴項中的問題。

* 在某些情況下，如果無法計算「已略過的測試」量度，會導致管道執行失敗。

## 錯誤修正 {#bug-fixes}

* 未正確剖析根元素名稱后包含新行的JCR節點定義。

* 清單儲存庫API不會篩選已刪除的儲存庫。

* 為排程步驟提供無效值時，顯示錯誤錯誤訊息。

* 在某些情況下，當管道執行完成部署至生產步驟，且使用者停止執行時，UI中的部署狀態訊息無法正確反映實際發生的情況。
