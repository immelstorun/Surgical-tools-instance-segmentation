[![TG profile](https://img.shields.io/badge/contact_me-blue?logo=telegram&logoColor=yellow)](https://t.me/immelst0run)
[![GitHub Repo](https://img.shields.io/badge/project-github-blue?style=flat&logo=github)](https://github.com/immelstorun/med_tools_seg)
[![Python](https://img.shields.io/badge/Python-3.11-3670A0?style=for-the-flat&logo=Python&logoColor=ffdd54)](https://www.r-project.org/)

МФТИ - Прикладной анализ данных в медицинской сфере
# Surgical tools instance segmentation
![Пример изображения](main.png)

Детекция хирургических инструментов методами машинного зрения

## Оглавление
[1. Описание проекта](#описание-проекта)

[2. Описание данных](#описание-данных)

[3. План работы](#план-работы)

[4. Результаты](#результаты)

[5. Выводы](#выводы)

## Описание проекта
Проект посвящен подробному описанию возможностей по полуавтоматизированной разметке самостоятельно собранных изображений и видеозаписей хирургических инструментов из гинекологического стационара г. Волгограда с использованием CVAT.ai и обучению нейронной сети YOLOv8_seg для сегментированной детекции.

### Команда 

- [Алексей Сейкин](https://github.com/immelstorun)
- [Дарья Курочкина](https://github.com/DariaShvetsova)
- [Геннадий Музыкантов](https://github.com/muzykantov)

### Цель
Сегментационная разметка собранных изображений для обучения нейронной сети в задаче классификации хирургических инструментов с демонстрацией качества распознавания инструментов.

### Задачи

1. Обосновать тему для датасета для задачи классификации
2. Собрать данные из открытых источников
3. Разметить и очистить данные (общий объем должен быть около 100 объектов)
4. *Разделить данные на обучающую и тестовую выборки
5. *Сохранить размеченные данные в формате YOLO
6. *Провести обучение YOLOv8 seg
7. *Провести тестирование YOLOv8 seg

### 1. Обоснование темы для датасета для задачи классификации
Детекция хирургических инструментов является важной задачей в медицинской практике и юридическом контроле, так как она помогает улучшить качество операций, повысить образовательный уровень медицинских специалистов и обеспечить соблюдение медицинских стандартов и протоколов.

- В кейсах с научными видео и фантомными операциями детекция инструментов позволяет:

  - `Обучение и тренировка медперсонала`: Научные видео и фантомные операции часто используются для демонстрации техник и методов хирургии. Автоматическая разметка инструментов помогает обучающимся быстрее и точнее идентифицировать инструменты и их применение.

  - `Анализ и улучшение хирургических техник`: Детекция инструментов позволяет анализировать использование различных инструментов в ходе операций, что способствует совершенствованию хирургических методик.

  - `Развитие компьютерного зрения в медицине`: Использование алгоритмов машинного обучения для анализа хирургических процедур открывает новые возможности в исследовании и практике.

- В кейсе юридического контроля правильности применения инструментов детекция важна для:

  - `Соблюдение стандартов и протоколов`: Проверка правильности использования инструментов по ходу операции для соответствия медицинским протоколам и стандартам.
  - `Фиксация ошибок и предотвращение медицинских осложнений`: Автоматическая детекция может помочь выявить ошибки в использовании инструментов, что может привести к нежелательным последствиям для пациента.
  - `Юридическая ответственность`: В случае судебных разбирательств, связанных с медицинской практикой, точная детекция инструментов может служить доказательственной базой.

Качественная разметка важна, поскольку она служит основой для обучения моделей машинного обучения. Без качественной разметки данных модель не сможет правильно идентифицировать объекты на новых изображениях.

YOLO (You Only Look Once) является одним из передовых методов для детекции объектов в реальном времени и часто используется из-за следующих преимуществ:

Скорость: YOLO может обрабатывать изображения очень быстро, что делает его идеальным для использования в реальном времени, например, во время операций.
Точность: YOLO обеспечивает хорошее сочетание скорости и точности, что критически важно для медицинских приложений.
Обучение на неполной разметке: YOLO может быть обучен даже с недостаточным количеством данных, что важно в медицинской отрасли, где размеченные данные могут быть ограничены.

## Описание данных

Датасет состоит из фото хирургических инструментов и видеозаписей их применения. Датасет собран нами самостоятельно в гинекологическом отделении ОКБ г. Волгограда.

В процессе сбора данных применялись как постановочные сцены для максимизации качества, так и непосредственные видеозаписи с хирургическими инструментами.

Общий обьем данных - 239 элементов - 1.18 Gb:
- 212 фото
- 27 видеозаписей

Исходные фото в папке `Raw` в формате .HEIC (Apple) были сконвертированы в формат .JPG и помещены в папку `converted`.
[Размеченный датасет 06_04_2024](https://github.com/immelstorun/Surgical-tools-instance-segmentation/blob/main/dataset_06_04_2024.zip)

## План работы

### Этапы работы:

1. **Подготовка инструментария для разметки данных**
   - Выбор и настройка платформы CVAT.ai для разметки изображений.
   - Создание проекта в CVAT и настройка рабочего окружения.

2. **Разметка данных**
   - Разметка изображений в ручном режиме для создания начального набора данных.
   - Применение полуавтоматического режима разметки в CVAT для ускорения процесса разметки.
   - Проверка и корректировка разметки для улучшения качества данных.

3. **Классификация инструментов**
   - Определение классов для сегментации хирургических инструментов.
   - Разметка инструментов по трем выбранным классам.

4. **Экспорт размеченных данных**
   - Выгрузка размеченных данных из CVAT в формате JSON.
   - Преобразование данных из JSON в формат, подходящий для обучения модели YOLOv8_seg.

5. **Подготовка данных для обучения**
   - Разделение данных на обучающую и тестовую выборки.
   - Подготовка данных в соответствующем формате для обучения модели.

6. **Обучение модели**
   - Настройка и обучение нейронной сети YOLOv8_seg на подготовленных данных.
   - Мониторинг процесса обучения и корректировка параметров при необходимости.

7. **Тестирование и оценка модели**
   - Тестирование обученной модели на тестовой выборке.
   - Анализ результатов и оценка качества распознавания инструментов.

### Разметка в CVAT

В процессе разметки использовались как полуавтоматический, так и ручной режимы. Полуавтоматический режим позволял ускорить процесс разметки за счет предварительного распознавания объектов, после чего разметчик вручную корректировал и уточнял границы объектов. В ручном режиме каждый объект размечался вручную без предварительного распознавания.

Были определены следующие классы инструментов для разметки:
- Класс 1: Зажим
- Класс 2: Пинцет
- Класс 3: Ножницы

После завершения процесса разметки данные были экспортированы из CVAT в формате JSON. Пример экспортированного JSON файла:

```json
{
    "licenses": [
        {
            "name": "",
            "id": 0,
            "url": ""
        }
    ],
    "info": {
        "contributor": "",
        "date_created": "",
        "description": "",
        "url": "",
        "version": "",
        "year": ""
    },
    "categories": [
        {
            "id": 1,
            "name": "clamp",
            "supercategory": ""
        },
        {
            "id": 2,
            "name": "tweezers",
            "supercategory": ""
        },
        {
            "id": 3,
            "name": "scissors",
            "supercategory": ""
        }
    ],
    "images": [
        {
            "id": 1,
            "width": 4032,
            "height": 3024,
            "file_name": "med_seg_00005.jpg",
            "license": 0,
            "flickr_url": "",
            "coco_url": "",
            "date_captured": 0
        },
        ....
    ],
    "annotations": [
        {
            "id": 1,
            "image_id": 1,
            "category_id": 1,
            "segmentation": [
                [
                    1005.0,
                    2102.0,
                    1022.0,
                    ....
                ]
            ],
            "area": 628463.0,
            "bbox": [
                956.0,
                1052.0,
                2123.0,
                1178.0
            ],
            "iscrowd": 0,
            "attributes": {
                "occluded": false
            }
        },
        ....
    ]
}
```

### Обучение модели

Обучение нейронной сети YOLOv8_seg будет проводиться следующим образом:

1. Подготовка конфигурационного файла для YOLOv8_seg с параметрами обучения, включая размер пакета, скорость обучения, количество эпох и т.д.
2. Преобразование размеченных данных из формата JSON в формат, необходимый для обучения модели YOLO (например, в формате .txt с координатами bounding box и классами объектов).
3. Инициализация обучения модели с использованием подготовленных данных и конфигурационного файла.
4. Мониторинг процесса обучения и валидации модели, анализ лосса и метрик точности.
5. Проведение тонкой настройки модели, если это необходимо, для улучшения результатов.
6. Сохранение обученной модели для последующего использования и тестирования.

## Результаты

Раздел находится в разработке.

## Выводы

Раздел находится в разработке.
=======
## Описание метода

Самый быстрый и рапространенный метод аннотации объектов — боксы. 
Ассесоры выставляют ограничивающие рамки вокруг объектов на изображении, присваивая различные классы в зависимости от типа объекта. Боксы могут иметь вид классического прямоугольника или прямоугольника со смещенными сторонами. Однако для задач разметки (как в данном примере), где необходимо получить более точные модели машинного обучения, лучше использовать сегментацию объектов  - когда каждый интересующий вас объект на изображении выделяется отдельным контуром и ему присваивается класс. 

В качестве примера приложены образцы изображений с уже нанесенной сегментационной разметкой, выполненной в программе CVAT.ai.  
В данных образцах зеленым контуром выделены зажимы, голубым — пинцеты и оранжевым — ножницы. 
![сегментировнные_инструменты](clamp_scissors.png)
![сегментировнные_инструменты](clamp_sciss2.png)
![сегментировнные_инструменты](clamp_sciss3.png)


## Критерии оценки
| Этап                   | Баллы | Критерии оценивания                                                                                               |
|------------------------|------------------------------|--------------------------------------------------------------------------------------------------------------------|
| Сбор данных            | 10                           | - Датасет состоит из подходящих данных (от 100 записей) (0-5 баллов)                                               |
|                        |                              | - Есть описание собранных данных и процесса сбора (0-3 балла)                                                        |
|                        |                              | - Есть описание идеи датасета и теоретических возможностей использования датасета (0-2 балла)                     |
| Очистка данных и разметка | 10                         | - Более 50% данных подготовлены, очищены и размечены корректно (0-5 баллов)                                         |
|                        |                              | - Есть качественное, детальное описание датасета, проделанных операций, присутствующих в датасете классов (0-5 баллов) |
| Презентация            | 10                           | - Презентация цели проекта (1 балл)                                                                                 |
|                        |                              | - Презентация процесса сбора данных (1 балл)                                                                         |
|                        |                              | - Презентация методов разметки и обработки изображений (1 балл)                                                    |
|                        |                              | - Презентация полученных результатов (2 балла)                                                                      |
|                        |                              | - Качество итогового датасета: датасет содержит 100 и более записей, корректно размеченных и подготовленных к работе (0-5 баллов) |

