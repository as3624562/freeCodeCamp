---
title: Python Set Types
localeTitle: Типы наборов Python
---
Заданный объект представляет собой неупорядоченный набор различных хешируемых объектов. Обычное использование включает тестирование членства, удаление дубликатов из последовательности и вычисление математических операций, таких как пересечение, объединение, разность и симметричная разность.

[Python Docs - Установить типы Установить Frozenset](https://docs.python.org/3/library/stdtypes.html#set-types-set-frozenset)

**TODO: Объяснить хэш / хешировать** Хэш-таблица представляет собой непрерывный вектор записей, чьи слоты входят в три ароматизаторы:

1.  Слоты с парами ключ + значение. Позвоните этим гражданам.
2.  Еще не используемые слоты. Назовите этих девственниц.
3.  Слоты, которые когда-то были гражданами, но чей ключ был удален, и где другая пара ключей + значение еще не перезаписала слот. Назовите эти turds (это технический термин <0.9 wink>).

Python изменяет размер таблицы, когда количество девственниц падает ниже трети общее количество слотов. В обычном случае Python удваивает размер таблицы (до максимального тока 1,073,741,824 слота). Однако, если многие удалений оставляют за собой много дерьмов, возможно, количество девственниц получить очень низкий уровень, несмотря на то, что осталось мало граждан; в этом случае Python фактически сокращает таблицу (вплоть до текущего минимума в 4 слота).

Во избежание избиения при добавлении и удалении комбинации, когда таблица находится рядом с порогом изменения размера, Python фактически не проверяет # девственники после удаления (в сущности, предполагается, что вы скоро замените турки с гражданами снова). Так что, как ни странно, удаление ключа _никогда_ сжимает стол. Длинная последовательность удалений, за которыми следует добавление, может сжиматься это, однако. Способ принудительной усадки без добавления ключа:
```
dict = dict.copy() 
```

dict.copy () всегда возвращает словарь без дерна, самого маленького мощность-2, которая оставляет не менее трети девственных делений.