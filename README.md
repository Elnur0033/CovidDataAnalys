---

## 📊 Анализ данных COVID-19 и вакцинации в Индии

Этот проект предоставляет визуальный и числовой анализ распространения COVID-19 и процесса вакцинации в Индии с использованием Python, Pandas, Matplotlib, Seaborn и Plotly.

---

### 🔍 Описание проекта

Проект включает в себя:

* Очистку и предварительную обработку данных
* Расчёт активных случаев COVID-19
* Анализ по штатам: количество заражённых, выздоровевших, умерших
* Расчёт коэффициента выздоровления и смертности
* Визуализацию:

  * Топ-10 штатов по активным случаям
  * Топ-10 штатов по смертям
  * Тренд роста активных случаев в 5 крупнейших штатах
  * Распределение вакцинации между мужчинами и женщинами
  * Топ-5 штатов по числу вакцинированных

---

### 🗂️ Используемые датасеты

1. `covid_19_india.csv` – содержит статистику по COVID-19 по датам и регионам.
2. `covid_vaccine_statewise.csv` – содержит информацию о вакцинации по штатам и времени.

---

### 🧰 Зависимости

Проект написан на Python и использует следующие библиотеки:

```bash
pip install pandas numpy matplotlib seaborn plotly
```

---

### 📌 Основные шаги анализа

#### ✅ 1. Загрузка и предварительная обработка данных

* Удаляются ненужные столбцы (например, "Sno", "Time")
* Дата приводится к правильному формату
* Добавляется столбец `Active_Cases`:

```python
covid_df['Active_Cases'] = covid_df['Confirmed'] - (covid_df['Cured'] + covid_df['Deaths'])
```

---

#### 📈 2. Сводная таблица по штатам

Создаётся сводная таблица со значениями по заражённым, смертям и выздоровевшим:

```python
statewise = pd.pivot_table(covid_df, values = ["Confirmed", "Deaths", "Cured"], 
                           index = "State/UnionTerritory", aggfunc="max")
```

К ней добавляются:

* Recovery Rate = Cured / Confirmed
* Mortality Rate = Deaths / Confirmed

---

#### 🏆 3. Топ-10 штатов по активным случаям

Barplot с наибольшим количеством активных случаев:

```python
sns.barplot(data = top_10_active_cases.iloc[:10], ...)
```

---

#### ⚰️ 4. Топ-10 штатов по количеству смертей

Ещё один barplot — по `Deaths`.

---

#### 📈 5. Тренд активных случаев по 5 штатам

Lineplot показывает, как менялись активные случаи с течением времени:

```python
sns.lineplot(data=covid_df[...], x='Date', y='Active_Cases', hue='State/UnionTerritory')
```

---

#### 💉 6. Анализ вакцинации

* Удаляются лишние столбцы, агрегируются значения
* Сравниваются значения мужчин и женщин:

```python
px.pie(names=["Male", "Female"], values=[male, female])
```

* Строится график для 5 штатов с наибольшим числом вакцинированных.

---
