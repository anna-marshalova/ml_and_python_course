### **Объектно-Ориентированное Программирование (ООП) в Python**

#### **Цель урока:**  
- Понять основные концепции ООП: **классы, объекты, инкапсуляция, наследование, полиморфизм**.  
- Научиться писать код, используя принципы ООП.  
- Пройти 10 практических заданий с автоматической проверкой.  

Каждый раздел содержит объяснение, пример кода и задание. Вам нужно дополнить код так, чтобы все `assert`-проверки успешно выполнялись.  

---

## **1. Классы и объекты**  
Класс — это шаблон для создания объектов. Объект — это экземпляр класса.

### **Пример:**
```python
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed
    
    def bark(self):
        return f"{self.name} говорит: Гав!"
        
my_dog = Dog("Барсик", "Кавказец")
print(my_dog.bark())  # Барсик говорит: Гав!
```

### **Задание 1:** Создайте класс `Cat` с атрибутами `name` и `age`, а также методом `meow`, который выводит `"Имя говорит: Мяу!"`.

```python
class Cat:
    # TODO: реализуйте класс Cat
    pass

# Проверка
cat = Cat("Мурка", 3)
assert cat.name == "Мурка"
assert cat.age == 3
assert cat.meow() == "Мурка говорит: Мяу!"
```

---

# **2. Инкапсуляция: защита данных внутри класса**  
Инкапсуляция помогает **защитить данные** от случайного или преднамеренного изменения извне. Например, в банковском аккаунте нельзя просто так поменять баланс, он должен изменяться только через методы пополнения и снятия денег.

### **Пример без инкапсуляции (Плохой код)**
```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance  # Открытая переменная
    
account = BankAccount(1000)
account.balance = -5000  # Ошибка! Мы изменили баланс напрямую
print(account.balance)  # -5000 (это неправильно!)
```
Здесь пользователь **может случайно или намеренно изменить баланс** на отрицательное значение, что не должно быть возможным.

### **Правильный вариант с инкапсуляцией**
```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Приватная переменная

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
        else:
            print("Недостаточно средств!")

    def get_balance(self):
        return self.__balance  # Возвращаем баланс безопасным способом

account = BankAccount(1000)
account.deposit(500)
account.withdraw(200)
print(account.get_balance())  # 1300

# Попробуем напрямую изменить баланс
# account.__balance = -5000  # Ошибка! Доступ запрещен
```
**Почему так лучше?**
- Теперь `__balance` **нельзя изменить напрямую**.
- Баланс можно менять только через методы `deposit` и `withdraw`, которые **проверяют корректность операции**.

## **3. Наследование**  
Позволяет одному классу унаследовать свойства и методы другого.

### **Пример:**
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "Этот животный издает звук"

class Dog(Animal):
    def speak(self):
        return f"{self.name} говорит: Гав!"
```

### **Задание 3:** Реализуйте класс `Bird`, унаследовав его от `Animal`, и добавьте метод `speak`, который возвращает `"Чирик!"`.

```python
class Animal:
    # Базовый класс
    pass

class Bird(Animal):
    # TODO: создайте подкласс
    pass

# Проверка
bird = Bird("Попугай")
assert bird.name == "Попугай"
assert bird.speak() == "Чирик!"
```

---

## **4. Полиморфизм: единый интерфейс для разных классов**  
Полиморфизм позволяет использовать **одинаковые методы** для разных типов объектов. Это удобно, когда у вас есть **разные классы с похожим поведением**.

### **Пример без полиморфизма (много дублирования кода)**
```python
class Dog:
    def make_sound(self):
        return "Гав!"

class Cat:
    def make_sound(self):
        return "Мяу!"

def animal_sound(animal):
    if isinstance(animal, Dog):
        return animal.make_sound()
    elif isinstance(animal, Cat):
        return animal.make_sound()
    
print(animal_sound(Dog()))  # Гав!
print(animal_sound(Cat()))  # Мяу!
```
Этот код **неудобен**, потому что нам приходится **явно проверять тип объекта** и добавлять новый `if` для каждого нового животного.

### **Используем полиморфизм**
```python
class Animal:
    def make_sound(self):
        raise NotImplementedError("Этот метод должен быть переопределен")

class Dog(Animal):
    def make_sound(self):
        return "Гав!"

class Cat(Animal):
    def make_sound(self):
        return "Мяу!"

class Cow(Animal):
    def make_sound(self):
        return "Муу!"

def animal_sound(animal: Animal):
    return animal.make_sound()

print(animal_sound(Dog()))  # Гав!
print(animal_sound(Cat()))  # Мяу!
print(animal_sound(Cow()))  # Муу!
```

**Почему так лучше?**
- Функция `animal_sound` работает с **любыми объектами**, унаследованными от `Animal`, без `if`.
- Если добавится новое животное, просто создаем новый класс с `make_sound`, и код будет **автоматически работать**. 

Полиморфизм делает код **более гибким** и **менее зависимым от конкретных классов**. Это полезно, если у вас много объектов с похожими методами.

---

### **Задание 4:** Создайте `Parrot`, который переопределяет `speak`, чтобы он возвращал `"Попугай говорит: Привет!"`.

```python
class Bird:
    # Базовый класс
    pass

class Parrot(Bird):
    # TODO: переопределите метод speak
    pass

# Проверка
parrot = Parrot()
assert parrot.speak() == "Попугай говорит: Привет!"
```

---

## **5. Дополнительные задания**

### **Задание 5:** Реализуйте класс `Rectangle` с методами `area` (площадь) и `perimeter` (периметр).

```python
class Rectangle:
    # TODO: реализуйте класс
    pass

# Проверка
rect = Rectangle(3, 4)
assert rect.area() == 12
assert rect.perimeter() == 14
```

---

### **Задание 6:** Создайте класс `Car` с инкапсулированной скоростью (`__speed`) и методами `accelerate` и `brake`.

```python
class Car:
    # TODO: реализуйте класс
    pass

# Проверка
car = Car(60)
car.accelerate(20)
assert car.get_speed() == 80
car.brake(50)
assert car.get_speed() == 30
```

---

### **Задание 7:** Класс `Student` с методом `get_average_grade`.

```python
class Student:
    # TODO: реализуйте класс
    pass

# Проверка
student = Student("Иван", [4, 5, 3, 5])
assert student.get_average_grade() == 4.25
```

---

### **Задание 8:** Класс `Library` с методами `add_book`, `remove_book`, `list_books`.

```python
class Library:
    # TODO: реализуйте класс
    pass

# Проверка
library = Library()
library.add_book("1984")
library.add_book("Гарри Поттер")
assert "1984" in library.list_books()
library.remove_book("1984")
assert "1984" not in library.list_books()
```

---

### **Задание 9:** Класс `Employee` с расчетом зарплаты.

```python
class Employee:
    # TODO: реализуйте класс
    pass

# Проверка
employee = Employee("Анна", 50000)
employee.increase_salary(5000)
assert employee.salary == 55000
```

---

### **Задание 10:** Класс `ShoppingCart` для управления покупками.

```python
class ShoppingCart:
    # TODO: реализуйте класс
    pass

# Проверка
cart = ShoppingCart()
cart.add_item("яблоко", 3, 10)
cart.add_item("банан", 2, 5)
assert cart.get_total_price() == 40
cart.remove_item("яблоко")
assert cart.get_total_price() == 10
```