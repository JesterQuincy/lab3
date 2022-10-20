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
Попробывать экспортировать данные между программами

## Задание 1 
·	Создал новый пустой 3D проект на Unity.
·	Скачал папку с ML агентом
·	В созданный проект добавьте ML Agent, выбрав Window - Package Manager - Add Package from disk. Последовательно добавил .json – файлы:
o	ml-agents-release_19 / com,unity.ml-agents / package.json
o	ml-agents-release_19 / com,unity.ml-agents.extensions / package.json
![image](https://user-images.githubusercontent.com/114616168/196903982-185e9bb8-6071-499f-91b6-34cbc0e610e6.png)

Видим строку ML Agent.
![image](https://user-images.githubusercontent.com/114616168/196904119-34db1dab-d17e-413b-b967-2c235e723555.png)

·	Далее запускаем Anaconda Prompt для возможности запуска команд через консоль.
·	Далее пишем серию команд для создания и активации нового ML-агента, а также для скачивания необходимых библиотек:
o	mlagents 0.28.0;
o	torch 1.7.1;
Создадем виртуальное окружение.
После этого добавим скрипт шару и еще добавим Decision Requester и Behavior Parameters:
Скрипт:
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;
    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }
    public Transform Target;
    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }
        Target.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target.localPosition);
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(rBody.velocity.x);
        sensor.AddObservation(rBody.velocity.z);
    }
    public float forceMultiplier = 10;
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * forceMultiplier);
        float distanceToTarget = Vector3.Distance(this.transform.localPosition, Target.localPosition);
        if(distanceToTarget < 1.42f)
        {
            SetReward(1.0f);
            EndEpisode();
        }
        else if (this.transform.localPosition.y < 0)
        {
            EndEpisode();
        }
    }
}
```
Запустим работу ml-агена:

![194754553-ec0a1776-2c71-41da-9820-d87992b622eb](https://user-images.githubusercontent.com/114616168/196921043-aa051b5d-f77a-4c79-8895-ee37bf7b5193.png)


Обучил созданные модели

![Screenshot_1](https://user-images.githubusercontent.com/101480666/196696354-f651390d-36ed-4c8d-a92d-105553aade1a.jpg)

![image](https://user-images.githubusercontent.com/114616168/196924307-bba8e8cc-a2a0-4d09-879a-a06dd6b75738.png)



## Задание 2
### Подробно опишите каждую строку файла конфигурации нейронной сети, доступного в папке с файлами проекта по ссылке. Самостоятельно найдите информацию о компонентах Decision Requester, Behavior Parameters, добавленных сфере.

```
behaviors: #Создание списка модель поведения
  RollerBall: #Создание списка отдельного объекта
    trainer_type: ppo #Тип тренажера
      batch_size: 10 #Количество опытов на каждой итерации градиентного спуска. Это всегда должно быть в несколько раз меньше, чем buffer_size. 
      buffer_size: 100 #Количество опыта, которое необходимо собрать перед обновлением
      learning_rate: 3.0e-4 #Начальная скорость обучения 
      beta: 5.0e-4 #Сила регуляризации энтропии, делает политику рандомной
      epsilon: 0.2 #Влияет на то, насколько может расходится старая и новая политика во время обучения
      lambd: 0.99 #Параметр регуляризации (лямбда), используемый при вычислении обобщенной оценки преимуществ (GAE).
      num_epoch: 3 #Количество скрытых проходов через буфер опыта при выполнении оптимизации градиентного спуска.
      learning_rate_schedule: linear #Определяет, как скорость обучения меняется с течением времени. 
    network_settings:
      normalize: false #Применяется ли нормализация к входным данным векторного наблюдения.
      hidden_units: 128 #Количество единиц в скрытых слоях нейронной сети.
      num_layers: 2 #Количество скрытых слоев в нейронной сети. 
    reward_signals: #Награды
      extrinsic: #Внешние награды
        gamma: 0.99 #Коэффициент скидки для будущих вознаграждений, поступающих из среды.
        strength: 1.0 #Коэффициент, на который умножается вознаграждение, предоставляемое средой.
    max_steps: 500000 #Общее количество шагов 
    time_horizon: 64 #Сколько шагов опыта нужно собрать для каждого агента, прежде чем добавлять его в буфер опыта. 
    summary_freq: 10000 #Количество опыта, которое необходимо собрать перед созданием и отображением статистики обучения. 
```
Компонент DecisionRequester предоставляет удобный и гибкий способ запуска процесса принятия решений агентом. Без DecisionRequester внедрение вашего агента должно вручную вызывать его функцию RequestDecision() 
Компонент Behavior Parameters (параметры поведения) определяет, как объект принимает решения.

## Задание 3
### Доработайте сцену и обучите ML-Agent таким образом, чтобы шар перемещался между двумя кубами разного цвета. Кубы должны, как и впервом задании, случайно изменять кооринаты на плоскости. 

Решение:

1. Создадим еще один куб:

![Screenshot_1](https://user-images.githubusercontent.com/101480666/196702304-235099ad-0497-4f32-be87-380fe5dd85fa.jpg)

2. После надо отредактировать код для двух:
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;
    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }
    public GameObject Target1;
    public GameObject Target2;
    private bool target1Collected;
    private bool target2Collected;
    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
    {
        this.rBody.angularVelocity = Vector3.zero;
        this.rBody.velocity = Vector3.zero;
        this.transform.localPosition = new Vector3(0, 0.5f, 0);
    }
    Target1.transform.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    Target2.transform.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    Target1.SetActive(true);
    Target2.SetActive(true);
    target1Collected = false;
    target2Collected = false;
    }
    public override void CollectObservations(VectorSensor sensor)
    {
    sensor.AddObservation(Target1.transform.localPosition);
    sensor.AddObservation(Target2.transform.localPosition);
    sensor.AddObservation(this.transform.localPosition);
    sensor.AddObservation(target1Collected);
    sensor.AddObservation(target2Collected);
    sensor.AddObservation(rBody.velocity.x);
    sensor.AddObservation(rBody.velocity.z);
    }
    public float forceMultiplier = 10;
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {Vector3 controlSignal = Vector3.zero;
    controlSignal.x = actionBuffers.ContinuousActions[0];
    controlSignal.z = actionBuffers.ContinuousActions[1];
    rBody.AddForce(controlSignal * forceMultiplier);
    float distanceToTarget1 = Vector3.Distance(this.transform.localPosition, Target1.transform.localPosition);
    float distanceToTarget2 = Vector3.Distance(this.transform.localPosition, Target2.transform.localPosition);
    if (!target1Collected & distanceToTarget1 < 1.42f)
    {
        target1Collected = true;
        Target1.SetActive(false);
    }
    if (!target2Collected & distanceToTarget2 < 1.42f)
    {
        target2Collected = true;
        Target2.SetActive(false);
    }
    if(target1Collected & target2Collected)
    {
        SetReward(1.0f);
        EndEpisode();
    }
    else if (this.transform.localPosition.y < 0)
    {
        EndEpisode();
    }
}
}
```
3. Также создал несколько моделей и обучил их, по итогу шар катается за двумя кубами

## Выводы
1.При увелечении количества копий модель обучается быстрее
2.Игровой баланс — улучшает равентсво между персонажами, командами, тактиками игры и другими игровыми объектами
3.Машинное обучение используется для настройки игрового баланса. Методика тестирования игр на основе ML позволяет эффективнее повышать интересность и баланс игр.


