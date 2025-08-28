# Analyzer — анализ речи и текста 🧠🎙️

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.11%2B-blue" alt="Python 3.11+">
  <img src="https://img.shields.io/badge/Type-Audio%20%26%20NLP-8A2BE2" alt="Type">
  <img src="https://img.shields.io/badge/Platform-macOS%20|%20Linux%20|%20Windows-lightgrey" alt="Platform">
  <img src="https://img.shields.io/badge/Status-Active-success" alt="Status">
</p>

Инструмент для оценки качества произношения, семантической близости текстов и грамматики. Проект объединяет обработку аудио, выравнивание текста с речью, вычисление метрик и визуальный интерфейс.

---

## ✨ Возможности

- **Акустика и просодика**: оценка темпа, пауз, интонации и чистоты произношения.
- **Семантика текста**: сравнение смысловой близости пары текстов, агрегирование сходства.
- **Грамматика**: проверка грамматических ошибок, вероятностные оценки моделью.
- **Алайнмент**: выравнивание текста и аудио по тайм-кодам для точных метрик.
- **Единые пороги**: конфигурация порогов метрик в одном месте.
- **UI**: удобный интерфейс Streamlit для мультистраничной работы.

---

## 🧭 Структура проекта

```
Analyzer/
├── analyzer/
│   ├── __init__.py
│   └── pronunciation_analyzer.py
├── configs/
│   ├── __init__.py
│   └── thresholds.py
├── pages/
│   ├── __init__.py
│   ├── 1_voice_analysis.py
│   └── 2_text_semantics.py
├── semantic/
│   ├── __init__.py
│   ├── evaluator.py
│   ├── grammar_analyzer.py
│   └── grammar_nn.py
├── utils/
│   ├── __init__.py
│   └── text.py
├── .gitignore
├── db_connector.py
├── ffmpeg
├── Home.py
├── README.md
├── requirements.txt
├── ruff.toml
└── text.py
```

**Файлы и назначение:**
- `1_🎯_Голосовой_анализ.py`
- `2_📝_Семантика_текста.py`
- `Home.py` — Главный экран приложения Streamlit для мультистраничного интерфейса.
- `alignment.py` — Синхронизация/алайнмент текста и аудио по времени.
- `audio_processor.py` — Загрузка, конвертация и разбиение аудио на фрагменты.
- `db_connector.py` — Подключение к базе данных (логирование, результаты, кэш).
- `evaluator.py` — Агрегация метрик и вычисление итоговых оценок.
- `grammar_analyzer.py` — Проверка грамматики/правописания, подготовка фич для модели.
- `grammar_nn.py` — Нейросетевая модель/классификатор для грамматического анализа.
- `pronunciation_analyzer.py` — Оценка произношения и близости к эталону, метрики сходства.
- `text.py` — Вспомогательные утилиты работы с текстом, нормализация.
- `thresholds.py` — Централизованные пороги/константы для метрик.

> Имена русскоязычных файлов приведены к английским: `1_voice_analysis.py`, `2_text_semantics.py`. Комментарии и докстринги очищены.

---

## 🚀 Быстрый старт

### 1) Установка окружения
```bash
git clone https://github.com/lewpanow/Analyzer.git
cd Analyzer
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

> При отсутствии `requirements.txt` установите зависимости, которые используются в коде (`streamlit`, `numpy`, `pandas`, `scikit-learn`, `torch`, `librosa`, `pydub`, `python-dotenv` и т.д.).

### 2) Запуск приложения (UI)
```bash
streamlit run Home.py
```

### 3) Запуск модулей напрямую
```bash
python 1_voice_analysis.py        # анализ речи
python 2_text_semantics.py        # семантика текста
```

---

## ⚙️ Конфигурация

- **Пороги метрик:** редактируйте значения в `thresholds.py`.
- **База данных:** параметры подключения задайте в `db_connector.py` или через переменные окружения:
  ```bash
  export DB_URI="postgresql://user:pass@host:5432/dbname"
  export DB_SCHEMA="public"
  ```
- **Модели/веса:** поместите файлы моделей туда, где их ожидает `grammar_nn.py`/`pronunciation_analyzer.py`, либо настройте пути через переменные окружения.

---

## 🧪 Пример использования в коде

```python
from audio_processor import load_audio  # чтение и подготовка аудио
from pronunciation_analyzer import score_pronunciation
from evaluator import aggregate_scores

waveform, sr = load_audio("sample.wav")
phoneme_scores = score_pronunciation(waveform, sr, reference_text="пример эталонного текста")
final = aggregate_scores(phoneme_scores)
print(final)
```

---

## 📊 Метрики (пример)

- **PronunciationScore** — доля корректно произнесённых фонем.
- **Tempo/Pause** — темп речи и длительность пауз.
- **SemanticSimilarity** — косинусная близость эмбеддингов текстов.
- **GrammarQuality** — вероятность грамматической корректности фразы.

Пороговые значения централизованы в `thresholds.py`.


---

<p align="center">
  Обновлено: 2025-08-27
</p>
