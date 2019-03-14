---
title: TypeName-элемент для SelectionCondition для EntrySelectedBy для WideControl (формат) | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6d6d43fa-c900-4e2f-952d-deccd584236f
caps.latest.revision: 11
ms.openlocfilehash: 0d7bbfd8be3bf2bd1af75a45ca4db016dfb6bff6
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56857960"
---
# <a name="typename-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format"></a><span data-ttu-id="ef430-102">Элемент TypeName для элемента SelectionCondition для элемента EntrySelectedBy для элемента WideControl (формат)</span><span class="sxs-lookup"><span data-stu-id="ef430-102">TypeName Element for SelectionCondition for EntrySelectedBy for WideControl (Format)</span></span>

<span data-ttu-id="ef430-103">Указывает тип .NET, который активирует условие.</span><span class="sxs-lookup"><span data-stu-id="ef430-103">Specifies a .NET type that triggers the condition.</span></span> <span data-ttu-id="ef430-104">При наличии этого типа используется определение.</span><span class="sxs-lookup"><span data-stu-id="ef430-104">When this type is present, the definition is used.</span></span>

<span data-ttu-id="ef430-105">Элемент (формат) элемент ViewDefinitions (формат) представление элемента (формат) элемент WideControl (формат) элемент WideEntries (формат) элемент WideEntry (формат) EntrySelectedBy элемент конфигурации для элемент SelectionCondition WideEntry (формат) для EntrySelectedBy WideEntry (формат) имя типа элемента для SelectionCondition для EntrySelectedBy для WideEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="ef430-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) SelectionCondition Element for EntrySelectedBy for WideEntry (Format) TypeName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="ef430-106">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="ef430-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="ef430-107">Атрибуты и элементы</span><span class="sxs-lookup"><span data-stu-id="ef430-107">Attributes and Elements</span></span>

<span data-ttu-id="ef430-108">Ниже описаны атрибуты, дочерние элементы и родительский элемент `TypeName` элемент.</span><span class="sxs-lookup"><span data-stu-id="ef430-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="ef430-109">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="ef430-109">Attributes</span></span>

<span data-ttu-id="ef430-110">Нет.</span><span class="sxs-lookup"><span data-stu-id="ef430-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="ef430-111">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="ef430-111">Child Elements</span></span>

<span data-ttu-id="ef430-112">Нет.</span><span class="sxs-lookup"><span data-stu-id="ef430-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="ef430-113">Родительские элементы</span><span class="sxs-lookup"><span data-stu-id="ef430-113">Parent Elements</span></span>

|<span data-ttu-id="ef430-114">Элемент</span><span class="sxs-lookup"><span data-stu-id="ef430-114">Element</span></span>|<span data-ttu-id="ef430-115">Описание</span><span class="sxs-lookup"><span data-stu-id="ef430-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ef430-116">Элемент SelectionCondition для EntrySelectedBy для WideEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="ef430-116">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|<span data-ttu-id="ef430-117">Определяет условие, которое должен существовать для данной записи, расширенный для использования.</span><span class="sxs-lookup"><span data-stu-id="ef430-117">Defines the condition that must exist for this wide entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="ef430-118">Текстовое значение</span><span class="sxs-lookup"><span data-stu-id="ef430-118">Text Value</span></span>

<span data-ttu-id="ef430-119">Укажите полное имя типа .NET, например `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="ef430-119">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="ef430-120">Замечания</span><span class="sxs-lookup"><span data-stu-id="ef430-120">Remarks</span></span>

<span data-ttu-id="ef430-121">Условию выбора можно указать тип .NET или выбор задать, но нельзя указать одновременно.</span><span class="sxs-lookup"><span data-stu-id="ef430-121">The selection condition can specify a .NET type or a selection set, but cannot specify both.</span></span> <span data-ttu-id="ef430-122">Дополнительные сведения об использовании условий выборки см. в разделе [определение условий при отображении данных](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="ef430-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="ef430-123">Дополнительные сведения о других компонентах широкое представление, см. в разделе [Создание широкое представление](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="ef430-123">For more information about other components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ef430-124">См. также</span><span class="sxs-lookup"><span data-stu-id="ef430-124">See Also</span></span>

[<span data-ttu-id="ef430-125">Creatng широкое представление</span><span class="sxs-lookup"><span data-stu-id="ef430-125">Creatng a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="ef430-126">Определение условия при отображении данных</span><span class="sxs-lookup"><span data-stu-id="ef430-126">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="ef430-127">Элемент SelectionCondition для EntrySelectedBy для WideEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="ef430-127">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="ef430-128">Элемент SelectionSetName для SelectionCondition для EntrySelectedBy для WideEntry (формат)</span><span class="sxs-lookup"><span data-stu-id="ef430-128">SelectionSetName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)

[<span data-ttu-id="ef430-129">Запись файла форматирования PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef430-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)