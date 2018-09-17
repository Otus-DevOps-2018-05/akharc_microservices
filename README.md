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
#HW14

Выполнена практика по запуску микросервисов в докер-контейнерах
Уменьшен объем контейнера ui с помощью оптимизации dockerfile
Настроено сохранение постов в mongodbс помощью docker-volume

1 задание со *:
bash-4.2# docker run -d --network=reddit --network-alias=post_db_asterisk --network-alias=comment_db_asterisk mongo:latest
bash-4.2# docker run -d --network=reddit --network-alias=post_asterisk --env POST_DATABASE_HOST=post_db_asterisk akha/post:1.0
bash-4.2# docker run -d --network=reddit --network-alias=comment_asterisk --env COMMENT_DATABASE_HOST=comment_db_asterisk akha/comment:1.0
bash-4.2# docker run -d --network=reddit -p 9292:9292 --env POST_SERVICE_HOST=post_asterisk --env COMMENT_SERVICE_HOST=comment_asterisk akha/ui:1.0

#HW15

При создании контейнера с сетью типа "host" выводы команд
```
docker exec -ti net_test ifconfig
docker-machine ssh docker-host ifconfig
```
идентичны, т.к. сеть контейнера в данном случае не изолирована от сети хоста и контейнеру доступны те же интерфейсы, что и хосту.

Имя префикса берется из названия каталога проекта. Префикс может быть перезfписан диреткивой -p или переменной COMPOSE_PROJECT_NAME

Задание со *:
Добавлен файл docker-compose.override.yml
