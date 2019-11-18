---
title: Форматирование отображаемых данных | Документация Майкрософт
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 38971643-2a3d-4f5b-a1fa-6334c162b8ed
caps.latest.revision: 4
ms.openlocfilehash: e915ac71feb50cb58cfa9195f0de94763affdb77
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72363703"
---
# <a name="formatting-displayed-data"></a><span data-ttu-id="b61df-102">Форматирование отображаемых данных</span><span class="sxs-lookup"><span data-stu-id="b61df-102">Formatting Displayed Data</span></span>

<span data-ttu-id="b61df-103">Можно указать способ отображения отдельных точек данных в списке, таблице или расширенном представлении.</span><span class="sxs-lookup"><span data-stu-id="b61df-103">You can specify how the individual data points in your List, Table, or Wide view are displayed.</span></span> <span data-ttu-id="b61df-104">При определении элементов представления можно использовать элемент `FormatString`. также можно использовать элемент `ScriptBlock` для вызова метода `FormatString` для данных.</span><span class="sxs-lookup"><span data-stu-id="b61df-104">You can use the `FormatString` element when defining the items of your view, or you can use the `ScriptBlock` element to call the `FormatString` method on the data.</span></span>

## <a name="using-the-formatstring-element"></a><span data-ttu-id="b61df-105">Использование элемента FormatString</span><span class="sxs-lookup"><span data-stu-id="b61df-105">Using the FormatString Element</span></span>

<span data-ttu-id="b61df-106">В следующем примере значение свойства `TotalProcessorTime` объекта [System. Diagnostics. Process](/dotnet/api/System.Diagnostics.Process) форматируется с помощью элемента FormatString.</span><span class="sxs-lookup"><span data-stu-id="b61df-106">In the following example the value of the `TotalProcessorTime` property of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object is formatted using the FormatString element.</span></span> <span data-ttu-id="b61df-107">Свойство `TotalProcessorTime`</span><span class="sxs-lookup"><span data-stu-id="b61df-107">the `TotalProcessorTime` property</span></span>

```
<TableColumnItem>
  <PropertyName>TotalProcessorTime</PropertyName>
  <FormatString>{0:MMM}{0:dd}{0:HH}:{0:mm}</FormatString>
</TableColumnItem>
```


