---
title: Параметры входного фильтра | Документация Майкрософт
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e45929d1-bbb4-4dc6-892f-f9eacdb1c84c
caps.latest.revision: 8
ms.openlocfilehash: 553878c34e74129f9876cca25a5393cb0d53445a
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2019
ms.locfileid: "72364393"
---
# <a name="input-filter-parameters"></a>Параметры фильтра ввода

Командлет может определять параметры `Filter`, `Include`и `Exclude`, которые фильтруют набор входных объектов, на которые влияет командлет.

Как правило, набор входных объектов задается параметром `InputObject`, `Path`или `Name`. Например, командлет может иметь параметр `Path`, который принимает несколько путей с помощью подстановочных знаков, и каждый путь указывает на входной объект. Параметры `Filter`, `Include`и `Exclude` дополнительно указывают пути, выполняемые командлетом при каждом вызове.

## <a name="include-and-exclude-parameters"></a>Параметры включения и исключения

Параметры `Include` и `Exclude` определяют объекты, которые включаются или исключаются из набора входных объектов, переданных в командлет. Используйте эти параметры, если фильтр можно выразить на стандартном языке с подстановочными знаками. (Дополнительные сведения о символах-шаблонах см. [в разделе Поддержка подстановочных знаков в параметрах командлета](./supporting-wildcard-characters-in-cmdlet-parameters.md).) Параметр `Include` включает все объекты, имена которых соответствуют фильтру включения. Параметр `Exclude` исключает все объекты, имена которых соответствуют фильтру.

## <a name="filter-parameter"></a>Параметр фильтра

Параметр `Filter` задает фильтр, который не выражается в стандартном языке с подстановочными знаками. Например, Active Directory интерфейсы ADSI или фильтры SQL могут передаваться в командлет через его параметр `Filter`. В командлетах, предоставляемых Windows PowerShell, эти фильтры указываются поставщиками Windows PowerShell, которые используют командлет для доступа к хранилищу данных. Каждый поставщик обычно определяет собственный фильтр.

## <a name="filtering-if-no-set-of-input-objects-is-specified"></a>Фильтрация, если не указано ни одного набора входных объектов

Если не указано ни одного набора входных объектов, обычно это означает фильтрацию по всем объектам. Дополнительные сведения см. в разделе[Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process).

## <a name="see-also"></a>См. также:

[Запись командлета Windows PowerShell](./writing-a-windows-powershell-cmdlet.md)