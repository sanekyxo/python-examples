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