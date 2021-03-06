---
title: Рассмотрение запросов на вытягивание
description: В этой статье описывается, как команда PowerShell-Docs управляет запросами на вытягивание.
ms.date: 03/05/2020
ms.topic: conceptual
ms.openlocfilehash: b9b37816dfdf38e4d8b7c2d66799164d0e97d257
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2020
ms.locfileid: "79060389"
---
# <a name="managing-pull-requests"></a>Управление запросами на вытягивание

В этой статье описывается, как мы управляем запросами на вытягивание в репозитории PowerShell-Docs. Изначально это памятка для участников команды PowerShell-Docs. Здесь она публикуется с целью обеспечить прозрачность процесса для широкого круга участников.

## <a name="best-practices"></a>Рекомендации

- Пользователь, отправляющий запрос на вытягивание, не должен выполнять его слияние, пока не будет проведена его оценка коллегами.
- Назначьте рецензента при отправке запроса на вытягивание. Чем раньше вы его назначите, тем раньше он сможет предоставить свои замечания.
- Используйте комментарии, чтобы описать характер изменения или тип запрашиваемой проверки. Обязательно упомяните (@mention) рецензента. Например, если изменение является незначительным и полная техническая проверка не требуется, поясните это в комментарии.

## <a name="pr-process-steps"></a>Процедура обработки запроса на вытягивание

1. Автор. Создает запрос на вытягивание.
   - Приводит ссылки на проблемы, устраняемые запросом на вытягивание.
   - Использует функцию [автоматического закрытия](https://help.github.com/en/articles/closing-issues-using-keywords) GitHub для закрытия проблемы.
1. Автор. Назначает рецензента из числа коллег.
1. Рецензент. Вычитывает текст и предоставляет комментарии (при необходимости).
1. Автор. Вносит предложенные правки.
1. Оба. Проверяют предварительную версию.
1. Оба. Проверяют отчет о проверке и исправляют предупреждения и ошибки.
1. Автор. Добавляет комментарий об утверждении (включая сведения Acrolinx).
1. Рецензент. Помечает запрос как утвержденный.
1. Администратор репозитория. Выполняет слияние запроса на вытягивание (критерии см. ниже).

## <a name="content-reviewer-checklist"></a>Контрольный список для рецензента содержимого

Более полный список см.в статье [Контрольный список для редактора](editorial-checklist.md).

- Проверка на наличие грамматических и стилистических ошибок, лаконичность, техническую точность
- Проверка актуальности примеров для целевой версии
- Проверка предварительной версии
- Проверка метаданных: правильно указано значение ms.date, удалено значение ms.assetid, имеются все требуемые поля
- Проверка правильности разметки Markdown
  - Сведения о форматировании см. в руководстве по стилю.
- Проверка правильности структуры примеров:
  - вводные предложения;
  - код и выходные данные;
  - подробное описание кода (при необходимости).
- Проверка точности гиперссылок
  - Замена или удаление ссылок на TechNet и MSDN
  - Обеспечение минимального количества перенаправлений к целевому адресу
  - Проверка использования HTTPS
  - Правильный тип ссылки
    - Ссылки на файлы для локальных файлов
    - URL-ссылки для файлов за пределами набора документов
  - Удаление языкового стандарта из URL-адресов
  - Упрощение URL-адресов, указывающих на `docs.microsoft.com`

## <a name="branch-merge-process"></a>Процедура слияния ветвей

Ветвь staging — это единственная ветвь, подлежащая слиянию с ветвью live. Слияние временных (рабочих) ветвей должно выполняться со сжатием.

| *Ветвь для слияния*  | *release-branch* | *staging*        | *live*      |
| ---------------- |:----------------:|:----------------:|:-----------:|
| *working-branch* | слияние со сжатием | слияние со сжатием | Не разрешено |
| *release-branch* | &mdash;          | merge            | Не разрешено |
| *staging*        | перемещение           | &mdash;          | merge       |

### <a name="pr-merger-checklist"></a>Контрольный список для выполняющего слияние запроса на вытягивание

- Проверка содержимого завершена
- Правильная целевая ветвь для изменения
- Конфликты при слиянии отсутствуют
- Все шаги проверки и сборки пройдены
  - Предупреждения и предложения учтены (исключения см. в разделе [Примечания](#notes))
  - Нет неработающих ссылок
- Слияние в соответствии с таблицей

### <a name="notes"></a>Примечания

Представленные ниже предупреждения можно игнорировать.

```
Can't find service name for `<version>/<modulepath>/About/About.md`
```

```
Metadata with following name(s) are not allowed to be set in Yaml header, or as file level
metadata in docfx.json, or as global metadata in docfx.json: `locale`. They are generated by
Docs platform, so the values set in these 3 places will be ignored. Please remove them from all
3 places to resolve the warning.
```

При слиянии запроса на вытягивание указатель HEAD целевой ветви меняется. Все открытые запросы на вытягивание, основанные на предыдущем указателе HEAD, устаревают. Для слияния устаревшего запроса на вытягивание требуются права администратора, которые позволяют игнорировать предупреждения о слиянии в GitHub. Это можно делать без риска, если запросы на вытягивание, слияние которых было выполнено ранее, не затрагивали те же файлы. Однако безопаснее будет нажать кнопку **Update Branch** (Обновить ветвь). Может потребоваться устранить неразрешенные конфликты.

## <a name="publishing-to-live"></a>Публикация в ветви Live

Изменения, накопленные в ветви `staging`, необходимо периодически публиковать на веб-сайте. Для этого нужно выполнить слияние ветви `staging` с ветвью `live`.

- Слияние ветви `staging` с ветвью `live` следует выполнять не реже одного раза в неделю.
- Слияние ветви `staging` с ветвью `live` следует выполнять после любого значительного изменения:
  - внесения изменений в 50 или более файлов;
  - слияния ветви выпуска;
  - внесения изменений в конфигурацию репозитория или набора документов (docfx.json, конфигурации OPS, скрипты сборки и т. д.);
  - внесения изменений в файл перенаправления;
  - внесения изменений в оглавление;
  - слияния ветви проекта (для реорганизации содержимого, массового обновления и т. д.).
