---
title: Рассмотрение сообщений о проблемах
description: В этой статье описывается, как команда PowerShell-Docs управляет запросами на вытягивание.
ms.date: 03/05/2020
ms.topic: conceptual
ms.openlocfilehash: cd7aba83d42a6a2eba1ce73910fdd34096342c21
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2020
ms.locfileid: "79060279"
---
# <a name="how-we-manage-issues"></a>Рассмотрение сообщений о проблемах

В этой статье описывается, как мы управляем проблемами в репозитории PowerShell-Docs. Изначально это памятка для участников команды PowerShell-Docs. Здесь она публикуется с целью обеспечить прозрачность процесса для широкого круга участников.

## <a name="sources-of-issues"></a>Источники проблем

- Участники из сообщества
- Внутренние участники
- Расшифровка комментариев из каналов социальных сетей
- Комментарии, полученные через форму отзыва в документации

## <a name="response-time-targets"></a>Целевые показатели времени отклика

- Рассмотрение — 5 рабочих дней
- Исправление или изменение — срок не определен, по мере возможности

### <a name="labeling--milestones"></a>Метки и вехи

#### <a name="label-types"></a>Типы меток

|Prefix  | Описание                                                         |
|------- | --------------------------------------------------------------------|
|Область    | Используется для указания того, к какой части PowerShell или документации относится проблема.<br>Позволяет разработчикам функций легко находить проблемы, связанные с их функциями.|
|Pri (Приоритет)     | Используется для указания приоритета проблемы. Диапазон значений: 0–4.        |
|Проблема   | Используется для классификации типа отзыва для проблемы.                     |
|Просмотр  | Используется для проблемы, требующей дальнейшей проверки командой.              |
|Состояние  | Используется для указания состояния рабочего элемента.                        |
|Waiting | Используется для указания на то, что мы ждем чего-либо.                   |

#### <a name="milestones"></a>Вехи

Проблемы и запросы на вытягивание должны помечаться соответствующими вехами. Если проблема не связана с конкретной версией, веха не используется. Проблемам, связанным с запросами на вытягивание для изменений, слияние которых еще не выполнено с базой кода PowerShell, следует назначать веху **Future** (В будущем). После слияния изменения кода измените веху на соответствующую версию.

|    Веха     |                    Описание                     |
| ---------------- | -------------------------------------------------- |
| 6.x              | Рабочие элементы, связанные с версиями PowerShell от 6.0 до 6.2.x |
| 7.0.0            | Рабочие элементы, связанные с PowerShell 7.0               |
| 7.1.0            | Рабочие элементы, связанные с PowerShell 7.1               |
| Планируется реализация.           | Рабочие элементы, связанные с будущей версией PowerShell          |
| PSReadline-vNext | Рабочие элементы, связанные с будущей версией PSReadline          |

## <a name="triage-process"></a>Процесс рассмотрения

Группа, ответственная за разработку документации по PowerShell, собирается один раз в неделю, чтобы обсудить все проблемы, добавленные с момента последнего собрания. Проблема считается рассмотренной, когда ей назначены метки или владелец. Участникам группы, ответственной за документацию по PowerShell, рекомендуется проверять проблемы ежедневно и рассматривать новые проблемы по мере их поступления. Затем на еженедельном собрании новые проблемы могут обсуждаться более подробно, если это необходимо.

### <a name="misplaced-product-feedback"></a>Ошибочно адресованный отзыв о продукте

- Введите комментарий для клиента о том, что это отзыв о продукте, и предоставьте ссылку на соответствующий канал обратной связи.
- Необязательное действие: Скопируйте проблему в соответствующий канал обратной связи, добавьте ссылку на скопированный элемент и закройте проблему. НЕ копируйте проблемы в UserVoice.

  | Набор документации    | URL-адрес для отзыва о продукте                                         |
  | --------- | ------------------------------------------------------------ |
  | developer | https://github.com/PowerShell/PowerShell/issues/new/choose   |
  | DSC       | https://windowsserver.uservoice.com/forums/301869-powershell |
  | gallery   | https://github.com/powershell/powershellgallery/issues/new   |
  | jea       | https://github.com/powershell/jea/issues/new                 |
  | reference | https://github.com/PowerShell/PowerShell/issues/new/choose   |
  | wmf       | https://windowsserver.uservoice.com/forums/301869-powershell |

### <a name="support-requests"></a>Запросы в службу поддержки

- Если вопрос в службу поддержки прост, ответьте на него и закройте проблему.
- Если вопрос сложный или отправитель задает дополнительные вопросы, перенаправьте его на форумы и в каналы поддержки. Вариант текста для перенаправления на форумы:

    > Это не самый подходящий форум для вопросов такого рода. Попробуйте опубликовать свой вопрос на форуме поддержки сообщества. Список форумов сообщества см. по следующему адресу: https://docs.microsoft.com/powershell/scripting/community/community-support

### <a name="code-of-conduct-violations"></a>Нарушение кодекса поведения

- При необходимости отредактируйте проблему, чтобы удалить оскорбительное содержимое.
- Введите комментарий о том, что проблема является спамом, закройте проблему и заблокируйте ее, чтобы запретить добавление комментариев.
- Каждое такое событие подлежит обсуждению на еженедельном собрании с целью решить, требуются ли дальнейшие действия (нужно ли сообщить о нарушении в GitHub или юридический отдел Майкрософт).
