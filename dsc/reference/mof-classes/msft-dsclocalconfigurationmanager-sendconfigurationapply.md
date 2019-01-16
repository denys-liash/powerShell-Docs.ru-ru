---
ms.date: 06/12/2017
keywords: dsc,powershell,конфигурация,установка
title: Метод SendConfigurationApply класса MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: da3a08307122ab38ee4a6fd5d4a9b97579a988f7
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MTE95
ms.contentlocale: ru-RU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54047504"
---
# <a name="sendconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="90306-103">Метод SendConfigurationApply класса MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="90306-103">SendConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="90306-104">Отправляет документ конфигурации на управляемый узел и использует агент конфигурации для применения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="90306-104">Sends the configuration document to the managed node and uses the Configuration Agent to apply the configuration.</span></span>

## <a name="syntax"></a><span data-ttu-id="90306-105">Синтаксис</span><span class="sxs-lookup"><span data-stu-id="90306-105">Syntax</span></span>

```mof
uint32 SendConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

## <a name="parameters"></a><span data-ttu-id="90306-106">Параметры</span><span class="sxs-lookup"><span data-stu-id="90306-106">Parameters</span></span>

<span data-ttu-id="90306-107">*ConfigurationData* \[in\] Данные среды для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="90306-107">*ConfigurationData* \[in\] The environment data for the configuration.</span></span>

<span data-ttu-id="90306-108">*force* \[in\] **true** для принудительной остановки конфигурации.</span><span class="sxs-lookup"><span data-stu-id="90306-108">*force* \[in\] **true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="90306-109">Возвращаемое значение</span><span class="sxs-lookup"><span data-stu-id="90306-109">Return value</span></span>

<span data-ttu-id="90306-110">Возвращает нуль в случае успешного выполнения; в противном случае возвращает код ошибки.</span><span class="sxs-lookup"><span data-stu-id="90306-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="90306-111">Замечания</span><span class="sxs-lookup"><span data-stu-id="90306-111">Remarks</span></span>

<span data-ttu-id="90306-112">Это статический метод.</span><span class="sxs-lookup"><span data-stu-id="90306-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="90306-113">Требования</span><span class="sxs-lookup"><span data-stu-id="90306-113">Requirements</span></span>

<span data-ttu-id="90306-114">MOF\*\* DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="90306-114">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="90306-115">-Namespace Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="90306-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="90306-116">См. также:</span><span class="sxs-lookup"><span data-stu-id="90306-116">See also</span></span>

[<span data-ttu-id="90306-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="90306-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)