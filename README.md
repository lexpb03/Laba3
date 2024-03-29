# Модель генерации подписей к изображениям (Лабораторная №3)

Этот проект представляет собой модель для генерации текстовых описаний к изображениям с использованием датасета Flickr8k. Модель основана на архитектуре VGG16 для извлечения признаков из изображений и LSTM для генерации описаний.

## Flickr8k :newspaper:
*Flickr8k Dataset* — это набор данных, предназначенный для задачи генерации текстовых описаний к изображениям. Этот набор данных содержит изображения, снимки которых были взяты с веб-сайта Flickr, а также соответствующие им описания, созданные пользователями.

Вот основные характеристики набора данных:

  * В наборе данных содержится 8092 цветных изображения различных объектов и сцен. Эти изображения предоставлены пользователями веб-сайта Flickr.

  * Каждому изображению в наборе данных прилагается пять различных описаний, созданных разными пользователями. Описания охватывают разнообразные аспекты изображений, включая объекты, действия, окружение и даже эмоции.

  * Для удобства использования, описания и изображения в наборе данных сопоставлены с помощью уникальных идентификаторов.

  * Основной задачей, которую можно решать с использованием этого набора данных, является генерация подписей (captions) к изображениям. Это задание подразумевает создание модели машинного обучения, способной автоматически генерировать текстовые описания для предоставленных изображений.

Использование таких наборов данных позволяет обучать модели на задачах, связанных с пониманием контента изображений и формированием связанных семантических описаний. *Flickr8k Dataset* широко используется в исследованиях области компьютерного зрения и обработки естественного языка.

## VGG16 :zap:
*VGG16* (Visual Geometry Group 16) — это модель глубокого обучения для распознавания изображений, представленная в статье "Very Deep Convolutional Networks for Large-Scale Image Recognition" от исследовательской группы Visual Geometry Group (VGG) в Университете Оксфорда. Модель была представлена в рамках участия VGG в соревновании ImageNet Large Scale Visual Recognition Challenge (ILSVRC) 2014.

Вот основные характеристики *VGG16*:

  * VGG16 представляет собой сверточную нейронную сеть (CNN) с 16 слоями, включая 13 сверточных слоев и 3 полносвязанных слоя. Основной особенностью архитектуры VGG16 является ее глубокость — она состоит из множества сверточных слоев, что делает модель глубокой и способной извлекать сложные признаки из изображений.

  * Все сверточные слои VGG16 используют фильтры размером 3x3 пикселя, а также операцию свертки с шагом 1 и функцию активации ReLU (Rectified Linear Unit) после каждого сверточного слоя.

  * После каждой группы сверточных слоев следует слой объединения (пулинга) для уменьшения пространственных размерностей. Обычно используется операция максимального пулинга с ядром размером 2x2.

  * В конце архитектуры VGG16 располагаются три полносвязанных слоя, включая выходной слой с софтмакс активацией для классификации.

  * VGG16 широко используется в качестве предварительно обученной модели для извлечения признаков из изображений. Модель обучалась на большом наборе данных ImageNet, что позволяет использовать ее в задачах классификации изображений, детекции объектов и других задач компьютерного зрения.

  * Благодаря своей глубокой архитектуре и хорошей обобщающей способности, VGG16 является популярным выбором для передачи обучения (transfer learning), где предобученные веса модели могут быть использованы для решения новых задач с меньшим объемом данных.

*VGG16* оказала значительное влияние на развитие глубокого обучения и продолжает служить основой для многих исследований и приложений в области компьютерного зрения.

## Как работает программа :cd:
1. **Извлечение признаков из изображений**:
    * Используется предварительно обученная модель VGG16 для извлечения признаков из изображений.
    * Извлеченные признаки сохраняются в файл features.pkl.

2. **Подготовка текстовых описаний**:
    * Загружаются текстовые описания из файла captions.txt.
    * Производится предварительная обработка текстов, такая как приведение к нижнему регистру, удаление цифр и специальных символов, добавление тегов начала и конца (startseq и endseq).
    * Создается словарь mapping, связывающий идентификаторы изображений с соответствующими им описаниями.

3. **Токенизация текста**:
    * Используется Tokenizer для токенизации текстовых данных.
    * Определяется размер словаря (vocab_size) и максимальная длина описания (max_length).

4. **Подготовка данных для обучения**:
    * Разделение данных на обучающую и тестовую выборки.
    * Создание генератора данных для обучения модели.

5. **Построение модели**:
    * Создается модель с использованием слоев для извлечения признаков из изображений (энкодер) и генерации текстовых описаний (декодер).
    * Модель компилируется с функцией потерь categorical crossentropy и оптимизатором Adam.

6. **Обучение модели**:
    * Модель обучается на обучающем наборе данных с использованием созданного генератора данных.

7. **Оценка качества модели**:
    * Используется тестовый набор данных для оценки качества модели с использованием метрики BLEU.

8. **Генерация подписей для изображений**:
    * Предоставленная функция predict_caption используется для генерации подписей для изображений из тестового набора.

9. **Визуализация результатов**:
    * Производится визуализация фактических и предсказанных описаний для одного изображения с использованием функции generate_caption.

### Предварительные требования

- Python 3
- Jupyter Notebook или Google Colab (для интерактивного запуска скрипта)
- Подключение к интернету (для загрузки предварительно обученных моделей и данных)

## 🦒 Colab
| Colab                                                                                                                                                                          | Info               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------ |
| [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lexpb03/work/blob/main/labaa-3.ipynb) | laba-3 |

## Использование :computer:

1. **Извлечение признаков из изображений**: Запустите скрипт `extract_features.py`, чтобы извлечь признаки с использованием предварительно обученной модели VGG16.

2. **Предобработка текста**: Запустите скрипт `preprocess_text.py`, чтобы подготовить текстовые описания для обучения.

3. **Обучение модели**: Запустите скрипт `train_model.py`, чтобы обучить модель на подготовленных данных.

4. **Генерация подписей**: Используйте функцию `generate_caption(image_name)` для получения описания для конкретного изображения.

## Зависимости :closed_book:

- TensorFlow
- NLTK
- Pillow
- tqdm

## Результаты :tv:

Модель обучена на протяжении 20 эпох, и ее качество оценено с использованием метрики BLEU. Вы можете протестировать модель на своих изображениях, запустив функцию `generate_caption(image_name)`.

**Пример на фотографиях из датасета**:

![xxxx](https://sun9-4.userapi.com/impg/ZVneEIanA-22_xLLVev36JPBnJAqkJcUElEUSA/_lUIijZxmDo.jpg?size=720x608&quality=96&sign=dc9009f816899f1478dcc0da3a4d166c&type=album)

![xxxx](https://sun9-39.userapi.com/impg/_YGvJfzh77L-Esi-Ewa4ClPEQjX5Y80xBEkaYA/xjvrZXBi2Tc.jpg?size=792x609&quality=96&sign=180a322583fd5bc3cb2ad82b9d0f5903&type=album)

**Пример на наших фотографиях**:

![xxxx](https://sun21-1.userapi.com/impg/iUR9EjjD1bw9XKKEpaTPIozCP_QxFRO9heiPPw/k1PHNv7IJ0I.jpg?size=662x423&quality=96&sign=6370767ab2929c2fda8f07bc63ea2467&type=album)

-----------
