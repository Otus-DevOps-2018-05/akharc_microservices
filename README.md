# akharc_microservices
akharc microservices repository
#HW12
Установлен докер, исследованы базовые основы работы с докер, даны объяснения разницы между образом и контейнером (Задание со *)

#HW13
```
docker run --rm -ti tehbilly/htop
```
Отображает только процессы внутри контейнера
```
docker run --rm --pid host -ti tehbilly/htop
```
Отображает все процессы на хосте, позволяет контейнеру видет все процессы локального хоста

В ходе задания сделано следующее:
1) при помощи docker-machine создан хост в GCP для тестирования и запуска докер-контейнеров
2) создан dockerfile для создания образа приложения puma, образ добавлен в докерхаб
3) из созданного образа запущены контейнеры на докер-хосте в GCP и на локальной ВМ.
