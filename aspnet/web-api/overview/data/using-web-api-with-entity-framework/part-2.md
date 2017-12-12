---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: "Добавление моделей и контроллеры | Документы Microsoft"
author: MikeWasson
description: 
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/16/2014
ms.topic: article
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
ms.technology: dotnet-webapi
ms.prod: .net-framework
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: b75eae11fd99b60864256f79d4770a3007487964
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2017
---
<a name="add-models-and-controllers"></a>Добавление моделей и контроллеры
====================
по [Mike Wasson](https://github.com/MikeWasson)

[Загрузка завершенного проекта](https://github.com/MikeWasson/BookService)

В этом разделе вы добавите модели классы, определяющие сущности базы данных. Затем нужно добавить контроллеры веб-API, которые выполняют операции CRUD над этими сущностями.

## <a name="add-model-classes"></a>Добавлять классы модели

В этом учебнике мы создадим базы данных на основе подхода «Первый кода» для Entity Framework (EF). В режиме Code First записи классов C#, которые соответствуют таблицам базы данных и EF создает базу данных. (Дополнительные сведения см. в разделе [принципы разработки с использованием Entity Framework](https://msdn.microsoft.com/en-us/library/ms178359%28v=vs.110%29.aspx#dbfmfcf).)

Начинается с определения наши объекты домена как POCO (plain old CLR объекты). Мы создадим POCO следующие:

- Дизайнер
- Книги

В обозревателе решений щелкните правой кнопкой мыши папку модели. Выберите **добавить**, а затем выберите **класса**. Присвойте классу имя `Author`.

![](part-2/_static/image1.png)

Замените весь код шаблона в Author.cs следующий код.

[!code-csharp[Main](part-2/samples/sample1.cs)]

Добавьте еще один класс с именем `Book`, с помощью следующего кода.

[!code-csharp[Main](part-2/samples/sample2.cs)]

Платформа Entity Framework будет использовать эти модели для создания таблиц базы данных. Для каждой модели `Id` свойство станет столбец первичного ключа таблицы базы данных.

В классе книги `AuthorId` определяет внешний ключ в `Author` таблицы. (Для простоты я полагаю, каждая книга имеет одного автора.) Книги класс также содержит свойства навигации для связанного `Author`. Свойство навигации можно использовать для доступа к связанной `Author` в коде. Подробнее о свойствах навигации в часть 4, [обработки отношениями сущностей](part-4.md).

## <a name="add-web-api-controllers"></a>Добавление контроллеров веб-API

В этом разделе мы добавим контроллеры веб-API, которые поддерживают операции CRUD (Создание, чтение, обновление и удаление). Контроллеры будет использовать Entity Framework для взаимодействия с уровня базы данных.

Во-первых можно удалить файл Controllers/ValuesController.cs. Этот файл содержит пример контроллер веб-API, но это не требуется для этого учебника.

![](part-2/_static/image2.png)

Затем выполните построение проекта. Формирование шаблонов веб-API использует отражение для поиска классы модели, поэтому он должен скомпилированную сборку.

В обозревателе решений щелкните правой кнопкой мыши папку Controllers. Выберите **добавить**, а затем выберите **контроллера**.

![](part-2/_static/image3.png)

В **Добавление формирования шаблонов** диалогового окна выберите «веб-API 2 контроллер с действиями, использующий Entity Framework». Нажмите кнопку **Добавить**.

![](part-2/_static/image4.png)

В **добавить контроллер** диалоговое окно, выполните следующие действия:

1. В **класс модели** раскрывающийся список, выберите `Author` класса. (Если вы не видите она появляется в раскрывающемся списке, убедитесь, что построение проекта.)
2. Проверьте «Используйте асинхронные действия контроллера».
3. Имя контроллера как оставить &quot;AuthorsController&quot;.
4. Щелкните плюс (+) рядом с кнопкой **класс контекста данных**.

![](part-2/_static/image5.png)

В **новый контекст данных** диалогового окна, оставьте имя по умолчанию и нажмите кнопку **добавить**.

![](part-2/_static/image6.png)

Нажмите кнопку **добавить** для завершения **добавить контроллер** диалогового окна. Диалоговое окно добавляет два класса в проект:

- `AuthorsController`Определяет контроллер веб-API. Контроллер реализует API REST, который клиенты используют для выполнения операций CRUD в списке авторов.
- `BookServiceContext`управляет объектами сущностей во время выполнения, включая заполнение данными из базы данных, отслеживание изменений и сохранения данных в базу данных. Он наследуется от `DbContext`.

![](part-2/_static/image7.png)

На этом этапе построения проекта. Теперь выполните те же шаги, чтобы добавить контроллер API для `Book` сущностей. На этот раз выберите `Book` класс модели и выберите существующий `BookServiceContext` класс для класса контекста данных. (Не создавать новый контекст данных). Нажмите кнопку **добавить** Добавление контроллера.

![](part-2/_static/image8.png)

>[!div class="step-by-step"]
[Назад](part-1.md)
[Вперед](part-3.md)