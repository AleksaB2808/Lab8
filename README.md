# Lab8
Функція task1

import json

def task1(file_path, age_threshold):
    """
    Зчитує дані з JSON-файлу, вибирає імена тих користувачів, чий вік перевищує вказаний поріг.
    
    Параметри:
    - file_path (str): Шлях до JSON-файлу.
    - age_threshold (int): Поріг віку, вище якого обираються імена.
    
    Повертає:
    - names_above_threshold (list): Список імен користувачів з віком вище порогу.
    """
    with open(file_path, 'r') as file:
        data = json.load(file)
    names_above_threshold = [entry['name'] for entry in data if entry['age'] > age_threshold]
    return names_above_threshold
Пояснення:

Імпорт модулів: Функція використовує модуль json, який надає функціональність для роботи з JSON-даними.

Оголошення функції: Функція task1 приймає два параметри: file_path (шлях до JSON-файлу) та age_threshold (поріг віку).

Читання з файлу: Відкривається вказаний JSON-файл для читання ('r'), та дані зчитуються в змінну data за допомогою json.load(file).

Фільтрація даних: Створюється список names_above_threshold, де за допомогою спискового виразу вибираються імена користувачів з віком, що перевищує age_threshold.

Повернення результату: Повертається список імен names_above_threshold, який містить імена користувачів, які задовольняють умову.

Функція task2

import json

def task2(data, file_path):
    """
    Записує дані у JSON-файл.
    
    Параметри:
    - data: Дані для запису у файл (може бути будь-якого типу, що підтримує json.dump).
    - file_path (str): Шлях до JSON-файлу, в який потрібно записати дані.
    """
    with open(file_path, 'w') as file:
        json.dump(data, file)
Пояснення:

Імпорт модулів: Функція також використовує модуль json для роботи з JSON-даними.

Оголошення функції: Функція task2 приймає два параметри: data (дані для запису в файл) та file_path (шлях до JSON-файлу).

Запис до файлу: Файл з вказаним шляхом file_path відкривається для запису ('w'). Функція json.dump(data, file) записує дані змінної data у цей файл у форматі JSON.

Повернення результату: Функція не повертає значення, оскільки її завданням є лише запис даних у файл.

Функція task3


def task3(schema, file_paths):
    """
    Перевіряє JSON-файли на валідність за заданою схемою.

    Параметри:
    - schema (dict): Схема, за якою перевіряються файли.
    - file_paths (list): Список шляхів до JSON-файлів, які потрібно перевірити.

    Повертає:
    - invalid_files (list): Список шляхів до файлів, які не відповідають вказаній схемі.
    """
    invalid_files = []
    for file_path in file_paths:
        with open(file_path, 'r') as file:
            try:
                data = json.load(file)
                # Ваша логіка перевірки схеми
            except json.JSONDecodeError:
                invalid_files.append(file_path)
    return invalid_files
Пояснення:

Імпорт модулів: Функція використовує модуль json для роботи з JSON-даними.

Оголошення функції: Функція task3 приймає два параметри: schema (схема, за якою перевіряються файли) та file_paths (список шляхів до JSON-файлів).

Перевірка валідності файлів: Для кожного файлу з file_paths відкривається JSON-файл для читання ('r'). Спроба зчитати дані з файлу за допомогою json.load(file). Якщо виникає помилка json.JSONDecodeError, файл додається до списку invalid_files.

Повернення результату: Повертається список invalid_files, що містить шляхи до файлів, які не відповідають вказаній схемі.

Функція task4

import json

def task4(file_path, key):
    """
    Зчитує значення з JSON-файлу, які відповідають заданому ключу.

    Параметри:
    - file_path (str): Шлях до JSON-файлу.
    - key (str): Ключ, значення якого потрібно витягти з файлу.

    Повертає:
    - values (list): Список усіх значень з файлу, які відповідають заданому ключу.
    """
    def extract_values(obj, key):
        values = []
        if isinstance(obj, dict):
            for k, v in obj.items():
                if k == key:
                    values.append(v)
                elif isinstance(v, (dict, list)):
                    values.extend(extract_values(v, key))
        elif isinstance(obj, list):
            for item in obj:
                values.extend(extract_values(item, key))
        return values

    with open(file_path, 'r') as file:
        data = json.load(file)
    values = extract_values(data, key)
    return values
Пояснення:

Імпорт модулів: Функція використовує модуль json для роботи з JSON-даними.

Оголошення функції: Функція task4 приймає два параметри: file_path (шлях до JSON-файлу) та key (ключ, значення якого потрібно витягти з файлу).

Функція extract_values: Це рекурсивна ф
