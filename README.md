# Звіт до роботи
## Тема: _згідно теми_
### Мета роботи: _згідно теми_

---
### Виконання роботи
* Результати виконання завдання *1...N*;
    1. Розробили/Створили ...
    1. Програма вивела значення ...
    1. Отримано наступні результати ...
    1. Навчились ...
* з використанням URL ![alt text](https://github.com/BobasB/it_college/raw/main/reports/pictures/logo-lit.jpg "ІТ Коледж")
    
* через локальні шляхи ![alt text](./pictures/logo-lit.jpg "ІТ Коледж")

* import numpy as np

def homework(message):
    print("\n>>>>>", message, "\n")

# Визначення однорідного масиву
lst = [[3.4, 8.7, 9.9],
       [1.1, -7.8, -0.7],
       [4.1, 12.3, 4.8]]

A = np.array(lst, dtype=np.int8)
print(f"Отриманий масив A має вигляд:\n{repr(A)}")

B = np.array(lst, dtype=np.float16)
print(f"Отриманий масив B має вигляд:\n{repr(B)}")

homework("Згадуючи ООП, що робить функція repr?")
homework("У чому різниця між масивами A і B?")

# Задаємо свій тип даних
dt = np.dtype([('name', np.compat.unicode, 20), ('mark', np.int8)])
arr = [
    ("Bohdan", 4),
    ("Marta", 5),
    ("Noname", 0)
]
C = np.array(arr, dtype=dt)
print(f"Отриманий масив C має вигляд:\n{C}")
print(f"Доступитись до певної колонки тепер можна за її іменем: {C['mark']}")

homework(f"Імена присутні в масиві: {C.dtype.names}")

# Збереження та завантаження з файлу
print("Вихідний масив: ", C)
np.savez("my_mass.npz", my_mass=C)
D = np.load("my_mass.npz")
print("Прочитаний з файлу: ", D["my_mass"])

# Запис та читання у форматі CSV
filename = "temp.csv"
print(f"Записуємо у CSV файл {filename} значення: {C}")
np.savetxt(filename, C, fmt="%s,%d", header="name,mark", delimiter=",")

import os
print(f"Перевіряємо чи файл {filename} створився: {os.listdir()}")

print("Читаємо файл за допомогою оператора with та методу readlines")
with open(filename) as f:
    D = f.readlines()

print(f"Прочитаний файл:\n {D} \n- як бачимо - {len(D)} елементи є стрічками {type(D[0])}.")

D = np.genfromtxt(filename, dtype=dt, delimiter=",")
print(f"Зчитане значення з файла:\n {D}, як бачимо - {D.size} елементи це {type(D[0])} \n- вбудований клас бібліотеки numpy.")
print(f"Доступитись до певного елемента можна наступним чином, наприклад імя першого елементу: {D[0]['name']}")

# Додаткове поле "group"
# Доповнюємо масив новим полем
C = np.insert(C, 2, values=["Group1", "Group2", "Group3"], axis=1, dtype=np.compat.unicode)

# Збереження та вичитування даних
np.savetxt(filename, C, fmt="%s,%d,%s", header="name,mark,group", delimiter=",")
E = np.genfromtxt(filename, dtype=[('name', np.compat.unicode, 20), ('mark', np.int8), ('group', np.compat.unicode, 10)], delimiter=",")

print(f"Масив з додатковим полем має вигляд:\n{E}")
print(f"Прочитане ім'я з масиву: {E[0]['name']}")
def homework(message):
    print("\n>>>>>", message, "\n")

# Задані масиви A і B
A = np.array([[1, 2, 3], [2, 2, 2], [3, 3, 3]])
B = np.array([[3, 2, 1], [1, 2, 3], [-1, -2, -3]])

print(f"Маємо два масиви:\n {A} \n {B}")

# Поелементне множення
R = A * B
print(f"Тут виконується поелементне множення:\n {R}")

# Матричне множення
R = np.dot(A, B)
print(f"Тут, масиви перемножуються як матриці:\n {R}")

# Матричне множення (з використанням матриць)
MA = np.mat(A)
MB = np.mat(B)
R = MA * MB
print(f"Тут масиви перетворені на матриці і далі перемножуються:\n {R}")

# Додаткове завдання
A = np.array([[11, 12, 13], [21, 22, 23], [31, 32, 33]])
B = np.array([1, 2, 3])
C = B[:, np.newaxis]

print(f"Вектор B є рядком {B.shape}: {B} тому додавання буде по рядках:\n {A + B}")

print(f"""Вектор C є стовпцем {C.shape}:
{C}
тому додавання буде по стовпцям:
{A + C}""")

print(f"У випадку додавання рядка до стовпця буде матриця, в якій доповнюються рядки і стовпці:\n {B + C}")

# Операції з масивами D та Z
D = np.ones(3)
Z = np.zeros((3, 1))

print(f"""
При конкатенації рядків маємо: {np.concatenate((D, D))}
При конкатенації стовпців маємо:\n{np.concatenate((Z, Z))}
Масив D {D} має розмірність {D.shape} тому може виконати операцію конкатенації з В {B} розмірністю {B.shape}:
{np.concatenate((B, D))}
Для конкатенації з С
{C}
де С має розмірність = {C.shape} потрібно змінити розмірність D = {D.shape}
Це можна ось так:
{D[:, np.newaxis].shape}
або
{D.reshape((3, 1)).shape}
в результаті ми можемо виконати конкатенацію:
{np.concatenate((C, D.reshape((3, 1))))}
При повторенні D {D} 2 рази для рядків та 3 для стовпців будемо мати:
{np.tile(D, (2, 3))}
Як бачимо, конкатенація та повторення є дещо схожими у деяких випадках:
- конкатенація: {np.concatenate((D, D))}
- повторення: {np.tile(D, 2)}
Також можна перетворити двовимірний масив A розмірністю {A.shape} на рядок: {A.flatten()} з розмірністю {A.flatten().shape}
""")

# Операції з масивом O
O = np.arange(6).reshape(3, 2)
O_r = O.reshape((2, 3))
O_f = O.flatten()
O_t = O.transpose()
O_fl = np.flip(O)
O_fa = np.flip(O, axis=1)

print(f"""{O}
Змінити розмірність shape {O.shape} на {O_r.shape} при цьому розмір size {O.size} = {O_r.size} та ndim {np.ndim(O)} = {np.ndim(O_r)}:
{O_r}
Також можна перетворити {np.ndim(O)}-х вимірний масив розмірністю {O.shape} на рядок:
{O_f} 
з розмірністю {O_f.shape} при цьому size = {O_f.size} та ndim стане {np.ndim(O_f)}-х вимірним 
Або транспонувати масив щоб він став {O_t.shape} але зверніть увагу на елементи:
{O_t}
Можна обернути масив (обертаємо по стовпцях і рядках одночасно): 
{O_fl}
Або обернути лише елементи в кожному рядку (або стовпці):
{O_fa}
""")

# Виконання homework
homework("Виконано завдання.")
---
### Висновок:
> у висновку потрібно відповісти на запитання:

- :question: Що зроблено в роботі;
Поелементне множення та матричне множення,Додаткове завдання,Операції з масивами D та Z.
- :question: Чи досягнуто мети роботи;
Так
- :question: Які нові знання отримано;
Поелементне множення та матричне множення,Додаткове завдання,Операції з масивами D та Z.
- :question: Чи вдалось відповісти на всі питання задані в ході роботи;
Так
- :question: Чи виникли складності у виконанні завдання;
Ні
- :question: Чи подобається такий формат здачі роботи (Feedback);
Так
- :question: Побажання для покращення (Suggestions);
Немає