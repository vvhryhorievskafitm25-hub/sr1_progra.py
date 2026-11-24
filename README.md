
# ============================================================
# СР №1
# РОЗРОБКА КОНСОЛЬНОЇ ПРОГРАМИ НА PYTHON
# Базові конструкції, структури даних, ітератори та генератори
# ============================================================

import math

# ============================================================
# ДОПОМІЖНА ФУНКЦІЯ ДЛЯ ВВЕДЕННЯ ЧИСЕЛ
# ============================================================

def get_number(message):
    """Отримання коректного числового значення від користувача."""
    while True:
        try:
            number = float(input(message))
            if not math.isfinite(number):
                print("Помилка! Введіть скінченне число.")
                continue
            return number
        except ValueError:
            print("Помилка! Потрібно ввести число.")

def get_integer(message):
    """Отримання цілого числа."""
    while True:
        try:
            return int(input(message))
        except ValueError:
            print("Помилка! Введіть ціле число.")

# ============================================================
# ЗАВДАННЯ 1. МАТЕМАТИЧНІ ОБЧИСЛЕННЯ
# ============================================================

def factorial(n):
    """Обчислення факторіала за допомогою циклу."""
    if n < 0:
        raise ValueError("Факторіал від'ємного числа не визначений.")

    result = 1

    for i in range(1, n + 1):
        result *= i

    return result

def mathematical_tasks():
    print("\n--- МАТЕМАТИЧНІ ОБЧИСЛЕННЯ ---")

    n = get_integer("Введіть ціле невід'ємне число: ")

    if n < 0:
        print("Помилка: число повинно бути невід'ємним.")
    elif n > 1000:
        print("Для демонстрації введіть число не більше 1000.")
    else:
        print(f"Факторіал числа {n} дорівнює {factorial(n)}")

    # Перевірка парності за допомогою умовного оператора
    number = get_integer("Введіть число для перевірки парності: ")

    if number % 2 == 0:
        print(f"Число {number} є парним.")
    else:
        print(f"Число {number} є непарним.")

    # Обчислення суми чисел за допомогою циклу
    limit = get_integer("Введіть межу для обчислення суми від 1 до N: ")

    if limit < 1:
        print("Межа повинна бути додатною.")
    else:
        total = 0

        for i in range(1, limit + 1):
            total += i

        print(f"Сума чисел від 1 до {limit} дорівнює {total}")

# ============================================================
# ЗАВДАННЯ 2. ГЕОМЕТРИЧНІ ФІГУРИ
# ============================================================

def geometry_tasks():
    print("\n--- ГЕОМЕТРИЧНІ ОБЧИСЛЕННЯ ---")
    print("1. Площа та довжина кола")
    print("2. Площа та периметр прямокутника")
    print("3. Площа трикутника")

    choice = input("Оберіть фігуру: ")

    if choice == "1":
        radius = get_number("Введіть радіус кола: ")

        if radius <= 0:
            print("Радіус повинен бути додатним.")
        else:
            area = math.pi * radius ** 2
            circumference = 2 * math.pi * radius

            print(f"Площа кола: {area:.2f}")
            print(f"Довжина кола: {circumference:.2f}")

    elif choice == "2":
        a = get_number("Введіть довжину прямокутника: ")
        b = get_number("Введіть ширину прямокутника: ")

        if a <= 0 or b <= 0:
            print("Сторони повинні бути додатними.")
        else:
            area = a * b
            perimeter = 2 * (a + b)

            print(f"Площа прямокутника: {area:.2f}")
            print(f"Периметр прямокутника: {perimeter:.2f}")

    elif choice == "3":
        a = get_number("Введіть першу сторону: ")
        b = get_number("Введіть другу сторону: ")
        c = get_number("Введіть третю сторону: ")

        if a <= 0 or b <= 0 or c <= 0:
            print("Сторони повинні бути додатними.")
        elif a + b <= c or a + c <= b or b + c <= a:
            print("Трикутник із такими сторонами не існує.")
        else:
            # Формула Герона
            p = (a + b + c) / 2
            area = math.sqrt(p * (p - a) * (p - b) * (p - c))

            print(f"Півпериметр трикутника: {p:.2f}")
            print(f"Площа трикутника: {area:.2f}")

    else:
        print("Невірний пункт меню.")

# ============================================================
# ЗАВДАННЯ 3. ТИПИ ДАНИХ ТА СТРУКТУРИ ДАНИХ
# ============================================================

def data_structures():
    print("\n--- РОБОТА ЗІ СТРУКТУРАМИ ДАНИХ ---")

    # Змінні різних типів
    name = "Вікторія"
    age = 19
    average_grade = 90.5
    is_student = True

    print("\nОсновні типи даних:")
    print("Рядок:", name, "| Тип:", type(name).__name__)
    print("Ціле число:", age, "| Тип:", type(age).__name__)
    print("Дійсне число:", average_grade,
          "| Тип:", type(average_grade).__name__)
    print("Логічне значення:", is_student,
          "| Тип:", type(is_student).__name__)

    # Список
    grades = [85, 90, 95, 88, 92]

    print("\nСписок оцінок:", grades)
    print("Перша оцінка:", grades[0])
    print("Кількість оцінок:", len(grades))
    print("Середній бал:", sum(grades) / len(grades))

    grades.append(97)
    print("Список після додавання оцінки:", grades)

    # Кортеж
    subjects = ("Python", "Математика", "Кібербезпека")

    print("\nКортеж предметів:", subjects)
    print("Перший предмет:", subjects[0])

    # Словник
    student = {
        "name": "Вікторія",
        "age": 19,
        "group": "БІКСб-2-25-4.О.д",
        "average_grade": 90.5
    }

    print("\nІнформація про студента:")
    for key, value in student.items():
        print(f"{key}: {value}")

    # Додавання нового елемента до словника
    student["status"] = "Студентка"

    print("\nСловник після оновлення:")
    print(student)

# ============================================================
# ЗАВДАННЯ 4. СТВОРЕННЯ ВЛАСНОГО ІТЕРАТОРА
# ============================================================

class NumberIterator:
    """Ітератор для послідовного перебору чисел."""

    def __init__(self, start, stop):
        self.current = start
        self.stop = stop

    def __iter__(self):
        return self

    def __next__(self):
        if self.current >= self.stop:
            raise StopIteration

        value = self.current
        self.current += 1

        return value

def iterator_task():
    print("\n--- РОБОТА З ІТЕРАТОРОМ ---")

    iterator = NumberIterator(1, 6)

    print("Елементи ітератора:")

    for number in iterator:
        print(number, end=" ")

    print("\nПеребір списку за допомогою iter() та next():")

    numbers = [10, 20, 30, 40]
    iterator = iter(numbers)

    try:
        while True:
            print(next(iterator))
    except StopIteration:
        print("Усі елементи списку переглянуто.")

# ============================================================
# ЗАВДАННЯ 5. СТВОРЕННЯ ТА ВИКОРИСТАННЯ ГЕНЕРАТОРІВ
# ============================================================

def fibonacci_generator(n):
    """Генератор перших n чисел Фібоначчі."""

    a, b = 0, 1

    for _ in range(n):
        yield a
        a, b = b, a + b

def even_numbers_generator(start, stop):
    """Генератор парних чисел у заданому діапазоні."""

    for number in range(start, stop + 1):
        if number % 2 == 0:
            yield number

def generator_task():
    print("\n--- РОБОТА З ГЕНЕРАТОРАМИ ---")

    n = get_integer("Скільки чисел Фібоначчі вивести? ")

    if n < 0:
        print("Кількість не може бути від'ємною.")
    else:
        print("Числа Фібоначчі:")
        print(list(fibonacci_generator(n)))

    start = get_integer("\nВведіть початок діапазону: ")
    stop = get_integer("Введіть кінець діапазону: ")

    if start > stop:
        print("Початок діапазону не може бути більшим за кінець.")
    else:
        print("Парні числа:")
        print(list(even_numbers_generator(start, stop)))

# ============================================================
# ГОЛОВНЕ МЕНЮ ПРОГРАМИ
# ============================================================

def main():
    while True:
        print("\n" + "=" * 55)
        print("          КОНСОЛЬНА ПРОГРАМА PYTHON")
        print("=" * 55)

        print("1. Математичні обчислення")
        print("2. Геометричні фігури")
        print("3. Типи та структури даних")
        print("4. Робота з ітераторами")
        print("5. Робота з генераторами")
        print("0. Вихід із програми")

        choice = input("\nОберіть пункт меню: ")

        if choice == "1":
            mathematical_tasks()

        elif choice == "2":
            geometry_tasks()

        elif choice == "3":
            data_structures()

        elif choice == "4":
            iterator_task()

        elif choice == "5":
            generator_task()

        elif choice == "0":
            print("\nРоботу програми завершено. До побачення!")
            break

        else:
            print("Невірний вибір. Спробуйте ще раз.")

# Запуск програми
if __name__ == "__main__":
    main()
