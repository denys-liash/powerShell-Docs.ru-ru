---
ms.date: 06/12/2017
contributor: Farehar
keywords: gallery,powershell,psgallery
title: Запрос на принятие условий лицензии
ms.openlocfilehash: eaed248895d14bd455d2d8d3c2222d8848eeccae
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50003903"
---
# <a name="require-license-acceptance"></a><span data-ttu-id="7b036-103">Запрос на принятие условий лицензии</span><span class="sxs-lookup"><span data-stu-id="7b036-103">Require license acceptance</span></span>

<span data-ttu-id="7b036-104">На странице сведений об элементах модулей, для использования которых требуется принять условия лицензии, отображается соответствующий текст.</span><span class="sxs-lookup"><span data-stu-id="7b036-104">Require License Acceptance text shows up on item details page for modules that require license acceptance.</span></span> <span data-ttu-id="7b036-105">Лицензию для модуля можно просмотреть, щелкнув ссылку View License.txt.</span><span class="sxs-lookup"><span data-stu-id="7b036-105">License for module can be viewed by clicking on 'View License.txt' link.</span></span>

![Запрос на принятие условий лицензии](../../Images/RequireLicenseAcceptance.png)

<span data-ttu-id="7b036-107">При установке, сохранении и обновлении модуля с помощью PowerShellGet или при развертывании в службе автоматизации Azure пользователям будет предложено принять условия лицензионного соглашения.</span><span class="sxs-lookup"><span data-stu-id="7b036-107">Users will be prompted to accept the license when installing, saving or updating the module through PowerShellGet or when deploying to Azure Automation.</span></span>

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a><span data-ttu-id="7b036-108">Запрос на принятие условий лицензии при развертывании в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="7b036-108">Require License Acceptance on Deploy to Azure Automation</span></span>

<span data-ttu-id="7b036-109">Если для использования модуля, который развертывается в службе автоматизации Azure, нужно принять условия лицензионного соглашения, в пользовательском интерфейсе портала отобразится текст "Этот модуль требует принять условия лицензии.</span><span class="sxs-lookup"><span data-stu-id="7b036-109">If the module being deployed to Azure Automation requires license acceptance, portal UI will show a disclaimer saying 'This module requires license acceptance.</span></span> <span data-ttu-id="7b036-110">Нажав кнопку "ОК", вы принимаете условия лицензии".</span><span class="sxs-lookup"><span data-stu-id="7b036-110">By clicking OK, you are accepting license terms.'</span></span>

![Запрос на принятие условий лицензии при развертывании в службе автоматизации Azure](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a><span data-ttu-id="7b036-112">Дополнительные подробности</span><span class="sxs-lookup"><span data-stu-id="7b036-112">More details</span></span>

<span data-ttu-id="7b036-113">[Запрос на принятие условий лицензии в PowerShellGet](../../concepts/module-license-acceptance.md)
[Веб-сайт службы автоматизации Azure](/azure/automation)</span><span class="sxs-lookup"><span data-stu-id="7b036-113">[Require License Acceptance in PowerShellGet](../../concepts/module-license-acceptance.md)
[Azure Automation website](/azure/automation)</span></span>