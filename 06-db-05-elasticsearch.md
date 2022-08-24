# Домашнее задание к занятию "6.5. Elasticsearch"

## Задача 1

В этом задании вы потренируетесь в:
- установке elasticsearch
- первоначальном конфигурировании elastcisearch
- запуске elasticsearch в docker

Используя докер образ [centos:7](https://hub.docker.com/_/centos) как базовый и
[документацию по установке и запуску Elastcisearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/targz.html):

- составьте Dockerfile-манифест для elasticsearch
- соберите docker-образ и сделайте `push` в ваш docker.io репозиторий
- запустите контейнер из получившегося образа и выполните запрос пути `/` c хост-машины

Требования к `elasticsearch.yml`:
- данные `path` должны сохраняться в `/var/lib`
- имя ноды должно быть `netology_test`

В ответе приведите:
- текст Dockerfile манифеста

```
FROM centos:7

RUN yum install -y perl-Digest-SHA
COPY elasticsearch-8.3.3-linux-x86_64.tar.gz .
RUN tar -xzf elasticsearch-8.3.3-linux-x86_64.tar.gz

RUN adduser elasticsearch && chown -R elasticsearch /elasticsearch-8.3.3 && chown -R elasticsearch /var/lib

CMD ["./bin/elasticsearch"]

USER elasticsearch
WORKDIR elasticsearch-8.3.3
COPY elasticsearch.yml ./config/
EXPOSE 9200
```

- ссылку на образ в репозитории dockerhub

https://hub.docker.com/repository/docker/e2sly4rz/elastic-ntlg

- ответ `elasticsearch` на запрос пути `/` в json виде

```bash
curl localhost:9200
{
  "name" : "netology_test",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "hlg2Ftc0T7eTLYPf_xy2hA",
  "version" : {
    "number" : "8.3.3",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "801fed82df74dbe537f89b71b098ccaff88d2c56",
    "build_date" : "2022-07-23T19:30:09.227964828Z",
    "build_snapshot" : false,
    "lucene_version" : "9.2.0",
    "minimum_wire_compatibility_version" : "7.17.0",
    "minimum_index_compatibility_version" : "7.0.0"
  },
  "tagline" : "You Know, for Search"
}
```

Подсказки:
- возможно вам понадобится установка пакета perl-Digest-SHA для корректной работы пакета shasum
- при сетевых проблемах внимательно изучите кластерные и сетевые настройки в elasticsearch.yml
- при некоторых проблемах вам поможет docker директива ulimit
- elasticsearch в логах обычно описывает проблему и пути ее решения

Далее мы будем работать с данным экземпляром elasticsearch.

## Задача 2

В этом задании вы научитесь:
- создавать и удалять индексы
- изучать состояние кластера
- обосновывать причину деградации доступности данных

Ознакомтесь с [документацией](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-create-index.html)
и добавьте в `elasticsearch` 3 индекса, в соответствии со таблицей:

| Имя | Количество реплик | Количество шард |
|-----|-------------------|-----------------|
| ind-1| 0 | 1 |
| ind-2 | 1 | 2 |
| ind-3 | 2 | 4 |

```bash
curl -X PUT localhost:9200/ind-1 -H 'Content-Type: application/json' -d'{ "settings": { "number_of_shards": 1,  "number_of_replicas": 0 }}'
curl -X PUT localhost:9200/ind-2 -H 'Content-Type: application/json' -d'{ "settings": { "number_of_shards": 2,  "number_of_replicas": 1 }}'
curl -X PUT localhost:9200/ind-3 -H 'Content-Type: application/json' -d'{ "settings": { "number_of_shards": 4,  "number_of_replicas": 2 }}'
```

Получите список индексов и их статусов, используя API и **приведите в ответе** на задание.

```bash
curl http://localhost:9200/_cat/indices?v

health status index uuid                   pri rep docs.count docs.deleted store.size pri.store.size
green  open   ind-1 V0_zLes7Tsuy_8GIOwEQEw   1   0          0            0       225b           225b
yellow open   ind-2 DK86WMAwSpygv7vvO77FUQ   2   1          0            0       450b           450b
yellow open   ind-3 qyvtLTksT_6wvA9wv486qg   4   2          0            0       900b           900b
```

Получите состояние кластера `elasticsearch`, используя API.

```bash
curl localhost:9200/_cat/shards?v

index            shard prirep state      docs  store ip         node
.geoip_databases 0     p      STARTED      41 38.8mb 172.17.0.2 netology_test
ind-2            0     p      STARTED       0   225b 172.17.0.2 netology_test
ind-2            0     r      UNASSIGNED
ind-2            1     p      STARTED       0   225b 172.17.0.2 netology_test
ind-2            1     r      UNASSIGNED
ind-1            0     p      STARTED       0   225b 172.17.0.2 netology_test
ind-3            0     p      STARTED       0   225b 172.17.0.2 netology_test
ind-3            0     r      UNASSIGNED
ind-3            0     r      UNASSIGNED
ind-3            1     p      STARTED       0   225b 172.17.0.2 netology_test
ind-3            1     r      UNASSIGNED
ind-3            1     r      UNASSIGNED
ind-3            2     p      STARTED       0   225b 172.17.0.2 netology_test
ind-3            2     r      UNASSIGNED
ind-3            2     r      UNASSIGNED
ind-3            3     p      STARTED       0   225b 172.17.0.2 netology_test
ind-3            3     r      UNASSIGNED
ind-3            3     r      UNASSIGNED



curl localhost:9200/_cluster/health?pretty
{
  "cluster_name" : "elasticsearch",
  "status" : "yellow",
  "timed_out" : false,
  "number_of_nodes" : 1,
  "number_of_data_nodes" : 1,
  "active_primary_shards" : 8,
  "active_shards" : 8,
  "relocating_shards" : 0,
  "initializing_shards" : 0,
  "unassigned_shards" : 10,
  "delayed_unassigned_shards" : 0,
  "number_of_pending_tasks" : 0,
  "number_of_in_flight_fetch" : 0,
  "task_max_waiting_in_queue_millis" : 0,
  "active_shards_percent_as_number" : 44.44444444444444
}

```

Как вы думаете, почему часть индексов и кластер находится в состоянии yellow?

> В кластере только 1 нода. Реплицировать шарды некуда.

Удалите все индексы.

```bash
curl -X DELETE localhost:9200/ind-{1..3}
```

**Важно**

При проектировании кластера elasticsearch нужно корректно рассчитывать количество реплик и шард,
иначе возможна потеря данных индексов, вплоть до полной, при деградации системы.

## Задача 3

В данном задании вы научитесь:
- создавать бэкапы данных
- восстанавливать индексы из бэкапов

Создайте директорию `{путь до корневой директории с elasticsearch в образе}/snapshots`.

```bash
sudo docker exec 61a18448dabc mkdir snapshots
```

Используя API [зарегистрируйте](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-register-repository.html#snapshots-register-repository)
данную директорию как `snapshot repository` c именем `netology_backup`.

**Приведите в ответе** запрос API и результат вызова API для создания репозитория.

```bash
curl -X PUT localhost:9200/_snapshot/netology_backup?pretty -H 'Content-Type: application/json' -d'{"type": "fs", "settings": { "location":"/elasticsearch-8.3.3/snapshots" }}'

{
  "acknowledged" : true
}
```

Создайте индекс `test` с 0 реплик и 1 шардом и **приведите в ответе** список индексов.

```bash
curl -X PUT localhost:9200/test?pretty -H 'Content-Type: application/json' -d'{ "settings": { "number_of_shards": 1,  "number_of_replicas": 0 }}'

{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "test"
}
```

[Создайте `snapshot`](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-take-snapshot.html)
состояния кластера `elasticsearch`.

**Приведите в ответе** список файлов в директории со `snapshot`ами.

```bash
curl -X PUT "localhost:9200/_snapshot/netology_backup/snapshot_1?wait_for_completion=true&pretty"

{
  "snapshot" : {
    "snapshot" : "snapshot_1",
    "uuid" : "gfl1gJ4XSZO6le25xClayw",
    "repository" : "netology_backup",
    "version_id" : 8030399,
    "version" : "8.3.3",
    "indices" : [
      ".geoip_databases",
      "test"
    ],
    "data_streams" : [ ],
    "include_global_state" : true,
    "state" : "SUCCESS",
    "start_time" : "2022-08-24T12:30:05.436Z",
    "start_time_in_millis" : 1661344205436,
    "end_time" : "2022-08-24T12:30:07.638Z",
    "end_time_in_millis" : 1661344207638,
    "duration_in_millis" : 2202,
    "failures" : [ ],
    "shards" : {
      "total" : 2,
      "failed" : 0,
      "successful" : 2
    },
    "feature_states" : [
      {
        "feature_name" : "geoip",
        "indices" : [
          ".geoip_databases"
        ]
      }
    ]
  }
}

sudo docker exec 8156fa8be7b4 ls snapshots

index-0
index.latest
indices
meta-gfl1gJ4XSZO6le25xClayw.dat
snap-gfl1gJ4XSZO6le25xClayw.dat
```

Удалите индекс `test` и создайте индекс `test-2`. **Приведите в ответе** список индексов.

```bash
curl -X DELETE "localhost:9200/test?pretty"

{
  "acknowledged" : true
}

curl -X PUT localhost:9200/test-2?pretty -H 'Content-Type: application/json' -d'{ "settings": { "number_of_shards": 1,  "number_of_replicas": 0 }}'

{
  "acknowledged" : true,
  "shards_acknowledged" : true,
  "index" : "test-2"
}

curl localhost:9200/_cat/indices?v
health status index  uuid                   pri rep docs.count docs.deleted store.size pri.store.size
green  open   test-2 rdZeLt5_Q32Xsy25-R7KUQ   1   0          0            0       225b           225b
```

[Восстановите](https://www.elastic.co/guide/en/elasticsearch/reference/current/snapshots-restore-snapshot.html) состояние
кластера `elasticsearch` из `snapshot`, созданного ранее.

**Приведите в ответе** запрос к API восстановления и итоговый список индексов.

```bash
curl -X POST localhost:9200/_snapshot/netology_backup/snapshot_1/_restore?pretty -H 'Content-Type: application/json' -d'{"include_global_state":true}'

{
  "accepted" : true
}

curl localhost:9200/_cat/indices?v

health status index  uuid                   pri rep docs.count docs.deleted store.size pri.store.size
green  open   test   ovJCL61mS1qCA9PCZQznWQ   1   0          0            0       225b           225b
green  open   test-2 rdZeLt5_Q32Xsy25-R7KUQ   1   0          0            0       225b           225b
```

Подсказки:
- возможно вам понадобится доработать `elasticsearch.yml` в части директивы `path.repo` и перезапустить `elasticsearch`

---
