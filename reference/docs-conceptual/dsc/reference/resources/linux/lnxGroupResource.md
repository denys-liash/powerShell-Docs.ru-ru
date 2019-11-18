---
ms.date: 09/20/2019
keywords: dsc,powershell,конфигурация,установка
title: Ресурс nxGroup в DSC для Linux
ms.openlocfilehash: 098ae2e8ab183934ec3c185c0fd237731b1353dc
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/04/2019
ms.locfileid: "71953211"
---
# <a name="dsc-for-linux-nxgroup-resource"></a><span data-ttu-id="a69fa-103">Ресурс nxGroup в DSC для Linux</span><span class="sxs-lookup"><span data-stu-id="a69fa-103">DSC for Linux nxGroup Resource</span></span>

<span data-ttu-id="a69fa-104">Ресурс **nxGroup** в DSC PowerShell предоставляет механизм управления локальными группами на узле Linux.</span><span class="sxs-lookup"><span data-stu-id="a69fa-104">The **nxGroup** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="a69fa-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="a69fa-105">Syntax</span></span>

```Syntax
nxGroup <string> #ResourceName
{
    GroupName = <string>
    [ Members = <string[]> ]
    [ MembersToInclude = <string[]> ]
    [ MembersToExclude = <string[]> ]
    [ PreferredGroupID = <string> ]
    [ DependsOn = <string[]> ]
    [ Ensure = <string> { Absent | Present } ]
}
```

## <a name="properties"></a><span data-ttu-id="a69fa-106">Свойства</span><span class="sxs-lookup"><span data-stu-id="a69fa-106">Properties</span></span>

|<span data-ttu-id="a69fa-107">Свойство</span><span class="sxs-lookup"><span data-stu-id="a69fa-107">Property</span></span> |<span data-ttu-id="a69fa-108">Описание</span><span class="sxs-lookup"><span data-stu-id="a69fa-108">Description</span></span> |
|---|---|
|<span data-ttu-id="a69fa-109">GroupName</span><span class="sxs-lookup"><span data-stu-id="a69fa-109">GroupName</span></span> |<span data-ttu-id="a69fa-110">Указывает имя группы, для которой требуется обеспечить определенное состояние.</span><span class="sxs-lookup"><span data-stu-id="a69fa-110">Specifies the name of the group for which you want to ensure a specific state.</span></span> |
|<span data-ttu-id="a69fa-111">Члены группы</span><span class="sxs-lookup"><span data-stu-id="a69fa-111">Members</span></span> |<span data-ttu-id="a69fa-112">Указывает членов группы.</span><span class="sxs-lookup"><span data-stu-id="a69fa-112">Specifies the members that form the group.</span></span> |
|<span data-ttu-id="a69fa-113">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="a69fa-113">MembersToInclude</span></span> |<span data-ttu-id="a69fa-114">Указывает пользователей, которых нужно добавить в группу.</span><span class="sxs-lookup"><span data-stu-id="a69fa-114">Specifies the users who you want to ensure are members of the group.</span></span> |
|<span data-ttu-id="a69fa-115">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="a69fa-115">MembersToExclude</span></span> |<span data-ttu-id="a69fa-116">Указывает пользователей, которых нужно исключить из группы.</span><span class="sxs-lookup"><span data-stu-id="a69fa-116">Specifies the users who you want to ensure are not members of the group.</span></span> |
|<span data-ttu-id="a69fa-117">PreferredGroupID</span><span class="sxs-lookup"><span data-stu-id="a69fa-117">PreferredGroupID</span></span> |<span data-ttu-id="a69fa-118">По возможности задает в качестве идентификатора группы указанное значение.</span><span class="sxs-lookup"><span data-stu-id="a69fa-118">Sets the group id to the provided value if possible.</span></span> <span data-ttu-id="a69fa-119">Если этот идентификатор группы сейчас используется, выбирается следующий доступный идентификатор группы.</span><span class="sxs-lookup"><span data-stu-id="a69fa-119">If the group id is currently in use, the next available group id is used.</span></span> |

## <a name="common-properties"></a><span data-ttu-id="a69fa-120">Общие свойства</span><span class="sxs-lookup"><span data-stu-id="a69fa-120">Common properties</span></span>

|<span data-ttu-id="a69fa-121">Свойство</span><span class="sxs-lookup"><span data-stu-id="a69fa-121">Property</span></span> |<span data-ttu-id="a69fa-122">Описание</span><span class="sxs-lookup"><span data-stu-id="a69fa-122">Description</span></span> |
|---|---|
|<span data-ttu-id="a69fa-123">DependsOn</span><span class="sxs-lookup"><span data-stu-id="a69fa-123">DependsOn</span></span> |<span data-ttu-id="a69fa-124">Указывает, что перед настройкой этого ресурса необходимо запустить настройку другого ресурса.</span><span class="sxs-lookup"><span data-stu-id="a69fa-124">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="a69fa-125">Например, если идентификатор первого запускаемого блока сценария для конфигурации ресурса — ResourceName, а его тип — ResourceType, то синтаксис использования этого свойства таков: `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="a69fa-125">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is ResourceType, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span> |
|<span data-ttu-id="a69fa-126">Ensure</span><span class="sxs-lookup"><span data-stu-id="a69fa-126">Ensure</span></span> |<span data-ttu-id="a69fa-127">Определяет, нужно ли проверять существование группы.</span><span class="sxs-lookup"><span data-stu-id="a69fa-127">Determines whether to check if the group exists.</span></span> <span data-ttu-id="a69fa-128">Чтобы гарантировать, что группа существует, укажите для этого свойства значение **Present**.</span><span class="sxs-lookup"><span data-stu-id="a69fa-128">Set this property to **Present** to ensure the group exists.</span></span> <span data-ttu-id="a69fa-129">Чтобы гарантировать, что группа не существует, укажите для этого свойства значение **Absent**.</span><span class="sxs-lookup"><span data-stu-id="a69fa-129">Set it to **Absent** to ensure the group does not exist.</span></span> <span data-ttu-id="a69fa-130">Значение по умолчанию — **Present**.</span><span class="sxs-lookup"><span data-stu-id="a69fa-130">The default value is **Present**.</span></span> |

## <a name="example"></a><span data-ttu-id="a69fa-131">Пример</span><span class="sxs-lookup"><span data-stu-id="a69fa-131">Example</span></span>

<span data-ttu-id="a69fa-132">В следующем примере удостоверяется, что пользователь monuser существует и является членом группы DBusers.</span><span class="sxs-lookup"><span data-stu-id="a69fa-132">The following example ensures that the user 'monuser' exists and is a member of the group 'DBusers'.</span></span>

```powershell
Import-DSCResource -Module nx

Node $node
{
    nxUser UserExample {
       UserName = 'monuser'
       Description = 'Monitoring user'
       Password = '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
       Ensure = 'Present'
       HomeDirectory = '/home/monuser'
    }

    nxGroup GroupExample {
       GroupName = 'DBusers'
       Ensure = 'Present'
       MembersToInclude = 'monuser'
       DependsOn = '[nxUser]UserExample'
    }
}
```