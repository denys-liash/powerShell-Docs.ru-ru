---
title: Создание поставщика Windows PowerShell навигации | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- navigation providers [PowerShell Programmer's Guide]
- providers [PowerShell Programmer's Guide], navigation provider
ms.assetid: 8bd3224d-ca6f-4640-9464-cb4d9f4e13b1
caps.latest.revision: 5
ms.openlocfilehash: cbc8ce0600553f9e9ab973d6f92ea5eafde310e2
ms.sourcegitcommit: 69abc5ad16e5dd29ddfb1853e266a4bfd1d59d59
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2019
ms.locfileid: "57430043"
---
# <a name="creating-a-windows-powershell-navigation-provider"></a><span data-ttu-id="f6450-102">Создание поставщика навигации Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6450-102">Creating a Windows PowerShell Navigation Provider</span></span>

<span data-ttu-id="f6450-103">В этом разделе описывается, как создать поставщик навигации Windows PowerShell, можно перейти в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="f6450-103">This topic describes how to create a Windows PowerShell navigation provider that can navigate the data store.</span></span> <span data-ttu-id="f6450-104">Этот тип поставщика поддерживает рекурсивной команды, вложенные контейнеры и относительные пути.</span><span class="sxs-lookup"><span data-stu-id="f6450-104">This type of provider supports recursive commands, nested containers, and relative paths.</span></span>

> [!NOTE]
> <span data-ttu-id="f6450-105">Вы можете скачать C# исходный файл (AccessDBSampleProvider05.cs) для данного поставщика, с помощью Microsoft Windows программное обеспечение Development Kit для Windows Vista и компоненты среды выполнения .NET Framework 3.0.</span><span class="sxs-lookup"><span data-stu-id="f6450-105">You can download the C# source file (AccessDBSampleProvider05.cs) for this provider using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="f6450-106">Инструкции по загрузке см. в разделе [как установка Windows PowerShell и загрузки пакета SDK для Windows PowerShell](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="f6450-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="f6450-107">Скачанный исходные файлы доступны в  **\<примеры PowerShell >** каталога.</span><span class="sxs-lookup"><span data-stu-id="f6450-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>
>
> <span data-ttu-id="f6450-108">Дополнительные сведения о других реализаций поставщика Windows PowerShell, см. в разделе [проектирование ваш поставщик PowerShell Windows](./designing-your-windows-powershell-provider.md).</span><span class="sxs-lookup"><span data-stu-id="f6450-108">For more information about other Windows PowerShell provider implementations, see [Designing Your Windows PowerShell Provider](./designing-your-windows-powershell-provider.md).</span></span>

<span data-ttu-id="f6450-109">Описанные здесь поставщик обеспечивает дескриптор пользователя базы данных Access как диск, таким образом, чтобы пользователь мог перейти к таблицам данных в базе данных.</span><span class="sxs-lookup"><span data-stu-id="f6450-109">The provider described here enables the user handle an Access database as a drive so that the user can navigate to the data tables in the database.</span></span> <span data-ttu-id="f6450-110">При создании собственного поставщика навигации, можно реализовать методы, которые можно сделать диск с указанием пути, необходимые для навигации, нормализовать относительные пути, перемещать элементы в хранилище данных, а также методы, которые получают имена дочерних, получить путь родительского элемента и тестирования Чтобы определить, если элемент является контейнером.</span><span class="sxs-lookup"><span data-stu-id="f6450-110">When creating your own navigation provider, you can implement methods that can make drive-qualified paths required for navigation, normalize relative paths, move items of the data store, as well as methods that get child names, get the parent path of an item, and test to identify if an item is a container.</span></span>

> [!CAUTION]
> <span data-ttu-id="f6450-111">Имейте в виду, что такой подход предполагает базу, которая содержит поле с именем Идентификатором и типом поля является LongInteger.</span><span class="sxs-lookup"><span data-stu-id="f6450-111">Be aware that this design assumes a database that has a field with the name ID, and that the type of the field is LongInteger.</span></span>

<span data-ttu-id="f6450-112">В следующем списке приведены разделы этой статьи.</span><span class="sxs-lookup"><span data-stu-id="f6450-112">The following list includes sections in this topic.</span></span> <span data-ttu-id="f6450-113">Если вы не знакомы с записью поставщик навигации Windows PowerShell, прочтите эти сведения, в том порядке, в котором она появляется.</span><span class="sxs-lookup"><span data-stu-id="f6450-113">If you are unfamiliar with writing a Windows PowerShell navigation provider, read this information in the order that it appears.</span></span> <span data-ttu-id="f6450-114">Тем не менее если вы знакомы с записью поставщик навигации Windows PowerShell, перейдите непосредственно к сведениям, вам потребуется.</span><span class="sxs-lookup"><span data-stu-id="f6450-114">However, if you are familiar with writing a Windows PowerShell navigation provider, please go directly to the information that you need.</span></span>

- [<span data-ttu-id="f6450-115">Определение класса поставщика навигации PS</span><span class="sxs-lookup"><span data-stu-id="f6450-115">Defining a PS Navigation Provider Class</span></span>](#Define-the-Windows-PowerShell-provider)

- [<span data-ttu-id="f6450-116">Определение базовой функциональности</span><span class="sxs-lookup"><span data-stu-id="f6450-116">Defining Base Functionality</span></span>](#Defining-Base-Functionality)

- [<span data-ttu-id="f6450-117">Создание контура PS</span><span class="sxs-lookup"><span data-stu-id="f6450-117">Creating a PS Path</span></span>](#Creating-a-Windows-PowerShell-Path)

- [<span data-ttu-id="f6450-118">Получение родительского пути</span><span class="sxs-lookup"><span data-stu-id="f6450-118">Retrieving the Parent Path</span></span>](#Retrieving-the-Parent-Path)

- [<span data-ttu-id="f6450-119">Получение имени дочерний путь</span><span class="sxs-lookup"><span data-stu-id="f6450-119">Retrieving the Child Path Name</span></span>](#Retrieve-the-Child-Path-Name)

- [<span data-ttu-id="f6450-120">Определение, является ли элемент контейнера</span><span class="sxs-lookup"><span data-stu-id="f6450-120">Determining if an Item is a Container</span></span>](#Determining-if-an-Item-is-a-Container)

- [<span data-ttu-id="f6450-121">Перемещение элемента</span><span class="sxs-lookup"><span data-stu-id="f6450-121">Moving an Item</span></span>](#Moving-an-Item)

- [<span data-ttu-id="f6450-122">Присоединение динамических параметров в `Move-Item` командлета</span><span class="sxs-lookup"><span data-stu-id="f6450-122">Attaching Dynamic Parameters to the `Move-Item` Cmdlet</span></span>](#Attaching-Dynamic-Parameters-to-the-Move-Item-Cmdlet)

- [<span data-ttu-id="f6450-123">Нормализация относительный путь</span><span class="sxs-lookup"><span data-stu-id="f6450-123">Normalizing a Relative Path</span></span>](#Normalizing-a-Relative-Path)

- [<span data-ttu-id="f6450-124">Пример кода</span><span class="sxs-lookup"><span data-stu-id="f6450-124">Code Sample</span></span>](#Code-Sample)

- [<span data-ttu-id="f6450-125">Определение типов объектов и форматирование</span><span class="sxs-lookup"><span data-stu-id="f6450-125">Defining Object Types and Formatting</span></span>](#Defining-Object-Types-and-Formatting)

- [<span data-ttu-id="f6450-126">Создание поставщика Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6450-126">Building the Windows PowerShell Provider</span></span>](#Building-the-Windows-PowerShell-provider)

- [<span data-ttu-id="f6450-127">Проверка поставщика в Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6450-127">Testing the Windows PowerShell Provider</span></span>](#Testing-the-Windows-PowerShell-provider)

## <a name="define-the-windows-powershell-provider"></a><span data-ttu-id="f6450-128">Определение поставщика Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6450-128">Define the Windows PowerShell provider</span></span>

<span data-ttu-id="f6450-129">Поставщик навигации Windows PowerShell необходимо создать класс .NET, который является производным от [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) базового класса.</span><span class="sxs-lookup"><span data-stu-id="f6450-129">A Windows PowerShell navigation provider must create a .NET class that derives from the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) base class.</span></span> <span data-ttu-id="f6450-130">Вот определение класса для поставщика навигации, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="f6450-130">Here is the class definition for the navigation provider described in this section.</span></span>

[!code-csharp[AccessDBProviderSample05.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample05/AccessDBProviderSample05.cs#L31-L32 "AccessDBProviderSample05.cs")]

<span data-ttu-id="f6450-131">Обратите внимание, что в этом поставщике [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) атрибут содержит два параметра.</span><span class="sxs-lookup"><span data-stu-id="f6450-131">Note that in this provider, the [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribute includes two parameters.</span></span> <span data-ttu-id="f6450-132">Первый параметр указывает понятное имя для поставщика, который используется Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6450-132">The first parameter specifies a user-friendly name for the provider that is used by Windows PowerShell.</span></span> <span data-ttu-id="f6450-133">Второй параметр указывает специальной совместимости с Windows PowerShell, которые предоставляет поставщик среды выполнения Windows PowerShell во время обработки команды.</span><span class="sxs-lookup"><span data-stu-id="f6450-133">The second parameter specifies the Windows PowerShell specific capabilities that the provider exposes to the Windows PowerShell runtime during command processing.</span></span> <span data-ttu-id="f6450-134">Для этого поставщика нет конкретных возможности Windows PowerShell, которые добавляются.</span><span class="sxs-lookup"><span data-stu-id="f6450-134">For this provider, there are no Windows PowerShell specific capabilities that are added.</span></span>

## <a name="defining-base-functionality"></a><span data-ttu-id="f6450-135">Определение базовой функциональности</span><span class="sxs-lookup"><span data-stu-id="f6450-135">Defining Base Functionality</span></span>

<span data-ttu-id="f6450-136">Как описано в разделе [разработки ваш поставщик PS](./designing-your-windows-powershell-provider.md), [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) базовый класс является производным от нескольких других классов для другого поставщика функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="f6450-136">As described in [Design Your PS Provider](./designing-your-windows-powershell-provider.md), the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) base class derives from several other classes that provided different provider functionality.</span></span> <span data-ttu-id="f6450-137">Поставщик навигации Windows PowerShell, поэтому необходимо определить все функциональные возможности, предоставляемые этими классами.</span><span class="sxs-lookup"><span data-stu-id="f6450-137">A Windows PowerShell navigation provider, therefore, must define all of the functionality provided by those classes.</span></span>

<span data-ttu-id="f6450-138">Чтобы реализовать функциональные возможности для добавления сведений инициализации сеанса, а также для освобождения ресурсов, которые используются поставщиком, см. в разделе [Создание базовый поставщик PS](./creating-a-basic-windows-powershell-provider.md).</span><span class="sxs-lookup"><span data-stu-id="f6450-138">To implement functionality for adding session-specific initialization information and for releasing resources that are used by the provider, see [Creating a Basic PS Provider](./creating-a-basic-windows-powershell-provider.md).</span></span> <span data-ttu-id="f6450-139">Тем не менее большинство поставщиков (включая поставщика, описанные здесь) можно использовать реализацию по умолчанию этой функции, предоставляемые Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6450-139">However, most providers (including the provider described here) can use the default implementation of this functionality provided by Windows PowerShell.</span></span>

<span data-ttu-id="f6450-140">Чтобы получить доступ к хранилищу данных через диск Windows PowerShell, необходимо реализовать методы [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) базового класса.</span><span class="sxs-lookup"><span data-stu-id="f6450-140">To get access to the data store through a Windows PowerShell drive, you must implement the methods of the [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) base class.</span></span> <span data-ttu-id="f6450-141">Дополнительные сведения о реализации этих методов см. в разделе [Создание поставщика диска Windows PowerShell](./creating-a-windows-powershell-drive-provider.md).</span><span class="sxs-lookup"><span data-stu-id="f6450-141">For more information about implementing these methods, see [Creating a Windows PowerShell Drive Provider](./creating-a-windows-powershell-drive-provider.md).</span></span>

<span data-ttu-id="f6450-142">Для работы с элементами в хранилище данных, например начало, параметр и очистка элементов, поставщик должен реализовывать методы, предоставленные [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) базового класса.</span><span class="sxs-lookup"><span data-stu-id="f6450-142">To manipulate the items of a data store, such as getting, setting, and clearing items, the provider must implement the methods provided by the [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) base class.</span></span> <span data-ttu-id="f6450-143">Дополнительные сведения о реализации этих методов см. в разделе [Создание поставщика Windows PowerShell элемента](./creating-a-windows-powershell-item-provider.md).</span><span class="sxs-lookup"><span data-stu-id="f6450-143">For more information about implementing these methods, see [Creating an Windows PowerShell Item Provider](./creating-a-windows-powershell-item-provider.md).</span></span>

<span data-ttu-id="f6450-144">Чтобы получить дочерние элементы, или их имена, хранилище данных, а также способы создания, копирования, переименования и удаления элементов, необходимо реализовать методы, предоставленные [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)базового класса.</span><span class="sxs-lookup"><span data-stu-id="f6450-144">To get to the child items, or their names, of the data store, as well as methods that create, copy, rename, and remove items, you must implement the methods provided by the [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) base class.</span></span> <span data-ttu-id="f6450-145">Дополнительные сведения о реализации этих методов см. в разделе [Создание поставщика Windows PowerShell контейнера](./creating-a-windows-powershell-container-provider.md).</span><span class="sxs-lookup"><span data-stu-id="f6450-145">For more information about implementing these methods, see [Creating a Windows PowerShell Container Provider](./creating-a-windows-powershell-container-provider.md).</span></span>

## <a name="creating-a-windows-powershell-path"></a><span data-ttu-id="f6450-146">Создание пути Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6450-146">Creating a Windows PowerShell Path</span></span>

<span data-ttu-id="f6450-147">Поставщик навигации Windows PowerShell используйте внутренний поставщик путь Windows PowerShell для перемещения элементов в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="f6450-147">Windows PowerShell navigation provider use a provider-internal Windows PowerShell path to navigate the items of the data store.</span></span> <span data-ttu-id="f6450-148">Для создания поставщика внутреннего пути поставщик должен реализовывать [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) вызывает метод для поддержки из командлета объединение-Path.</span><span class="sxs-lookup"><span data-stu-id="f6450-148">To create a provider-internal path the provider must implement the [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) method to supports calls from the Combine-Path cmdlet.</span></span> <span data-ttu-id="f6450-149">Этот метод объединяет родительский и дочерний путь в поставщик внутреннего пути, используя разделитель пути поставщика между родительским и дочерним путями.</span><span class="sxs-lookup"><span data-stu-id="f6450-149">This method combines a parent and child path into a provider-internal path, using a provider-specific path separator between the parent and child paths.</span></span>

<span data-ttu-id="f6450-150">Реализация по умолчанию получает пути с «/» или "\\«как разделитель пути, нормализует разделитель пути для»\\«, объединяет части пути к родительским и дочерним с разделителем между ними, а затем возвращает строку, содержащую объединенные пути.</span><span class="sxs-lookup"><span data-stu-id="f6450-150">The default implementation takes paths with "/" or "\\" as the path separator, normalizes the path separator to "\\", combines the parent and child path parts with the separator between them, and then returns a string that contains the combined paths.</span></span>

<span data-ttu-id="f6450-151">Этот поставщик навигации не реализует этот метод.</span><span class="sxs-lookup"><span data-stu-id="f6450-151">This navigation provider does not implement this method.</span></span> <span data-ttu-id="f6450-152">Тем не менее, следующий код является реализация по умолчанию [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) метод.</span><span class="sxs-lookup"><span data-stu-id="f6450-152">However, the following code is the default implementation of the [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) method.</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidermakepath](Msh_samplestestcmdlets#testprovidermakepath)]  -->

#### <a name="things-to-remember-about-implementing-makepath"></a><span data-ttu-id="f6450-153">О чем следует помнить о реализации MakePath</span><span class="sxs-lookup"><span data-stu-id="f6450-153">Things to Remember About Implementing MakePath</span></span>

<span data-ttu-id="f6450-154">Следующие условия могут относиться к реализации [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath):</span><span class="sxs-lookup"><span data-stu-id="f6450-154">The following conditions may apply to your implementation of [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath):</span></span>

- <span data-ttu-id="f6450-155">Реализация [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) метод не следует проверить путь как юридические полный путь в пространстве имен поставщика.</span><span class="sxs-lookup"><span data-stu-id="f6450-155">Your implementation of the [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) method should not validate the path as a legal fully-qualified path in the provider namespace.</span></span> <span data-ttu-id="f6450-156">Имейте в виду, каждый параметр может представлять только часть пути, что объединенный частей может не создаваться, полный путь.</span><span class="sxs-lookup"><span data-stu-id="f6450-156">Be aware that each parameter can only represent a part of a path, and the combined parts might not generate a fully-qualified path.</span></span> <span data-ttu-id="f6450-157">Например [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) метод для поставщика filesystem может появиться «windows\system32» в `parent` параметр и «abc.dll» в `child` параметра.</span><span class="sxs-lookup"><span data-stu-id="f6450-157">For example, the [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) method for the filesystem provider might receive "windows\system32" in the `parent` parameter and "abc.dll" in the `child` parameter.</span></span> <span data-ttu-id="f6450-158">Метод объединяет эти значения с "\\" Разделитель "и" возвращает «windows\system32\abc.dll», не являющийся указания полного пути.</span><span class="sxs-lookup"><span data-stu-id="f6450-158">The method joins these values with the "\\" separator and returns "windows\system32\abc.dll", which is not a fully-qualified file system path.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f6450-159">Части пути, предоставленные в вызове [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) может содержать символы не допускаются в пространство имен поставщика.</span><span class="sxs-lookup"><span data-stu-id="f6450-159">The path parts provided in the call to [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) might contain characters not allowed in the provider namespace.</span></span> <span data-ttu-id="f6450-160">Эти символы чаще всего используются для подстановочных знаков и реализация этого метода не следует удалять их.</span><span class="sxs-lookup"><span data-stu-id="f6450-160">These characters are most likely used for wildcard expansion and the implementation of this method should not remove them.</span></span>

## <a name="retrieving-the-parent-path"></a><span data-ttu-id="f6450-161">Получение родительского пути</span><span class="sxs-lookup"><span data-stu-id="f6450-161">Retrieving the Parent Path</span></span>

<span data-ttu-id="f6450-162">Поставщики Windows PowerShell переходов реализуют [System.Management.Automation.Provider.Navigationcmdletprovider.Getparentpath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetParentPath) метод для извлечения родительского часть указанный полный или частичный путь от поставщика.</span><span class="sxs-lookup"><span data-stu-id="f6450-162">Windows PowerShell navigation providers implement the [System.Management.Automation.Provider.Navigationcmdletprovider.Getparentpath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetParentPath) method to retrieve the parent part of the indicated full or partial provider-specific path.</span></span> <span data-ttu-id="f6450-163">Метод удаляет дочерний часть пути и возвращает путь в родительский объект.</span><span class="sxs-lookup"><span data-stu-id="f6450-163">The method removes the child part of the path and returns the parent path part.</span></span> <span data-ttu-id="f6450-164">`root` Параметр указывает полный путь к корневому каталогу диска.</span><span class="sxs-lookup"><span data-stu-id="f6450-164">The `root` parameter specifies the fully-qualified path to the root of a drive.</span></span> <span data-ttu-id="f6450-165">Этот параметр может быть null или пусто, если не используется для операции по извлечению подключенного диска.</span><span class="sxs-lookup"><span data-stu-id="f6450-165">This parameter can be null or empty if a mounted drive is not in use for the retrieval operation.</span></span> <span data-ttu-id="f6450-166">Если корень указан, метод должен возвращать путь к контейнеру в качестве корневого элемента дерева.</span><span class="sxs-lookup"><span data-stu-id="f6450-166">If a root is specified, the method must return a path to a container in the same tree as the root.</span></span>

<span data-ttu-id="f6450-167">Поставщик навигации пример переопределения этого метода, но использует реализацию по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f6450-167">The sample navigation provider does not override this method, but uses the default implementation.</span></span> <span data-ttu-id="f6450-168">Он принимает пути, которые используются оба «/» и "\\" в качестве разделителей пути.</span><span class="sxs-lookup"><span data-stu-id="f6450-168">It accepts paths that use both "/" and "\\" as path separators.</span></span> <span data-ttu-id="f6450-169">Сначала он нормализует путь к только "\\" разделителей, затем разделяет родительский путь из системы последнего "\\" и возвращает путь к родительскому.</span><span class="sxs-lookup"><span data-stu-id="f6450-169">It first normalizes the path to have only "\\" separators, then splits the parent path off at the last "\\" and returns the parent path.</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidergetparentpath](Msh_samplestestcmdlets#testprovidergetparentpath)]  -->

#### <a name="to-remember-about-implementing-getparentpath"></a><span data-ttu-id="f6450-170">Следует помнить о реализации GetParentPath</span><span class="sxs-lookup"><span data-stu-id="f6450-170">To Remember About Implementing GetParentPath</span></span>

<span data-ttu-id="f6450-171">Реализация [System.Management.Automation.Provider.Navigationcmdletprovider.Getparentpath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetParentPath) метод следует разбить путь лексически на разделитель пути для пространства имен поставщика.</span><span class="sxs-lookup"><span data-stu-id="f6450-171">Your implementation of the [System.Management.Automation.Provider.Navigationcmdletprovider.Getparentpath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetParentPath) method should split the path lexically on the path separator for the provider namespace.</span></span> <span data-ttu-id="f6450-172">Например, поставщик filesystem использует этот метод для поиска последнего "\\" и возвращает все, что слева от разделителя.</span><span class="sxs-lookup"><span data-stu-id="f6450-172">For example, the filesystem provider uses this method to look for the last "\\" and returns everything to the left of the separator.</span></span>

## <a name="retrieve-the-child-path-name"></a><span data-ttu-id="f6450-173">Получить имя пути дочерних</span><span class="sxs-lookup"><span data-stu-id="f6450-173">Retrieve the Child Path Name</span></span>

<span data-ttu-id="f6450-174">Пользовательский поставщик реализует навигации [System.Management.Automation.Provider.Navigationcmdletprovider.Getchildname\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetChildName) метод для извлечения имени дочернего элемента (конечный элемент), расположенный в указанной полной или частичный путь от поставщика.</span><span class="sxs-lookup"><span data-stu-id="f6450-174">Your navigation provider implements the [System.Management.Automation.Provider.Navigationcmdletprovider.Getchildname\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetChildName) method to retrieve the name (leaf element) of the child of the item located at the indicated full or partial provider-specific path.</span></span>

<span data-ttu-id="f6450-175">Пример поставщика навигации не Переопределите этот метод.</span><span class="sxs-lookup"><span data-stu-id="f6450-175">The sample navigation provider does not override this method.</span></span> <span data-ttu-id="f6450-176">Реализация по умолчанию. ниже.</span><span class="sxs-lookup"><span data-stu-id="f6450-176">The default implementation is shown below.</span></span> <span data-ttu-id="f6450-177">Он принимает пути, которые используются оба «/» и "\\" в качестве разделителей пути.</span><span class="sxs-lookup"><span data-stu-id="f6450-177">It accepts paths that use both "/" and "\\" as path separators.</span></span> <span data-ttu-id="f6450-178">Сначала он нормализует путь к только "\\" разделителей, затем разделяет родительский путь из системы последнего "\\" и возвращает имя дочернего элемента, часть пути.</span><span class="sxs-lookup"><span data-stu-id="f6450-178">It first normalizes the path to have only "\\" separators, then splits the parent path off at the last "\\" and returns the name of the child path part.</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidergetchildname](Msh_samplestestcmdlets#testprovidergetchildname)]  -->

#### <a name="things-to-remember-about-implementing-getchildname"></a><span data-ttu-id="f6450-179">О чем следует помнить о реализации GetChildName</span><span class="sxs-lookup"><span data-stu-id="f6450-179">Things to Remember About Implementing GetChildName</span></span>

<span data-ttu-id="f6450-180">Реализация [System.Management.Automation.Provider.Navigationcmdletprovider.Getchildname\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetChildName) метод следует разбить путь лексически на разделитель пути.</span><span class="sxs-lookup"><span data-stu-id="f6450-180">Your implementation of the [System.Management.Automation.Provider.Navigationcmdletprovider.Getchildname\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetChildName) method should split the path lexically on the path separator.</span></span> <span data-ttu-id="f6450-181">Если указанный путь содержит без разделителей пути, метод должен вернуть путь без изменений.</span><span class="sxs-lookup"><span data-stu-id="f6450-181">If the supplied path contains no path separators, the method should return the path unmodified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6450-182">Путь, указанный в вызове этого метода может содержать символы, недопустимые в пространство имен поставщика.</span><span class="sxs-lookup"><span data-stu-id="f6450-182">The path provided in the call to this method might contain characters that are illegal in the provider namespace.</span></span> <span data-ttu-id="f6450-183">Эти символы, скорее всего, используемых для подстановочных знаков или сопоставление регулярных выражений и реализация этого метода не следует удалять их.</span><span class="sxs-lookup"><span data-stu-id="f6450-183">These characters are most likely used for wildcard expansion or regular expression matching, and the implementation of this method should not remove them.</span></span>

## <a name="determining-if-an-item-is-a-container"></a><span data-ttu-id="f6450-184">Определение, является ли элемент контейнера</span><span class="sxs-lookup"><span data-stu-id="f6450-184">Determining if an Item is a Container</span></span>

<span data-ttu-id="f6450-185">Поставщик навигации может реализовать [System.Management.Automation.Provider.Navigationcmdletprovider.Isitemcontainer\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) метод, чтобы определить, если указанный путь контейнера.</span><span class="sxs-lookup"><span data-stu-id="f6450-185">The navigation provider can implement the [System.Management.Automation.Provider.Navigationcmdletprovider.Isitemcontainer\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) method to determine if the specified path indicates a container.</span></span> <span data-ttu-id="f6450-186">Она возвращает значение true, если путь представляет контейнер и false в противном случае.</span><span class="sxs-lookup"><span data-stu-id="f6450-186">It returns true if the path represents a container, and false otherwise.</span></span> <span data-ttu-id="f6450-187">Пользователь должен иметь возможность использовать этот метод `Test-Path` командлет для предоставленного пути.</span><span class="sxs-lookup"><span data-stu-id="f6450-187">The user needs this method to be able to use the `Test-Path` cmdlet for the supplied path.</span></span>

<span data-ttu-id="f6450-188">В следующем коде показан [System.Management.Automation.Provider.Navigationcmdletprovider.Isitemcontainer\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) реализацию в наш образец поставщика навигации.</span><span class="sxs-lookup"><span data-stu-id="f6450-188">The following code shows the [System.Management.Automation.Provider.Navigationcmdletprovider.Isitemcontainer\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) implementation in our sample navigation provider.</span></span> <span data-ttu-id="f6450-189">Метод проверяет правильность указанного пути, и если таблица существует и возвращает значение true, если путь указывает на контейнер.</span><span class="sxs-lookup"><span data-stu-id="f6450-189">The method verifies that  the specified path is correct and if the table exists, and returns true if the path indicates a container.</span></span>

[!code-csharp[AccessDBProviderSample05.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample05/AccessDBProviderSample05.cs#L847-L872 "AccessDBProviderSample05.cs")]

#### <a name="things-to-remember-about-implementing-isitemcontainer"></a><span data-ttu-id="f6450-190">О чем следует помнить о реализации IsItemContainer</span><span class="sxs-lookup"><span data-stu-id="f6450-190">Things to Remember About Implementing IsItemContainer</span></span>

<span data-ttu-id="f6450-191">Поставщик навигации класс .NET может объявлять возможностей поставщика ExpandWildcards фильтра, Include и Exclude, из [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) перечисления.</span><span class="sxs-lookup"><span data-stu-id="f6450-191">Your navigation provider .NET class might declare provider capabilities of ExpandWildcards, Filter, Include, or Exclude, from the [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration.</span></span> <span data-ttu-id="f6450-192">В этом случае реализация [System.Management.Automation.Provider.Navigationcmdletprovider.Isitemcontainer\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) необходимо убедиться, что путь, переданный соответствует требованиям.</span><span class="sxs-lookup"><span data-stu-id="f6450-192">In this case, the implementation of [System.Management.Automation.Provider.Navigationcmdletprovider.Isitemcontainer\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) needs to ensure that the path passed meets requirements.</span></span> <span data-ttu-id="f6450-193">Чтобы сделать это, метод должен получить доступ к соответствующее свойство, например, [System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) свойство.</span><span class="sxs-lookup"><span data-stu-id="f6450-193">To do this, the method should access the appropriate property, for example, the [System.Management.Automation.Provider.Cmdletprovider.Exclude\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) property.</span></span>

## <a name="moving-an-item"></a><span data-ttu-id="f6450-194">Перемещение элемента</span><span class="sxs-lookup"><span data-stu-id="f6450-194">Moving an Item</span></span>

<span data-ttu-id="f6450-195">Поддержки `Move-Item` реализует поставщик навигации командлета, [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) метод.</span><span class="sxs-lookup"><span data-stu-id="f6450-195">In support of the `Move-Item` cmdlet, your navigation provider implements the [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) method.</span></span> <span data-ttu-id="f6450-196">Этот метод перемещает элемент, заданный параметром `path` параметр контейнера по пути, предоставленного в `destination` параметра.</span><span class="sxs-lookup"><span data-stu-id="f6450-196">This method moves the item specified by the `path` parameter to the container at the path supplied in the `destination` parameter.</span></span>

<span data-ttu-id="f6450-197">Пример поставщика навигации не переопределяет [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) метод.</span><span class="sxs-lookup"><span data-stu-id="f6450-197">The sample navigation provider does not override the [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) method.</span></span> <span data-ttu-id="f6450-198">Ниже приводится реализация по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f6450-198">The following is the default implementation.</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidermoveitem](Msh_samplestestcmdlets#testprovidermoveitem)]  -->

#### <a name="things-to-remember-about-implementing-moveitem"></a><span data-ttu-id="f6450-199">О чем следует помнить о реализации MoveItem</span><span class="sxs-lookup"><span data-stu-id="f6450-199">Things to Remember About Implementing MoveItem</span></span>

<span data-ttu-id="f6450-200">Поставщик навигации класс .NET может объявлять возможностей поставщика ExpandWildcards фильтра, Include и Exclude, из [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) перечисления.</span><span class="sxs-lookup"><span data-stu-id="f6450-200">Your navigation provider .NET class might declare provider capabilities of ExpandWildcards, Filter, Include, or Exclude, from the [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumeration.</span></span> <span data-ttu-id="f6450-201">В этом случае реализация [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) необходимо убедиться, что путь, переданный соответствует требованиям.</span><span class="sxs-lookup"><span data-stu-id="f6450-201">In this case, the implementation of [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) must ensure that the path passed meets requirements.</span></span> <span data-ttu-id="f6450-202">Чтобы сделать это, метод должен получить доступ к соответствующее свойство, например, **CmdletProvider.Exclude** свойство.</span><span class="sxs-lookup"><span data-stu-id="f6450-202">To do this, the method should access the appropriate property, for example, the **CmdletProvider.Exclude** property.</span></span>

<span data-ttu-id="f6450-203">По умолчанию переопределения этого метода не следует перемещать объекты через существующие объекты Если [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) свойству `true`.</span><span class="sxs-lookup"><span data-stu-id="f6450-203">By default, overrides of this method should not move objects over existing objects unless the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is set to `true`.</span></span> <span data-ttu-id="f6450-204">Например, поставщик filesystem не будет копировать c:\temp\abc.txt через существующий файл c:\bar.txt Если [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) свойству `true`.</span><span class="sxs-lookup"><span data-stu-id="f6450-204">For example, the filesystem provider will not copy c:\temp\abc.txt over an existing c:\bar.txt file unless the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is set to `true`.</span></span> <span data-ttu-id="f6450-205">Если путь, указанный в `destination` параметр существует и является контейнером, [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) свойство не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="f6450-205">If the path specified in the `destination` parameter exists and is a container, the [System.Management.Automation.Provider.Cmdletprovider.Force\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) property is not required.</span></span> <span data-ttu-id="f6450-206">В этом случае [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) следует переместить элемент обозначается `path` параметр в контейнер обозначается `destination` параметр как дочерний элемент.</span><span class="sxs-lookup"><span data-stu-id="f6450-206">In this case, [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) should move the item indicated by the `path` parameter to the container indicated by the `destination` parameter as a child.</span></span>

<span data-ttu-id="f6450-207">Реализация [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) метод должен вызывать [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) и проверьте его возвращаемое значение перед внесением любых изменений в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="f6450-207">Your implementation of the [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) method should call [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) and check its return value before making any changes to the data store.</span></span> <span data-ttu-id="f6450-208">Этот метод используется для подтверждения выполнения операции, при изменении состояния системы, например, удаление файлов.</span><span class="sxs-lookup"><span data-stu-id="f6450-208">This method is used to confirm execution of an operation when a change is made to system state, for example, deleting files.</span></span> <span data-ttu-id="f6450-209">[System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) отправляет имя ресурса, необходимо изменить на пользователя, в среде выполнения Windows PowerShell, принимая во внимание любые параметры командной строки или привилегированных переменных в Определяет, что должно быть отображено пользователю.</span><span class="sxs-lookup"><span data-stu-id="f6450-209">[System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) sends the name of the resource to be changed to the user, with the Windows PowerShell runtime taking into account any command line settings or preference variables in determining what should be displayed to the user.</span></span>

<span data-ttu-id="f6450-210">После вызова [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) возвращает `true`, [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) метод должен вызывать [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) метод.</span><span class="sxs-lookup"><span data-stu-id="f6450-210">After the call to [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) returns `true`, the [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) method should call the [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) method.</span></span> <span data-ttu-id="f6450-211">Этот метод отправляет сообщение пользователю, чтобы разрешить отзыв, чтобы сказать, если операция должна быть продолжено.</span><span class="sxs-lookup"><span data-stu-id="f6450-211">This method sends a message to the user to allow feedback to say if the operation should be continued.</span></span> <span data-ttu-id="f6450-212">Поставщик должен вызывать [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) как дополнительную проверку для изменения потенциально опасных системы.</span><span class="sxs-lookup"><span data-stu-id="f6450-212">Your provider should call [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) as an additional check for potentially dangerous system modifications.</span></span>

## <a name="attaching-dynamic-parameters-to-the-move-item-cmdlet"></a><span data-ttu-id="f6450-213">Присоединение динамических параметров в командлет Move-Item</span><span class="sxs-lookup"><span data-stu-id="f6450-213">Attaching Dynamic Parameters to the Move-Item Cmdlet</span></span>

<span data-ttu-id="f6450-214">Иногда `Move-Item` командлета требуется Дополнительные параметры, которые можно динамически во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="f6450-214">Sometimes the `Move-Item` cmdlet requires additional parameters that are provided dynamically at runtime.</span></span> <span data-ttu-id="f6450-215">Для обеспечения этих динамических параметров, необходимо реализовать поставщик навигации [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItemDynamicParameters) метод для получения значения обязательных параметров из элемента в заданный путь и возвращают объект, имеющий свойства и поля с помощью синтаксического анализа атрибуты аналогично классу командлета или [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) объекта.</span><span class="sxs-lookup"><span data-stu-id="f6450-215">To provide these dynamic parameters, the navigation provider must implement the [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItemDynamicParameters) method to get the required parameter values from the item at the indicated path, and return an object that has properties and fields with parsing attributes similar to a cmdlet class or a [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) object.</span></span>

<span data-ttu-id="f6450-216">Этот поставщик навигации не реализует этот метод.</span><span class="sxs-lookup"><span data-stu-id="f6450-216">This navigation provider does not implement this method.</span></span> <span data-ttu-id="f6450-217">Тем не менее, следующий код является реализация по умолчанию [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItemDynamicParameters).</span><span class="sxs-lookup"><span data-stu-id="f6450-217">However, the following code is the default implementation of [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitemdynamicparameters\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItemDynamicParameters).</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidermoveitemdynamicparameters](Msh_samplestestcmdlets#testprovidermoveitemdynamicparameters)]  -->

## <a name="normalizing-a-relative-path"></a><span data-ttu-id="f6450-218">Нормализация относительный путь</span><span class="sxs-lookup"><span data-stu-id="f6450-218">Normalizing a Relative Path</span></span>

<span data-ttu-id="f6450-219">Пользовательский поставщик реализует навигации [System.Management.Automation.Provider.Navigationcmdletprovider.Normalizerelativepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.NormalizeRelativePath) метод для нормализации полный путь, указанный в `path` параметр как относительно пути, указанному свойством `basePath` параметра.</span><span class="sxs-lookup"><span data-stu-id="f6450-219">Your navigation provider implements the [System.Management.Automation.Provider.Navigationcmdletprovider.Normalizerelativepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.NormalizeRelativePath) method to normalize the fully-qualified path indicated in the `path` parameter as being relative to the path specified by the `basePath` parameter.</span></span> <span data-ttu-id="f6450-220">Метод возвращает строковое представление нормализованный путь.</span><span class="sxs-lookup"><span data-stu-id="f6450-220">The method returns a string representation of the normalized path.</span></span> <span data-ttu-id="f6450-221">Записывает ошибку, если `path` параметр указывает несуществующий путь.</span><span class="sxs-lookup"><span data-stu-id="f6450-221">It writes an error if the `path` parameter specifies a nonexistent path.</span></span>

<span data-ttu-id="f6450-222">Пример поставщика навигации не Переопределите этот метод.</span><span class="sxs-lookup"><span data-stu-id="f6450-222">The sample navigation provider does not override this method.</span></span> <span data-ttu-id="f6450-223">Ниже приводится реализация по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f6450-223">The following is the default implementation.</span></span>

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidernormalizepath](Msh_samplestestcmdlets#testprovidernormalizepath)]  -->

#### <a name="things-to-remember-about-implementing-normalizerelativepath"></a><span data-ttu-id="f6450-224">О чем следует помнить о реализации NormalizeRelativePath</span><span class="sxs-lookup"><span data-stu-id="f6450-224">Things to Remember About Implementing NormalizeRelativePath</span></span>

<span data-ttu-id="f6450-225">Реализация [System.Management.Automation.Provider.Navigationcmdletprovider.Normalizerelativepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.NormalizeRelativePath) синтаксический анализ `path` параметр, но его не нужно использовать исключительно синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="f6450-225">Your implementation of [System.Management.Automation.Provider.Navigationcmdletprovider.Normalizerelativepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.NormalizeRelativePath) should parse the `path` parameter, but it does not have to use purely syntactical parsing.</span></span> <span data-ttu-id="f6450-226">Рекомендуется для разработки, что этот метод следует использовать путь для поиска сведения о пути в хранилище данных и создать путь, который соответствует регистр и стандартизированный синтаксис пути.</span><span class="sxs-lookup"><span data-stu-id="f6450-226">You are encouraged to design this method to use the path to look up the path information in the data store and create a path that matches the casing and standardized path syntax.</span></span>

## <a name="code-sample"></a><span data-ttu-id="f6450-227">Пример кода</span><span class="sxs-lookup"><span data-stu-id="f6450-227">Code Sample</span></span>

<span data-ttu-id="f6450-228">Полный пример кода см. в разделе [пример кода AccessDbProviderSample05](./accessdbprovidersample05-code-sample.md).</span><span class="sxs-lookup"><span data-stu-id="f6450-228">For complete sample code, see [AccessDbProviderSample05 Code Sample](./accessdbprovidersample05-code-sample.md).</span></span>

## <a name="defining-object-types-and-formatting"></a><span data-ttu-id="f6450-229">Определение типов объектов и форматирование</span><span class="sxs-lookup"><span data-stu-id="f6450-229">Defining Object Types and Formatting</span></span>

<span data-ttu-id="f6450-230">Это возможно для поставщика для добавления членов к существующим объектам или определения новых объектов.</span><span class="sxs-lookup"><span data-stu-id="f6450-230">It is possible for a provider to add members to existing objects or define new objects.</span></span> <span data-ttu-id="f6450-231">Дополнительные сведения см. в разделе[расширение типов объектов и форматирование](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span><span class="sxs-lookup"><span data-stu-id="f6450-231">For more information, see[Extending Object Types and Formatting](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span></span>

## <a name="building-the-windows-powershell-provider"></a><span data-ttu-id="f6450-232">Создание поставщика Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6450-232">Building the Windows PowerShell provider</span></span>

<span data-ttu-id="f6450-233">Дополнительные сведения см. в разделе [как регистрация командлетов, поставщиков и ведущих приложений](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span><span class="sxs-lookup"><span data-stu-id="f6450-233">For more information, see [How to Register Cmdlets, Providers, and Host Applications](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span></span>

## <a name="testing-the-windows-powershell-provider"></a><span data-ttu-id="f6450-234">Проверка поставщика в Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6450-234">Testing the Windows PowerShell provider</span></span>

<span data-ttu-id="f6450-235">После регистрации поставщиком Windows PowerShell с помощью Windows PowerShell, можно проверить его, выполнив Поддерживаемые командлеты в командной строке, включая командлеты, доступные через наследование.</span><span class="sxs-lookup"><span data-stu-id="f6450-235">When your Windows PowerShell provider has been registered with Windows PowerShell, you can test it by running the supported cmdlets on the command line, including cmdlets made available by derivation.</span></span> <span data-ttu-id="f6450-236">В этом примере тестирование навигации к образцу поставщика.</span><span class="sxs-lookup"><span data-stu-id="f6450-236">This example will test the sample navigation provider.</span></span>

1. <span data-ttu-id="f6450-237">Запуска новой оболочки и использовать `Set-Location` командлет, чтобы задать путь для указания базы данных Access.</span><span class="sxs-lookup"><span data-stu-id="f6450-237">Run your new shell and use the `Set-Location` cmdlet to set the path to indicate the Access database.</span></span>

   ```powershell
   Set-Location mydb:
   ```

2. <span data-ttu-id="f6450-238">Теперь запустите `Get-Childitem` командлет, чтобы получить список элементов базы данных, которые являются таблицами базы данных.</span><span class="sxs-lookup"><span data-stu-id="f6450-238">Now run the `Get-Childitem` cmdlet to retrieve a list of the database items, which are the available database tables.</span></span> <span data-ttu-id="f6450-239">Для каждой таблицы этот командлет также извлекает количество строк таблицы.</span><span class="sxs-lookup"><span data-stu-id="f6450-239">For each table, this cmdlet also retrieves the number of table rows.</span></span>

   ```powershell
   Get-ChildItem | Format-Table rowcount,name -AutoSize
   ```

   ```output
   RowCount   Name
   --------   ----
        180   MSysAccessObjects
          0   MSysACEs
          1   MSysCmdbars
          0   MSysIMEXColumns
          0   MSysIMEXSpecs
          0   MSysObjects
          0   MSysQueries
          7   MSysRelationships
          8   Categories
         91   Customers
          9   Employees
       2155   Order Details
        830   Orders
         77   Products
          3   Shippers
         29   Suppliers
   ```

3. <span data-ttu-id="f6450-240">Используйте `Set-Location` еще раз, чтобы задать расположение данных таблицы «Сотрудники».</span><span class="sxs-lookup"><span data-stu-id="f6450-240">Use the `Set-Location` cmdlet again to set the location of the Employees data table.</span></span>

   ```powershell
   Set-Location Employees
   ```

4. <span data-ttu-id="f6450-241">Давайте теперь используем `Get-Location` командлет, чтобы получить путь к таблице сотрудников.</span><span class="sxs-lookup"><span data-stu-id="f6450-241">Let's now use the `Get-Location` cmdlet to retrieve the path to the Employees table.</span></span>

   ```powershell
   Get-Location
   ```

   ```output
   Path
   ----
   mydb:\Employees
   ```

5. <span data-ttu-id="f6450-242">Теперь с помощью `Get-Childitem` командлет по конвейеру в `Format-Table` командлета.</span><span class="sxs-lookup"><span data-stu-id="f6450-242">Now use the `Get-Childitem` cmdlet piped to the `Format-Table` cmdlet.</span></span> <span data-ttu-id="f6450-243">Этот набор командлетов извлекает элементы для таблицы данных сотрудников, которые являются строки таблицы.</span><span class="sxs-lookup"><span data-stu-id="f6450-243">This set of cmdlets retrieves the items for the Employees data table, which are the table rows.</span></span> <span data-ttu-id="f6450-244">Они форматируются в соответствии со значениями `Format-Table` командлета.</span><span class="sxs-lookup"><span data-stu-id="f6450-244">They are formatted as specified by the `Format-Table` cmdlet.</span></span>

   ```powershell
   Get-ChildItem | Format-Table rownumber,psiscontainer,data -AutoSize
   ```

   ```output
   RowNumber   PSIsContainer   Data
   ---------   --------------   ----
   0           False            System.Data.DataRow
   1           False            System.Data.DataRow
   2           False            System.Data.DataRow
   3           False            System.Data.DataRow
   4           False            System.Data.DataRow
   5           False            System.Data.DataRow
   6           False            System.Data.DataRow
   7           False            System.Data.DataRow
   8           False            System.Data.DataRow
   ```

6. <span data-ttu-id="f6450-245">Теперь вы можете запустить `Get-Item` командлет, чтобы получить элементы для строк 0 таблицы данных сотрудников.</span><span class="sxs-lookup"><span data-stu-id="f6450-245">You can now run the `Get-Item` cmdlet to retrieve the items for row 0 of the Employees data table.</span></span>

   ```powershell
   Get-Item 0
   ```

   ```output
   PSPath        : AccessDB::C:\PS\Northwind.mdb\Employees\0
   PSParentPath  : AccessDB::C:\PS\Northwind.mdb\Employees
   PSChildName   : 0
   PSDrive       : mydb
   PSProvider    : System.Management.Automation.ProviderInfo
   PSIsContainer : False
   Data           : System.Data.DataRow
   RowNumber      : 0
   ```

7. <span data-ttu-id="f6450-246">Используйте `Get-Item` еще раз, чтобы получить данные о сотрудниках для элементов в строке 0.</span><span class="sxs-lookup"><span data-stu-id="f6450-246">Use the `Get-Item` cmdlet again to retrieve the employee data for the items in row 0.</span></span>

   ```powershell
   (Get-Item 0).data
   ```

   ```output
   EmployeeID      : 1
   LastName        : Davis
   FirstName       : Sara
   Title           : Sales Representative
   TitleOfCourtesy : Ms.
   BirthDate       : 12/8/1968 12:00:00 AM
   HireDate        : 5/1/1992 12:00:00 AM
   Address         : 4567 Main Street
                     Apt. 2A
   City            : Buffalo
   Region          : NY
   PostalCode      : 98052
   Country         : USA
   HomePhone       : (206) 555-9857
   Extension       : 5467
   Photo           : EmpID1.bmp
   Notes           : Education includes a BA in psychology from
                     Colorado State University. She also completed "The
                     Art of the Cold Call."  Nancy is a member of
                     Toastmasters International.
   ReportsTo       : 2
   ```

## <a name="see-also"></a><span data-ttu-id="f6450-247">См. также</span><span class="sxs-lookup"><span data-stu-id="f6450-247">See Also</span></span>

[<span data-ttu-id="f6450-248">Создание поставщиков Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6450-248">Creating Windows PowerShell providers</span></span>](./how-to-create-a-windows-powershell-provider.md)

[<span data-ttu-id="f6450-249">Поставщик разработки Your Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6450-249">Design Your Windows PowerShell provider</span></span>](./designing-your-windows-powershell-provider.md)

[<span data-ttu-id="f6450-250">Расширение типов объектов и форматирование</span><span class="sxs-lookup"><span data-stu-id="f6450-250">Extending Object Types and Formatting</span></span>](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[<span data-ttu-id="f6450-251">Реализация поставщика Windows PowerShell для контейнеров</span><span class="sxs-lookup"><span data-stu-id="f6450-251">Implement a Container Windows PowerShell provider</span></span>](./creating-a-windows-powershell-container-provider.md)

[<span data-ttu-id="f6450-252">Регистрация командлетов, поставщиков и ведущих приложений</span><span class="sxs-lookup"><span data-stu-id="f6450-252">How to Register Cmdlets, Providers, and Host Applications</span></span>](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="f6450-253">Руководство программиста Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6450-253">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="f6450-254">Пакет SDK для Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6450-254">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)