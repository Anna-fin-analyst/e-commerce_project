# e-commerce_project

## Анализ аудитории интернет-магазина с помощью метода когорт и метода сегментации


Задача взята с [Karpov.Courses](https://karpov.courses/analytics?_gl=1*psy4n7*_ga*MTI0OTM2MzQyMC4xNzExNDQwNDU2*_ga_DZP7KEXCQQ*MTcyMDQ3ODM1OS40MDAuMS4xNzIwNDc4NDMyLjQ5LjAuMA)


### В данном проекте нам необходимо проанализировать совершённые покупки и ответить на следующие вопросы продакт-менеджера:

    1. Сколько у нас пользователей, которые совершили покупку только один раз? 
    2. Сколько заказов в месяц в среднем не доставляется по разным причинам (с указанием причин)?
    3. По каждому товару определить, в какой день недели товар чаще всего покупается.
    4. Сколько у каждого из пользователей в среднем покупок в неделю (по месяцам с учетом того, что в некоторых месяцах неполное количество недель)?
    5.1. Выполнить когортный анализ пользователей.
    5.2. В период с января по декабрь выявить когорту с самым высоким retention на 3-й месяц.
    6. Провести качественный анализ аудитории используя подход, основанный на сегментации.
    Чтобы качественно оценить свою аудиторию, необходимо построить RFM-сегментацию пользователей с помощью Python, использовав следующие метрики:
        - R - время от последней покупки пользователя до текущей даты, 
        - F - суммарное количество покупок у пользователя за всё время, 
        - M - сумма покупок за всё время. 

В качестве данных были использованы следующие файлы:

 - olist_customers_datase.csv — таблица с уникальными идентификаторами пользователей
     - customer_id — позаказный идентификатор пользователя
     - customer_unique_id —  уникальный идентификатор пользователя (аналог номера паспорта)
     - customer_zip_code_prefix —  почтовый индекс пользователя
     - customer_city —  город доставки пользователя
     - customer_state —  штат доставки пользователя

 - olist_orders_dataset.csv —  таблица заказов
     - order_id —  уникальный идентификатор заказа (номер чека)
     - customer_id —  позаказный идентификатор пользователя
     - order_status —  статус заказа
     - order_purchase_timestamp —  время создания заказа
     - order_approved_at —  время подтверждения оплаты заказа
     - order_delivered_carrier_date —  время передачи заказа в логистическую службу
     - order_delivered_customer_date —  время доставки заказа
     - order_estimated_delivery_date —  обещанная дата доставки

 - olist_order_items_dataset.csv —  товарные позиции, входящие в заказы
     - order_id —  уникальный идентификатор заказа (номер чека)
     - order_item_id —  идентификатор товара внутри одного заказа
     - product_id —  ид товара (аналог штрихкода)
     - seller_id — ид производителя товара
     - shipping_limit_date —  максимальная дата доставки продавцом для передачи заказа партнеру по логистике
     - price —  цена за единицу товара
     - freight_value —  вес товара

 - Уникальные статусы заказов в таблице olist_orders_dataset:
     - created —  создан
     - approved —  подтверждён
     - invoiced —  выставлен счёт
     - processing —  в процессе сборки заказа
     - shipped —  отгружен со склада
     - delivered —  доставлен пользователю
     - unavailable —  недоступен
     - canceled —  отменён





# План реализации:

    1. Загрузка необходимых библиотек:
        pandas для работы с данными
        datetime для работы с датами
        seaborn и matplotlib для визуализации
    2. Загрузка данных
    3. Проверка типов данных, нулевых строк, размеров таблиц
    4. Преобразование колонок с датой в формат datetime
    5. Соеднинение необходимых таблиц
    6. Анализ данных на предмет, того, что считать покупкой

### Вопрос 1. Сколько у нас пользователей, которые совершили покупку только один раз?

    - Для решения данного вопроса нам необходимо воспользоваться группировкой по уникальному идентификатору пользователя и подсчетом количества позаказных идентификаторов пользователей. Далее выбираем только те группы пользователей, у которых число покупок рабвно 1.


### Вопрос 2. Сколько заказов в месяц в среднем не доставляется по разным причинам (с детализацией по причинам)?

В данном вопросе нам необходимо:

    - Добавить расчётные колонки
    - Соединить таблицы
    - Проанализировать результаты в разных разрезах, сделать выводы
    - Объединить все причины недоставленных заказов в одну таблицу с общей таблицей недоставленных заказов (пишем функцию)
    - Посчитать среднее недоставленных заказов и сгруппировать в разбивке по причинам помесячно
    
Использовались методы: сортировки, удаления дубликатов, группировки, расчета уникальных и неуникальных значений


### Вопрос 3. По каждому товару определить, в какой день недели товар чаще всего покупается.

В данном вопросе нам необходимо:

    - Создать колонку с днями недели по каждому заказу
    - Для визуализации полученных данных используем график (barplot)
    
Использовать методы: сортировки, переименования колонок, группировки, расчета неуникальных значений, выбор максимальных значений, объединение таблиц


### Вопрос 4. Сколько у каждого из пользователей в среднем покупок в неделю (по месяцам)? 

В данном вопросе нам необходимо:

    - Скопировать нужные таблицы
    - Добавить колонку со сременем доставки заказов
    - Рассчитать количество недель
    
Использовать методы: сортировки, переименования колонок, группировки, расчета неуникальных значений; здесь применили lambda функцию


### Вопрос 5.1. Выполните когортный анализ пользователей.

В данном вопросе нам необходимо:

    - Скопировать нужные таблицы, оставить нужные колонки
    - Определить дату первой покупки, добавить её в новую колонку
    - Создать когортную табицу, визуализировать её с помощью тепловой карты
    - Посчитать, сколько в среднем заказов совершают клиенты в течение первого года. 

Использовались методы: объениения таблиц, написания функции, связанной с получением отдельных частей дат; вычитания дат, группировки, расчета уникальных и неуникальных значений, сортировки, переименования колонок, создания сводной таблицы    


### Вопрос 5.2. В период с января по декабрь выявите когорту с самым высоким retention на 3-й месяц.

В данном вопросе нам необходимо:

    - Выделить период, за который необходимо произвести наблюдение
    - Создать когортную табицу, визуализировать её с помощью тепловой карты
    - Рассчитать % удержания клиентов на каждый из месяцев по формуле:
    CRR = ('Кол-во клиентов на конец периода' — 'Кол-во клиентов, которые пришли за весь период') / 'Кол-во клиентов на начало периода')
    - Визуализировать полученный результат с помощью тепловой карты, подсветив интересующие нас значения
    
Использовались методы: фильтрации, группировки, расчета уникальных и неуникальных значений, переименования колонок, создания сводной таблицы


### Вопрос 6. С помощью python провести качественный анализ аудитории используя подходы, основанные на сегментации. 

 В кластеризации выбрать следующие метрики: 
     R - время от последней покупки пользователя до текущей даты, 
     F - суммарное количество покупок у пользователя за всё время, 
     M - сумма покупок за всё время. 
 Подробно описать, как создавались кластеры. 
 Для каждого RFM-сегмента построить границы метрик recency, frequency и monetary для интерпретации этих кластеров.
 

В данном вопросе нам необходимо:

    - Объединить 3 датафрейма, оставив нужные столбцы и отфильтровав непустые значения дат доставки
    - Создать колонку "год-месяц" 
    - Провести анализ распределения числа уникальных клиентов и выручки по месяцам за все время с помощью графиков
    - Сократить таблицу до интересующего нас периода (который интересен на графике)
    - Проверить временные рамки наших данных и установить текущую дату
    - Добавить в наш датафрейм столбец с количеством дней от даты последней покупки по текущий момент, найти минимум этого столбца для каждого клиента для расчета времени с момента его последней покупки
    - Сформировать таблицу RFM, в которой будут данные о времени с момента последней покупки, о количестве заказов и о сумме заказов за исследуемый период по каждому клиенту.
    - Перед тем, как создать границы метрик, проанализировать их с помощью различных группировок и графиков
    - Создать границы метрик ('Frequency' и 'Monetary' вручную экспертно на основании визуальных наблюдений, 'Recency' с помощью 'разрезания' на равные ингтервалы методом qcut())
    - Создать категории для метрик
    - Сгруппировать категории в кластеры с помощью функции
    - Посчитать количество клиентов в каждом сегменте и визуализировать данные 

Использовались методы: объединения таблиц, фильтрации, группировки, расчета уникальных и неуникальных значений, переименования колонок, форматирования, поиска минимальных и максимальных значений, построения графиков, деления данных на интервалы, написания функций.