---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Метод PerformRequiredConfigurationChecks
ms.openlocfilehash: 909e3a48d08e0220ab0efc6a03bea7ead5d9843e
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2020
ms.locfileid: "71955011"
---
# <a name="performrequiredconfigurationchecks-method"></a>Метод PerformRequiredConfigurationChecks

Запускает проверку согласованности с помощью планировщика заданий.

## <a name="syntax"></a>Синтаксис

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

## <a name="parameters"></a>Параметры

*Flags* \[in\] Битовая маска, определяющая тип выполняемой проверки согласованности. Допустимы следующие значения, которые можно объединить с помощью битовой операции **OR**:

|Значение |Описание |
|:--- |:---|
|**1** | Обычная проверка согласованности. |
|**2** | Продолжение проверки согласованности после перезагрузки. Это значение не следует использовать в сочетании с другими значениями. |
|**4** | Конфигурация должна извлекаться с запрашивающего сервера, указанного в метаконфигурации для узла. Это значение следует всегда использовать в сочетании с **1**, если указано значение **5**. |
|**8** | Состояние отправки на сервер отчетов. |

## <a name="return-value"></a>Возвращаемое значение

Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.

## <a name="remarks"></a>Remarks

Это статический метод.

## <a name="requirements"></a>Требования

**MOF-файл:** DscCore.mof

**Пространство имен**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>См. также раздел

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
