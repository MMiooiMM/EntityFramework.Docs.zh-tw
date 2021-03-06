---
title: 非同步查詢 - EF Core
author: rowanmiller
ms.date: 01/24/2017
ms.assetid: b6429b14-cba0-4af4-878f-b829777c89cb
uid: core/querying/async
ms.openlocfilehash: 415c57df599f1cb1a255f01d1072890fedfd6d2b
ms.sourcegitcommit: b2b9468de2cf930687f8b85c3ce54ff8c449f644
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/12/2019
ms.locfileid: "70921685"
---
# <a name="asynchronous-queries"></a>非同步查詢

非同步查詢可避免在資料庫中執行查詢時封鎖執行緒。 若要避免凍結大型用戶端應用程式的 UI，這非常實用。 非同步作業也可以提高 Web 應用程式中的輸送量，其中可在資料庫作業完成時釋出執行緒，來為其他要求提供服務。 如需詳細資訊，請參閱[使用 C# 進行非同步程式設計](https://docs.microsoft.com/dotnet/csharp/async)。

> [!WARNING]  
> EF Core 不支援在同一個內容執行個體上執行多個平行作業。 您應該一律等候作業完成，再開始下一項作業。 這通常會在每個非同步作業上使用 `await` 關鍵字來完成。

Entity Framework Core 提供一組非同步擴充方法，這組方法可用來作為會導致執行查詢並傳回結果的 LINQ 方法替代項目。 範例包括 `ToListAsync()`、`ToArrayAsync()`、`SingleAsync()` 等。沒有 LINQ 運算子的非同步版本 (例如 `Where(...)`、`OrderBy(...)` 等)，因為這些方法只會逐漸形成 LINQ 運算式樹狀架構，而不會導致查詢在資料庫中執行。

> [!IMPORTANT]  
> EF Core 非同步擴充方法定義於 `Microsoft.EntityFrameworkCore` 命名空間中。 您必須先匯入此命名空間，才能使用方法。

[!code-csharp[Main](../../../samples/core/Querying/Async/Sample.cs#Sample)]
