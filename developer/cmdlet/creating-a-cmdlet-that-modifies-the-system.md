---
title: Создание командлета, который изменяет система | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- should process [PowerShell Programmer's Guide]
- should continue [PowerShell Programmer's Guide]
- user feedback [PowerShell Programmer's Guide]
- confirm impact [PowerShell Programmer's Guide]
ms.assetid: 59be4120-1700-4d92-a308-ef4a32ccf11a
caps.latest.revision: 8
ms.openlocfilehash: d93cc4a05a6625d073791c067d1e9b6662c3a565
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56856340"
---
# <a name="creating-a-cmdlet-that-modifies-the-system"></a><span data-ttu-id="f3c57-102">Создание командлета, который изменяет систему</span><span class="sxs-lookup"><span data-stu-id="f3c57-102">Creating a Cmdlet that Modifies the System</span></span>

<span data-ttu-id="f3c57-103">Иногда командлета необходимо изменить состояние системы, а не только состояние среды выполнения Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3c57-103">Sometimes a cmdlet must modify the running state of the system, not just the state of the Windows PowerShell runtime.</span></span> <span data-ttu-id="f3c57-104">В этих случаях командлет должен позволять пользователю шанс подтвердить необходимость внесения изменений.</span><span class="sxs-lookup"><span data-stu-id="f3c57-104">In these cases, the cmdlet should allow the user a chance to confirm whether or not to make the change.</span></span>

<span data-ttu-id="f3c57-105">Для поддержки подтверждения командлета необходимо сделать две вещи.</span><span class="sxs-lookup"><span data-stu-id="f3c57-105">To support confirmation a cmdlet must do two things.</span></span>

- <span data-ttu-id="f3c57-106">Объявите, что командлет поддерживает подтверждение при указании [System.Management.Automation.Cmdletattribute](/dotnet/api/System.Management.Automation.CmdletAttribute) атрибута, задав ключевое слово SupportsShouldProcess `true`.</span><span class="sxs-lookup"><span data-stu-id="f3c57-106">Declare that the cmdlet supports confirmation when you specify the [System.Management.Automation.Cmdletattribute](/dotnet/api/System.Management.Automation.CmdletAttribute) attribute by setting the SupportsShouldProcess keyword to `true`.</span></span>

- <span data-ttu-id="f3c57-107">Вызовите [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) во время выполнения командлета (как показано в следующем примере).</span><span class="sxs-lookup"><span data-stu-id="f3c57-107">Call [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) during the execution of the cmdlet (as shown in the following example).</span></span>

<span data-ttu-id="f3c57-108">Благодаря поддержке подтверждения, предоставляет командлет `Confirm` и `WhatIf` параметры, предоставляемые Windows PowerShell, а также соответствуют рекомендации по разработке для командлетов (Дополнительные сведения о рекомендации по разработке командлет, см. в разделе [ Рекомендации по разработке командлет](./cmdlet-development-guidelines.md).).</span><span class="sxs-lookup"><span data-stu-id="f3c57-108">By supporting confirmation, a cmdlet exposes the `Confirm` and `WhatIf` parameters that are provided by Windows PowerShell, and also meets the development guidelines for cmdlets (For more information about cmdlet development guidelines, see [Cmdlet Development Guidelines](./cmdlet-development-guidelines.md).).</span></span>

## <a name="changing-the-system"></a><span data-ttu-id="f3c57-109">Изменение системы</span><span class="sxs-lookup"><span data-stu-id="f3c57-109">Changing the System</span></span>

<span data-ttu-id="f3c57-110">Операция «Изменение системы» относится к любой командлет, потенциально изменяет состояние системы за пределами Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3c57-110">The act of "changing the system" refers to any cmdlet that potentially changes the state of the system outside Windows PowerShell.</span></span> <span data-ttu-id="f3c57-111">Например остановка процесса, включение или отключение учетной записи пользователя или добавление строк в таблицу базы данных являются все изменения в системе, которая должна быть подтверждена.</span><span class="sxs-lookup"><span data-stu-id="f3c57-111">For example, stopping a process, enabling or disabling a user account, or adding a row to a database table are all changes to the system that should be confirmed.</span></span> <span data-ttu-id="f3c57-112">Напротив операции, которые считывать данные, или установить временные подключения и не меняются системы обычно не требуют подтверждение.</span><span class="sxs-lookup"><span data-stu-id="f3c57-112">In contrast, operations that read data or establish transient connections do not change the system and generally do not require confirmation.</span></span> <span data-ttu-id="f3c57-113">Подтверждения не требуется также для действий, эффект которого ограничено внутри среды выполнения Windows PowerShell, такие как `set-variable`.</span><span class="sxs-lookup"><span data-stu-id="f3c57-113">Confirmation is also not needed for actions whose effect is limited to inside the Windows PowerShell runtime, such as `set-variable`.</span></span> <span data-ttu-id="f3c57-114">Командлеты, которые могут или не может внести постоянные изменения должны объявлять `SupportsShouldProcess` и вызвать [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) только в том случае, если они будут внесены постоянные изменения.</span><span class="sxs-lookup"><span data-stu-id="f3c57-114">Cmdlets that might or might not make a persistent change should declare `SupportsShouldProcess` and call [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) only if they are about to make a persistent change.</span></span>

> [!NOTE]
> <span data-ttu-id="f3c57-115">Подтверждение ShouldProcess применяется только к командлетам.</span><span class="sxs-lookup"><span data-stu-id="f3c57-115">ShouldProcess confirmation applies only to cmdlets.</span></span> <span data-ttu-id="f3c57-116">Если команда или сценарий изменяет состояние системы путем прямого вызова методов .NET или свойства, или вызывающий приложениями за пределы Windows PowerShell, эта форма подтверждения будет недоступен.</span><span class="sxs-lookup"><span data-stu-id="f3c57-116">If a command or script modifies the running state of a system by directly calling .NET methods or properties, or by calling applications outside of Windows PowerShell, this form of confirmation will not be available.</span></span>

## <a name="the-stopproc-cmdlet"></a><span data-ttu-id="f3c57-117">Командлет StopProc</span><span class="sxs-lookup"><span data-stu-id="f3c57-117">The StopProc Cmdlet</span></span>

<span data-ttu-id="f3c57-118">В этом разделе описывается командлет Stop-Proc, который пытается остановить процессы, которые можно получить с помощью командлета Get-Proc (описано в разделе [Создание свой первый командлет](./creating-a-cmdlet-without-parameters.md)).</span><span class="sxs-lookup"><span data-stu-id="f3c57-118">This topic describes a Stop-Proc cmdlet that attempts to stop processes that are retrieved using the Get-Proc cmdlet (described in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md)).</span></span>

<span data-ttu-id="f3c57-119">Следующие подразделы этого раздела.</span><span class="sxs-lookup"><span data-stu-id="f3c57-119">Topics in this section include the following:</span></span>

- [<span data-ttu-id="f3c57-120">Определение командлета</span><span class="sxs-lookup"><span data-stu-id="f3c57-120">Defining the Cmdlet</span></span>](#Defining-the-Cmdlet)

- [<span data-ttu-id="f3c57-121">Определение параметров для изменения системы</span><span class="sxs-lookup"><span data-stu-id="f3c57-121">Defining Parameters for System Modification</span></span>](#Defining-Parameters-for-System-Modification)

- [<span data-ttu-id="f3c57-122">Переопределив метод обработки входных данных</span><span class="sxs-lookup"><span data-stu-id="f3c57-122">Overriding an Input Processing Method</span></span>](#Overriding-an-Input-Processing-Method)

- [<span data-ttu-id="f3c57-123">Вызов метода ShouldProcess</span><span class="sxs-lookup"><span data-stu-id="f3c57-123">Calling the ShouldProcess Method</span></span>](#Calling-the-ShouldProcess-Method)

- [<span data-ttu-id="f3c57-124">Вызов метода ShouldContinue</span><span class="sxs-lookup"><span data-stu-id="f3c57-124">Calling the ShouldContinue Method</span></span>](#Calling-the-ShouldContinue-Method)

- [<span data-ttu-id="f3c57-125">Остановка обработки ввода</span><span class="sxs-lookup"><span data-stu-id="f3c57-125">Stopping Input Processing</span></span>](#Stopping-Input-Processing)

- [<span data-ttu-id="f3c57-126">Пример кода</span><span class="sxs-lookup"><span data-stu-id="f3c57-126">Code Sample</span></span>](#Code-Sample)

- [<span data-ttu-id="f3c57-127">Определение типов объектов и форматирование</span><span class="sxs-lookup"><span data-stu-id="f3c57-127">Defining Object Types and Formatting</span></span>](#Defining-Object-Types-and-Formatting)

- [<span data-ttu-id="f3c57-128">Создание командлета</span><span class="sxs-lookup"><span data-stu-id="f3c57-128">Building the Cmdlet</span></span>](#Building-the-Cmdlet)

- [<span data-ttu-id="f3c57-129">Тестирование командлет</span><span class="sxs-lookup"><span data-stu-id="f3c57-129">Testing the Cmdlet</span></span>](#Testing-the-Cmdlet)

## <a name="defining-the-cmdlet"></a><span data-ttu-id="f3c57-130">Определение командлета</span><span class="sxs-lookup"><span data-stu-id="f3c57-130">Defining the Cmdlet</span></span>

<span data-ttu-id="f3c57-131">Первым шагом в создании командлет всегда присвоение имени командлета и объявление класса .NET, который реализует командлет.</span><span class="sxs-lookup"><span data-stu-id="f3c57-131">The first step in cmdlet creation is always naming the cmdlet and declaring the .NET class that implements the cmdlet.</span></span> <span data-ttu-id="f3c57-132">Так как вы записываете командлета для изменения системы, его имя должно соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="f3c57-132">Because you are writing a cmdlet to change the system, it should be named accordingly.</span></span> <span data-ttu-id="f3c57-133">Этот командлет останавливает системные процессы, чтобы имя команды, выбираем «Stop», определяемый [System.Management.Automation.Verbslifecycle](/dotnet/api/System.Management.Automation.VerbsLifeCycle) класс с существительным «Proc», чтобы указать, что командлет останавливает процессы.</span><span class="sxs-lookup"><span data-stu-id="f3c57-133">This cmdlet stops system processes, so the verb name chosen here is "Stop", defined by the [System.Management.Automation.Verbslifecycle](/dotnet/api/System.Management.Automation.VerbsLifeCycle) class, with the noun "Proc" to indicate that the cmdlet stops processes.</span></span> <span data-ttu-id="f3c57-134">Дополнительные сведения о командлет утвержденные глаголы, см. в разделе [имен команд командлет](./approved-verbs-for-windows-powershell-commands.md).</span><span class="sxs-lookup"><span data-stu-id="f3c57-134">For more information about approved cmdlet verbs, see [Cmdlet Verb Names](./approved-verbs-for-windows-powershell-commands.md).</span></span>

<span data-ttu-id="f3c57-135">Ниже приведен в определении класса для этого командлета Stop-Proc.</span><span class="sxs-lookup"><span data-stu-id="f3c57-135">The following is the class definition for this Stop-Proc cmdlet.</span></span>

```csharp
[Cmdlet(VerbsLifecycle.Stop, "Proc",
        SupportsShouldProcess = true)]
public class StopProcCommand : Cmdlet
```

<span data-ttu-id="f3c57-136">Имейте в виду, что в [System.Management.Automation.Cmdletattribute](/dotnet/api/System.Management.Automation.CmdletAttribute) объявление, `SupportsShouldProcess` атрибут ключевого слова задано `true` для включения командлет, чтобы выполнять вызовы [ System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) и [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).</span><span class="sxs-lookup"><span data-stu-id="f3c57-136">Be aware that in the [System.Management.Automation.Cmdletattribute](/dotnet/api/System.Management.Automation.CmdletAttribute) declaration, the `SupportsShouldProcess` attribute keyword is set to `true` to enable the cmdlet to make calls to [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) and [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).</span></span> <span data-ttu-id="f3c57-137">Без этого набора ключевое слово `Confirm` и `WhatIf` параметры не будут доступны пользователю.</span><span class="sxs-lookup"><span data-stu-id="f3c57-137">Without this keyword set, the `Confirm` and `WhatIf` parameters will not be available to the user.</span></span>

### <a name="extremely-destructive-actions"></a><span data-ttu-id="f3c57-138">Очень разрушительные действия</span><span class="sxs-lookup"><span data-stu-id="f3c57-138">Extremely Destructive Actions</span></span>

<span data-ttu-id="f3c57-139">Некоторые операции являются очень уничтожения данных, например переформатирования active жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="f3c57-139">Some operations are extremely destructive, such as reformatting an active hard disk partition.</span></span> <span data-ttu-id="f3c57-140">В этих случаях следует установить командлет `ConfirmImpact`  =  `ConfirmImpact.High` при объявлении [System.Management.Automation.Cmdletattribute](/dotnet/api/System.Management.Automation.CmdletAttribute) атрибута.</span><span class="sxs-lookup"><span data-stu-id="f3c57-140">In these cases, the cmdlet should set `ConfirmImpact` = `ConfirmImpact.High` when declaring the [System.Management.Automation.Cmdletattribute](/dotnet/api/System.Management.Automation.CmdletAttribute) attribute.</span></span> <span data-ttu-id="f3c57-141">Этот параметр заставляет командлет для запроса подтверждения пользователя, даже в том случае, если пользователь не указал `Confirm` параметра.</span><span class="sxs-lookup"><span data-stu-id="f3c57-141">This setting forces the cmdlet to request user confirmation even when the user has not specified the `Confirm` parameter.</span></span> <span data-ttu-id="f3c57-142">Тем не менее, разработчикам командлетов следует избегать чрезмерное `ConfirmImpact` для операций, которые являются просто потенциально необратимыми, например, удаление учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="f3c57-142">However, cmdlet developers should avoid overusing `ConfirmImpact` for operations that are just potentially destructive, such as deleting a user account.</span></span> <span data-ttu-id="f3c57-143">Помните, что если `ConfirmImpact` присваивается [System.Management.Automation.Confirmimpact.High](/dotnet/api/System.Management.Automation.ConfirmImpact.High).</span><span class="sxs-lookup"><span data-stu-id="f3c57-143">Remember that if `ConfirmImpact` is set to [System.Management.Automation.Confirmimpact.High](/dotnet/api/System.Management.Automation.ConfirmImpact.High).</span></span>

<span data-ttu-id="f3c57-144">Аналогично некоторые операции вряд ли уничтожения данных, несмотря на то, что они в теории изменяют состояние системы за пределами Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3c57-144">Similarly, some operations are unlikely to be destructive, although they do in theory modify the running state of a system outside Windows PowerShell.</span></span> <span data-ttu-id="f3c57-145">Можно задать такие командлеты `ConfirmImpact` для [System.Management.Automation.Confirmimpact.Low](/dotnet/api/system.management.automation.confirmimpact?view=powershellsdk-1.1.0).</span><span class="sxs-lookup"><span data-stu-id="f3c57-145">Such cmdlets can set `ConfirmImpact` to [System.Management.Automation.Confirmimpact.Low](/dotnet/api/system.management.automation.confirmimpact?view=powershellsdk-1.1.0).</span></span> <span data-ttu-id="f3c57-146">Эта конструкция запросы подтверждения, где пользователю поступает запрос на подтверждение операции только влияние medium и значительное влияние.</span><span class="sxs-lookup"><span data-stu-id="f3c57-146">This will bypass confirmation requests where the user has asked to confirm only medium-impact and high-impact operations.</span></span>

## <a name="defining-parameters-for-system-modification"></a><span data-ttu-id="f3c57-147">Определение параметров для изменения системы</span><span class="sxs-lookup"><span data-stu-id="f3c57-147">Defining Parameters for System Modification</span></span>

<span data-ttu-id="f3c57-148">В этом разделе описывается, как задать параметры командлета, включая те, которые необходимы для поддержки системы изменения.</span><span class="sxs-lookup"><span data-stu-id="f3c57-148">This section describes how to define the cmdlet parameters, including those that are needed to support system modification.</span></span> <span data-ttu-id="f3c57-149">См. в разделе [Добавление параметров командной строки этого процесса входа](./adding-parameters-that-process-command-line-input.md) Общие сведения об определении параметров.</span><span class="sxs-lookup"><span data-stu-id="f3c57-149">See [Adding Parameters that Process CommandLine Input](./adding-parameters-that-process-command-line-input.md) if you need general information about defining parameters.</span></span>

<span data-ttu-id="f3c57-150">Командлет Stop-Proc определяет три параметра: `Name`, `Force`, и `PassThru`.</span><span class="sxs-lookup"><span data-stu-id="f3c57-150">The Stop-Proc cmdlet defines three parameters: `Name`, `Force`, and `PassThru`.</span></span>

<span data-ttu-id="f3c57-151">`Name` Параметр соответствует параметру `Name` свойства входного объекта процесса.</span><span class="sxs-lookup"><span data-stu-id="f3c57-151">The `Name` parameter corresponds to the `Name` property of the process input object.</span></span> <span data-ttu-id="f3c57-152">Имейте в виду, что `Name` параметр в этом образце обязателен, так как командлет завершится ошибкой, если он не имеет именованный процесс для остановки.</span><span class="sxs-lookup"><span data-stu-id="f3c57-152">Be aware that the `Name` parameter in this sample is mandatory, as the cmdlet will fail if it does not have a named process to stop.</span></span>

<span data-ttu-id="f3c57-153">`Force` Параметр позволяет переопределить вызовы [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).</span><span class="sxs-lookup"><span data-stu-id="f3c57-153">The `Force` parameter allows the user to override calls to [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).</span></span> <span data-ttu-id="f3c57-154">На самом деле, любой командлет, который вызывает [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) должны иметь `Force` параметр, чтобы при `Force` указан, командлет пропускает вызов [ System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) , после чего с операцией.</span><span class="sxs-lookup"><span data-stu-id="f3c57-154">In fact, any cmdlet that calls [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) should have a `Force` parameter so that when `Force` is specified, the cmdlet skips the call to [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) and proceeds with the operation.</span></span> <span data-ttu-id="f3c57-155">Имейте в виду, что это не влияет на вызовы [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess).</span><span class="sxs-lookup"><span data-stu-id="f3c57-155">Be aware that this does not affect calls to [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess).</span></span>

<span data-ttu-id="f3c57-156">`PassThru` Параметр позволяет пользователю указать, командлет прошло ли объект вывода через конвейер, в этом случае после остановки процесса.</span><span class="sxs-lookup"><span data-stu-id="f3c57-156">The `PassThru` parameter allows the user to indicate whether the cmdlet passes an output object through the pipeline, in this case, after a process is stopped.</span></span> <span data-ttu-id="f3c57-157">Имейте в виду, что этот параметр привязан к командлету сам вместо свойства входного объекта.</span><span class="sxs-lookup"><span data-stu-id="f3c57-157">Be aware that this parameter is tied to the cmdlet itself instead of to a property of the input object.</span></span>

<span data-ttu-id="f3c57-158">Ниже приведено объявление параметра для командлета Stop-Proc.</span><span class="sxs-lookup"><span data-stu-id="f3c57-158">Here is the parameter declaration for the Stop-Proc cmdlet.</span></span>

```csharp
[Parameter(
           Position = 0,
           Mandatory = true,
           ValueFromPipeline = true,
           ValueFromPipelineByPropertyName = true
)]
public string[] Name
{
  get { return processNames; }
  set { processNames = value; }
}
private string[] processNames;

/// <summary>
/// Specify the Force parameter that allows the user to override
/// the ShouldContinue call to force the stop operation. This
/// parameter should always be used with caution.
/// </summary>
[Parameter]
public SwitchParameter Force
{
  get { return force; }
  set { force = value; }
}
private bool force;

/// <summary>
/// Specify the PassThru parameter that allows the user to specify
/// that the cmdlet should pass the process object down the pipeline
/// after the process has been stopped.
/// </summary>
[Parameter]
public SwitchParameter PassThru
{
  get { return passThru; }
  set { passThru = value; }
}
private bool passThru;
```

## <a name="overriding-an-input-processing-method"></a><span data-ttu-id="f3c57-159">Переопределив метод обработки входных данных</span><span class="sxs-lookup"><span data-stu-id="f3c57-159">Overriding an Input Processing Method</span></span>

<span data-ttu-id="f3c57-160">Командлет необходимо переопределить метод обработки входных данных.</span><span class="sxs-lookup"><span data-stu-id="f3c57-160">The cmdlet must override an input processing method.</span></span> <span data-ttu-id="f3c57-161">В следующем коде показано [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) переопределение, используемых в командлет Stop-Proc образец.</span><span class="sxs-lookup"><span data-stu-id="f3c57-161">The following code illustrates the [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) override used in the sample Stop-Proc cmdlet.</span></span> <span data-ttu-id="f3c57-162">Для каждого запроса имя процесса, этот метод гарантирует, что процесс не специального процесса, пытается остановить процесс, а затем отправляет выходного объекта, если `PassThru` указан параметр.</span><span class="sxs-lookup"><span data-stu-id="f3c57-162">For each requested process name, this method ensures that the process is not a special process, tries to stop the process, and then sends an output object if the `PassThru` parameter is specified.</span></span>

```csharp
protected override void ProcessRecord()
{
  foreach (string name in processNames)
  {
    // For every process name passed to the cmdlet, get the associated
    // process(es). For failures, write a non-terminating error
    Process[] processes;

    try
    {
      processes = Process.GetProcessesByName(name);
    }
    catch (InvalidOperationException ioe)
    {
      WriteError(new ErrorRecord(ioe,"Unable to access the target process by name",
                 ErrorCategory.InvalidOperation, name));
      continue;
    }

    // Try to stop the process(es) that have been retrieved for a name
    foreach (Process process in processes)
    {
      string processName;

      try
      {
        processName = process.ProcessName;
      }

      catch (Win32Exception e)
        {
          WriteError(new ErrorRecord(e, "ProcessNameNotFound",
                     ErrorCategory.ReadError, process));
          continue;
        }

        // Call Should Process to confirm the operation first.
        // This is always false if WhatIf is set.
        if (!ShouldProcess(string.Format("{0} ({1})", processName,
                           process.Id)))
        {
          continue;
        }
        // Call ShouldContinue to make sure the user really does want
        // to stop a critical process that could possibly stop the computer.
        bool criticalProcess =
             criticalProcessNames.Contains(processName.ToLower());

        if (criticalProcess &&!force)
        {
          string message = String.Format
                ("The process \"{0}\" is a critical process and should not be stopped. Are you sure you wish to stop the process?",
                processName);

          // It is possible that ProcessRecord is called multiple times
          // when the Name parameter reveives objects as input from the
          // pipeline. So to retain YesToAll and NoToAll input that the
          // user may enter across mutilple calls to ProcessRecord, this
          // information is stored as private members of the cmdlet.
          if (!ShouldContinue(message, "Warning!",
                              ref yesToAll,
                              ref noToAll))
          {
            continue;
          }
        } // if (cricicalProcess...
        // Stop the named process.
        try
        {
          process.Kill();
        }
        catch (Exception e)
        {
          if ((e is Win32Exception) || (e is SystemException) ||
              (e is InvalidOperationException))
          {
            // This process could not be stopped so write
            // a non-terminating error.
            string message = String.Format("{0} {1} {2}",
                             "Could not stop process \"", processName,
                             "\".");
            WriteError(new ErrorRecord(e, message,
                       ErrorCategory.CloseError, process));
                       continue;
          } // if ((e is...
          else throw;
        } // catch

        // If the PassThru parameter argument is
        // True, pass the terminated process on.
        if (passThru)
        {
          WriteObject(process);
        }
    } // foreach (Process...
  } // foreach (string...
} // ProcessRecord
```

## <a name="calling-the-shouldprocess-method"></a><span data-ttu-id="f3c57-163">Вызов метода ShouldProcess</span><span class="sxs-lookup"><span data-stu-id="f3c57-163">Calling the ShouldProcess Method</span></span>

<span data-ttu-id="f3c57-164">Необходимо вызвать метод командлета обработки ввода [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) метод для подтверждения выполнения операции, прежде чем с запуском вносится изменение (например, удаление файлов) состояние системы.</span><span class="sxs-lookup"><span data-stu-id="f3c57-164">The input processing method of your cmdlet should call the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) method to confirm execution of an operation before a change (for example, deleting files) is made to the running state of the system.</span></span> <span data-ttu-id="f3c57-165">Это позволяет среде выполнения Windows PowerShell для предоставления правильного поведения «WhatIf» и «Подтвердить», в оболочке.</span><span class="sxs-lookup"><span data-stu-id="f3c57-165">This allows the Windows PowerShell runtime to supply the correct "WhatIf" and "Confirm" behavior within the shell.</span></span>

> [!NOTE]
> <span data-ttu-id="f3c57-166">Если командлет определяет, что он поддерживает должен обработать и не может обеспечить [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) вызова, пользователь может изменять система неожиданно.</span><span class="sxs-lookup"><span data-stu-id="f3c57-166">If a cmdlet states that it supports should process and fails to make the [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) call, the user might modify the system unexpectedly.</span></span>

<span data-ttu-id="f3c57-167">Вызов [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) отправляет имя ресурса, необходимо изменить на пользователя, в среде выполнения Windows PowerShell, принимая во внимание любые параметры командной строки или привилегированные переменные При определении, что должно быть отображено пользователю.</span><span class="sxs-lookup"><span data-stu-id="f3c57-167">The call to [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) sends the name of the resource to be changed to the user, with the Windows PowerShell runtime taking into account any command-line settings or preference variables in determining what should be displayed to the user.</span></span>

<span data-ttu-id="f3c57-168">В следующем примере показано вызов [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) из переопределение метода [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) метод в командлет Stop-Proc образец.</span><span class="sxs-lookup"><span data-stu-id="f3c57-168">The following example shows the call to [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) from the override of the [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method in the sample Stop-Proc cmdlet.</span></span>

```csharp
if (!ShouldProcess(string.Format("{0} ({1})", processName,
                   process.Id)))
{
  continue;
}
```

## <a name="calling-the-shouldcontinue-method"></a><span data-ttu-id="f3c57-169">Вызов метода ShouldContinue</span><span class="sxs-lookup"><span data-stu-id="f3c57-169">Calling the ShouldContinue Method</span></span>

<span data-ttu-id="f3c57-170">Вызов [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) метод отправляет сообщение-получателя для пользователя.</span><span class="sxs-lookup"><span data-stu-id="f3c57-170">The call to the [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) method sends a secondary message to the user.</span></span> <span data-ttu-id="f3c57-171">Этот вызов выполняется после вызова [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) возвращает `true` и если `Force` параметра не было задано значение `true`.</span><span class="sxs-lookup"><span data-stu-id="f3c57-171">This call is made after the call to [System.Management.Automation.Cmdlet.Shouldprocess\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) returns `true` and if the `Force` parameter was not set to `true`.</span></span> <span data-ttu-id="f3c57-172">Затем пользователь может указать отзыв, чтобы сказать, следует ли продолжить операцию.</span><span class="sxs-lookup"><span data-stu-id="f3c57-172">The user can then provide feedback to say whether the operation should be continued.</span></span> <span data-ttu-id="f3c57-173">В командлет вызывается [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) как дополнительную проверку для изменения потенциально опасных системы или если вы хотите предоставить пользователю Да для все и нет все параметры.</span><span class="sxs-lookup"><span data-stu-id="f3c57-173">Your cmdlet calls [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) as an additional check for potentially dangerous system modifications or when you want to provide yes-to-all and no-to-all options to the user.</span></span>

<span data-ttu-id="f3c57-174">В следующем примере показано вызов [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) из переопределение метода [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) метод в командлет Stop-Proc образец.</span><span class="sxs-lookup"><span data-stu-id="f3c57-174">The following example shows the call to [System.Management.Automation.Cmdlet.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) from the override of the [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method in the sample Stop-Proc cmdlet.</span></span>

```csharp
if (criticalProcess &&!force)
{
  string message = String.Format
        ("The process \"{0}\" is a critical process and should not be stopped. Are you sure you wish to stop the process?",
        processName);

  // It is possible that ProcessRecord is called multiple times
  // when the Name parameter reveives objects as input from the
  // pipeline. So to retain YesToAll and NoToAll input that the
  // user may enter across mutilple calls to ProcessRecord, this
  // information is stored as private members of the cmdlet.
  if (!ShouldContinue(message, "Warning!",
                      ref yesToAll,
                      ref noToAll))
  {
    continue;
  }
} // if (cricicalProcess...
```

## <a name="stopping-input-processing"></a><span data-ttu-id="f3c57-175">Остановка обработки ввода</span><span class="sxs-lookup"><span data-stu-id="f3c57-175">Stopping Input Processing</span></span>

<span data-ttu-id="f3c57-176">Метод командлета, который вносит изменения системы обработки входных данных необходимо указать способ остановки обработки входных данных.</span><span class="sxs-lookup"><span data-stu-id="f3c57-176">The input processing method of a cmdlet that makes system modifications must provide a way of stopping the processing of input.</span></span> <span data-ttu-id="f3c57-177">В случае этот командлет Stop-Proc вызов выполняется из [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) метод [System.Diagnostics.Process.Kill\*](/dotnet/api/System.Diagnostics.Process.Kill) метод.</span><span class="sxs-lookup"><span data-stu-id="f3c57-177">In the case of this Stop-Proc cmdlet, a call is made from the [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method to the [System.Diagnostics.Process.Kill\*](/dotnet/api/System.Diagnostics.Process.Kill) method.</span></span> <span data-ttu-id="f3c57-178">Так как `PassThru` параметр имеет значение `true`, [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) также вызывает [System.Management.Automation.Cmdlet.Writeobject\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) для передает объект процесса в конвейере.</span><span class="sxs-lookup"><span data-stu-id="f3c57-178">Because the `PassThru` parameter is set to `true`, [System.Management.Automation.Cmdlet.Processrecord\*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) also calls [System.Management.Automation.Cmdlet.Writeobject\*](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) to send the process object to the pipeline.</span></span>

## <a name="code-sample"></a><span data-ttu-id="f3c57-179">Пример кода</span><span class="sxs-lookup"><span data-stu-id="f3c57-179">Code Sample</span></span>

<span data-ttu-id="f3c57-180">Для полной C# пример кода, см. в разделе [пример StopProcessSample01](./stopprocesssample01-sample.md).</span><span class="sxs-lookup"><span data-stu-id="f3c57-180">For the complete C# sample code, see [StopProcessSample01 Sample](./stopprocesssample01-sample.md).</span></span>

## <a name="defining-object-types-and-formatting"></a><span data-ttu-id="f3c57-181">Определение типов объектов и форматирование</span><span class="sxs-lookup"><span data-stu-id="f3c57-181">Defining Object Types and Formatting</span></span>

<span data-ttu-id="f3c57-182">Windows PowerShell передает данные между командлетами, используя объекты .net.</span><span class="sxs-lookup"><span data-stu-id="f3c57-182">Windows PowerShell passes information between cmdlets using .Net objects.</span></span> <span data-ttu-id="f3c57-183">Следовательно командлета может потребоваться определить его собственного типа, или командлет может потребоваться расширить существующий тип предоставляемые другому командлету.</span><span class="sxs-lookup"><span data-stu-id="f3c57-183">Consequently, a cmdlet may need to define its own type, or the cmdlet may need to extend an existing type provided by another cmdlet.</span></span> <span data-ttu-id="f3c57-184">Дополнительные сведения о определение новых типов или расширения существующих типов, см. в разделе [расширение типов объектов и форматирование](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span><span class="sxs-lookup"><span data-stu-id="f3c57-184">For more information about defining new types or extending existing types, see [Extending Object Types and Formatting](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span></span>

## <a name="building-the-cmdlet"></a><span data-ttu-id="f3c57-185">Создание командлета</span><span class="sxs-lookup"><span data-stu-id="f3c57-185">Building the Cmdlet</span></span>

<span data-ttu-id="f3c57-186">После реализации командлета, его необходимо зарегистрировать с помощью Windows PowerShell через оснастку Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3c57-186">After implementing a cmdlet, it must be registered with Windows PowerShell through a Windows PowerShell snap-in.</span></span> <span data-ttu-id="f3c57-187">Дополнительные сведения о регистрации командлетов см. в разделе [как регистрация командлетов, поставщиков и ведущих приложений](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span><span class="sxs-lookup"><span data-stu-id="f3c57-187">For more information about registering cmdlets, see [How to Register Cmdlets, Providers, and Host Applications](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span></span>

## <a name="testing-the-cmdlet"></a><span data-ttu-id="f3c57-188">Тестирование командлет</span><span class="sxs-lookup"><span data-stu-id="f3c57-188">Testing the Cmdlet</span></span>

<span data-ttu-id="f3c57-189">При командлета был зарегистрирован с помощью Windows PowerShell, его можно проверить, запустив его в командной строке.</span><span class="sxs-lookup"><span data-stu-id="f3c57-189">When your cmdlet has been registered with Windows PowerShell, you can test it by running it on the command line.</span></span> <span data-ttu-id="f3c57-190">Ниже приведены несколько тестов, которые проверяют командлет Stop-Proc.</span><span class="sxs-lookup"><span data-stu-id="f3c57-190">Here are several tests that test the Stop-Proc cmdlet.</span></span> <span data-ttu-id="f3c57-191">Дополнительные сведения об использовании командлетов из командной строки см. в разделе [Приступая к работе с Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span><span class="sxs-lookup"><span data-stu-id="f3c57-191">For more information about using cmdlets from the command line, see the [Getting Started with Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span></span>

- <span data-ttu-id="f3c57-192">Запустите Windows PowerShell и используйте командлет Stop-Proc для остановки обработки, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="f3c57-192">Start Windows PowerShell and use the Stop-Proc cmdlet to stop processing as shown below.</span></span> <span data-ttu-id="f3c57-193">Так как командлет задает `Name` параметр как обязательные, командлет запросы для параметра.</span><span class="sxs-lookup"><span data-stu-id="f3c57-193">Because the cmdlet specifies the `Name` parameter as mandatory, the cmdlet queries for the parameter.</span></span>

    ```powershell
    PS> stop-proc
    ```

<span data-ttu-id="f3c57-194">Появляется следующий результат.</span><span class="sxs-lookup"><span data-stu-id="f3c57-194">The following output appears.</span></span>

    ```
    Cmdlet stop-proc at command pipeline position 1
    Supply values for the following parameters:
    Name[0]:
    ```

- <span data-ttu-id="f3c57-195">Теперь давайте используем командлет для остановки процесса с именем «Блокнот».</span><span class="sxs-lookup"><span data-stu-id="f3c57-195">Now let's use the cmdlet to stop the process named "NOTEPAD".</span></span> <span data-ttu-id="f3c57-196">Командлет запрашивает подтверждение действия.</span><span class="sxs-lookup"><span data-stu-id="f3c57-196">The cmdlet asks you to confirm the action.</span></span>

    ```powershell
    PS> stop-proc -Name notepad
    ```

<span data-ttu-id="f3c57-197">Появляется следующий результат.</span><span class="sxs-lookup"><span data-stu-id="f3c57-197">The following output appears.</span></span>

    ```
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "notepad (4996)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    ```

- <span data-ttu-id="f3c57-198">Используйте Stop-Proc, как показано для остановки критических процесса с именем «WINLOGON».</span><span class="sxs-lookup"><span data-stu-id="f3c57-198">Use Stop-Proc as shown to stop the critical process named "WINLOGON".</span></span> <span data-ttu-id="f3c57-199">Вы являетесь запрос и получает предупреждение о выполнении этого действия, так как он вызовет перезагрузку операционной системы.</span><span class="sxs-lookup"><span data-stu-id="f3c57-199">You are prompted and warned about performing this action because it will cause the operating system to reboot.</span></span>

    ```powershell
    PS> stop-proc -Name Winlogon
    ```

<span data-ttu-id="f3c57-200">Появляется следующий результат.</span><span class="sxs-lookup"><span data-stu-id="f3c57-200">The following output appears.</span></span>

    ```output
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "winlogon (656)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
    Warning!
    The process " winlogon " is a critical process and should not be stopped. Are you sure you wish to stop the process?
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): N
    ```

- <span data-ttu-id="f3c57-201">Давайте теперь попробуйте остановить процесс WINLOGON без получения предупреждения.</span><span class="sxs-lookup"><span data-stu-id="f3c57-201">Let's now try to stop the WINLOGON process without receiving a warning.</span></span> <span data-ttu-id="f3c57-202">Имейте в виду, что эта запись команды использует `Force` параметр можно переопределить предупреждение.</span><span class="sxs-lookup"><span data-stu-id="f3c57-202">Be aware that this command entry uses the `Force` parameter to override the warning.</span></span>

    ```powershell
    PS> stop-proc -Name winlogon -Force
    ```

<span data-ttu-id="f3c57-203">Появляется следующий результат.</span><span class="sxs-lookup"><span data-stu-id="f3c57-203">The following output appears.</span></span>

    ```output
    Confirm
    Are you sure you want to perform this action?
    Performing operation "stop-proc" on Target "winlogon (656)".
    [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): N
    ```

## <a name="see-also"></a><span data-ttu-id="f3c57-204">См. также</span><span class="sxs-lookup"><span data-stu-id="f3c57-204">See Also</span></span>

[<span data-ttu-id="f3c57-205">Добавление параметров, которые обрабатывают данные в командной строке</span><span class="sxs-lookup"><span data-stu-id="f3c57-205">Adding Parameters that Process Command-Line Input</span></span>](./adding-parameters-that-process-command-line-input.md)

[<span data-ttu-id="f3c57-206">Расширение типов объектов и форматирование</span><span class="sxs-lookup"><span data-stu-id="f3c57-206">Extending Object Types and Formatting</span></span>](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[<span data-ttu-id="f3c57-207">Регистрация командлетов, поставщиков и ведущих приложений</span><span class="sxs-lookup"><span data-stu-id="f3c57-207">How to Register Cmdlets, Providers, and Host Applications</span></span>](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="f3c57-208">Пакет SDK для Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3c57-208">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)

[<span data-ttu-id="f3c57-209">Примеры командлетов</span><span class="sxs-lookup"><span data-stu-id="f3c57-209">Cmdlet Samples</span></span>](./cmdlet-samples.md)