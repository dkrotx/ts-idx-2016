# ДЗ по курсу Инфопоиск (Техносфера)

## Дано: дамп lenta.ru (10k документов)

Документы доступны по адресу: https://cloud.mail.ru/public/FnMq/qCNif6bFG/dataset

Для чтения документов используем docreader.py 
Используем поля .url и .text

Разбор документов на слова лучше организовать с помощью regexp-а r'\w+', см. doc2words.py  
Необходимая нормализация: приводим все слова к нижнему регистру.  
Лемматизацию и пр. - в этом ДЗ не используем.


## Необходимо:
- Создать индекс
- Реализовать булев поиск

### А конкретно

#### На оценку 15 (набор - 1.5К документов):
- имплементировать кодирование varbyte
- создать словарь термов (в любом виде)
- разобрать текстовый запрос простого формата (см. далее)
- вывести подходящие под булев запрос URL-ы

#### На оценку 20 (10К документов):
Дополнительно к предыдущему:
- имплементировать метод Simple9

#### На оценку 25 (100К документов):
Дополнительно к предыдущему:
- реализовать текстовый запрос полного формата (см. далее)

#### На оценку 35 (600К документов):
Дополнительно к предыдущему:
- потоковая обработка дерева запроса
- обязательно: индекс в бинарном виде
- обязательно: словарь в бинарном виде (см. 2ю лекцию)

### Состав пакета

Помимо исходников на Python Ваш пакет должен содержать 3 .sh-файла:

- index.sh (varbyte|simple9) path/to/\*.gz : создение индекса
- make\_dict.sh: создание словаря и оптимизация индекса
- search.sh: непосредственно поиск
- [опционально] preinstall.sh: скрипт, в котором вы можете установить необходимые пакеты


Вывод (stdout) подразумевается только от утилиты поиска.

### Формат ввода

На stdin searcher.sh будет дана последовательность запросов в виде

запрос #1  
запрос #2  
...

Форматы запросов:

#### простой:
присутствуют только термы и конъюнкция ("&")

Пример: власти & бельгии

#### полный:
Формат каждого запроса - булево выражение содержашее слова и операторы: "(", ")", "&", "|", "!"

Пример: власти & (бельгии | парижа) & !теракт

*Гарантируется что запрос валидный*


### Формат вывода:
ИСХОДНЫЙ ЗАПРОС  
КОЛ-ВО результатов  
URL1  
URL2  
...

Пример:  
Путин & Медведев  
2  
https://lenta.ru/news/2015/08/30/putin/  
https://lenta.ru/photo/2015/08/30/medput/


## Куда отправлять код

Код запакованный в .tgz отправляйте на ts2016idx@mail.ru

В теме письма обязательно указывайте вариант (баллы). 
Формат: [Ir-ts] idx, Иван Иванов (var: 35)

## Как будет происходить проверка

Для проверки будет использоваться набор документов lenta.ru в 10 и 50 раз больше данного.  
Ограничение по RAM: 2Gb

Из-за необходимости проверки реализации, оценка *не будет* автоматической.  
После получения оценки от робота, пришлите письмо еще раз со словом FINALTRY в теме.

Срок сдачи: 
ИТМО: 22 марта 2017
МГУ: 30 марта 2017 (на семинаре 31-го подробно разберем решение).

## Вопросы?

МГУ: Обсуждаем совместно в топике https://sphere.mail.ru/blog/topic/1672/
