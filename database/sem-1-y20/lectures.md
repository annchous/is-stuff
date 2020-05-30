## Лекция от 19.10.16
**Иерархические формы хранения** – это ограниченный подтип сетевой модели. В ней данные как коллекция записи, а связи как наборы. Особенность - каждый узел может иметь только 1 родителя, т.е. иерархическая модель-древовидный граф, записи – узлы графа(сегменты), от каждой записи несколько ребер.

**Исходный сегмент** – некоторый сегмент в дереве по отношению к непосредственно ниже лежащему.
**Зависимый сегмент** – сегмент к которому существует путь от некоторого исходного по цепочке пар: исходной - непосредственно порожденной.
**Корневой сегмент** – сегмент не имеющий исходного.
**Запись** в такой конструкции БД – это любой экземпляр корневого сегмента и все зависимые от него сегменты.
Основной **метод доступа к записи** – индексно-последовательный. Имеется иерархия индексов, каждый пункт индекса содержит физический адрес начала подчиненных ему группы данных и ключ последнего экземпляра сегмента в этой группы.
При использовании сетевых или иерархических моделей требуется знание физической организации БД, при работе с реляционной моделью обеспечивается независимость от данных
### Предикатные формы хранения данных
Информацию, представленную в таблице можно эквивалентно отобразить в предикатной форме.
**Предикат**     (пропозициональная функция) – функция $p(i)$ которая отображает упорядоченный набор конечного числа n-независимых переменных в множество истинностных значений, при этом каждый x принадлежит своей области определения.
Содержательно это определение означает – данная сущность предметной области описывается таким то набором переменных $(x_1, x_2, \cdots)$ и они имеют значения (0 или 1 / false или true), М-домены реляционной БД и информации о структуре реляционных таблиц можно выразить введением предикатных символов branch (branch №, City, …), информация о содержимом таблиц выделяется применением этих предикатных символов к тем конкретным наборам аргументов, на которых значение предикатов будут true:
- $P(B005, London) = true$
- $P(B005, Moscow) = false$

На первых взгляд предикатная форма идентична табличной, однако математическое обоснование для предикатной формы – это не алгебра, а исчисление предикатов.
### Рекурсивная форма хранения данных
**Экстенсионал** - явное перечисления фактов, относящихся к понятию.
**Интенсионал** – описание понятия через другое, более высокого уровня или через механизм его формирования. Все предыдущие поля – экстенсиональные.
Многие типы связи, используемые в БД, по смыслу предполагают вложенность, н-р связь является начальником по отношению к предыдущему. Такого типа связи отношения род-вид, часть-целое или другие отношения старшинства, в общем это называется **отношение частичного порядка**. такого типа можно описать с помощью рекурсии, любую связь можно определить, как рекурсивную с различной глубиной вложенности, в частности с глубиной = 1, тогда рекурсивная форма хранения становится вполне общей.
### Модель данных
Для описания одной предметной области может быть предложено много способов, которые объединяются понятием «модели данных».
Обобщенное определение: **модель данных** – интегрированный набор понятий для описания и обработки данных, связей между ними и ограничений на данные в некоторой предметной области.
**Модель данных** – система типов данных, типов связей между ними и допустимых видов ограничений целостности
$$DM = <D, R, A>$$
D - заданное множество, которое называется «носитель структуры»
R – конечный набор отношений, в которых находятся элементы множества (типовая характеристика структуры)
А – ограничение, накладываемое на отношение (аксиомы структуры)

Аксиомы могут пониматься расширительно, т.е. включать в себя и правила вывода новых формул.
Однако в любой модели данных имеются моделе-независимые понятия:
- **Элемент данных** – понимается аналогично программированию как элемент базового или абстрактно типа данных.
- **Запись** – минимальная, уникально идентифицируемая единица независимого хранения данных.
- **Схема записи** – описание внутренней структуры записи на языке, используемом в конкретной БД, каждая запись должна быть объявлена вместе со своей схемой.
- **Поле записи** – позиция в структуре хранения записей.
- **Ключ** – одно или более полей записи, объявленные для ее уникальной идентификации.

### Модели архитектуры БД, понятие о СУБД
**Многоуровневая архитектура БД** – 2 уровневая схема: схема + набор подсхем.
**Подсхемы** - пользовательские преставления, т.е. часть БД, которое отдается пользователю или приложению
3 уровневый подход:
- **Внешний** - это представление БД с точки зрения пользователей. View - каждому пользователю предоставляются те сущности атрибута и связи реального мира, которые соответствуют его месту в бизнес модели. Внутри разных view могут по-разному отображаться одни и те же данные.
- **Концептуальный** - это полное представление требований к данным со стороны организации, которая не зависит от любых соображений относительно способа хранения. На концептуальном уровне представлены следующие компоненты:
  - все сущности
  - их атрибуты и связи
  - накладываемые на данные ограничения
  - семантическая информация о данных
  - информация о мере обеспечения безопасности и поддержке целостности данных)
- Внутренний – физическое представление базы в сети. Входит распределение дискового пространства для хранения данных и индексов, описание подробностей сохранения записей с указанием реальных размеров хранимых элементов, сведения о размещении записей, сведения о сжатии данных и выбранных методах шифрования.
- Ниже внутреннего уровня находится физический уровень, который частично контролируется СУБД, а частично ОС.

**СУБД** – ПО, которое взаимодействует с прикладными программами пользователей и БД, с помощью которого пользователи могут определять, создавать и поддерживать БД, а также осуществлять к ней контролируемый доступ.

## Лекция 2 (от 02.11.16)
### Нормализация реляционной БД. Теоретика множества написания отношений, характеристика функций.
Критерий может быть задан по умолчанию
$$R = R(D1, D2, ..., Dn) di D = {Di}$$
Отношение R на D называется декартовым произведением, где в каждом из кортежей d каждый элемент di является компонентом D.
Множество D – домен отношения, подмножество доменов отношений, выделение заданием d* называет атрибутами отношений. В этих определениях отношение R можно изобразить как табличную форму.
**Атрибут-отношения** - это выделенное определением отношение подмножества некоторых членов семейства доменов отношения, при этом каждый атрибут отношения однозначно характеризуется позицией в перечне аргументных мест и критерием принадлежности их значений к определённому кортежу отношения.
**Атрибут реляционной таблицы** – это атрибут отношения, представленный данным в реляционной таблице, при этом каждый атрибут отношения характеризуется:
- Локализованным в реляционной таблице уникальным именем.
- Однозначно ассоциированным с ним доменом БД, который в общем случае является абстрактным видом данных.
- Ассоциированным с ним набором условии целостности БД, относящихся к этому атрибуту.

Условие целостности в реляционной таблице в базе данных – это особые отдельно хранящиеся данные, которыми на концептуальном уровне обычно в табличной или предикатной форме представлен критерий принадлежности кортежей к отношению, представленными этими данными, а так же спецификации условий принадлежности значений каждого атрибута к соответствующему домену. 
Из этих определений видна разница между понятием «отношение» и «реляционная таблица». Отношение - это информация, а таблица – данные, которыми эта информация представлена.
Различия:
- Множество кортежей отношения может быть бесконечным, в том числе континуально бесконечным. Множество может быть счетным (можно соотнести с рациональными числами) и континуальными (можно отнести с действительными числами). В то время как количество строк в реляционной таблице всегда конечно. Однако в практике работы БД и литературе часто реляционные таблице синонимичны отношениям.
- Табличную форму отношений можно эквивалентно представить в виде функции. F(x1, x2, …, xn) = {1(true) на каждом наборе значений или строках таблицы или 0(false) в других случаях}. F- характеристическая функция отношения. При этом если множество значений функции задается как 0, 1, то F это функция, а если как true или false, то F - предикат.
### Характеристики функциональных зависимостей.
Функциональная зависимость является смысловым (семантическим) свойством атрибутов отношения.
Пусть R является переменной отношения, а X и Y это произвольные подмножества из множества атрибутов переменной отношения R. Тогда Y функционально зависимо от X, если для любого допустимого значения переменной отношения R при совпадении двух кортежей по X они так же совпадают по Y. Подмножество Х называется детерминантом а Y называется зависимой частью.
**Функциональная зависимость** называется тривиальной если ее зависимая часть является подмножеством ее детерминанта.
Содержательно функциональная зависимость называется тривиальной если она справедлива при любых условиях.
A -> B (A – детерминант, В – зависимая часть)
**Функциональная зависимость** называется свойством реляционной схемы, а не свойством конкретного экземпляра схемы. Функциональна зависимость в математике и БД - это разные вещи.
- Функциональная зависимость в математике – тройка Х, Y F. Х – это область определения, Y – множество значение, F – правило, согласно которому каждому элементу из Х ставится в соответствие одно значение Y.
- Функциональная зависимость атрибутов отношения:
    - Х – это домен, на котором определен атрибут Х (может быть 1 домен, может быть декартово произведение)
	- Y – домен, на котором определены значения, F по данному значению атрибута Х найти любой кортеж отношения содержащий это значение, при это сохраняется в том смысле, что найденные значение Y не зависят от выбора кортежа.

В отношениях значения зависимого атрибута может быть в разных состояниях БД. На области определения
Функциональные зависимости в БД связаны с различными состояниями этой базы, следовательно, зависимые значения могут меняться непредсказуемо.

В процессе проектирования необходимо рассматривать только те функциональные зависимости, которые распространяются на множество всех возможных значений атрибутов и исключать все тривиальные зависимости
В процессе нормализации должны учитываться следующие основные характеристики функциональных зависимостей:
1. Определяющая связь 1:1 между атрибутами в левой и правой части зависимости.
2. Остается справедливыми при любых условиях.
3. Являются нетривиальными.

### Аксиомы Армстронга. Минимальное множество функциональных зависимостей
Полный набор функциональных зависимостей для некоторых отношений оказывается избыточно большим, хочется сократить это набор до приемлемого уровня. Основ сокращения является то, что некоторые функциональные зависимости можно вывести из других.
Множество всех функциональных зависимостей, которые могут быть выведены из заданного множества функциональных зависимостей Х называется **замыканием Х** и обозначается **Х\***. Замыкание определяет те объекты, внутри которых работает данная математическая теория. Для вычисления Х* из Х используется набор правил вывода, который называется **аксиомами Армстронга**:
1. Рефлексивность – если Р – подмножество А то существует такой переход: Р->A.
2. Дополнение $A \to B 	\implies (A,C) \to (B,C)$
3. Транзитивность 
4. Самоопределение $A \to A$
5. Декомпозиция $A \to (B,C) \implies A \to B, A \to C$. Повторное применение этого правила позволяет разложить функциональную зависимость на ряд более более простых
6. Объединение – можно объединить ряд зависимостей в 1 более сложную функциональную зависимость $A \to B, A \to C \implies A \to (B,C)$
7. Для получения еще одной актуальной зависимости можно объединять ряд неперекрывающихся зависимостей $A \to B, C \to D \implies (A,C) \to (B,D)$

Для заданного набора функциональных зависимостей F и любого множества атрибутов А,можно определить А*, которая функционально определяются из А на основе F, тогда множество А* называется замыканием А в соответствие с F. 
Множество функциональных зависимостей Y покрывается множество функциональных зависимостей X, если каждая функциональная зависимость из Y присутствует каждом замыкании X*.
Множество функциональных зависимостей Х является минимальным, если оно удовлетворяет следующим условиям:
- Каждая зависимость в Х имеет единственный атрибут в правой части.
- Ни одну зависимость вида $A \to B$ нельзя заменить на зависимость $C \to B$, где C – собственное подмножество А, и получить в результате множество зависимостей эквивалентное Х.
- Из множества Х нельзя удалить ни оной зависимости и получить в результате множество зависимостей, эквивалентное Х, это значит исключает зависимости, которые могут быть выведены из остальных функциональны зависимостей множества Х.

**Минимальное покрытие множества функциональных зависимостей Х** – это минимальное множество функциональных зависимостей, эквивалентное Х. Может существовать несколько различных минимальных покрытий для множества функциональных зависимостей	
Свойства:
- каждое из этих аксиом обосновывается из определения функциональной зависимости
- набор является полным
- набор является непротиворечивым

### Процесс нормализации

**Нормализация** – формальный метод анализа отношений, на основе из первичного ключа или потенциальных ключей и существующих функциональных зависимостей. Она осуществляется чаще всего в виде нескольких последовательно выполняемых этапов, каждый из которых соответствует определённой **нормальной форме** (НФ), при этом исходное отношения делятся на более мелкие, а также могут возникнуть таблицы-связки.
В ходе нормализации формат отношений становится всё менее восприимчивым к аномалия обновлений. Минимально необходимыми является выполнение только 1НФ, все остальные формы могут использоваться по желанию проектировщиков. Подавляющее большинство аномалий покрываются нормализацией до 3НФ. Именно 3НФ – форма которая почти прямо получается и модели логической структуры базы.
**0НФ**(ненормализованная форма, нулевая) – таблица, содержащая 1 или несколько повторяющихся групп данных.
**1НФ** – отношение, в котором на пересечении каждой строки и каждого столбца содержится 1 значение. Как правило таблица заполняемая менеджером находится в 0НФ. Для преобразование из 0НФ в 1НФ нужно найти и устранить все повторяющиеся группы данных. Повторяющаяся группа - группа, состоящая из 1 или нескольких атрибутов таблицы, в которой возможно несколько значений для единственного значения ключевого атрибута.
2 подхода исключения:
- флетеннинг(выравнивание таблицы) – состоит в том, что пустые места заполняются дубликатами неповторяющихся данных.
- 1 атрибут или группа атрибутов назначаются ключом ненормализованной таблицы, затем повторяющиеся группы изымаются и помещаются в отдельные таблицы, вместе с копиями ключа исходной таблицы и в этих новых таблицах устанавливаются свои первичные ключи.

**2НФ** основана на понятии «**полная функциональная зависимость**» (функциональная зависимость $A \to B$ является полной, если удаление какого - нибудь атрибута из А приводит к полной утрате этой зависимости, а частичная – если в А есть атрибут, при удалении которого зависимость сохраняется).

Операция перевода из 1НФ в 2НФ  применяется к отношениям с составными ключами. 2НФ – отношение которое находится уже в 1НФ и каждый атрибут которого, не входящий в состав первичного ключа характеризуется полной функциональной зависимостью от этого первичного ключа. Если в отношении  между атрибутами существует частичная зависимость, то функционально зависимые атрибуты удаляются и помещаются в новое отношение вместе с копией детерминанта, т.е. атрибуты, которые зависят от части составного ключа, вносятся в отельную таблицу.

Приведение к отношению **3НФ** имеет цель устранение транзитивных зависимостей. 3НФ - отношение, которое уже находится в 2НФ и не имеет атрибутов, не входящих в первичный ключ, которые бы находились в транзитивной функциональной зависимости от этого первичного ключа. Если обнаруживается транзитивная зависимость, то транзитивно зависимые атрибут вынимаются и помещаются в новое отношение вместе с копией детерминантом.
В общем случае при приведение в 2НФ и 3НФ нужно учитывать и потенциальные ключи отношений. Общее для 2НФ – отношение, находящиеся в 1 НФ, в котором каждый атрибут, отличный от атрибута первичного ключа, является  полностью функционально независимым от любого потенциального ключа. 3НФ – отношения, находящиеся в 2НФ, в котором ни один атрибут, отличный от атрибута первичного ключа, не является транзитивно зависимым ни от одного потенциального ключа.

**Сотрудники_отдел_проекты(№ сотр, ФИО, № отд, тел, № проекта, проект, № зад)**
$$\begin{matrix}
\text{Номер сотр} & \text{ФИО} & \text{Номер отдела} & \text{Тел} & \text{Номер проекта} & \text{проект} & \text{Номер задания} \\
1 & \text{Иванов} & 1 & \text{Т1} & 1 & \text{Космос} & 1\\
1 & \text{Иванов} & 1 & \text{Т1} & 2 & \text{Климат} & 1 \\
2 & \text{Петров} & 1 & \text{Т1} & 1 & \text{Космос} & 2 \\
3 & \text{Сидоров} & 2 & \text{Т2} & 1 & \text{Космос} & 3 \\
3 & \text{Сидоров} & 2 & \text{Т2} & 2 & \text{Климат} & 2
\end{matrix}$$


Плохо то, что имеются функциональные зависимости, например, зависимости атрибутов от ключа отношения, т.е. составной ключ (№ сотр. № про) и все остальны зависимы. Имеется зависимость атрибутов, характеризующих сотрудника от табельного номера сотрудника. Во-первых, номер сотрудника – ФИО, другая частчина зависимость имя проекта от его номера, имеется зависимость омера тел от номера отдела. Эти функциональные зависимости являются семантическими, т.е. не из таблицы,  а из жизни.

Чтобы устранить зависимости атрибутов от чатси составного ключа мы декомпозируем нашу таблицу на **сотрудники – отделы – проекты – задания**
- Сотр_отделы(№ сотр, ФИО, № отд, тел)
- Проекты(№ проекта, проект)
- Задание(№ сотр, № проекта, № задания)
Сотр_отделы не находятся в 3НФ, т.к. тел зависит от отдела(функциональная зависимость между неключевыми)
Получилось сотр(№ сотр, ФИО, № отд) и отделы(№ отд, тел)
Как правило требуется проектировать базу на уровне самого бизнес процесса, получаем 3НФ и параллельно проверять на исключения.
Критерии:
- Адекватность БД предметной области.(1, 2 НФ – плохо, 3НФ – хорошо)
- Легкость разработки и сопровождения(1, 2НФ - сложно, 3НФ – легко)
- Скорость выполнения вставки, обновления и удаления(1,2 НФ – медленнее, 3НФ – быстрее)
- Скорость выполнения выборки данных(1, 2НФ – быстрее, 3НФ – медленнее)

В скорость обработки входит и скорость пересылки, в зависимости от распределённости базы идут ее денормализации
**Сильнонормализованные модели** – это онлайн транзакшн процессинг(OLTP) и онлайн аналитикал процессинг(OLAP). 
**Пример OLTP** – много маленьких транзакций. Транзакций много, они выполняются одновременно, они короткие, при возникновении ошибки нужно обеспечить откат. Основные операции – вставка, удаление, обновление, поэтому чем выше уровень нормализации тем надёжнее приложение. Единственное исключение если среди операций имеются типовые join'ы.
**OLAP** – базы знаний любых систем продаж, истории. На таких системах можно строить прогнозы, т.е. искать свзь между агрегированными данными. Основной операцией является операция выборки, добавление в систему новых данных происходит редко, обновление не происходит никогда, перезагрузкой данных производятся различные очистки, запросы редко и только сотрудникам особого доступа. В этой ситуации нам нужна многомерная модель даны – гиперкуб.
### НФБК(норм форма Боса-Корда)
Отношение находится в НБК тогда, когда каждый его детерминант является его потенциальным ключом. **Детерминант** – один или группа атрибутов, оот которых полностью функционально зависит другой атрибут, .т.е $A \to B$ допускается в отношении 3НФ. НФБК является более строгой версией 3НФ, потому что каждая НФБК принадлежит 3НФ, но обратное верно не всегда.

ClientInterview(clientNo, intDate, IntTime,StaffNo, roomNo). Если собеседование производится в 1 помещении несколькими разными сотрудниками, то возникает необходимость в НФБК, следовательно разделяем отношение на 2:
- Interview(clientNo, intDate, intTime, StafNo)
- StaffRoom(staffNo, intDate, roomNo)

Решение о том, достаточно ли остановится на 3НФ или переходит к НФБК определяетя характеристиками бизнес процесса, которые мы поддерживаем, т.е. насколько критична ситуация, описанная выше.

**4НФ** призвана устранить многозначные зависимости. **Многозначаня зависимость** – это зависимость между атрибутами A,B,C, при которых существует множество значений для B  и множество для C, однако B и C не зависят друг от друга. 4НФ – отношение, уже в НФБК, которая не содержит нетривиальных многозначных зависимостей. Зависимость между A и В тривиальна, если B – подмножество А, или A – всё множество зависимостей, имеющее место в базе. Нормализация до 4НФ заключается в устранении многозначной зависимости из НФБК путём выеления в новое отношение 1 или нескольких атрибутов вместе с копией соответствующих детерминантов.

**Сюжет:**
Есть несколько ресторанов, они проихводян разные виды пиццы и служба доставки по нескольким районам, если хотим описать процесс что мы заказываем, то будет первичный ключ из 3 сущностей: pizza(ресторан, пицца, район). Имеет место 2 зависимости: 
- ресторан $\to$ вид_пиццы
- ресторан $\to$ районы

Декомпозируем сложную таблицу на 2:
- Pizza_дост(ресторанб район,…)
- Pizza_произв(ресторан, вид пиццы,…)

Если имеется еще зависимость цены от всех 3 атрибутов, то эту композицию до 4НФ сделать невозможно, и такая многозначная зависимость называется внедренной.

Зависимость соединения без потерь (**5НФ**) – свойство декомпозиции, которая гарантирует отсутствие фиктивных строк, при восстановлении первоначального отношения с помощью операций естественного соединения. Неформально говоря, при декомпозиции без потерь, отношение разделяется на отношение проекций, таким образом, что, из полученных проекция возможна сборки исходного отношения с помощью операций естественного соединения.

# Еще не обработанный тест:

**Сюжет:**
Есть продавец, который торгует товарами какой то фирмы. Есть ассортимент несксольких продавцов, они торгуют товарами нескольких фирм. Ограничение: данный продавец рабоатет с данным подмножеством фирм и данным списком номенклатуры товара, т.е. продавец не имеет права торговать какими угодно товарами каких угодно фирм.
Продавец	фирмы 	товар
(продавец, товар) (продавец, фирма) (фирма, товар)
Отношение находится в 5НФ или Проекционно-соединительной НФ, когда каждая нетривиальная зависимость соединения в нём определяется потенциальными ключами этого отношения
ЭТОТ ПРИМЕР ДЛЯ РУБЕЖКИ НОРМ!
ВВЕДЕНИЕ В РЕЛЯЦИОННУЮ АЛГЕБРУ
Общие определения реляционной алгебры.
Понятие алгебры используется для конструктивного описания того, что можно делать  отношениями.
универсальной парой является <m,Ω>, где   м - непустое множество элементов, а Ω-множество операций, определённых на М. множество М – носитель алгебры.
Реляцонная алгеба – пара <T,O>, где Т – множество реляционных таблиц, О – множество логических операций над ними, причём все операнды, принадлежащие Т – отображаются обратно в Т. Реляционная алгебра обладает свойством замкнутости, независимо от глубины вложенности операции. 
ОБЗОР ОПЕРАЦИЙ РЕЛЯЦИОННОЙ АЛГЕБРЫ.
Унарные:
	Выборка – selection – R’=σ предикат(R) – применяется к 1 отношению R  и определяет результирующее отношение R’, которые содержит только те кортежи из отношения R, удовлетворяющие заданному предикату. Предикат мондо создать с помощью логических операций И, ИЛИ, НЕ  и их комбинирования. Если предикат только в операции сравнения, то операция называется ограничением.
	Проекция –projection -  R’=П_(a1,a2,…,an) (R) применяется к 1 отношению Rи определяет новое отношение R’, содержащее вертикальное подмножество отношения R, создаваемое посредством извлечения значений указанных атрибутов и исключение из результата строк дубликата.
Бинарные:
	Объединение – union – R=RUS объединение 2 отношений R и S определяет новое отношение, которое включает все кортежи, содержащиеся только в R, только в S, а также одновременно в R и S, при этом все дубликаты кортежей исключаются, а кортежи R и S должны быть совместимыми по объединении. Совместимость по объединению – объединение возможно только если схемы 2 отношений совпадают, т.е. состоят из одинакового количества атрибутов,  и каждая пара соответствующих атрибутов имеет одинаковый домен. Не предполагается, что при объединении атрибуты должны иметь одинаковые имена.
	Разность – difference – R’=R-S – состоит из кортежей, которые имеются в отношении R, но отсутствуют в отношении S, при этом отношения R и S должны быть совместимы по объединению.
	Пересечение – intersection – R’ = R∩S – определяет отноения, которое содержит кортежи присутствующие и в R, и в S, при этом отношения должны быть совместимы объединению.
	Декартово произведение – CortesianProduct – R'=RxS – определяет новое отношение, которое является результатом конкатенации(сложение) каждого кортежа из R с каждым кортежем из S. Результирующее количество атрибутов – сумма количества атрибутов в исходных таблицах, количество кортежей – произведение каждого кортежа на каждый. Если исходное отношение содержит атрибуты с одинаковыми именами, то в имена атрибутов включаются названия отношений  виде префиксов.
	Декомпозиция сложных операций. Для упрощения операции можно разбить на ряд меньших и присвоить самостоятельные имена для упрощения операции можно разбить на ряд меньших операции и присвоить имена результатам промежуточных операций. Для этого используется 2 операции – присваивание( ->)(полностью аналогично проге, т..е результат выражения справа от стрелки присваивается выражению слева от стрелки), переименование позволяет задать произвольное имя для любого из атрибутов любого из отношений
Классификации:
	Унарные(selection, projection) и бинарные(все остальные)
	Теоретик- множественные(union, intersection, difference, cortesianproduct) и характерные только для БД(selection, join, projection, division)
	C параметрами(join, Projection) и без(остальные)
	Общие алгебраического типа(union, intersection, difference, corteesianproduct, projection) и процедурно доопределяемые(selection, join, division)
Операции соединения!
Как правило операции декартового произведения очень избыточны и вместо этого используются различные варианты операции соединения.
 Операции соединения являются производной от декартового произведения, т.к. она эквивалента паре декартового произведения+выборка. С точки зрения эффективности реализации это самая неудачная операция
	Тета соединение(teta join)
	Equijoin
	Naturaljoin
	Внещнее соединение(outes join)
	Левое
	Правое
	Полное
	Полусоединение(semijoin)
	Theta
	Equ
	Natural

# Лекция 8 (02.12)
Различные операции соединения.
Тэта соединения – определяет отношения, которые содержат кортежи из декартова произведения R и S удовлетворяющие предикату F. Предикат имеет вид R.aiθS.bj , где вместо тэта может быть указана операция сравнения. σ_F (RxS)=R><fS  это операция выборки и декартового произведения если предикат F содержит сравнение только по строгому равенству, то это называют соединением по эквиваленции.  Естественным соединением называется – соединение по эквиваленции R и S выполненное по всем общим атрибутам, из результатов которого исключаются по одному экземпляру каждого общего атрибута. σ_F (RxS)=R><S. Степень соединения по эквиваленции и любого тэта соединения – сумма степеней исходных отношений, а степень естественного соединения – сумма степеней исходных отношений минус количество общих атрибутов. 
Внешнее соединение.
При соединении двух отношений может возникнуть ситуации, что для кортежа одного отношения не находятся соответствия в другом отношении. Но часто требуется, чтобы эта строка без пары была представлена в результатах соединения, для этого мы используем внешнее соединение. Левое внешнее соединение – соединение при котором в результирующее отношение включаются так же кортежи отношения R не имеющие совпадающих значений в общих столбцах с отношением S. Для обозначения отсутствующих отношений ставится NULL и  σ_F (RxS)=R⊃<S. Правое соединение определяется симметрично. Полное внешнее соединение определяется аналогично, но в результирующее отношение помещаются все кортежи из обоих отношении и несовпадающие значения обозначаются как NULL. 
	Полу соединение. 
Операция определяет отношение, которое содержит те кортежи отношения R, которые войдут в соединение отношений R и S. Операцию можно сформулировать с помощью операции проекции и соединения R><fS=П_A (R><fS). 
	Деление.
Имеется два отношения: склад и запчасти.
Склад(№зап.части,№склада,Местоположение_склада). (A,B,C)
Запчасти(№зап.части.) (A)
Делимое
A	B	C
a	c	d
b	c	d
a	p	q
b	x	y
Делитель
A
a
b
Частное
B	C
c	d
Остаток
A	B	C
a	b	a
b	x	y


После выполнения операции деления будет получено унарное отношение содержащие номера складов, на которых можно получить интересующие запчасти с одного склада всем комплектом.
Чтобы понять происходящее нужно сделать обратную операцию, т.е. умножить делитель на частное методом декартового произведения, и прибавить остаток с помощью операции объединения.
Специфика: 
	нужно соблюдать все условия доменов
Заключительные замечания:
	8 оператором Кодда, которые мы обозначили не представляют минимальный набор операторов, т.е. не все из них являются примитивами (сущность, которая в данной задачи принимается как неразложимая)
	Все операции соединения являются составными
	Составными являются операции пересечение и деление
	Примитивами являются только 5:
	Выборка
	Проекция
	Произведение
	Объединение
	Вычитание
	Для трёх остальных операций осуществляется поддержка.
	Введение любой алгебры, предполагает возможность составления и решения соответствующих уравнений. Такие уравнения можно написать для поиска результирующего набора из исходного через алгебраические операции. Т.е. запросы можно написать в форме уравнений. Как правило для реальных приложений эти уравнения получаются очень сложными и поддаются решению итерационными методами.