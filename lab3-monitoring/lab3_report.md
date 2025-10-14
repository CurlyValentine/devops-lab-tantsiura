# Лабораторная работа №3

**University:** ITMO University  
**Faculty:** FICT  
**Course:** Introduction in Web Technologies  
**Year:** 2025/2026  
**Group:** U4225  
**Author:** Tantsiura Valentin Olegovich  
**Lab:** Lab0  
**Date of create:** 29.09.2025  
**Date of finished:** 29.09.2025  

Доказательствами выполнения лабораторной работы прошу считать историю изменений данного репозитория.

---

## Мониторинг с Prometheus и Grafana

### Цель работы
Настроить систему мониторинга с использованием Prometheus для сбора метрик и Grafana для их визуализации.

---

## Этап 1. Подготовка конфигурации Prometheus

1.  Создал папку **prometheus** для конфигурационных файлов.
2.  Создал файл `prometheus/prometheus.yml` со следующими параметрами:
    -   Интервал сбора метрик — 15 секунд.
    -   Добавлены цели для сбора данных:
        -   **Prometheus** — `localhost:9090`
        -   **Node Exporter** — `node-exporter:9100`
3.  Подготовил файл `docker-compose.yml` для автоматического запуска всех сервисов (Prometheus, Grafana, Node Exporter).

![telegram-cloud-photo-size-2-5438408635714765604-y](https://github.com/user-attachments/assets/c0fe836a-6146-4e35-81ee-2612b49e8c56)

![telegram-cloud-photo-size-2-5438408635714765622-y](https://github.com/user-attachments/assets/0e09a1be-6727-4fbf-8465-3b78951d660d)

![telegram-cloud-photo-size-2-5438408635714765623-y](https://github.com/user-attachments/assets/8be47b85-11cb-445c-a4fc-c7f6998a6635)

![telegram-cloud-photo-size-2-5438408635714765626-y](https://github.com/user-attachments/assets/055040ae-b112-44a5-9c54-9846d2516a31)

<img width="896" height="824" alt="image" src="https://github.com/user-attachments/assets/d5a3751f-863e-4298-ba14-6cf90decfb49" />

---

## Этап 2. Запуск Node Exporter

1.  Запустил контейнер **Node Exporter** для сбора системных метрик.
2.  Проверил работу команды:
    ```bash
    curl http://localhost:9100/metrics
    ```
    Метрики успешно выводятся в терминале.
![telegram-cloud-photo-size-2-5438408635714765621-y](https://github.com/user-attachments/assets/33433325-c3c7-4f1d-b57e-f0370753ca52)

![telegram-cloud-photo-size-2-5438408635714765636-y](https://github.com/user-attachments/assets/d6fd57f0-0348-43bf-a2d5-4152e8ba33a1)


---

## Этап 3. Запуск Prometheus

1.  Создал том `prometheus-data` для хранения данных Prometheus.
2.  Запустил контейнер Prometheus с подключённой конфигурацией и томом данных.
3.  Проверил работу:
    -   Открыл `http://localhost:9090`
    -   Выполнил запрос `up` — отобразились активные источники метрик (Prometheus и Node Exporter).

![telegram-cloud-photo-size-2-5438408635714765627-y](https://github.com/user-attachments/assets/ea86f967-d93b-4037-9cb5-93d6492dec41)

![telegram-cloud-photo-size-2-5438408635714765630-y](https://github.com/user-attachments/assets/67a58728-fb94-4ac3-8519-3ef713811e9b)

![telegram-cloud-photo-size-2-5438408635714765639-y](https://github.com/user-attachments/assets/6d2c4cec-c825-4c1f-a740-bad33b9b6e6e)


---

## Этап 4. Запуск Grafana

1.  Создал том `grafana-data` для хранения данных Grafana.
2.  Запустил контейнер Grafana:
    -   **Логин:** `admin`
    -   **Пароль:** `admin`
3.  Проверил доступ по адресу `http://localhost:3000` — интерфейс Grafana открылся успешно.

![telegram-cloud-photo-size-2-5438408635714765631-y](https://github.com/user-attachments/assets/890ef3a4-c8d3-4131-8186-9a1b864bf9b9)


---

## Этап 5. Настройка Grafana и создание дашборда

1.  В Grafana добавил источник данных Prometheus:
    -   `Configuration` → `Data Sources` → `Add data source`
    -   **Тип:** Prometheus
    -   **URL:** `http://prometheus:9090`
    -   Нажал `Save & Test` → появилось сообщение “Data source is working”.
2.  Создал новый дашборд (`Create` → `Dashboard` → `Add visualization`).
3.  Добавил панели с метриками:
    -   **CPU Load (%)**
        ```promql
        100 * (1 - avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])))
        ```
    -   **Memory Available (%)**
        ```promql
        100 * node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes
        ```
    -   **Disk Usage (%)**
        ```promql
        100 * (1 - (node_filesystem_avail_bytes{fstype!~"tmpfs|overlay"} / node_filesystem_size_bytes{fstype!~"tmpfs|overlay"}))
        `
4.  Сохранил дашборд под названием `System Overview`.

![telegram-cloud-photo-size-2-5438408635714765652-y](https://github.com/user-attachments/assets/2e0f6d5b-6b3c-4729-bb52-2a29deaa266d)

![telegram-cloud-photo-size-2-5438408635714765667-y](https://github.com/user-attachments/assets/111ce8e3-ddd6-48b8-bc94-d1c3c9e44187)

![telegram-cloud-photo-size-2-5438408635714765673-y](https://github.com/user-attachments/assets/50e9b7cb-4faf-4ff5-8a8f-2fdcbd3e4b8d)

![telegram-cloud-photo-size-2-5438408635714765680-y](https://github.com/user-attachments/assets/2a8a3bc3-464b-4ba4-82fd-78940f42de40)

![telegram-cloud-photo-size-2-5438408635714765681-y](https://github.com/user-attachments/assets/93281d25-fe71-46fc-9288-d51bee915da0)

![telegram-cloud-photo-size-2-5438408635714765687-y](https://github.com/user-attachments/assets/9d0fc9a1-9c3e-4aa1-acfd-434ffeb8804f)

![telegram-cloud-photo-size-2-5438408635714765694-y](https://github.com/user-attachments/assets/6679796d-f804-43ca-a9f7-159fa6364009)

---

## Этап 6. Тестирование системы

1.  Проверил работу всех контейнеров:
    ```bash
    docker ps
    ```
    Все сервисы работают в статусе `Up`.

2.  Убедился, что:
    -   В Prometheus отображаются активные цели.
    -   В Grafana визуализируются метрики CPU, памяти и диска.
<img width="674" height="177" alt="image" src="https://github.com/user-attachments/assets/88fa1813-4dc3-4ed2-b852-b1bc96c5c33f" />

---

## Результаты

-   Все контейнеры успешно запущены.
-   Метрики собираются Prometheus и отображаются в Grafana.
-   Создан рабочий дашборд для мониторинга системных показателей.

---

## Вывод

Получены практические навыки настройки системы мониторинга на основе Prometheus и Grafana: развёртывание контейнеров, сбор метрик, настройка источников данных и визуализация показателей в виде дашбордов.
