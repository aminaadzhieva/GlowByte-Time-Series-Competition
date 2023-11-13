# GlowByte-Time-Series-competition
Хакатон по временным рядам от компании "GlowByte" - "Энергетический Оракул".

**Задача:**  
Разработать надежную и точную модель прогнозирования объема
энергопотребления на сутки для Калининградской области с использованием
доступных исторических данных и соответствующих переменных.


**Данные:**
- `train_dataset.csv` – исторические данные о потреблении энергии за период 2019-01-01 - 2023-03-31
     * *date* – дата;
     * *time* – время,  время  представлено  в  диапазоне  0  –  23,  что  означает  24 часа в сутках;
     * *target* – фактическое потребление на указанную дату;
     * *temp* – фактическая температура на указанную дату;
     * *temp_pred* – прогноз температуры на указанную дату;
     * *weather_fact* – фактическая погода на указанную дату;
     * *weather_pred* – прогноз погоды на указанную дату;

- `test_dataset.csv` – исторические данные о потреблении энергии за период 2023-04-01 – 2023-07-31

**Метрики качества**:
- MAE (Главная метрика)
- MAPE (Вспомогательная метрика)
- R2-score (Вспомогательная метрика)

  ## Содержание репозитория:
- [orakul_final.ipynb](https://github.com/aminaadzhieva/GlowByte-Time-Series-competition/blob/main/orakul_final.ipynb) - ноутбук с ходом работы
- [count_vectorizer.pkl](https://github.com/aminaadzhieva/GlowByte-Time-Series-competition/blob/main/count_vectorizer.pkl) - векторайзер для обработки текста
- [скрипт предсказания](https://github.com/aminaadzhieva/GlowByte-Time-Series-competition/blob/main/main.py), [обученная модель](https://github.com/aminaadzhieva/GlowByte-Time-Series-competition/blob/main/pipe.pkl)
- [sun_data.json](https://github.com/aminaadzhieva/GlowByte-Time-Series-competition/blob/main/sun_data.json)  - спарсенные данные о восходе и закате
- [важность признаков](https://github.com/aminaadzhieva/GlowByte-Time-Series-competition/blob/main/feature-importance.xlsx)
- test_dataset.csv,train_dataset.csv,holidays_calendar.csv - тестовая, обучающая выборки + календарь праздников

  ## Описание решения:
- Выбран StackingRegressor для всех моделей
- Дополнительно сгенерировано 113 признаков: лаговые признаки, длительность светодого дня, флаг праздничного, предпраздничного, и рабочего дней, флаг погоды, порядковый номер года, месяца, недели, дисперсия  для прогнозированной температуры за 24 часа, скользящее среднее таргета, периодическая функция cos, флаг времени суток 
- Обучение, валидация и выбор лучшего набора гиперпараметров.
- Предсказание объема энергопотребления обученной моделью делается последовательно на каждый час. Профилактика утечки данных предусмотрена.

Для оценки модели использовалась метрика качества  **MAE**:
Полученный результат: 6.19

## Использованные библиотеки:
pandas, matplotlib, seaborn, numpy, joblib, datetime, phik, statsmodels: plot_acf, seasonal_decompose, adfuller; sklearn: GridSearchCV, TimeSeriesSplit, ParameterGrid, Pipeline, mean_absolute_error, mean_absolute_percentage_error, r2_score, StandardScaler, LinearRegression, CountVectorizer, StackingRegressor; LGBMRegressor, re, nltk: word_tokenize.
