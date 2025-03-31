## Что такое Elasticsearch

![](my-obsidian/langs%20and%20more/SQL/ElasticSearch/images/01.png)

[Elasticsearch](https://www.elastic.co/elasticsearch/) — это хранилище документов, c возможностью создавать полнотекстовые индексы для последующего поиска, чаще всего используемое в качестве поискового движка. ElasticSearch добавляет к возможностям библиотеки [Apache Lucene](https://lucene.apache.org/), на котором основан, такие функции, как шардирование, репликацию, удобный JSON API и множество других улучшений. Это делает ElasticSearch одним из самых популярных решений для полнотекстового поиска.

## Основные понятия

![](my-obsidian/langs%20and%20more/SQL/ElasticSearch/images/02.png)

### Индекс

Индекс предназначен для группировки данных в логические структуры. У нас может быть индекс по фильмам, или индекс по товарам, или какой-то еще. Если проводить аналогию с реляционными базами данных – то это как таблица в реляционной базе (только более гибкая, так как может хранить документы разной схемы).

### Документы

Это непосредственно записи в индексе, если мы опять сравниваем с реляционными базами данных, то это аналогично строке в таблице, но со своими отличиями.

### Запросы

Запросы в Elastic Search предназначены для поиска и фильтрации данных в индексах. С помощью запросов мы можем находить документы, соответствующие определенным условиям, сортировать результаты по релевантности, выполнять агрегации и многое другое.  
Если сравнивать с реляционной базой данных – то это как обычные sql запросы, только выглядят по-другому.

## Установка и запуск через Docker

Для запуска Elasticsearch локально проще всего воспользоваться Docker:

```bash
docker run -p 9200:9200 -e "discovery.type=single-node" elasticsearch:7.17.22
```

Проверить что все работает как надо можно перейдя в браузере по адресу `localhost:9200`

В ответ должно появиться следующее

```json
{
  "name" : "8038cbce69bf",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "S5nOCHwSQC6dLhUN8iZDZQ",
  "version" : {
    "number" : "7.17.22",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "38e9ca2e81304a821c50862dafab089ca863944b",
    "build_date" : "2024-06-06T07:35:17.876121680Z",
    "build_snapshot" : false,
    "lucene_version" : "8.11.3",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

## API Elasticsearch

Взаимодействие с Elasticsearch происходит по http протоколу. Ниже представлена коллекция Postman с различными запросами к Elasticsearch: создание индекса, добавление, получение и удаление документов, поиск.

[ElasticSearch Postman collection](https://suchkov.tech/wp-content/uploads/2024/08/ElasticSearch-Postman-collection.zip)[Скачать](https://suchkov.tech/wp-content/uploads/2024/08/ElasticSearch-Postman-collection.zip)

## Материалы

Репозиторий с проектом [github.com/SuchkovDenis/elasticexample](https://github.com/SuchkovDenis/elasticexample)

Видео на youtube [https://youtu.be/vxE1aGTEnbE](https://youtu.be/vxE1aGTEnbE)