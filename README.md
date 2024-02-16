# MariyaKustova-Design-Patterns

Паттерны проектирования, или как разобраться в архитектуре приложения и не сойти с ума…

Всем привет, меня зовут Маша и я работаю разработчиком в крупной IT-компании “IBS”. Моя история с организацией началась со стажерской программы и продолжается по сей день) Придя на проект, после первого шока и состояния «легкого удивления» от увиденного (это мое первое рабочее место в этой сфере, плюс проект не из разряда лэндингов и SPA), поняла что, для того чтобы не сойти с ума нужно открыть package.json и монотонно и последовательно изучать все технологии, которые скрываются за незнакомыми «аглицкми словесами». 
1,5 года спустя после ряда однотипных задач невольно приходишь к выводу, что знания одних технологий недостаточно и неплохо было бы освоить что-то, так сказать, находящееся над кодовой базой. Если быть точнее - узнать по каким же магическим правилам и принципам один файл должен находиться здесь, а другой отвечать за что-то индивидуально-специфическое. Как сделать так, чтобы новое желание заказчика или умозаключение аналитика не одарило тебя бессонными ночами, так как спроектированная тобой система не расположена одобрительно к расширению и требует нескольких десятков условных конструкций для реализации нового функционала. Это небольшая предыстория причины написания данной статьи, которая (смею надеяться) будет полезна и интересна к прочтению.
Итак, поехали)

Что такое паттерн?

Паттерн – это некий образец или шаблон. Это ситуация, когда множество разработчиков работали над задачей, решающей подобную твоей проблему, и при этом 50 раз «упали», 100 раз «набили шишек», 150 раз изобрели уникальный ни на что другое не похожий «велосипед» и пришли к единому мнению. Это конечно ирония, но достаточно верно трактующаяся простым правилом «Посмотри, как сделали другие и примени их решение! Сэкономь время себе, коллегам и заказчику)»
Стоит оговориться, что паттерны проектирования представляют собой незаконченные примеры. Они просто показывают пример решения типовой проблемы, поэтому готовый код придётся дорабатывать.
	Существует огромное количество паттернов, но все из них можно отнести к одному из трех шаблонов:
- Порождающему;
- Структурному;
- Поведенческому.

Чтобы познакомиться с паттернами проектирования и узнать в чем их профит, начнем с того, что уделим внимание каждому шаблону, описанному выше.

Порождающие шаблоны

Порождающие шаблоны помогают осуществить процесс создания большого количества похожих сущностей или групп сущностей. Они инкапсулируют знания о конкретных классах, которые применяются в системе. То есть скрывают детали, как эти классы создаются и стыкуются. Единственная информация об объектах, известная системе, — их интерфейсы, определённые с помощью абстрактных классов.

Список порождающих шаблонов:
- «Абстрактная фабрика» — Abstract factory;
- «Строитель» — Builder;
- «Фабричный метод» — Factory method;
- «Объектный пул» — Object pool;
- «Прототип» — Prototype;
- «Одиночка» — Singleton.

Паттерн «Фабричный метод» (Factory method)

Этот паттерн помогает снизить количество кода и существенно упростить его использование в программе. «Фабричный метод» — это принцип создания оболочки, которая принимает решение, какой из типов отображения показать в интерфейсе в конкретный момент времени в зависимости от полученных данных.

Представим, что у нас в проекте существует несколько компонентов, которые отвечают за отрисовку кнопок. Как это часто бывает, все эти компоненты были написаны в разное время и разными разработчиками, у каждого из которых было свое «чувство прекрасного» в плане написания кода)

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/fff2ef18-72f8-4328-981c-22b055b8accb)

Как мы видим, у каждого компонента есть свой метод, отвечающий за отрисовку разметки. Чем это неудобно? Тем, что каждый раз при использовании одного из компонентов придется вспоминать название нужного метода или «идти искать истины» в сам компонент. Трата драгоценного времени! Для решения этой проблемы мы спокойно можем применить паттерн «Фабрика».

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/7dba01e3-4d21-464d-b0fe-0c7436c960d2)

Профит: мы создали класс Fabric, который помогает получать готовый компонент, используя одинаковый интерфейс. Еще один плюс такого подхода – простота расширения, если в будущем нужно будет добавить новую разновидность кнопок, достаточно включить еще один кейс в фабричный класс.

Паттерн «Одиночка» (Singleton)

Суть: класс должен гарантированно иметь только один объект в глобальной области видимости.
«Одиночка» — лучший способ управления общими данными без использования Redux.

Например, представим, что для получения данных, нам нужно установить соединение с базой данных. Благодаря этому паттерну выполняется соединение, если оно не было установлено, или возвращается ссылка на уже установленное соединение.
Также в качестве примера можно привести счетчик, которым пользуются разные компоненты. Объявляем класс Counter (Singleton), описываем два метода: getCounter() – возвращает состояние счетчика, incCounter() – увеличивает счетчик на 1.

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/8497702a-f824-46f3-994c-49bd08778260)

С помощью данного класса можно создавать объекты в любом месте, причем все экземпляры будут ссылаться на один и тот же объект.

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/2b266c00-270e-4c9f-be48-76c34109a1ed)

Паттерн «Абстрактная фабрика» (Abstract factory)

«Абстрактная фабрика» инкапсулирует внутри себя один или несколько «Фабричных методов», каждый из которых реализует свою фабрику. Методы фабрики возвращают экземпляры прочих интерфейсов, а также инициализируются внешними компонентами. «Абстрактная фабрика» позволяет при изменении реализации одного интерфейса менять реализацию других интерфейсов.

Представим, что нам нужно отрисовать несколько карточек товара, причем некоторые из них являются новинками и их нужно отобразить с дополнительным заголовком. Для этого создадим абстрактную фабрику с 3 методами.

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/3acb1929-539e-4047-b446-96f9535bee49)

Метод factoryTitle – это фабрика, которая отвечает за создание заголовка для карточки.
Метод factoryCard – это фабрика, которая отвечает за создание карточки.
Метод create – это фабрика, которая в зависимости от передаваемого типа, вызывает методы создания заголовка или создания карточки.
Теперь давайте посмотрим, как применяется абстрактная фабрика.

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/55bcf682-beeb-407a-b336-633708cd3874)

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/3f599e4d-a27a-4298-ba22-1eca17477fcf)

Паттерн «Строитель» (Builder)

«Строитель» — это шаблон проектирования, который инкапсулирует создание объекта и позволяет разделить его на разные этапы. Он позволяет собирать объекты пошагово, вызывая только те шаги, которые вам нужны.

Представим, что нам нужно отрисовать главную страницу интернет-магазина, а также страницу каталога товара. В данный момент проходит акция, но информация о ней должна быть представлена только на главной странице.
Для начала создадим «Builder» для страниц магазина.

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/49c7c6cd-c928-41f3-872e-22e9fc2887e2)

А вот так мы будем применять его на главной странице:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/80d2eddf-46d6-40cf-87fe-aca25d98e177)

Паттерн «Объектный пул» (Object pool)

«Объектный пул» — это набор объектов, которые хранятся в состоянии полной готовности к использованию. Когда в коде нужен новый подобный объект, используется один из хранящихся в пуле. При этом новый объект, использующий динамическую память системы, не создаётся.
Паттерн особенно полезен, если ваше приложение содержит отработку множества одинаковых методов для получения одного и того же результата в разные промежутки работы. Каждый новый запрос на однотипное действие — это затрата ресурсов приложения. При большой трате ресурсов приложение может аварийно завершиться, и пользователь потеряет текущие данные.

Предположим, что нам нужно отображать на главной странице некий список преимуществ представляемых товаров. Список товаров, в качестве примера, мы будем получать с помощью фейкового метода getFeatures, суть которого будет заключаться в ассинхронном получении данных с помощью динамического импорта. Необходимый список уже хранится в моковых данных. Наша задача сымитировать его 

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/a5cfb74b-3553-4201-a7a7-fb696e0953d6)

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/98828494-0d59-4cf8-a22a-7528e1ce154d)

Паттерн «Прототип» (Prototype)

Паттерн «Прототип» позволяет создавать объекты на основе уже готового экземпляра — прототипа. Классы-наследники способны добавить новый тип на основе главного объекта. Экземпляры объекта получают программный код, который содержится в прототипе конструктора. Новые экземпляры наследуют все атрибуты и методы их собственного типа вдобавок к свойствам, которые содержит их родитель.
«Прототип» сокращает время, потраченное на разработку программных компонентов, за счёт стандартизации и использования общего шаблона для построения компонента.

Предположим, нам нужно создать каталог с карточками товара. Чтобы все карточки получились единообразными можем воспользоваться паттерном Прототип, чтобы задать единую структуру.

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/22cf244b-6676-41c2-bde7-fb00d1a75e4a)

«Прототип» — это макет с определённой структурой. Основная цель его создания — черновая реализация компонента, которая позволяет избежать повторной разработки базовых механизмов компонента.
Паттерн используют, когда нужно задать общую базовую структуру для компонента, которую в последствии можно удобно и быстро изменить, редактируя только код в «Прототипе».


Структурные паттерны

Структурные шаблоны направлены на решение проблем при создании более крупных структур из классов и объектов.
Структурные паттерны помогают совместить сущности для корректного взаимодействия. Их главная задача — составить программный компонент, который сможет без дополнительных изменений взаимодействовать с другими компонентами и работать внутри разных программных систем.
Какие проблемы решают структурные паттерны:
- Позволяют использовать несколько библиотек в одной программе и обеспечивают их взаимодействие.
- Помогают регулировать формат данных внутри программы, чтобы его можно было использовать внутри всей системы.
- Позволяют взаимодействовать объектам с разными интерфейсами. Паттерны внедряются в классы и, не меняя их, помогают им взаимодействовать с другими объектами.

Список структурных шаблонов проектирования:
- «Адаптер» — Adapter;
- «Мост» — Bridge;
- «Компоновщик» — Composite;
- «Декоратор» — Decorator;
- «Фасад» — Facade;
- «Заместитель» — Proxy.

«Адаптер»

Паттерн «Адаптер» помогает изменить данные, которые возвращает один объект, чтобы их мог использовать другой. Он создаёт «оболочку», с помощью которой объекты с разными несовместимыми интерфейсами могут взаимодействовать друг с другом.
Какие проблемы решает «Адаптер»:
- Делает несколько независимых программных компонентов совместимыми, чтобы их можно было использовать в одной программе.
- Адаптирует формат данных для определённого интерфейса. Благодаря этому интерфейс работает корректно.
- 
Предположим, что у нас есть сервис по продаже подержанных автомобилей, который использует JSON-файл для отрисовки интерфейса. Однако на сервере произошла ошибка, и некоторые элементы стали приходить в другом формате, а именно названия полей стали приходить в верхнем регистре. 

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/4c34957b-e837-4710-80af-2773afcb20d2)

Применение

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/0c3bae54-15f3-4661-a647-04bff7013d40)

«Мост»

Паттерн «Мост» отвечает за разделение на независимые друг от друга блоки абстракции и реализации. Здесь используется инкапсуляция и агрегирование. Также можно использовать наследование, чтобы распределить ответственность среди классов. «Мост» позволяет параллельным иерархиям развиваться самостоятельно. При этом связь между ними сохраняется.
Какую проблему решает «Мост»:
«Мост» помогает, когда в проекте объекты зависят от определённой реализации. Без паттерна такие объекты сложно переиспользовать.

Предположим, нам нужно реализовать механизм, который отвечает за цветовое оформление страницы. Переключение должно происходить по клику на кнопку «Изменить тему». Должно быть две темы: тёмная и светлая.
Для начала создаем абстрактный класс

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/ca885e08-0681-461e-8a07-6724dec1d2a4)

Затем создаем класс 

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/8e4f5d2c-e300-48f5-aa25-4602951c1dd4)

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/07bacb6a-5f79-4e7d-9134-0424b1b69258)

«Декоратор»

Паттерн расширяет возможности объектов за счёт того, что оборачивает эти объекты в обёртки с дополнительной функциональностью.
Что делает паттерн: «Декоратор» динамически дополняет объект новым поведением. Этот паттерн — альтернатива созданию подклассов для расширения функциональности.

Примером паттерна «Декоратор» может служить ситуация, когда нам нужно закэшировать данные.
Функция декоратора

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/b3a56066-b150-4135-a347-7b2b0da87b95)

Мы создали «Декоратор», который принимает решение в динамике. Он либо выполняет AJAX-запрос к JSON, требующий значительных ресурсов приложения, или обращается к локальному хранилищу, которое предварительно может содержать записанные данные.
Каждый запрос к серверу — ресурсоёмкая операция. «Декоратор» позволяет избежать лишних запросов и повышает эффективность приложения, его скорость и корректность работы.

«Фасад»

Паттерн создаёт объект, который содержит определённый набор операций для работы со сложной системой. «Фасад» упрощает работу методов внутри подсистемы.
«Фасад» скрывает сложные участки кода в отдельные методы или классы, чтобы упростить работу с ними. При этом вы можете использовать их повторно, не занимаясь настройкой библиотеки заново.
В каких ситуациях нужен паттерн: «Фасад» используют, когда нужно работать с большим числом объектов сложной библиотеки или фреймворка. Без паттерна разработчикам приходится создавать эти объекты и следить за порядком всех зависимостей в программе. В результате бизнес-логика классов смешивается с деталями реализации внешних классов. Код становится сложно поддерживать и расширять.
Какую проблему решает паттерн: «Фасад» упрощает работу со сложными структурами, инкапсулируя их некоторые логические блоки кода в отдельные методы. 

Предположим, что нам потребовалось выполнять еще один запрос на получение данных, но на другой сервер. При этом настройки запроса должны остаться одинаковыми. Можно воспользоваться паттерном «Фасад» и инкапсулировать базовую настройку работы объекта XMLHttpRequest в отдельный объект, чтобы можно было его использовать в дальнейшем для новых запросов.

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/62d8f0c8-cf13-42d9-b633-3d98adb5f8ed)

Мы убрали все подробности о XMLHttpRequest, который используем для запроса к серверу, а все настройки этого механизма вынесли в параметры функции.

«Компоновщик»

«Компоновщик» объединяет объекты в структуру древовидного типа — от частного к целому. Он позволяет одинаково обращаться как к каждому объекту отдельно, так и к группе объектов.
Паттерн используют, когда главная модель программы имеет структуру в виде дерева.
Что делает паттерн: объекты, созданные на основе паттерна, группируют внутри себя похожие по функциональности объекты, к которым можно обращаться через интерфейс «Компоновщика». Например, можно одновременно удалить несколько объектов.
Какую проблему решает паттерн: паттерн оптимизирует работу программы и экономит её ресурсы. Он позволяет выполнять меньше операций благодаря общему интерфейсу «Компоновщика».

Примером реализации паттерна может служить фича, когда можно выбрать как конкретный товар с помощью чекбокса, так и кнопка, по нажатию которой будут выбраны все товары.

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/2d99af1e-1931-4795-88e8-f58415ca95c9)

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/16e9fef4-314b-4e7a-abc7-aa27dc74e0c5)

«Прокси» или "Заместитель"

Паттерн «Заместитель» (его ещё называют «Прокси») представляет собой объект, контролирующий доступы другого объекта — происходит перехват всех вызовов.
Что делает паттерн
- Оборачивает метод и получает контроль над его выполнением.
- Может влиять на результаты выполнения метода, анализируя их и определяя дальнейшие действия.
В первую очередь «Прокси» необходим, когда у разработчика нет доступа к модификации сторонней программы, и в это же время для её работы требуются дополнительные методы. Ещё паттерн пригодится, когда нужно дополнить ответ от сторонних сервисов для корректной работы программы.

В качестве примера можно реализовать фичу ограничения доступа пользователя к сервису на определенный период времени.

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/d8fa62ad-e987-47be-ad80-d88d2ce7298e)

Паттерн «Прокси» способен динамически изменить поведение алгоритма в зависимости от определённых, чётко установленных условий. В нашем примере это условие — промежуток времени больше пяти утра и меньше девяти часов вечера. Если условие не соблюдалось, «Прокси» блокировал вывод данных.

Поведенческие шаблоны

Поведенческие шаблоны определяют алгоритмы и способы реализации взаимодействия разных структур, объектов и классов.
Поведенческие паттерны строят связи и распределяют обязанности между объектами и компонентами для их корректного взаимодействия внутри программы.

Список поведенческих шаблонов:
-	«Цепочка обязанностей» — Chain of Responsibility;
-	«Команда» — Command;
-	«Итератор» — Iterator;
-	«Посредник» — Mediator;
-	«Хранитель» — Memento;
-	«Наблюдатель» — Observer;
-	«Посетитель» — Visitor;
-	«Стратегия» — Strategy;
-	«Состояние» — State;
-	«Шаблонный метод» — Template Method.
Они в первую очередь направлены на решение конфликтов при взаимодействии независимых объектов программы.

«Цепочка обязанностей»

«Цепочка обязанностей» позволяет исключить жёсткую привязку между отправителем запроса и его получателем. Обработчики запроса создают цепочку, по которой перемещается запрос.
Паттерн используют для отправки объектам запросов, когда неизвестно, выполнение какой операции запрошено и кто является получателем.
Паттерн позволяет передавать запросы поочерёдно по цепочке, от одного обработчика к другому. Каждый обработчик самостоятельно принимает решение, нужно ли ему самому обработать запрос или передать следующему.
Какую проблему решает паттерн: паттерн помогает программе, когда обработчик не может справиться с поставленной задачей — передать запрос следующему обработчику вместо возврата неудачно отработанного запроса. Таким образом, повышается стабильность работы системы в целом.

Предположим, у нас есть три счета (A, B, C) с разными суммами и разным приоритетом использования. Сначала проверяется A, если на нем достаточно денег для покупки, то цепочка прерывается. Иначе проверяется B, затем C. Цепь будет продолжаться, пока не найдет подходящий обработчик.
Вот ваша учетная запись, которая реализует логику связи счетов:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/50b675ee-a8a8-4e45-aa5f-dfbc653790f9)
![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/1db7b67b-184c-4797-926c-5d47cd26ef01)

Теперь составим цепочку:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/76ce5a8b-3a92-4509-8efb-45d02cc94a7a)

«Команда»

Паттерн «Команда» позволяет инкапсулировать запрос определённого действия внутри отдельного объекта. Объект, который внутри своего действия вызывает определённый метод, и называется «Командой». Объекты, которые инициируют запросы на исполнение действия, разделяются с объектами, выполняющими это действие.
Паттерн используют, когда нужно реализовать алгоритм, созданный на основе отдельных частей, взаимозаменяемых и независимых друг от друга.
Что делает паттерн: «Команда» преобразует запросы в отдельные объекты, позволяя передавать их в качестве аргумента, составлять очередь запросов, логировать их и отменять операции.
Какую проблему решает паттерн: паттерн позволяет настроить класс при помощи объекта «Команды», который применяется для исполнения запроса. Классы не завязываются на конкретные запросы и не зависят от них.

Например, Вы приходите в ресторан и делаете заказ официанту. Он перенаправляет вашу Команду шеф-повару, который знает, что и как готовить. 
Паттерн Команда инкапсулирует некоторые действия и необходимые для них данные и позволяет отделить Клиента от Получателя.
Это Получатель, который умеет совершать различные действия:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/f3e48df7-75a2-460a-9d91-91df59c2a9a8)

А вот набор команд:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/c5c8be85-cafd-4485-b7da-c94b7b777a01)

Это код Вызывающего (официанта из примера):

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/4371b1d4-93a0-4e84-b668-02ca798ce98d)

А вот пример использования:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/943fc3c3-036c-4209-9e1f-eca960db6826)

«Итератор»

«Итератор» представляет собой объект, который может получить поочерёдный доступ ко всем дочерним объектам, не используя описания для них.
Паттерн используют, когда нужно реализовать общий подход для обработки нескольких массивов информации.
Что делает паттерн: «Итератор» инкапсулирует внутри себя алгоритм обхода данных с единым интерфейсом для перечисления. Алгоритм перебора скрыт внутри «Итератора» и это позволяет объекту данных иметь много «Итераторов», которые реализуют разные алгоритмические подходы. Проще говоря, «Итератор» предоставляет метод next() в коде, который возвращает последующий элемент из массива.
Какую проблему решает паттерн: паттерн «Итератор» позволяет перебирать объекты с применением установленных правил.

Представим, что у музыкальных плееров есть кнопки next и previous, которые позволяют последовательно перебирать песни или радиостанции.
Паттерн Итератор предоставляет доступ к элементам объекта, не раскрывая способ их внутреннего представления.
Радиостанция:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/0267ccb4-28b3-492c-86ca-4849db0c119a)

Итератор:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/a0d22c83-2852-42fa-bd8b-7c92eef56879)

Можно добавлять и удалять станции, а также получать их частоту:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/15a0bdad-f327-4e95-99ea-545e0e2d3f24)

«Посредник»

Паттерн «Посредник» обеспечивает взаимосвязь нескольких объектов без использования взаимных ссылок друг на друга. Достигается слабосвязанность во взаимодействии объектов.
«Посредник» используют, когда в коде множество сложно связанных друг с другом объектов. Повторное использование таких объектов затрудняется из-за сильных взаимосвязей с иными объектами.
Что делает паттерн: Паттерн вводит «посредника» для развязывания множества взаимодействующих объектов.
Какую проблему решает паттерн: Паттерн «Посредник» избавляет объекты от необходимости ссылаться друг на друга, что делает систему более слабосвязанной.

Давайте создадим простой чат, в котором пользователи (Коллеги) могут отправлять сообщения друг другу.
Чат выглядит так:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/254012a3-58b4-4eac-b622-3ebb1f980277)

А это сами пользователи:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/add37644-a4e7-4d2a-8c4b-513aa6cc29bc)

Начнем беседу:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/530287b2-12f7-49c2-8c9f-d90ade65d3a4)

«Хранитель»

«Хранитель», известный также как «Снимок» — это паттерн проектирования, который помогает определять, сохранять и восстанавливать прежние состояния объектов, не нарушая принцип инкапсуляции.
Паттерн используют, когда необходимо сохранить исходное состояние объекта для последующего восстановления. Прямой интерфейс получения состояния объекта открывает подробности реализации объекта и ухудшает его инкапсуляцию.
Что делает паттерн: «Хранитель» сохраняет состояние объекта и запрещает доступ к изменению и просмотру информации всем другим объектам, за исключением хозяина.
Какую проблему решает паттерн: паттерн помогает сохранять и восстанавливать внутреннее состояние объекта, при этом сохраняя инкапсуляцию.

Создадим текстовый редактор с функцией сохранения контента.

Объект Хранителя:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/1408fb08-b908-48f3-87ea-243be6e3bb62)

Сам редактор:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/cd6a8e73-58ac-45f7-ba96-b1fcfe84399c)

Теперь смело можете писать курсовую, все данные сохранятся!

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/56583d0e-3e52-404b-aed6-e914ae92cf44)

«Наблюдатель»

Паттерн «Наблюдатель» использует стратегию взаимодействия «один ко многим». В таком взаимодействии присутствует один наблюдаемый объект и несколько наблюдателей. Если наблюдаемый объект меняется, наблюдатели автоматически реагируют на это.
Паттерн используют чтобы отследить изменение формы или состояния объекта и активировать определённый обработчик.
Что делает паттерн: Паттерн предлагает располагать внутри наблюдаемого объекта коллекцию ссылок на объекты подписчиков. Объект предоставляет методы, благодаря которым другие объекты могут добавлять или убирать ссылку на себя из наблюдаемого объекта.
Какие проблемы решает паттерн: Он помогает при снижении производительности у более простых подходов (активное ожидание или периодический опрос).

Представим, что соискатели хотят получать уведомления:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/7abef217-aaf8-4b6c-97c3-bea38282c641)

А Доска объявлений может эти уведомления рассылать:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/b23cf702-0210-4d8e-ac71-c21375eaa5cc)

Подпишемся на рассылку:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/0fa0d3f3-7844-4c37-8d1b-3d497de595e0)

«Посетитель»

«Посетитель» описывает операцию, которая выполняется над объектами разных классов. Изменяя паттерн, не нужно менять классы, которые он обслуживает.
«Посетитель» используют, когда нет возможности изменить метод внутри объекта или класса.
Что делает паттерн: Паттерн используют для расширения возможностей объектов. Он позволяет дополнять объекты различными дополнительными операциями, не требуя изменения их исходного кода.
Какие проблемы решает паттерн: «Посетитель» помогает изменить поведение объекта, при этом не затрагивая его код. Это снижает риск нарушения работы программы при её изменении.

В качестве примера смоделируем зоопарк с разными видами животных:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/03e1e9b3-586d-446c-9bc5-e9bded16f098)

Теперь мы хотим послушать, какие звуки они издают. Для этого создадим Посетителя:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/d5427ad4-ed9e-445c-9996-c325f72bb8b6)

Он просто обращается к каждому классу и вызывает нужный метод:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/0a305651-3cd9-4a6d-bdde-66777d3c8376)

Посетитель позволяет не изменять существующие объекты. С его помощью можно, например, добавить всем этим животным возможность прыгать без создания дополнительных методов.

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/4ecca572-02fb-4c08-bf39-516ce9d3c098)

Вуаля:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/94a4555c-7598-4268-a14f-3ac38d164135)

«Стратегия»

«Стратегия» используется для семейства алгоритмов, инкапсуляции каждого из них, а также обеспечения их взаимозаменяемости. Паттерн необходим для управления поведением определённых классов.
Что делает паттерн: Основная задача «Стратегии» — выделить похожие алгоритмы, решающие определённую задачу.
Какие проблемы решает паттерн: Паттерн «Стратегия» позволяет отказаться от работы с переключателями или условными операторами, а также стандартизировать вызов методов с использованием единого интерфейса.

Воплотить Стратегию в JavaScript помогут функции первого класса.

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/0bcdb9fc-066b-469b-94fb-532d6444b22c)

А это клиент, который может использовать любую стратегию:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/dfee1b2e-fce0-48f6-b137-f315319adda9)

Теперь можно сортировать массивы:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/f3e66c33-8a85-44d8-8d8b-09e5137454e3)

«Состояние»

Паттерн «Состояние» позволяет объектам регулировать своё поведение, исходя из внутреннего состояния.
Паттерн используют, когда во время исполнения программы объекту нужно изменить логику поведения, исходя из своего состояния.
Что делает паттерн: паттерн создаёт зависимость между состоянием и поведением объекта в программе.
Какие проблемы решает паттерн: паттерн «Состояние» помогает автоматически менять форму при изменении данных в программе.

В качестве примера создадим текстовый редактор, в котором можно менять состояние текста – жирный, курсив и т. д.
Это функции преобразования:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/c8b86e1d-724a-4ca0-b532-5f8acbab889b)

А вот и сам редактор:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/57831b6f-00f7-4f6a-ac26-1039d6407b68)

Можно работать:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/726879e1-9ae0-4045-95f3-a1733a989613)

«Шаблонный метод»

Паттерн «Шаблонный метод» определяет основу алгоритма, а также позволяет наследникам корректировать некоторые шаги внутри алгоритма, не затрагивая его структуру.
Паттерн используют, когда в классах с похожим алгоритмом есть дублирование кода.
Что делает паттерн: «Шаблонный метод» задаёт основу алгоритма внутри метода, при этом оставляя определение основной реализации нескольких шагов своим подклассам.

Какие проблемы решает паттерн: паттерн помогает избавиться от дублирования кода, который остаётся неизменным для подклассов.

В качестве примера создадим инструмент для тестирования, сборки и разворачивания приложения.
Базовый класс определяет скелет алгоритма сборки:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/3f1867e5-9b1e-41a4-96bc-add1dc115d10)

А дочерние классы – конкретную реализацию каждого шага:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/4748211c-9c9f-48da-94b7-fdaf0a083bea)
![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/5b40f43a-27b5-4603-8a3c-4c6778187df8)

Соберем проект:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/fdd5ced7-a8ed-4f1d-a09b-1e9dc8cbfe71)

MV-паттерны для проектирования веб-приложений

MVC

Шаблон MVC (Модель-Вид-Контроллер или Модель-Состояние-Поведение) описывает простой способ построения структуры приложения, целью которого является отделение бизнес-логики от пользовательского интерфейса. В результате, приложение легче масштабируется, тестируется, сопровождается и конечно же реализуется.

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/c68c988d-2099-47f4-b901-77847dcec5db)

1. При заходе пользователя на веб-ресурс, скрипт инициализации создает экземпляр приложения и запускает его на выполнение.
2. Выполняется действие index фронт-контроллера, которое генерирует представление главной страницы.
3. Представление отображается пользователю.
Первые три шага — это простая цепочка, без использования модели. Далее идет последовательность, где задействована модель:
4. После того, как приложение получит запрос от пользователя, создается экземпляр запрошенного контроллера и вызывается указанное действие.
5. В этом действии вызываются методы модели, изменяющие ее.
6. Генерируется представление (или же представление оповещается об обновлении модели).
7. Представление запрашивает данные для отображения.
8. Модель возвращает запрошенные данные.
9. Представление отображает результаты пользователю.

Встречается и такая схема — схема 2:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/18cdd377-31c1-4eba-914c-ef1a19aa2305)

1. Контроллера получает следующий запрос от пользователя.
2. Далее в зависимости от внутренней логики:
      2a. Формируется представление какой-то страницы.
      2b. Либо, вызываются методы модели.
3. Модель уведомляет представление об изменениях.
4. Представление обновляется (если в цепочке была задействована модель) и отображается пользователю.

На некоторых схемах можно увидеть стрелку от представления к контроллеру. Рассмотрим этот случай — схема 3:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/2e59a8cd-abcc-4485-a08b-94b624571d3e)

1.	Приложение получает еще один запрос от пользователя: создает экземпляр запрашиваемого контроллера и вызывает указанное действие.
2.	В действии генерируется представление содержащее некоторую форму ввода данных.
3.	Представление с формой отображается пользователю.
4.	После того как пользователь заполнит форму и нажмет на кнопку «Submit» вызывается тот же контроллер, который проверяет и обрабатывает полученные из формы данные и формирует другое представление или же обновляет текущее.

Шаг 4, по сути, эквивалентен еще одному шагу 1, инициализирующему новый цикл… Поэтому на всех схемах можно предполагать неявную связь в направлении от вида к контроллеру.

MVP

А теперь посмотрим на схему паттерна MVP (Model-View-Presenter) — схема 4:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/69c64bbf-158b-4df0-a536-29be816fcdd3)

1.	После того, как приложение получит запрос от пользователя, определяется запрошенный Presenter и действие. Приложение создает экземпляр этого Presenter'а и запускает метод действия.
2.	В методе действия могут содержаться вызовы модели, к примеру, считывающие информацию из базы данных.
3.	Модель возвращает данные.
4.	После этого действие формирует представление, в которое передаются данные полученные из модели.
5.	Сформированное представление отображается пользователю.

Помимо MVP существуют и другие, производные от MVC, паттерны, например MVVM и HMVC.

HMVC

Реализация паттерна HMVC (Hierarchical Model View Controller — Иерарархические Модель-Контроллер-Вид) используется в веб-фреймворке Kohana. Рассмотрим в чем же ключевое отличие от MVC — схема 5:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/ba1a454e-6702-455e-a378-1aac2f44a7d7)

Приложение представляет иерархию независимых друг от друга MVC триад. При этом, каждая триада может напрямую обратиться к контроллеру другой триады. Такой подход позволяет решить некоторые проблемы масштабируемости приложений, имеющих классическую MVC-архитектуру, уменьшить зависимость между различными частями приложения, облегчить дальнейшую поддержку и повторное использование кода. 

MVVM

MVC прижился в веб-приложениях во многом потому, что он отлично справляется со сценарием запрос-ответ. Основная черта такого сценария — короткое время жизни View. Приходит запрос, который передается на соответствующий контроллер, он инициирует какие-то процессы в модели, а затем создается View, который просто заполняется данными из модели и передается клиенту в браузер. Все в один проход.
Когда появился Ajax и богатые клиент-сайд приложения (RIA), оказалось, что MVC не очень хорошо подходит для работы с областями страницы или приложения, что привело к несколько иным моделям: MVP (Model View Presenter) и затем к MVVM (Model View ViewModel). Если c паттернами MVC и MVP большинство более-менее знакомо, то о последнем слышали очень немногие.
Первоначально MVVM был описан для Silverlight и имеет преимущества для сложных интерфейсов с определенной логикой, которая отличается от логики приложения. MVVM отличается более «тесной» связью между Моделью и Представлением посредством слоя Представление-Модель, который синхронизирует данные как при событии на стороне Модели, так и на стороне Представления.
В MVC логика зашита в Модели, ее можно также помещать в Контроллер, но это справедливо подвергается критике (Stupid Fat Controller). В MVVM, напротив, логика помещается в «промежуточный» слой ViewModel. Рассмотрим схему MVVM — схема 6:

![image](https://github.com/MariyaKustova/MariyaKustova-Design-Patterns/assets/58948550/a59f1455-152a-4b7d-a268-d19d99b69091)

Вы определяете видимую область экрана и задаете самые общие данные о нем, не зная, какое содержание будет показываться во время выполнения. Для HTML схема MVVM особо удачна благодаря DOM, который, как известно, вполне может вмещать данные. Поэтому MVVM была успешна реализована во фреймворке KnockOut.JS. Изначально все просто. Есть Модель данных, предоставленная сервером. Есть Представление в виде DOM, в виде разметки. А есть Представление-Модель (Вид Модели, если хотите), которая описывает изменение Представления, связывает Модель и Представление, причем синхронизует эту связь.
Стоит отметить, что MVC часто трактуют просто как разделение трех уровней приложения, и никак не регламентируют связи между ними. Поэтому, довольно часто, встречаются диаграммы (выше была приведена одна из таких), на которых Модель и Представление связаны стрелками, хотя очевидно, что таким образом теряются полезные свойства масштабируемости при использовании разных Представлений и иерархичность Контроллеров.
