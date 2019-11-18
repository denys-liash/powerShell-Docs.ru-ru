---
title: Элемент Итемселектионкондитион для ExpressionBinding для GroupBy (Format) | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6af3be7d-921e-4cf7-bd5a-d87aa0b4efbd
caps.latest.revision: 7
ms.openlocfilehash: b2b0a0d1996392614807e08b820a72978e38a0cb
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2019
ms.locfileid: "72365293"
---
# <a name="itemselectioncondition-element-for-expressionbinding-for-groupby-format"></a><span data-ttu-id="0af6f-102">Элемент ItemSelectionCondition для элемента ExpressionBinding для элемента GroupBy (формат)</span><span class="sxs-lookup"><span data-stu-id="0af6f-102">ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format)</span></span>

<span data-ttu-id="0af6f-103">Определяет условие, которое должно существовать для использования этого элемента управления.</span><span class="sxs-lookup"><span data-stu-id="0af6f-103">Defines the condition that must exist for this control to be used.</span></span> <span data-ttu-id="0af6f-104">Количество условий выбора, которое можно указать для элемента управления, не ограничено.</span><span class="sxs-lookup"><span data-stu-id="0af6f-104">There is no limit to the number of selection conditions that can be specified for a control item.</span></span> <span data-ttu-id="0af6f-105">Этот элемент используется при определении того, как отображается новая группа объектов.</span><span class="sxs-lookup"><span data-stu-id="0af6f-105">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="0af6f-106">Элемент конфигурации (Format) Виевдефинитионс элемент (Format) элемент представления (формат) элемент GroupBy для элемента Ошибка customcontrol представления (Format) для элемента Кустоментриес (Format) для ошибка customcontrol для элемента GroupBy (Format) Кустоментри для Ошибка customcontrol для элемента Кустомитем GroupBy для Кустоментри для GroupBy (Format) ExpressionBinding элемента для Кустомитем для элемента итемселектионкондитион в ExpressionBinding для GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="0af6f-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format) ExpressionBinding Element for CustomItem for GroupBy (Format) ItemSelectionCondition Element for ExpressionBinding for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0af6f-107">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="0af6f-107">Syntax</span></span>

```xml
<ItemSelectionCondition>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</ItemSelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0af6f-108">Атрибуты и элементы</span><span class="sxs-lookup"><span data-stu-id="0af6f-108">Attributes and Elements</span></span>

<span data-ttu-id="0af6f-109">В следующих разделах описываются атрибуты, дочерние элементы и родительский элемент элемента `ItemSelectionCondition`.</span><span class="sxs-lookup"><span data-stu-id="0af6f-109">The following sections describe attributes, child elements, and the parent element of the `ItemSelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="0af6f-110">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="0af6f-110">Attributes</span></span>

<span data-ttu-id="0af6f-111">Нет.</span><span class="sxs-lookup"><span data-stu-id="0af6f-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0af6f-112">Дочерние элементы</span><span class="sxs-lookup"><span data-stu-id="0af6f-112">Child Elements</span></span>

|<span data-ttu-id="0af6f-113">Элемент</span><span class="sxs-lookup"><span data-stu-id="0af6f-113">Element</span></span>|<span data-ttu-id="0af6f-114">Описание</span><span class="sxs-lookup"><span data-stu-id="0af6f-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0af6f-115">Элемент PropertyName для Итемселектионкондитион для GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="0af6f-115">PropertyName Element for ItemSelectionCondition for GroupBy (Format)</span></span>](./propertyname-element-for-itemselectioncondition-for-groupby-format.md)|<span data-ttu-id="0af6f-116">Необязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="0af6f-116">Optional element.</span></span><br /><br /> <span data-ttu-id="0af6f-117">Указывает свойство .NET, которое запускает условие.</span><span class="sxs-lookup"><span data-stu-id="0af6f-117">Specifies the .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="0af6f-118">Элемент ScriptBlock для Итемселектионкондитион для GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="0af6f-118">ScriptBlock Element for ItemSelectionCondition for GroupBy (Format)</span></span>](./scriptblock-element-for-itemselectioncondition-for-groupby-format.md)|<span data-ttu-id="0af6f-119">Необязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="0af6f-119">Optional element.</span></span><br /><br /> <span data-ttu-id="0af6f-120">Указывает скрипт, который запускает условие.</span><span class="sxs-lookup"><span data-stu-id="0af6f-120">Specifies the script that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="0af6f-121">Родительские элементы</span><span class="sxs-lookup"><span data-stu-id="0af6f-121">Parent Elements</span></span>

|<span data-ttu-id="0af6f-122">Элемент</span><span class="sxs-lookup"><span data-stu-id="0af6f-122">Element</span></span>|<span data-ttu-id="0af6f-123">Описание</span><span class="sxs-lookup"><span data-stu-id="0af6f-123">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0af6f-124">Элемент ExpressionBinding для Кустомитем для GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="0af6f-124">ExpressionBinding Element for CustomItem for GroupBy (Format)</span></span>](./expressionbinding-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="0af6f-125">Определяет данные, отображаемые элементом управления.</span><span class="sxs-lookup"><span data-stu-id="0af6f-125">Defines the data that is displayed by the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="0af6f-126">Замечания</span><span class="sxs-lookup"><span data-stu-id="0af6f-126">Remarks</span></span>

<span data-ttu-id="0af6f-127">Можно указать одно имя свойства или скрипт для этого условия, но не указывать оба значения.</span><span class="sxs-lookup"><span data-stu-id="0af6f-127">You can specify one property name or a script for this condition but cannot specify both.</span></span>

## <a name="see-also"></a><span data-ttu-id="0af6f-128">См. также:</span><span class="sxs-lookup"><span data-stu-id="0af6f-128">See Also</span></span>

[<span data-ttu-id="0af6f-129">Написание файла форматирования PowerShell</span><span class="sxs-lookup"><span data-stu-id="0af6f-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)

[<span data-ttu-id="0af6f-130">Элемент ExpressionBinding для Кустомитем для GroupBy (Format)</span><span class="sxs-lookup"><span data-stu-id="0af6f-130">ExpressionBinding Element for CustomItem for GroupBy (Format)</span></span>](./expressionbinding-element-for-customitem-for-groupby-format.md)