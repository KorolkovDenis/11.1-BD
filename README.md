Домашнее задание к занятию «Базы данных, их типы»

Задание 1. СУБД
Кейс
Крупная строительная компания, которая также занимается проектированием и девелопментом, решила создать правильную архитектуру для работы с данными. Ниже представлены задачи, которые необходимо решить для каждой предметной области.

Какие типы СУБД, на ваш взгляд, лучше всего подойдут для решения этих задач и почему?

1.1. Бюджетирование проектов с дальнейшим формированием финансовых аналитических отчётов и прогнозирования рисков. СУБД должна гарантировать целостность и чёткую структуру данных.

Ответ:

Реляционные базы данных, или базы данных SQL Основная особенность — надежность и неизменяемость данных, низкий риск потери информации. При обновлении данных их целостность гарантирована, они заменяются в одной таблице. Подойдут Oracle, Microsoft SQL, PostgreSQL, MySQL

1.1.* Хеширование стало занимать длительно время, какое API можно использовать для ускорения работы?

Ответ:

СУБД типа key-value. Так как запрос возвращает только одно значение, а ключ уникальный – такие СУБД работают быстро. Соответственно такие СУБД лучше использовать для кэширования. Подойдут Redis, Memcached.

1.2. Под каждый девелоперский проект создаётся отдельный лендинг, и все данные по лидам стекаются в CRM к маркетологам и менеджерам по продажам. Какой тип СУБД лучше использовать для лендингов и для CRM? СУБД должны быть гибкими и быстрыми.

1.2.* Можно ли эту задачу закрыть одной СУБД? И если да, то какой именно СУБД и какой реализацией?

Ответ:

PostgeSQL в наборе с JSON (JSON-текст представляет собой (в закодированном виде) одну из двух структур: Набор пар ключ: значение  и Упорядоченный набор значений) нас тут интересует как раз Набор пар ключ: значение.

1.3. Отдел контроля качества решил создать базу по корпоративным нормам и правилам, обучающему материалу и так далее, сформированную согласно структуре компании. СУБД должна иметь простую и понятную структуру.

Ответ:

По сути, это хранилище документов без использования схематичного или табличного форматов, поэтому ее еще называют документоориентированной. MongoDB базы данных подключаются к приложениям через драйверы баз данных. Несколько типов данных обрабатываются одновременно и для этой цели используется внутренний кэш. Плюсы MongoDB 1) Простой доступ к данным, их хранение, ввод и извлечение. Одним из преимуществ MongoDB, вытекающих из его природы NoSQL, является быстрая и простая обработка данных. СУБД MongoDB рекомендуют использовать там, где отсутствуют потребности в сложных выборках.

1.3.* Можно ли под эту задачу использовать уже существующую СУБД из задач выше и если да, то как лучше это реализовать?

Ответ:

У MongoDB открытый исходный код. С помощью идентификатора можно осуществлять манипуляции над объектом с высокой скоростью. При сложных операциях СУБД тоже демонстрирует весьма хорошие показатели. Это связано с тем, что ПО относится к типу NoSQL и использует объектный язык запросов, который намного легче SQL.

1.4. Департамент логистики нуждается в решении задач по быстрому формированию маршрутов доставки материалов по объектам и распределению курьеров по маршрутам с доставкой документов. СУБД должна уметь быстро работать со связями.

Ответ:

Графовые Особые СУБД, предназначенные для хранения информации, связанной с графами (узлы, вершины, связи между узлами). Хорошо подходят для социальных сетей, где требуется хранить связи между пользователями по разным критериям.

1.4.* Можно ли к этой СУБД подключить отдел закупок или для них лучше сформировать свою СУБД в связке с СУБД логистов?

1.5.* Можно ли все перечисленные выше задачи решить, используя одну СУБД? Если да, то какую именно?

Приведите ответ в свободной форме.

Задание 2. Транзакции
2.1. Пользователь пополняет баланс счёта телефона, распишите пошагово, какие действия должны произойти для того, чтобы транзакция завершилась успешно. Ориентируйтесь на шесть действий.

Ответ:
```
1. Проверить, есть ли необходимая для оплаты сумма на счету
2. Ввод номера телефона
3. Подтвердить правильность телефона
4. Ввод необходимой суммы
5. Подтвердить оплату, тем самым подтвердить перевод денежных средств со счета на баланс телефона.
6. Проверить баланс телефона - необходимая сумма должна поступить на счет телефона.
```

2.1.* Какие действия должны произойти, если пополнение счёта телефона происходило бы через автоплатёж?

Приведите ответ в свободной форме.

Ответ:

Создаем шаблон авто платежа в личном кабинете оператора связи:
```
1. Оператор отслеживает баланс счета мобильного телефона
2. При падении баланса на телефоне ниже заданного значения, сеть отправляет команду в банк
3. Создается автоматический запрос на пополнение средств со счета в банке на баланс телефона.
4. Банк перечисляет заранее установленную сумму с счета в банке на указанный номер телефона
5. Далее происходит автоматическая транзакция и подтверждение поступления денежных средств на номер телефона.
```

Задание 3. SQL vs NoSQL
3.1. Напишите пять преимуществ SQL-систем по отношению к NoSQL.

Ответ:

SQL - лучший выбор, когда: 
1.	Доступна предопределенная структура и заданные схемы
2.	Все данные в наборе данных должны быть строго согласованы 
3.	Анализ поведенческих и настраиваемых сеансов 
4.	Разработка пользовательских панелей мониторинга 
5.	Выполнение операций объединения и сложных запросов 
6.	Необходимо выполнить многорядные транзакции

3.1.* Какие, на ваш взгляд, преимущества у NewSQL систем перед SQL и NoSQL.

Приведите ответ в свободной форме.

Ответ:

Он вводит новую реализацию в традиционные реляционные базы данных. 
Он объединяет преимущества SQL и NoSQL. 
Легко переключаться между типом и потребностями пользователя. 
Оптимизация обработки онлайн-транзакций, масштабируемость, гибкость и бессерверная архитектура. При этом структуры NewSQL, как и реляционные базы данных, поддерживают принципы ACID и согласованность. 
Они могут масштабироваться, зачастую по запросу, не влияя на логику приложения и не нарушая модель транзакций. Гибкость и бессерверная архитектура в сочетании с высокой степенью безопасности и доступности без применения резервных систем. 
Наиболее популярные базы данных NewSQL: ClustrixDB, CockroachDB, NuoDB, MemSQL и VoltDB.

Задание 4. Кластеры
Необходимо производить большое количество вычислений при работе с огромным количеством данных, под эту задачу выделено 1000 машин.

На основе какого критерия будете выбирать тип СУБД и какая модель распределённых вычислений здесь справится лучше всего и почему?

Приведите ответ в свободной форме.

Ответ:

Можно использовать Hadoop. Считается одной из основополагающих технологий «больших данных».

Hadoop помогает хранить и обрабатывать массивы информации, готовить ее для выгрузки в другие сервисы, собирать статистику. По сути, это конструктор, на основе которого строят хранилища данных под потребности бизнеса.
Лучше всего Hadoop подходит для работы с неструктурированными данными — неупорядоченной информацией без определенной структуры, которую сложно классифицировать и разбить на группы.
Проще говоря, это база данных (database), предназначенная для работы с большими данными (Big Data). Набор утилит, библиотек и фреймворк для разработки и выполнения распределенных программ, работающих на кластерах из сотен и тысяч узлов.
Из преимуществ поисковые и контекстные механизмы высоконагруженных веб-сайтов и интернет-магазинов в том числе аналитики поисковых запросов и пользовательских логов, хранение, сортировка огромных объемов данных и разбор содержимого чрезвычайно больших файлов, быстрая обработка графических данных.

## Моя подробная работа в Google:

[Моя работа по «Базы данных, их типы»](https://docs.google.com/document/d/1PjzOaSpj--PD-gFnNTfeXvWgqs2T_ROZ/edit?usp=share_link&ouid=104113173630640462528&rtpof=true&sd=true)
