---
title: Пример кода AccessDbProviderSample05 | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fea5d923-8001-4407-8975-743918bc8c80
caps.latest.revision: 6
ms.openlocfilehash: 212f6e0256778dc293daefdbc8264777bf6191b1
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72366953"
---
# <a name="accessdbprovidersample05-code-sample"></a><span data-ttu-id="e2053-102">Пример кода AccessDbProviderSample05</span><span class="sxs-lookup"><span data-stu-id="e2053-102">AccessDbProviderSample05 Code Sample</span></span>

<span data-ttu-id="e2053-103">В следующем коде показана реализация поставщика навигации Windows PowerShell, описанного в статье [Создание поставщика навигации Windows PowerShell](./creating-a-windows-powershell-navigation-provider.md).</span><span class="sxs-lookup"><span data-stu-id="e2053-103">The following code shows the implementation of the Windows PowerShell navigation provider described in [Creating a Windows PowerShell Navigation Provider](./creating-a-windows-powershell-navigation-provider.md).</span></span> <span data-ttu-id="e2053-104">Этот поставщик поддерживает рекурсивные команды, вложенные контейнеры и относительные пути, позволяющие перемещаться по хранилищу данных.</span><span class="sxs-lookup"><span data-stu-id="e2053-104">This provider supports recursive commands, nested containers, and relative paths that allow it to navigate the data store.</span></span>

## <a name="code-sample"></a><span data-ttu-id="e2053-105">Пример кода</span><span class="sxs-lookup"><span data-stu-id="e2053-105">Code Sample</span></span>

[!code-csharp[AccessDBProviderSample05.cs](../../../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample05/AccessDBProviderSample05.cs#L11-L1960 "AccessDBProviderSample05.cs")]

## <a name="see-also"></a><span data-ttu-id="e2053-106">См. также:</span><span class="sxs-lookup"><span data-stu-id="e2053-106">See Also</span></span>

[<span data-ttu-id="e2053-107">Пакет SDK для Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2053-107">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)