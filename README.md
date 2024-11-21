# Задача №1:
from pprint import pprint
cook_book = {}
with open('recipes.txt', 'rt', encoding='utf-8') as file:
    dishes = ''
    for x in file:
        x = x.strip()
        if x.isdigit():
            continue
        elif x and '|' not in x:
            cook_book[x] = []
            dishes = x
        elif x and '|' in x:
            a, b, c = x.split(" | ")
            cook_book.get(dishes).append(dict(ingredient_name=a, quantity=int(b), measure=c))

pprint(cook_book)


# Задача №2:
def get_shop_list_by_dishes(dishes_list, person_count):
    shop_list = {}
    for dish in dishes_list:
        if dish in cook_book:
            for ingredient in cook_book[dish]:
                if ingredient['ingredient_name'] in shop_list:
                    shop_list[ingredient['ingredient_name']]['quantity'] += ingredient['quantity'] * person_count
                else:
                    shop_list[ingredient['ingredient_name']] = ({'measure': ingredient['measure'], 'quantity':
                                                                (ingredient['quantity'] * person_count)})
        else:
            print('Такого блюда нет в книге')
    return shop_list


pprint(get_shop_list_by_dishes(['Фахитос', 'Омлет'], 2))

# Задача №3:
# from pprint import pprint
import os  # для возможности задать значение переменной name_1(2 or 3).
with open('1.txt', 'r', encoding='utf-8') as file_1:
    file_list_1 = file_1.readlines()  # делаю список
    # pprint(file_list_1)
    name_1 = os.path.basename(r'D:\света\День рождения 2024\обучение2024\1.txt')
    # print(name_1)

with open('2.txt', 'r', encoding='utf-8') as file_2:
    file_list_2 = file_2.readlines()
    name_2 = os.path.basename(r'D:\света\День рождения 2024\обучение2024\2.txt')

with open('3.txt', 'r', encoding='utf-8') as file_3:
    file_list_3 = file_3.readlines()
    name_3 = os.path.basename(r'D:\света\День рождения 2024\обучение2024\3.txt')

temp_dict = {name_1: file_list_1, name_2: file_list_2, name_3: file_list_3}
sorted_tuple = sorted(temp_dict.items(), key=lambda x: len(x[1]))  # создаю кортеж и сортирую при помощи лямбда
# по длине списка(количество строк).

sorted_dict = dict(sorted_tuple)  # создаю обратно словарь.

#
with open('result_text.txt', 'w', encoding='utf-8') as final_file:
    for key, value in sorted_dict.items():
        print(key)
        final_file.write('\n')
        final_file.writelines(sorted_dict[key])
        for i in range(len(value)):
            print(f'Строка {i + 1} файла {key}')
            final_file.write(f'Строка {i + 1} файла {key} - {value[i]}')
