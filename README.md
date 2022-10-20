# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Бабенко Александр Алексеевич
- 2072118
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | # | 20 |

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

·	Если все сделано правильно, то во вкладке с компонентами (Components) внутри Unity вы увидите строку ML Agent.
![image](https://user-images.githubusercontent.com/114616168/196904119-34db1dab-d17e-413b-b967-2c235e723555.png)

·	Далее запускаем Anaconda Prompt для возможности запуска команд через консоль.
·	Далее пишем серию команд для создания и активации нового ML-агента, а также для скачивания необходимых библиотек:
o	mlagents 0.28.0;
o	torch 1.7.1;
Создадем виртуальное окружение.
После этого добавим скрипт шару и еще добавим Decision Requester и Behavior Parameters:
Скрипт:
`
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

## Задание 2
Срипт для обучния модели с помощью линейной регресии 
![image](https://user-images.githubusercontent.com/114616168/194242570-30e5bb8f-22ac-41da-abed-ba46139e9cb4.png)





## Выводы
Узнал про экспорт данных, более углублённо поработал с Unity

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
