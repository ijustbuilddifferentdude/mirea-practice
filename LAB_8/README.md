# LAB_8

Калинов Артем

Информационно-аналитические технологии поиска угроз инорфмационной
безопасности

# Анализ данных сетевого трафика с использованием аналитической in-memory СУБД DuckDB

## Цель работы

1.  Изучить возможности СУБД DuckDB для обработки и анализ больших
    данных
2.  Получить навыки применения DuckDB совместно с языком
    программирования R
3.  Получить навыки анализа метаинфомации о сетевом трафике
4.  Получить навыки применения облачных технологий хранения, подготовки
    и анализа данных: Yandex Object Storage, Rstudio Server.

## Исходные данные

1.  Операционная система Windows 10
2.  Rstudio Desktop
3.  Интерпретатор языка R версии 4.4.2
4.  Github
5.  Yandex Object Storage
6.  DuckDB

## План выполнения работы

1.  Подключиться к БД
2.  Выполнить аналитические задания

## Содержание Работы

### Шаг 1. Подключиться к БД

```r
library(dplyr)
```

    Присоединяю пакет: 'dplyr'

    Следующие объекты скрыты от 'package:stats':

        filter, lag

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union

```r
library(DBI)
library(duckdb)

#download.file('https://storage.yandexcloud.net/arrow-datasets/tm_data.pqt', destfile = "tm_data.pqt")

con <- dbConnect(duckdb())
dbExecute(con,"CREATE TABLE efimov_df as SELECT * FROM read_parquet('tm_data.pqt')")
```

    [1] 105747730

### Шаг 2. Выполнить аналитические задания

#### 1. Надите утечку данных из Вашей сети

```r
dbGetQuery(con,"SELECT src FROM efimov_df WHERE (src LIKE '12.%' OR src LIKE '13.%' OR src LIKE '14.%') AND NOT (dst LIKE '12.%' AND dst LIKE '13.%' AND dst LIKE '14.%') GROUP BY src ORDER by sum(bytes) DESC LIMIT 1")
```

               src
    1 13.37.84.125

#### 2. Надите утечку 2

```r
dbGetQuery(con,"SELECT time, COUNT(*) AS trafictime
FROM (
    SELECT
        timestamp,src,dst,bytes,
        (
            (src LIKE '12.%' OR src LIKE '13.%' OR src LIKE '14.%')
            AND (dst NOT LIKE '12.%' AND dst NOT LIKE '13.%' AND dst NOT LIKE '14.%')
        ) AS trafic,
        EXTRACT(HOUR FROM epoch_ms(CAST(timestamp AS BIGINT))) AS time
    FROM efimov_df
) sub
WHERE trafic = TRUE AND time BETWEEN 0 AND 24
GROUP BY time
ORDER BY trafictime DESC;")
```

       time trafictime
    1    16    4490576
    2    22    4489703
    3    18    4489386
    4    23    4488093
    5    19    4487345
    6    21    4487109
    7    17    4483578
    8    20    4482712
    9    13     169617
    10    7     169241
    11    0     169068
    12    3     169050
    13   14     169028
    14    6     169015
    15   12     168892
    16   10     168750
    17    2     168711
    18   11     168684
    19    1     168539
    20    4     168422
    21   15     168355
    22    5     168283
    23    9     168283
    24    8     168205

```r
dbGetQuery(con,"
SELECT src
FROM (
    SELECT src, SUM(bytes) AS total_bytes
    FROM (
        SELECT *,
            EXTRACT(HOUR FROM epoch_ms(CAST(timestamp AS BIGINT))) AS time
        FROM efimov_df
    ) sub
    WHERE src <> '13.37.84.125'
        AND (src LIKE '12.%' OR src LIKE '13.%' OR src LIKE '14.%')
        AND (dst NOT LIKE '12.%' AND dst NOT LIKE '13.%' AND dst NOT LIKE '14.%')
        AND time BETWEEN 1 AND 15
    GROUP BY src
) grp
ORDER BY total_bytes DESC
LIMIT 1;")
```

              src
    1 12.55.77.96

#### 3. Надите утечку 3

```r
dbGetQuery(con,"SELECT port, MAX(bytes) - AVG(bytes)
        FROM efimov_df
        WHERE src != '13.37.84.125' AND src != '12.55.77.96'
        AND (regexp_matches(src,'^(12|13|14)\\.'))
        AND NOT (regexp_matches(dst,'^(12|13|14)\\.'))
        GROUP BY port
        ORDER BY MAX(bytes) - AVG(bytes) DESC")
```

       port (max(bytes) - avg(bytes))
    1    37               174312.0109
    2    39               163385.8261
    3   105               162681.0147
    4    40               160069.5736
    5    75               159551.3910
    6    89               159019.7193
    7   102               158498.2456
    8    81               157301.8304
    9   119               155052.6375
    10   74               154721.2971
    11  118               151821.6760
    12   29               150729.4813
    13  114               149597.0905
    14   52               149457.2073
    15   56               148400.3599
    16   55               147062.5682
    17   92               146951.4479
    18   57               145375.1491
    19   44               144456.6315
    20   65               143321.7749
    21  115               140656.5430
    22   34                  840.5010
    23   50                  785.4990
    24   72                  754.4533
    25   82                  749.4924
    26   68                  745.6607
    27   27                  741.4552
    28   96                  739.3726
    29   23                  737.3030
    30   22                  731.6059
    31  121                  731.4658
    32   80                  723.7275
    33   77                  720.5506
    34   61                  710.6674
    35   26                  701.5026
    36   94                  700.8950
    37   79                  693.4624
    38  124                  212.4346
    39   25                    0.0000
    40   42                    0.0000
    41   51                    0.0000
    42   90                    0.0000
    43  106                    0.0000
    44  112                    0.0000
    45  117                    0.0000
    46  123                    0.0000

```r
dbGetQuery(con,"SELECT src, AVG(bytes)
          FROM efimov_df
          WHERE src != '13.37.84.125' AND src != '12.55.77.96'
          AND (regexp_matches(src,'^(12|13|14)\\.'))
          AND NOT (regexp_matches(dst,'^(12|13|14)\\.'))
          AND port = 37
          GROUP BY src
          ORDER BY AVG(bytes) DESC
          LIMIT 1;")
```

               src avg(bytes)
    1 14.31.107.42    42953.8

## Оценка результата

В результате практической работы были выполнены аналитические задания с
использованием DuckDB

## Вывод

В результате выполнения практической работы были освоены инструменты
работы с DuckDB и Yandex Object Storage
