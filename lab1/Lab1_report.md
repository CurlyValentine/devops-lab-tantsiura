# Лабораторная работа №1  
**University:** ITMO University  
**Faculty:** FICT  
**Course:** Introduction in Web Technologies  
**Year:** 2025/2026  
**Group:** U4225  
**Author:** *Tantsiura Valentin Olegovich*  
**Lab:** Lab0  
**Date of create:** 11.10.2025  
**Date of finished:** 12.09.2025  

> Доказательствами выполнения лабораторной работы считаю историю изменений репозитория и приложенные скриншоты терминала.

---

## Ход работы

### Шаг 1. Установка Docker:

- Установлен Docker Desktop для macOS  
- Проверена установка командой `docker --version`  
- Запущен тестовый контейнер `hello-world`  
- Изучены базовые команды: `docker images`, `docker ps`, `docker ps -a`

  <img width="734" height="417" alt="image" src="https://github.com/user-attachments/assets/e34dc1a0-0d67-40e5-a8d3-f9231be33f3f" />

<img width="731" height="586" alt="image" src="https://github.com/user-attachments/assets/213dae40-64b2-435c-a6c1-5fde61e675f4" />
---

### Шаг 2. Работа с готовыми образами:

- Скачан образ Ubuntu командой `docker pull ubuntu:latest`  
- Запущен интерактивный контейнер `docker run -it ubuntu bash`  
- Внутри контейнера выполнена установка пакета `curl` командой `apt update && apt install -y curl`  
- Проверена установка с помощью `curl --version`  
- Выполнен выход из контейнера командой `exit`

  <img width="585" height="137" alt="image" src="https://github.com/user-attachments/assets/182c4682-f8e2-4ebf-ade5-3bd8078fe79a" />

  <img width="578" height="311" alt="image" src="https://github.com/user-attachments/assets/aa2a110f-fe02-4372-a4db-0c5a8cfdb627" />

  <img width="584" height="327" alt="image" src="https://github.com/user-attachments/assets/a3f2f2af-d0fd-47cd-998a-b4634e4a4f4d" />

  <img width="581" height="348" alt="image" src="https://github.com/user-attachments/assets/db010a80-518e-4cd8-920f-0b0d205315f5" />

<img width="584" height="332" alt="image" src="https://github.com/user-attachments/assets/86453cab-74c7-4b6c-a43a-2ddca5af8bdd" />

---

### Шаг 3. Запуск веб-сервера:

- Запущен контейнер с Nginx командой `docker run -d -p 8080:80 --name web-server nginx:alpine`  
- Проверена работа веб-сервера в браузере по адресу [http://localhost:8080](http://localhost:8080)  
- Просмотрены логи контейнера командой `docker logs web-server`  
- Выполнено подключение к контейнеру командой `docker exec -it web-server sh`

  <img width="580" height="372" alt="image" src="https://github.com/user-attachments/assets/26f2209f-bea2-477c-b201-756841ef0eb4" />

  <img width="585" height="301" alt="image" src="https://github.com/user-attachments/assets/b675c067-17ff-4440-9090-f5bb41fa4a68" />

  <img width="580" height="374" alt="image" src="https://github.com/user-attachments/assets/a19d9864-e7a9-41f4-a5c7-ba0ced14a437" />

  <img width="585" height="365" alt="image" src="https://github.com/user-attachments/assets/c3dab42b-2159-45a2-9609-297643057861" />

---

### Шаг 4.Управление контейнерами:

- Просмотрены запущенные контейнеры командой `docker ps`  
- Просмотрены все контейнеры (включая остановленные) командой `docker ps -a`  
- Остановлен контейнер командой `docker stop web-server`  
- Повторно запущен контейнер командой `docker start web-server`  
- Удалён контейнер командой `docker rm web-server`  
- Удалён образ командой `docker rmi nginx:alpine`

<img width="1011" height="657" alt="image" src="https://github.com/user-attachments/assets/9f6ae1db-5320-4fd9-9ae1-eb1e6cff7493" />

<img width="1009" height="620" alt="image" src="https://github.com/user-attachments/assets/29e1d587-e431-449d-82f3-f7ff51a5dcd3" />

<img width="1011" height="629" alt="image" src="https://github.com/user-attachments/assets/fae40a32-f453-4e73-b549-2e4c65437bbc" />

<img width="1012" height="632" alt="image" src="https://github.com/user-attachments/assets/87360617-cdb9-4f3d-b8e9-d5e48c133298" />

<img width="1018" height="639" alt="image" src="https://github.com/user-attachments/assets/0dd31282-0f3f-4ff9-9a9c-b1a9add10ba8" />

---

### Шаг 5 Работа с томами (volumes):

- Создан том командой `docker volume create my-volume`  
- Запущен контейнер с подключённым томом командой `docker run -it --name volume-test -d -v my-volume:/data ubuntu bash`  
- Выполнено подключение к контейнеру командой `docker exec -it volume-test bash`  
- Внутри контейнера создан файл командой `echo "Hello from volume" > /data/test.txt`  
- Контейнер удалён и создан новый с тем же томом  
- Проверено, что файл сохранился в томе


<img width="1012" height="647" alt="image" src="https://github.com/user-attachments/assets/e8aadf39-e606-49d3-83ff-bbad1ff7a7c2" />

<img width="1012" height="628" alt="image" src="https://github.com/user-attachments/assets/ca5a9560-ad8a-4134-a38a-7cddfc27815b" />

<img width="1011" height="665" alt="image" src="https://github.com/user-attachments/assets/4c3bb1c5-c84f-47eb-a328-f716e7e00a9c" />

<img width="1016" height="636" alt="image" src="https://github.com/user-attachments/assets/cdc0afa5-3726-411c-9c69-d4e579c6b181" />

---

### Шаг 6 Лабораторная работа со звездочкой. Создание файлов проекта:
<img width="1199" height="395" alt="image" src="https://github.com/user-attachments/assets/20c3bb14-00fe-4d73-a394-03ecd30c8dd5" />

<img width="1185" height="569" alt="image" src="https://github.com/user-attachments/assets/dc68178a-8845-47c7-b824-00a970aba42c" />
---


### Шаг 7 Создание Dockerfile:
<img width="1188" height="790" alt="image" src="https://github.com/user-attachments/assets/cbdfe039-a8d0-4a3b-8da5-0c2e3cf0629f" />

---

### Шаг 8 Проверка работы:
<img width="1215" height="611" alt="image" src="https://github.com/user-attachments/assets/abe49301-3971-4397-89ad-b2b8ceb18bfe" />


<img width="1898" height="1050" alt="image" src="https://github.com/user-attachments/assets/73e045d0-7f47-4bdf-95e3-0841a344799a" />





