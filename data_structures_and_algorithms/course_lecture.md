#Структуры данных и алгоритмы
###Глава 1. Знакомство с алгоритмами.
Алгоритмом называется набор инструкций для выполнения некоторой задачи.
#####Простой поиск. Бинарный поиск
При бинарном поиске исключается половина списка.
Бинарный поиск работает только в том случае, если список отсортирован. Например, имена в телефонной книге хранятся в алфавитном порядке, и вы можете воспользоваться бинарным поиском.

Пример задачи бинарного поиска:
```python
def binary_search(my_list, items):
    low = 0
    high = len(my_list) - 1
    while low <= high:
        mid = (low + high) // 2
        guess = my_list[mid]
        if guess == items:
            return mid
        if guess > items:
            high = mid - 1
        else:
            low = mid + 1
    return None
```
#####Время выполнения алгоритма
Специальная нотация «О-большое» описывает скорость работы алгоритма. Время выполнения алгоритма растёт с разной скоростью. 
«О-большое» не сообщает скорость в секундах, а позволяет сравнить количество операций.
«О-большое» определяет время выполнения в худшем случае.
#####Типичные примеры «О-большого»
Ниже перечислены пять разновидностей «О-большого», которые будут встречаться вам особенно часто, в порядке убывания скорости выполнения:
- O(log n ), или логарифмическое время. Пример: бинарный поиск. 
- О(n), или линейное время. Пример: простой поиск. 
- О(n * log n). Пример: эффективные алгоритмы сортировки (быстрая сортировка - но об этом в главе 4).
- О(n2 ). Пример: медленные алгоритмы сортировки (сортировка выбором - см. главу 2). 
- О(n!). Пример: очень медленные алгоритмы (задача о коммивояжере - о ней будет рассказано в следующем разделе).
#####Основные результаты
- Скорость алгоритмов измеряется не в секундах, а в темпе роста количества операций. 
- По сути формула описывает, насколько быстро возрастает время выполнения алгоритма с увеличением размера входных данных. 
- Время выполнения алгоритмов выражается как «О-большое». 
- Бинарный поиск работает намного быстрее простого. 
- Время выполнения O(log n) быстрее О(n), а с увеличением размера списка, в котором ищется значение, оно становится намного быстрее. 
- Время выполнения алгоритма описывается ростом количества операций. 
#####Задача о коммивояжёре
Нужно обойти несколько точек. Для решения следует перебрать все возможные комбинации обхода. Скорость увеличения операций алгоритма увеличивается с факториальной скоростью.
#####*Упражнения из первой главы*
**1.1**	Имеется отсортированный список из 128 имен, и вы ищете в нем значение методом бинарного поиска. Какое максимальное количество проверок для этого может потребоваться? 

**Ответ:** 7 

**1.2**	Предположим, размер списка увеличился вдвое. Как изменится максимальное количество проверок? 

**Ответ:** 8 

**1.3**	Известна фамилия, нужно найти номер в телефонной книге. 

**Ответ:** O(log n) 

**1.4**	Известен номер, нужно найти фамилию в телефонной книге. (Подсказка: вам придется провести поиск по всей книге!) 

**Ответ:** О(n). 

**1.5**	Нужно прочитать номера всех людей в телефонной книге. 

**Ответ:** О(n). 

**1.6**	Нужно прочитать телефоны всех людей, фамилии которых начинаются с буквы «А». (Вопрос с подвохом! В нем задействованы концепции , которые более подробно рассматриваются в главе 4. Прочитайте ответ - скорее всего, он вас удивит!) Глава 2 275 

**Ответ:** О(n). Возможно, кто-то подумает: «Я делаю это только для одной из 26 букв, а значит, время выполнения должно быть равно О(n/26).» Запомните простое правило: в «О-большое» игнорируются числа, задействованные в операциях сложения, вычитания, умножения или деления. Ни одно из следующих значений не является правильной записью «О-большое»: О(n + 26), О(n - 26), О(n * 26), О(n / 26). Все они эквивалентны О(n)! Почему? Если вам интересно, найдите раздел «Снова об "О-большом"» в главе 4 и прочитайте о константах в этой записи (константа - это просто число; в этом вопросе 26 является константой).
