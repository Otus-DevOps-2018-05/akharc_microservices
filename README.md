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

#HW16

При помощи docker-machine создана ВМ для запуска gitlab-ci:
```
docker-machine create --driver google  --google-machine-image https://www.googleapis.com/compute/v1/projects/ubuntu-os-cloud/global/images/family/ubuntu-1604-lts  --google-machine-type n1-standard-1  --google-disk-size 100 --google-zone europe-west1-b  docker-ci-gitlab

```
Затем вручную запущена Omnibus-инсталяция gitlab-ci


Создан gitlab-runner:
```
docker-machine ssh docker-ci-gitlab
docker run -d --name gitlab-runner --restart always \
-v /srv/gitlab-runner/config:/etc/gitlab-runner \
-v /var/run/docker.sock:/var/run/docker.sock \
gitlab/gitlab-runner:latest 
```
#HW 17

Получена практика по работе с окружениями в Gitlab-CI

#HW 18

Создан Dockerfile для Prometheus, пересобраны образы для приложения reddit;
переписан файл docker-compose для мониторинга ui, post и comment;
исследованы базовые функции Прометеуса;
добавлен node exporter для мониторинга дополнительных метрик;

Ссылка на докерхаб:
https://hub.docker.com/u/akha/

# HW 19

Настроен мониторинг контейнеров с помощью Cadviser;
Настроена визуализация с помощью Grafana;
Настроен сбор метрик приложений и бизнес-метрик;
Настроен алертинг с импортом в слак.

Ссылка на докерхаб:

https://hub.docker.com/u/akha/

# HW 20

Настроен сбор логов с помощью Fluentd
Настроена передача логов в ELK и их визуализация
Настроен парсинг структурированных и неструктурированных логов.

#HW 12
- Созданы yaml-файлы с манифестами приложений
- Пройден туториал Kubernetes The Hard way
- Проверен запуск подов:

 ```
 kubectl apply -f mongo-deployment.yml
 deployment.apps/mongo-deployment created
 kubectl apply -f comment-deployment.yml
 deployment.apps/comment-deployment created
 kubectl apply -f ui-deployment.yml
 deployment.apps/ui-deployment created
 kubectl apply -f post-deployment.yml
 deployment.apps/post-deployment created
 ```
