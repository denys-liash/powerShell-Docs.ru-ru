---
title: Runspace01 пример кода (VB.NET) | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 12ee5382-95ba-41c7-8291-7f69a6f63514
caps.latest.revision: 7
ms.openlocfilehash: c45e802605bf0b4fd84a8847787bcc937b7f417b
ms.sourcegitcommit: 69abc5ad16e5dd29ddfb1853e266a4bfd1d59d59
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2019
ms.locfileid: "57429777"
---
# <a name="runspace01-vbnet-code-sample"></a><span data-ttu-id="c94ca-102">Пример кода Runspace01 (VB.NET)</span><span class="sxs-lookup"><span data-stu-id="c94ca-102">Runspace01 (VB.NET) Code Sample</span></span>

<span data-ttu-id="c94ca-103">Ниже приведены примеры кода для пространства выполнения, описанных в [Создание консольного приложения, запускающегося команды указан](http://msdn.microsoft.com/en-us/793a6570-a072-4799-840b-172f28ce620e).</span><span class="sxs-lookup"><span data-stu-id="c94ca-103">Here are the code samples for the runspace described in [Creating a Console Application That Runs a Specified Command](http://msdn.microsoft.com/en-us/793a6570-a072-4799-840b-172f28ce620e).</span></span> <span data-ttu-id="c94ca-104">Чтобы сделать это, приложение вызывает пространство выполнения и затем вызывает команду.</span><span class="sxs-lookup"><span data-stu-id="c94ca-104">To do this, the application invokes a runspace, and then invokes a command.</span></span> <span data-ttu-id="c94ca-105">(Обратите внимание, что это приложение не содержит сведения о конфигурации пространства выполнения, а также его явным образом создает конвейер.) Команда, вызываемая `Get-Process` командлета.</span><span class="sxs-lookup"><span data-stu-id="c94ca-105">(Note that this application does not specify runspace configuration information, nor does it explicitly create a pipeline.) The command that is invoked is the `Get-Process` cmdlet.</span></span>

## <a name="code-sample"></a><span data-ttu-id="c94ca-106">Пример кода</span><span class="sxs-lookup"><span data-stu-id="c94ca-106">Code Sample</span></span>

```vb
Imports System
Imports System.Collections.Generic
Imports System.Text
Imports System.Management.Automation
Imports System.Management.Automation.Host
Imports System.Management.Automation.Runspaces

Namespace Microsoft.Samples.PowerShell.Runspaces

    Module Runspace01
        ' <summary>
        ' This sample uses the RunspaceInvoke class to execute
        ' the get-process cmdlet synchronously. The name and
        ' handlecount are then extracted from  the PSObjects
        ' returned and displayed.
        ' </summary>
        ' <param name="args">Unused</param>
        ' <remarks>
        ' This sample demonstrates the following:
        ' 1. Creating an instance of the RunspaceInvoke class.
        ' 2. Using this instance to invoke a PowerShell command.
        ' 3. Using PSObject to extract properties from the objects
        '    returned by this command.
        ' </remarks>
        Sub Main()
            ' Create an instance of the RunspaceInvoke class.
            ' This takes care of all building all of the other
            ' data structures needed...
            Dim invoker As RunspaceInvoke = New RunspaceInvoke()

            Console.WriteLine("Process              HandleCount")
            Console.WriteLine("--------------------------------")

            ' Now invoke the runspace and display the objects that are
            ' returned...
            For Each result As PSObject In invoker.Invoke("get-process")
                Console.WriteLine("{0,-20} {1}", _
                    result.Members("ProcessName").Value, _
                    result.Members("HandleCount").Value)
            Next
            System.Console.WriteLine("Hit any key to exit...")
            System.Console.ReadKey()
        End Sub
    End Module
End Namespace
```

<!-- TODO!!!: [!code-csharp[Runspace01.vb](../../powershell-sdk-samples/SDK-2.0/vb/Runspace01/Runspace01.vb#L09-L53 "Runspace01.vb")] -->

## <a name="see-also"></a><span data-ttu-id="c94ca-107">См. также</span><span class="sxs-lookup"><span data-stu-id="c94ca-107">See Also</span></span>

[<span data-ttu-id="c94ca-108">Пакет SDK для Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c94ca-108">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)