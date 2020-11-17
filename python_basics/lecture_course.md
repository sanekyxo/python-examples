###1.6 Наследование классов
Наследование используется когда нам нужно, чтобы новый класс имел функции от предка плюс дополнительные функции.

Синтаксис:
```python
class DerivedClassName(Base1, Base2, Base3):
    <statement-1>
    .
    .
    .
    <statement-N>
```
Расширим возможности класса list, добавив в него функцию проверки на чётность.
```python
class MyList(list):
    def even_length(self):
        return len(self) % 2 == 0
x = MyList()
print(x) # []
x.extend([1, 2, 3, 4, 5])
print(x) # [1, 2, 3, 4, 5]
print(x.even_length()) # False
x.append(6)
print(x.even_length()) # True  
```
Python поддерживает множественное наследование. Мы можем выбрать несколько классов, от которых наследуется наш класс. Классы от которых мы наследуемся называются родителями, а родителей родителей называют предками.
```python
class D: pass
class E: pass
class B(D, E): pass
class C: pass
class A(B, C): pass

issubclass(A, A) # True
issubclass(C, D) # False
issubclass(A, D) # True
issubclass(C, object) # True
issubclass(object, C) # False
```
Функция issubclass() принимает два аргумента и проверяет, что первый аргумент является наследником второго. От класса object наследуются все классы.
```python
x = A()
isinstance(x, A) # True
isinstance(x, B) # True
isinstance(x, object) # True
isinstance(x, str) # False
```
Функция isinstance() позволяет узнать является ли объект экземплером класса.
Функция принимает два аргумента и отвечает на вопрос является ли первый аргумент наследником второго. То каким образом мы можем использовать экземпляр класса зависит не только от класса, но и от классов от которых он наследуется.

```python
class MyList(list):
    def even_length(self):
        return len(self) % 2 == 0
x = MyList()
print(x) # []
x.extend([1, 2, 3, 4, 5])
print(x) # [1, 2, 3, 4, 5]
print(x.even_length()) # False
x.append(6)
print(x.even_length()) # True  
```
Когда мы вызываем extend у x этот метод будет найден в list, так как в MyList мы его не определяли. При вызове конструктора интерпретатор будет искать метод `__init__` и найдёт её в list, так же будет с вызовом функции print - интепретатор будет искать метод `__repr__`, который содержит в себе строковое предстваление эземпляра, и найдёт его снова в list. Поэтому очень важно в какой последовательности интепретатор будет обходить классы предки.
В Python есть порядок разрешения методов. Этот порядок определяется в момент создания класса.
```python
class D: pass
class E: pass
class B(D, E): pass
class C: pass
class A(B, C): pass

print(A.mro())
#[<class '__main__.A'>, <class '__main__.B'>,
# <class '__main__.D'>, <class '__main__.E'>,
# <class '__main__.C'>, <class 'object'>]
```
mro() или method resolution order - порядок разрешения методов, который есть у любого класса.

Данный метод гарантирует, что в списке обхода данный предок будет в единственном числе.
Также гарантируется, что предок будет после потомка в последовательности обхода.
Если используется множественное наследование, то классы родители будут следовать в той же последовательности, что и при объявлении.

Здесь порядок разрешения методов рассмотрен подробнее - [тут](https://habr.com/ru/post/62203/).
```python
class EvenLengthMixin:
    def even_length(self):
        return len(self) % 2 == 0
class MyList(list, EvenLengthMixin):
    pass
print(MyList.mro())
#[<class '__main__.MyList'>, <class 'list'>,
# <class '__main__.EvenLengthMixin'>, <class 'object'>]
x = MyList([1, 2, 3])
print(x.even_length()) # False
x.append(4)
print(x.even_length()) # True
```
```python
class EvenLengthMixin:
    def even_length(self):
        return len(self) % 2 == 0
class MyList(list, EvenLengthMixin):
    pass
class MyDict(dict, EvenLengthMixin):
    pass
x = MyDict()
x['key'] = 'value'
x['another key'] = 'another value'
print(x.even_length()) # True
```
Что будет если испольвазовать метод с одинаковым именем с методом в родительских классах?

Пример:
```python
class EvenLengthMixin:
    def even_length(self):
        return len(self) % 2 == 0
class MyList(list, EvenLengthMixin):
    def pop(self):
        x = super(MyList, self).pop()
        print('Last value is', x)
        return x
ml = MyList([1, 2, 4, 17])
z = ml.pop() # Last value is 17
print(z) # 17
print(ml) # [1, 2, 4]
```
Иногда нам нужно использовать метод так, будто его нет в нашем классе, а определён в каком-то из родительских. Для этого есть функция super.
Она принимает два аргумента: первый - это класс, родителей которого мы хотим проверить, а второй - это объект, с которым мы хотим проассоциировать метод.

x = super(MyList, self).pop() данная запись эквивалентна list.pop(self).