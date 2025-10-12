# Базовый образ
FROM python:3.9-slim

# Установить системные пакеты: curl и vim
RUN apt-get update \
    && apt-get install -y --no-install-recommends curl vim \
    && rm -rf /var/lib/apt/lists/*

# Рабочая директория
WORKDIR /app

# Установить python-пакеты из requirements.txt
COPY requirements.txt /app/requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Создать пользователя appuser с UID 1000
RUN useradd -u 1000 -m -s /bin/bash appuser

# Скопировать приложение (сразу назначим владельца)
COPY --chown=appuser:appuser app.py /app/app.py

# Переключиться на пользователя appuser
USER appuser

# Переменная окружения и порт
ENV FLASK_ENV=production
EXPOSE 5000

# Запуск приложения
CMD ["python", "app.py"]