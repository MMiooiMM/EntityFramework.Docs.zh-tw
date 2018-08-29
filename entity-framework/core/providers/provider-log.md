---
title: 記錄檔的提供者影響的變更-EF Core
author: ajcvickers
ms.author: avickers
ms.date: 08/08/2018
ms.assetid: 7CEF496E-A5B0-4F5F-B68E-529609B23EF9
ms.technology: entity-framework-core
uid: core/providers/provider-log
ms.openlocfilehash: ee73940e3c0030b76e73438b1852cc29ebeadb45
ms.sourcegitcommit: dadee5905ada9ecdbae28363a682950383ce3e10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "42998349"
---
# <a name="provider-impacting-changes"></a>提供者影響的變更

此頁面包含提取要求可能需要其他的資料庫提供者，以回應的作者在 EF Core 存放庫上所做的連結。 目的是要讓現有的協力廠商資料庫提供者作者提供一個起始點，其提供者更新為新版本時。

我們會將此記錄檔開頭 2.1 2.2 的變更。 我們用之前 2.1 [ `providers-beware` ](https://github.com/aspnet/EntityFrameworkCore/labels/providers-beware)並[ `providers-fyi` ](https://github.com/aspnet/EntityFrameworkCore/labels/providers-fyi)上我們的問題和提取要求標籤。

### <a name="21-----22"></a>2.1---> 2.2

#### <a name="test-only-changes"></a>僅限測試的變更

* https://github.com/aspnet/EntityFrameworkCore/pull/12057 -在測試中允許可自訂的 SQL 分隔符號
  * 測試可讓非嚴格的浮動點比較 BuiltInDataTypesTestBase 中的變更
  * 允許要重複使用不同的 SQL 分隔符號使用的查詢測試的測試變更
* https://github.com/aspnet/EntityFrameworkCore/pull/12072 -將 DbFunction 測試加入至關聯式規格測試
  * 例如，針對所有的資料庫提供者，可以執行這些測試
* https://github.com/aspnet/EntityFrameworkCore/pull/12362 -非同步測試清除
  * 移除`Wait`呼叫，不需要非同步處理，並重新命名某些測試方法
* https://github.com/aspnet/EntityFrameworkCore/pull/12666 -統一記錄測試基礎結構
  * 新增`CreateListLoggerFactory`和移除一些先前記錄基礎結構，而這需要使用這些測試回應的提供者
* https://github.com/aspnet/EntityFrameworkCore/pull/12500 -執行更多的查詢測試，以同步和非同步
  * 測試名稱和分解已經變更，這將需要使用這些測試回應的提供者
* https://github.com/aspnet/EntityFrameworkCore/pull/12766 -重新命名 ComplexNavigations 模型中的巡覽
  * 使用這些測試的提供者可能需要做出回應
* https://github.com/aspnet/EntityFrameworkCore/pull/12141 -傳回集區，而不是功能測試在處置內容
  * 這項變更會包含可能需要提供者，以因應一些測試重構


#### <a name="test-and-product-code-changes"></a>測試和產品程式碼變更

* https://github.com/aspnet/EntityFrameworkCore/pull/12109 -彙總 RelationalTypeMapping.Clone 方法
  * 允許在衍生類別中簡化 RelationalTypeMapping 的 2.1 中的變更。 我們不認為這重大提供者，但提供者可以利用這項變更其衍生類型中對應的類別。
* https://github.com/aspnet/EntityFrameworkCore/pull/12069 -已標記或具名查詢
  * 新增用於標記 LINQ 查詢以及做為 SQL 中的註解會顯示這些標記的基礎結構。 這可能需要以回應 SQL 層代中的提供者。