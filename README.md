# RAG_Profagro

## 🛠️ Основной стек проекта

![Python](https://img.shields.io/badge/-Python_3.10+-090909?style=for-the-badge&logo=python)
![FastAPI](https://img.shields.io/badge/-FastAPI-090909?style=for-the-badge&logo=fastapi)
![Gradio](https://img.shields.io/badge/-Gradio-090909?style=for-the-badge&logo=gradio)
![Aiogram](https://img.shields.io/badge/-Aiogram-090909?style=for-the-badge&logo=telegram)
![OpenSearch](https://img.shields.io/badge/-OpenSearch-090909?style=for-the-badge&logo=opensearch)
![Milvus](https://img.shields.io/badge/-Milvus-090909?style=for-the-badge&logo=milvus)
![Prefect](https://img.shields.io/badge/-Prefect-090909?style=for-the-badge&logo=prefect)
![Docker](https://img.shields.io/badge/-Docker-090909?style=for-the-badge&logo=docker)
![KServe](https://img.shields.io/badge/-KServe-090909?style=for-the-badge&logo=kubernetes)
![vLLM](https://img.shields.io/badge/-vLLM-090909?style=for-the-badge&logo=cloudsmith)
![Cloud.ru S3](https://img.shields.io/badge/-Cloud.ru_S3-090909?style=for-the-badge&logo=amazon-aws)

## Описание

Данный проект реализован по заказу агрохолдинга ООО «ПрофАгро» и посвящён промышленному внедрению мультимодального LLM-ассистента, использующего Retrieval-Augmented Generation (RAG) для автоматизации калибровки центробежных разбрасывателей удобрений. Цель — построение воспроизводимого производственного пайплайна, обеспечивающего механизатору мгновенный доступ к инструкциям, фото-схемам и видеогайдам AMAZONE и Kverneland, минимизируя ошибки дозирования и человеческий фактор, а также максимизируя соответствие работ картам заданий.

## Архитектура решения

- **Гибридный ретривер**: OpenSearch + Milvus (embedder — bge-m3), объединяющий лексический и семантический поиск.
- **Cross-Encoder-реранкер**: bge-reranker-v2-m3 для фильтрации шума.
- **LLM**: GPT-4o (OpenAI) или GigaChat-MAX-2 (СБЕР), формирующий ответы с точными ссылками на источники.
- **Корпус знаний**: 1 182 страницы PDF-руководств и транскрипции корпоративных видеороликов (>8 часов речи), извлечённые с помощью GPT-4o-mini и whisper-v3-large-turbo.
- **Оценка качества**: русифицированный RAGAS, граф знаний 60Гб, 1314 синтетических вопросов.
- **Оркестрация**: Prefect.
- **Хранение данных**: Cloud.ru S3.
- **Инфраструктура**: Docker-compose, 16 сервисов, inference embedder/реранкер на vLLM.

## Практическая значимость

Ассистент внедрён в ООО «ПрофАгро», снижает вероятность перерасхода удобрений и ускоряет настройку агрегата в полевых условиях. Прототип контейнеризирован, готов к масштабированию и расширению на другие марки техники и языки документации.

## Технологический стек

- Python 3.10+
- FastAPI, Gradio, aiogram
- OpenSearch, Milvus, Prefect
- Docker, docker-compose
- KServe, vLLM
- Cloud.ru S3

## Быстрый старт

1. Клонируйте репозиторий:
   ```bash
   git clone https://github.com/DmitrySirakov/RAG_Profagro
   cd RAG_Profagro
   ```
2. Запустите инфраструктуру:
   ```bash
   docker-compose up --build
   ```
3. Для запуска отдельных сервисов — см. инструкции в подпапках backend, frontend, ml

## Структура репозитория

- `backend/` — сервисы индексации, поиска, генерации
- `frontend/` — web-интерфейсы и Telegram-бот
- `ml/` — деплой и тестирование моделей
- `notebooks/` — эксперименты и анализ
- `certs/` — сертификаты

## Перспективы развития

- Разработка панели администратора для нативного добавления документов и мониторинга системы.
- Расширение на новые типы техники и языки.
