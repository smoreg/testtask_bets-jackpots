# testtask_bets-jackpots

В попытках оптимизировать тестовое задание я понял что просто описать addBet с одной транзакцией, и таблицы/вызовы в sql запросах будет мало.

###Таблицы:

*users
| user_name  | deposit |
| ------------- | ------------- |
| pk char(50) | money |
| index unique  |  |
with fillfactor == 90

Таблица пользователей и их счетов. Примерно раз в указанное время(updateDeamonTimer) обновляется данными из operations.

*old_jackpot
| value  |
| ------------- |
| money |

Джекпот после последнего обновления. Сложив его с operaions.deposit можно получить актуальный джекпот

*operations
| id | user_name | deposit  | jackpot_part |
| ------------- | ------------- | ------------ | ------------- |
| pk SERIAL | char(50) | money | money |

Недавно сделанные ставки. Переодически updateDaemon обновляет этими данными users, old_jackpot и очищает таблицу.

### Суть
