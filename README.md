# Kakashki_v_karmashki

LabWork4

import random

# 5.1 Запрос количества элементов и заполнение случайными числами
n = int(input("Введите количество элементов списка: "))
random_list = [random.randint(0, 100) for _ in range(n)]
for index, value in enumerate(random_list):
    print(f"{index}: {value}")

# 5.2 Заполнение списка пользователем
n = int(input("Введите количество элементов нового списка: "))
user_list = [input(f"Введите элемент {i+1}: ") for i in range(n)]
print("Список:", " ".join(user_list))

# 5.3 Добавление четных элементов из одного списка в другой
filtered_list = [num for num in random_list if num % 2 == 0]
user_list.extend(filtered_list)
print("Объединенный список:", " ".join(map(str, user_list)))

# 5.4 Сортировка списка по убыванию без циклов
sorted_list = sorted(random_list, reverse=True)
print("Отсортированный список:", " ".join(map(str, sorted_list)))

# 5.5 Поиск и удаление числа
search_num = int(input("Введите число для поиска и удаления: "))
count = random_list.count(search_num)
random_list = list(filter(lambda x: x != search_num, random_list))
print(f"Число {search_num} встречается {count} раз(а).")
print("Обновленный список:", " ".join(map(str, random_list)))

# 5.6 Вставка элементов по индексу
n = int(input("Сколько элементов добавить в список? "))
for _ in range(n):
    index = int(input("Введите индекс для вставки: "))
    value = input("Введите значение: ")
    if 0 <= index <= len(random_list):
        random_list.insert(index, value)
print("Список после вставки:", " ".join(map(str, random_list)))

# 5.7 Создание словаря с кодами и названиями книг
book_count = int(input("Сколько книг добавить в словарь? "))
books = {input("Введите код книги: "): input("Введите название книги: ") for _ in range(book_count)}

# 5.8 Вывод ключей, значений и поиск по ключу
print("Ключи:", " ".join(books.keys()))
print("Значения:", " ".join(books.values()))
search_key = input("Введите код книги для поиска: ")
print("Название книги:", books.get(search_key, "Книга не найдена"))


LabWork5

import re

# 5.1 Работа со строкой
string = input("Введите строку: ")
print((string + '\n') * 5, end='')
print(f"Длина строки: {len(string)}")
for index, char in enumerate(string):
    print(f"{index}: {char}")
print("Каждый второй символ с позицией:")
print(" ".join([f"{i+1}:{char}" for i, char in enumerate(string) if i % 2 != 0]))

# 5.2 Вывод подстроки по индексам
start, end = map(int, input("Введите начальную и конечную позиции: ").split())
print("Подстрока:", string[start:end])

# 5.3 Замена первого и последнего символа
print("Измененная строка:", "#" + string[1:-1] + "#" if len(string) > 1 else "#")

# 5.4 Проверка состава строки
if string.isdigit():
    print("Строка состоит только из цифр.")
elif string.isalpha():
    case_info = "только из строчных" if string.islower() else "только из прописных"
    print(f"Строка состоит только из букв ({case_info}).")
elif string.isalnum():
    print("Строка состоит из букв и цифр.")
else:
    print("Строка содержит другие символы.")

# 5.5 Разделение и объединение подстрок
words = string.split()
print("Новая строка:", ", ".join(words))

# 5.6 Поиск подстроки в строке
substr, main_str = input("Введите подстроку: "), input("Введите основную строку: ")
indices = [m.start() for m in re.finditer(re.escape(substr), main_str)]
print(f"Подстрока встречается {len(indices)} раз(а) на позициях: {', '.join(map(str, indices))}")

# 5.7 Проверка на палиндром
word = input("Введите слово: ").lower()
print("Палиндром" if word == word[::-1] else "Не палиндром")

# 5.8 Замена двойных пробелов
cleaned_string = re.sub(r'\s+', ' ', string)
print("Строка после удаления лишних пробелов:", cleaned_string)

LabWork6

import math

# 5.1 Деление с обработкой исключения
try:
    a = float(input("Введите число a: "))
    b = float(input("Введите число b: "))
    result = a / b
    print(f"Результат деления: {result}")
except ZeroDivisionError:
    print("Ошибка: деление на 0 невозможно.")

# 5.2 Деление с повторным вводом при нуле
while True:
    try:
        a = float(input("Введите число a: "))
        b = float(input("Введите число b: "))
        if b == 0:
            raise ValueError("Ошибка: 0 вводить нельзя. Попробуйте снова.")
        break
    except ValueError as e:
        print(e)
finally:
    print(f"Результат деления: {a / b}")

# 5.3 Вычисление выражения с обработкой исключений
try:
    x = float(input("Введите x: "))
    y = float(input("Введите y: "))
    z = float(input("Введите z: "))
    numerator = math.sqrt(x + y + z)
    denominator = (x - y + z) ** 2
    result = numerator / denominator
    print(f"Результат выражения: {result}")
except ZeroDivisionError:
    print("Ошибка: деление на 0 невозможно.")
except ValueError:
    print("Ошибка: введены некорректные данные.")

# 5.4 Добавление генерации исключения при отрицательном корне
try:
    x = float(input("Введите x: "))
    y = float(input("Введите y: "))
    z = float(input("Введите z: "))
    numerator = x + y + z
    if numerator < 0:
        raise ValueError("Ошибка: под корнем оказалось отрицательное число.")
    denominator = (x - y + z) ** 2
    if denominator == 0:
        raise ZeroDivisionError("Ошибка: деление на 0 невозможно.")
    result = math.sqrt(numerator) / denominator
    print(f"Результат выражения: {result}")
except ValueError as e:
    print(e)
except ZeroDivisionError as e:
    print(e)
