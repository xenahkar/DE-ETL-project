# ETL по выявлению мошеннических банковских операций


В данном проекте разработан ETL-процесс, который ежедневно выполняет следующие задачи:

**Прием входящих данных**:
   - Данные о транзакциях, терминалах и черном списке паспортов из файлов.
   - Данные о клиентах, счетах и картах из базы данных.

**Загрузка данных в бд**:
   - Создание временных таблиц для предварительной обработки данных (STG).
   - Наполнение основных таблиц измерений (DIM) и фактов (FACT).

**Выявление мошеннических операций**:

Генерация отчета о мошеннических операциях (`rep_fraud`) на основе заданных правил.

Каждая операция, соответствующая одному из следующих типов мошенничества, будет записана в таблицу `rep_fraud`:

1 - Совершение операции при просроченном или заблокированном паспорте.
     
2 - Совершение операции при недействующем договоре.
     
3 - Совершение операций в разных городах в течение одного часа.
     
4 - Попытка подбора суммы: в течение 20 минут происходит более 3 операций с последовательными суммами, где каждая последующая меньше предыдущей, при этом отклонены все, кроме последней. Последняя операция (успешная) в такой цепочке считается мошеннической.


**Автоматизация процесса**:
   - Настройка ежедневного запуска `main.py` через планировщик задач (cron).
  
-----
В файле `config.py` в классе нужно указать данные для подключения к базе данных:

    class Config:
        remote = {
            'database': DB,
            'host': HOST,
            'user': USER,
            'password': PASSWORD,
            'port': PORT
        }
