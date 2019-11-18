---
title: Пример PowerShell02 для Windows | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 92492a7e-257d-47d3-b119-89df3c5545e8
caps.latest.revision: 9
ms.openlocfilehash: db7ff3a2dbd92f562379d206db494ab92ef08736
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72367303"
---
# <a name="windows-powershell02-sample"></a><span data-ttu-id="9f807-102">Пример Windows PowerShell02</span><span class="sxs-lookup"><span data-stu-id="9f807-102">Windows PowerShell02 Sample</span></span>

<span data-ttu-id="9f807-103">В этом примере показано, как асинхронно выполнять команды с помощью пространств выполнения пула.</span><span class="sxs-lookup"><span data-stu-id="9f807-103">This sample shows how to run commands asynchronously by using the runspaces of a runspace pool.</span></span> <span data-ttu-id="9f807-104">В примере создается список команд, а затем выполняется выполнение этих команд, когда подсистема Windows PowerShell открывает пространство выполнения из пула, когда оно требуется.</span><span class="sxs-lookup"><span data-stu-id="9f807-104">The sample generates a list of commands, and then runs those commands while the Windows PowerShell engine opens a runspace from the pool when it is needed.</span></span>

## <a name="requirements"></a><span data-ttu-id="9f807-105">Требования</span><span class="sxs-lookup"><span data-stu-id="9f807-105">Requirements</span></span>

- <span data-ttu-id="9f807-106">Для работы с этим образцом требуется Windows PowerShell 2,0.</span><span class="sxs-lookup"><span data-stu-id="9f807-106">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="9f807-107">Демонстрирующее</span><span class="sxs-lookup"><span data-stu-id="9f807-107">Demonstrates</span></span>

<span data-ttu-id="9f807-108">В этом образце демонстрируется следующее.</span><span class="sxs-lookup"><span data-stu-id="9f807-108">This sample demonstrates the following:</span></span>

- <span data-ttu-id="9f807-109">Создание объекта Рунспацепул с минимальным и максимальным числом пространств выполнения, которые могут быть открыты одновременно.</span><span class="sxs-lookup"><span data-stu-id="9f807-109">Creating a RunspacePool object with a minimum and maximum number of runspaces allowed to be open at the same time.</span></span>

- <span data-ttu-id="9f807-110">Создание списка команд.</span><span class="sxs-lookup"><span data-stu-id="9f807-110">Creating a list of commands.</span></span>

- <span data-ttu-id="9f807-111">Асинхронное выполнение команд.</span><span class="sxs-lookup"><span data-stu-id="9f807-111">Running the commands asynchronously.</span></span>

- <span data-ttu-id="9f807-112">Вызов метода [System. Management. Automation. пространства выполнения. рунспацепул. жетаваилаблерунспацес \*](/dotnet/api/System.Management.Automation.Runspaces.RunspacePool.GetAvailableRunspaces) , чтобы узнать, сколько пространств выполнения свободно.</span><span class="sxs-lookup"><span data-stu-id="9f807-112">Calling the [System.Management.Automation.Runspaces.Runspacepool.Getavailablerunspaces\*](/dotnet/api/System.Management.Automation.Runspaces.RunspacePool.GetAvailableRunspaces) method to see how many runspaces are free.</span></span>

- <span data-ttu-id="9f807-113">Запись выходных данных команды с помощью метода [System. Management. Automation. PowerShell. EndInvoke \*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) .</span><span class="sxs-lookup"><span data-stu-id="9f807-113">Capturing the command output with the [System.Management.Automation.Powershell.Endinvoke\*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) method.</span></span>

## <a name="example"></a><span data-ttu-id="9f807-114">Пример</span><span class="sxs-lookup"><span data-stu-id="9f807-114">Example</span></span>

<span data-ttu-id="9f807-115">В этом образце показано, как открыть пространства выполнения пула и как асинхронно выполнять команды в этих пространствах.</span><span class="sxs-lookup"><span data-stu-id="9f807-115">This sample shows how to open the runspaces of a runspace pool, and how to asynchronously run commands in those runspaces.</span></span>

[!code-csharp[PowerShell02.cs](../../../../powershell-sdk-samples/SDK-2.0/csharp/PowerShell02/PowerShell02.cs#L11-L96 "PowerShell02.cs")]

## <a name="see-also"></a><span data-ttu-id="9f807-116">См. также:</span><span class="sxs-lookup"><span data-stu-id="9f807-116">See Also</span></span>

[<span data-ttu-id="9f807-117">Написание ведущего приложения Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f807-117">Writing a Windows PowerShell Host Application</span></span>](./writing-a-windows-powershell-host-application.md)