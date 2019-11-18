---
title: Создание рабочего процесса с помощью действий Windows PowerShell | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fb55971a-4ea4-4c51-aeff-4e0bb05a51b2
caps.latest.revision: 6
ms.openlocfilehash: 98cac43698b3f537ee318cd2570b2174631665a7
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72359633"
---
# <a name="creating-a-workflow-with-windows-powershell-activities"></a><span data-ttu-id="3f4bf-102">Создание рабочего процесса с помощью действий Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f4bf-102">Creating a Workflow with Windows PowerShell Activities</span></span>

<span data-ttu-id="3f4bf-103">Вы можете создать рабочий процесс Windows PowerShell, выбрав действия из панели элементов Visual Studio и перетащив их в окно конструктор рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-103">You can create a Windows PowerShell workflow by selecting activities from the Visual Studio Toolbox and dragging them to the Workflow Designer window.</span></span> <span data-ttu-id="3f4bf-104">Сведения о добавлении действий Windows PowerShell в панель элементов Visual Studio см. в разделе [Добавление действий Windows PowerShell в панель элементов Visual Studio](./adding-windows-powershell-activities-to-the-visual-studio-toolbox.md).</span><span class="sxs-lookup"><span data-stu-id="3f4bf-104">For information about adding Windows PowerShell activities to the Visual Studio Toolbox, see [Adding Windows PowerShell Activities to the Visual Studio Toolbox](./adding-windows-powershell-activities-to-the-visual-studio-toolbox.md).</span></span>

<span data-ttu-id="3f4bf-105">В следующих процедурах описывается создание рабочего процесса, который проверяет состояние домена указанных пользователем компьютеров, присоединяет их к домену, если они еще не присоединены, а затем снова проверяет состояние.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-105">The following procedures describe how to create a workflow that checks the domain status of a group of user-specified computers, joins them to a domain if they are not already joined, and then checks the status again.</span></span>

### <a name="setting-up-the-project"></a><span data-ttu-id="3f4bf-106">Настройка проекта</span><span class="sxs-lookup"><span data-stu-id="3f4bf-106">Setting up the Project</span></span>

1. <span data-ttu-id="3f4bf-107">Выполните процедуру, описанную в разделе [Добавление действий Windows PowerShell в панель элементов Visual Studio](./adding-windows-powershell-activities-to-the-visual-studio-toolbox.md) , чтобы создать проект рабочего процесса и добавить действия из [Microsoft. PowerShell. activitys](/dotnet/api/Microsoft.PowerShell.Activities) и [Microsoft. PowerShell. Management. activitys. ](/dotnet/api/Microsoft.PowerShell.Management.Activities)сборки на панель элементов.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-107">Follow the procedure in [Adding Windows PowerShell Activities to the Visual Studio Toolbox](./adding-windows-powershell-activities-to-the-visual-studio-toolbox.md) to create a workflow project and add the activities from the [Microsoft.Powershell.Activities](/dotnet/api/Microsoft.PowerShell.Activities) and [Microsoft.Powershell.Management.Activities](/dotnet/api/Microsoft.PowerShell.Management.Activities) assemblies to the toolbox.</span></span>

2. <span data-ttu-id="3f4bf-108">Добавьте System. Management. Automation, Microsoft. PowerShell. Activitys, System. Management, Microsoft. PowerShell. Management. Activitys и Microsoft. PowerShell. Commands. Management как в проект в качестве эталонных сборок.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-108">Add System.Management.Automation, Microsoft.PowerShell.Activities, System.Management, Microsoft.PowerShell.Management.Activities, and Microsoft.PowerShell.Commands.Management as to the project as reference assemblies.</span></span>

### <a name="adding-activities-to-the-workflow"></a><span data-ttu-id="3f4bf-109">Добавление действий в рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="3f4bf-109">Adding Activities to the Workflow</span></span>

1. <span data-ttu-id="3f4bf-110">Добавьте действие **Sequence** в рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-110">Add a **Sequence** activity to the workflow.</span></span>

2. <span data-ttu-id="3f4bf-111">Создайте аргумент с именем `ComputerName` с типом аргумента `String[]`.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-111">Create an argument named `ComputerName` with an argument type of `String[]`.</span></span> <span data-ttu-id="3f4bf-112">Этот аргумент представляет имена компьютеров для проверки и присоединение.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-112">This argument represents the names of the computers to check and join.</span></span>

3. <span data-ttu-id="3f4bf-113">Создайте аргумент с именем `DomainCred` типа [System. Management. Automation. PSCredential](/dotnet/api/System.Management.Automation.PSCredential).</span><span class="sxs-lookup"><span data-stu-id="3f4bf-113">Create an argument named `DomainCred` of type [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential).</span></span> <span data-ttu-id="3f4bf-114">Этот аргумент представляет учетные данные домена учетной записи домена, которая имеет право присоединить компьютер к домену.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-114">This argument represents the domain credentials of a domain account that is authorized to join a computer to the domain.</span></span>

4. <span data-ttu-id="3f4bf-115">Создайте аргумент с именем `MachineCred` типа [System. Management. Automation. PSCredential](/dotnet/api/System.Management.Automation.PSCredential).</span><span class="sxs-lookup"><span data-stu-id="3f4bf-115">Create an argument named `MachineCred` of type [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential).</span></span> <span data-ttu-id="3f4bf-116">Этот аргумент представляет учетные данные администратора на компьютерах, которые необходимо проверить и присоединить.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-116">This argument represents the credentials of an administrator on the computers to check and join.</span></span>

5. <span data-ttu-id="3f4bf-117">Добавьте действие **ParallelForEach** в действие **Sequence** .</span><span class="sxs-lookup"><span data-stu-id="3f4bf-117">Add a **ParallelForEach** activity inside the **Sequence** activity.</span></span> <span data-ttu-id="3f4bf-118">Введите `comp` и `ComputerName` в текстовые поля, чтобы цикл пробирал элементы массива `ComputerName`.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-118">Enter `comp` and `ComputerName` in the text boxes so that the loop iterates through the elements of the `ComputerName` array.</span></span>

6. <span data-ttu-id="3f4bf-119">Добавьте действие **Sequence** в тело действия **ParallelForEach** .</span><span class="sxs-lookup"><span data-stu-id="3f4bf-119">Add a **Sequence** activity to the body of the **ParallelForEach** activity.</span></span> <span data-ttu-id="3f4bf-120">Задайте для свойства **DisplayName** последовательности значение `JoinDomain`.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-120">Set the **DisplayName** property of the sequence to `JoinDomain`.</span></span>

7. <span data-ttu-id="3f4bf-121">Добавьте действие **жетвмиобжект** в последовательность **JoinDomain** .</span><span class="sxs-lookup"><span data-stu-id="3f4bf-121">Add a **GetWmiObject** activity to the **JoinDomain** sequence.</span></span>

8. <span data-ttu-id="3f4bf-122">Измените свойства действия **жетвмиобжект** следующим образом.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-122">Edit the properties of the **GetWmiObject** activity as follows.</span></span>

   |<span data-ttu-id="3f4bf-123">Свойство</span><span class="sxs-lookup"><span data-stu-id="3f4bf-123">Property</span></span>|<span data-ttu-id="3f4bf-124">Применение</span><span class="sxs-lookup"><span data-stu-id="3f4bf-124">Value</span></span>|
   |--------------|-----------|
   |<span data-ttu-id="3f4bf-125">**См**</span><span class="sxs-lookup"><span data-stu-id="3f4bf-125">**Class**</span></span>|<span data-ttu-id="3f4bf-126">"Win32_ComputerSystem"</span><span class="sxs-lookup"><span data-stu-id="3f4bf-126">"Win32_ComputerSystem"</span></span>|
   |<span data-ttu-id="3f4bf-127">**PSComputerName**</span><span class="sxs-lookup"><span data-stu-id="3f4bf-127">**PSComputerName**</span></span>|<span data-ttu-id="3f4bf-128">соответствовал</span><span class="sxs-lookup"><span data-stu-id="3f4bf-128">{comp}</span></span>|
   |<span data-ttu-id="3f4bf-129">**PSCredential**</span><span class="sxs-lookup"><span data-stu-id="3f4bf-129">**PSCredential**</span></span>|<span data-ttu-id="3f4bf-130">мачинекред</span><span class="sxs-lookup"><span data-stu-id="3f4bf-130">MachineCred</span></span>|

9. <span data-ttu-id="3f4bf-131">Добавьте действие **аддкомпутер** в последовательность **JoinDomain** после действия **жетвмиобжект** .</span><span class="sxs-lookup"><span data-stu-id="3f4bf-131">Add an **AddComputer** activity to the **JoinDomain** sequence after the **GetWmiObject** activity.</span></span>

10. <span data-ttu-id="3f4bf-132">Измените свойства действия **аддкомпутер** следующим образом.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-132">Edit the properties of the **AddComputer** activity as follows.</span></span>

    |<span data-ttu-id="3f4bf-133">Свойство</span><span class="sxs-lookup"><span data-stu-id="3f4bf-133">Property</span></span>|<span data-ttu-id="3f4bf-134">Применение</span><span class="sxs-lookup"><span data-stu-id="3f4bf-134">Value</span></span>|
    |--------------|-----------|
    |<span data-ttu-id="3f4bf-135">**ComputerName**</span><span class="sxs-lookup"><span data-stu-id="3f4bf-135">**ComputerName**</span></span>|<span data-ttu-id="3f4bf-136">соответствовал</span><span class="sxs-lookup"><span data-stu-id="3f4bf-136">{comp}</span></span>|
    |<span data-ttu-id="3f4bf-137">**домаинкредентиал**</span><span class="sxs-lookup"><span data-stu-id="3f4bf-137">**DomainCredential**</span></span>|<span data-ttu-id="3f4bf-138">домаинкред</span><span class="sxs-lookup"><span data-stu-id="3f4bf-138">DomainCred</span></span>|

11. <span data-ttu-id="3f4bf-139">Добавьте действие **рестарткомпутер** в последовательность **JoinDomain** после действия **аддкомпутер** .</span><span class="sxs-lookup"><span data-stu-id="3f4bf-139">Add a **RestartComputer** activity to the **JoinDomain** sequence after the **AddComputer** activity.</span></span>

12. <span data-ttu-id="3f4bf-140">Измените свойства действия **рестарткомпутер** следующим образом.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-140">Edit the properties of the **RestartComputer** activity as follows.</span></span>

    |<span data-ttu-id="3f4bf-141">Свойство</span><span class="sxs-lookup"><span data-stu-id="3f4bf-141">Property</span></span>|<span data-ttu-id="3f4bf-142">Применение</span><span class="sxs-lookup"><span data-stu-id="3f4bf-142">Value</span></span>|
    |--------------|-----------|
    |<span data-ttu-id="3f4bf-143">**ComputerName**</span><span class="sxs-lookup"><span data-stu-id="3f4bf-143">**ComputerName**</span></span>|<span data-ttu-id="3f4bf-144">соответствовал</span><span class="sxs-lookup"><span data-stu-id="3f4bf-144">{comp}</span></span>|
    |<span data-ttu-id="3f4bf-145">**Записям**</span><span class="sxs-lookup"><span data-stu-id="3f4bf-145">**Credential**</span></span>|<span data-ttu-id="3f4bf-146">мачинекред</span><span class="sxs-lookup"><span data-stu-id="3f4bf-146">MachineCred</span></span>|
    |<span data-ttu-id="3f4bf-147">**Предмет**</span><span class="sxs-lookup"><span data-stu-id="3f4bf-147">**For**</span></span>|<span data-ttu-id="3f4bf-148">Microsoft. PowerShell. Commands. Ваитфорсервицетипес. PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f4bf-148">Microsoft.PowerShell.Commands.WaitForServiceTypes.PowerShell</span></span>|
    |<span data-ttu-id="3f4bf-149">**Перевести**</span><span class="sxs-lookup"><span data-stu-id="3f4bf-149">**Force**</span></span>|<span data-ttu-id="3f4bf-150">True</span><span class="sxs-lookup"><span data-stu-id="3f4bf-150">True</span></span>|
    |<span data-ttu-id="3f4bf-151">Wait</span><span class="sxs-lookup"><span data-stu-id="3f4bf-151">Wait</span></span>|<span data-ttu-id="3f4bf-152">True</span><span class="sxs-lookup"><span data-stu-id="3f4bf-152">True</span></span>|
    |<span data-ttu-id="3f4bf-153">PSComputerName</span><span class="sxs-lookup"><span data-stu-id="3f4bf-153">PSComputerName</span></span>|<span data-ttu-id="3f4bf-154">{""}</span><span class="sxs-lookup"><span data-stu-id="3f4bf-154">{""}</span></span>|

13. <span data-ttu-id="3f4bf-155">Добавьте действие **жетвмиобжект** в последовательность **JoinDomain** после действия **рестарткомпутер** .</span><span class="sxs-lookup"><span data-stu-id="3f4bf-155">Add a **GetWmiObject** activity to the **JoinDomain** sequence after the **RestartComputer** activity.</span></span> <span data-ttu-id="3f4bf-156">Измените его свойства, чтобы они совпадали с предыдущим действием **жетвмиобжект** .</span><span class="sxs-lookup"><span data-stu-id="3f4bf-156">Edit its properties to be the same as the previous **GetWmiObject** activity.</span></span>

    <span data-ttu-id="3f4bf-157">После завершения процедур окно конструктора рабочих процессов должно выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="3f4bf-157">When you have finished the procedures, the workflow design window should look like this.</span></span>

    <span data-ttu-id="3f4bf-158">![JoinDomain XAML в конструкторе рабочих процессов @ no__t-1![JOINDOMAIN XAML в конструкторе рабочих процессов](../media/joindomainworkflow.png "жоиндомаинворкфлов")</span><span class="sxs-lookup"><span data-stu-id="3f4bf-158">![JoinDomain XAML in Workflow designer](../media/joindomainworkflow.png)
    ![JoinDomain XAML in Workflow designer](../media/joindomainworkflow.png "JoinDomainWorkflow")</span></span>