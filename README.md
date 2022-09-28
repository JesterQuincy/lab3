# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Бабенко Александр Алексеевич
- 2072118
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Ознакомиться с основными операторами зыка Python на примере реализации линейной регрессии.

## Задание 1
Установил Visual Studio Code и вывел в консоль "Hello World"
![image](https://user-images.githubusercontent.com/114616168/192889596-9d42707c-cef0-43b3-9248-8739fabf1dbe.png)
![image](https://user-images.githubusercontent.com/114616168/192894808-55dde89d-abf5-4f4f-affb-2c1f6e078f6e.png)

Установил Unity


![image](https://user-images.githubusercontent.com/114616168/192891129-f93a67d0-8003-4fe8-96df-1bd2c8b00bf9.png)

Создал папку для скриптов, пустой объект, написал код и вывел в консоль:
![image](https://user-images.githubusercontent.com/114616168/192891352-346bbe06-5e49-4123-9b91-4471b70e6e8b.png)
![image](https://user-images.githubusercontent.com/114616168/192891264-26c20bd8-2c1b-438a-9c08-b94c10955eae.png)
## Задание 2
Пошагово выполнить каждый пункт раздела "ход работы" с описанием и примерами реализации задач
Ход работы:

1.Произвести подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.
![image](https://user-images.githubusercontent.com/114616168/192896388-9ec2a6db-751a-4320-be3f-0bdefd66411b.png)

2. Определите связанные функции. Функция модели: определяет модель линейной регрессии wx+b. Функция потерь: функция потерь среднеквадратичной ошибки. Функция оптимизации: метод градиентного спуска для нахождения частных производных w и b.
![image](https://user-images.githubusercontent.com/114616168/192899067-85ef0f2f-113e-46b4-8076-35325d1589bb.png)

3.Начать итерацию 

## Задание 3
Шаг 1 Инициализация и модель итеративной оптимизации 
![image](https://user-images.githubusercontent.com/114616168/192899185-de2c6407-94b8-4572-bcf4-93531712159e.png)
![image](https://user-images.githubusercontent.com/114616168/192899214-12a6b192-aff9-484b-a3f2-fa9449dc2a87.png)
Шаг 2 На второй итерации отображаются значения параметров, значения.
![image](https://user-images.githubusercontent.com/114616168/192899356-dafc0461-ed3e-4128-ae90-5648b5feb3e4.png)
Шаг 3 Третья итерация показывает значения параметров, значения потерь и визуализацию после итерации 

![image](https://user-images.githubusercontent.com/114616168/192903785-f12a1b47-6778-42b7-b362-e6c601883f56.png)

Шаг 4 На четвертой итерации отображаются значения параметров, значения потерь и эффекты визуализации 
![image](https://user-images.githubusercontent.com/114616168/192899850-3bd2b7b0-4dae-4da5-88ba-5385c68b5a44.png)

Шаг 5 Пятая итерация показывает значение параметра, значение потерь и эффект визуализации после итерации 
![image](https://user-images.githubusercontent.com/114616168/192899938-980e2e23-bae0-47c0-8c40-d5e31c5c3b78.png)

Шаг 6 10000-я итерация, показывающая значения параметров, потери и визуализацию после итерации 
![image](https://user-images.githubusercontent.com/114616168/192899989-e2583c79-79a1-42a1-8346-f06a04640476.png)




Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.

Да, должна, так при большем количестве итераций loss уменьшается, что показывает, что модель становится более точной, пример:

Тут совершена 1 итерация
![image](https://user-images.githubusercontent.com/114616168/192901292-25eaa1db-191b-4556-972f-11af6a767301.png)
![image](https://user-images.githubusercontent.com/114616168/192901389-16cb9b90-7af1-4b01-adf5-c46b10b6035c.png)
Тут 10 тысяч итераций
![image](https://user-images.githubusercontent.com/114616168/192901478-58f26601-a910-48bd-96f5-adf0b3bd4043.png)


### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.
![Screenshot_1](https://user-images.githubusercontent.com/114616168/192902171-900100fe-b041-470e-856a-e117af6eae5a.png)
При увелечении параметра lr модель становится более быстрой и обучается за меньшее количество итерций, но точность оставляет желать лучшего:

Lr = 0.000001 

![image](https://user-images.githubusercontent.com/114616168/192902430-3826d413-dcf2-4ea4-8070-c04a7a09cd66.png)

Lr = 0.0001 

![image](https://user-images.githubusercontent.com/114616168/192903020-c1272be4-4f47-4b52-a3e8-b2ece059281a.png)

## Выводы
Узнал новые программы, немного про обучение моделей и параметры которые используется.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
