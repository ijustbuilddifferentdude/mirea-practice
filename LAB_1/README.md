# LAB_1

Калинов Артем

Информационно-аналитические технологии поиска угроз инорфмационной
безопасности

# Введение в R

## Цель работы

Развить навыки работы с языком программирования R и закрепить знания
базовых типов данных и операций с ними

## Исходные данные

1.  Операционная система Windows 10
2.  Rstudio Desktop
3.  Интерпретатор языка R версии 4.4.2
4.  Github
5.  Программный пакет swirl

## План выполнения работы

1.  Установить программный пакет swirl
2.  Выполнить курсы, указанные в задание

## Содержание Работы

### Шаг 1. Установка программного пакет swirl.

На данном шаге необходимо установить программный пакет swirl.

![](./Images/1.png)

### Шаг 2. Запуск swirl и выбор обучения

![](./Images/2.png)

![](./Images/3.png)

### Шаг 3. Выполнение курсов

```r
5 + 7
```

    [1] 12

```r
x <- 5 + 7
```

```r
x
```

    [1] 12

```r
y <- x - 3
```

```r
y
```

    [1] 9

```r
z <- c(1.1, 9, 3.14)
```

```r
?c
```

    запускаю httpd сервер помощи... готово

```r
z
```

    [1] 1.10 9.00 3.14

```r
z2 <- c(z,555)
```

```r
c (z,555,z)
```

    [1]   1.10   9.00   3.14 555.00   1.10   9.00   3.14

```r
z * 2 + 100
```

    [1] 102.20 118.00 106.28

```r
my_sqrt <- sqrt(z - 1)
```

```r
my_sqrt
```

    [1] 0.3162278 2.8284271 1.4628739

```r
 my_div <- z / my_sqrt
```

```r
my_div
```

    [1] 3.478505 3.181981 2.146460

```r
c(1, 2, 3, 4) + c(0, 10)
```

    [1]  1 12  3 14

```r
c(1, 2, 3, 4) + c(0, 10, 100)
```

    Warning in c(1, 2, 3, 4) + c(0, 10, 100): длина большего объекта не является
    произведением длины меньшего объекта

    [1]   1  12 103   4

```r
z * 2 + 100
```

    [1] 102.20 118.00 106.28

```r
z * 2 + 1000
```

    [1] 1002.20 1018.00 1006.28

```r
my_div
```

    [1] 3.478505 3.181981 2.146460

```r
getwd()
```

    [1] "C:/Users/NEfimov/Desktop/Учеба/IATPUIB/LAB_1"

```r
ls()
```

    [1] "my_div"  "my_sqrt" "x"       "y"       "z"       "z2"

```r
x <- 9
```

```r
ls()
```

    [1] "my_div"  "my_sqrt" "x"       "y"       "z"       "z2"

```r
dir()
```

    [1] "Images"           "mytest2.R"        "mytest3.R"        "README.md"
    [5] "README.qmd"       "README.rmarkdown" "testdir"

```r
?list.files
```

```r
args(list.files())
```

    NULL

```r
args(list.files)
```

    function (path = ".", pattern = NULL, all.files = FALSE, full.names = FALSE,
        recursive = FALSE, ignore.case = FALSE, include.dirs = FALSE,
        no.. = FALSE)
    NULL

```r
old.dir <- getwd()
```

```r
dir.create("testdir")
```

    Warning in dir.create("testdir"): 'testdir' уже существует

```r
setwd("testdir")
```

```r
file.create("mytest.R")
```

    [1] TRUE

```r
ls()
```

    [1] "my_div"  "my_sqrt" "old.dir" "x"       "y"       "z"       "z2"

```r
list.files()
```

    [1] "Images"           "mytest.R"         "mytest2.R"        "mytest3.R"
    [5] "README.md"        "README.qmd"       "README.rmarkdown" "testdir"

```r
file.exists("mytest.R")
```

    [1] TRUE

```r
file.info("mytest.R")
```

             size isdir mode               mtime               ctime
    mytest.R    0 FALSE  666 2024-11-24 19:46:21 2024-11-24 19:46:21
                           atime exe
    mytest.R 2024-11-24 19:46:21  no

```r
file.rename("mytest.R", "mytest2.R")
```

    [1] TRUE

```r
file.copy("mytest2.R", "mytest3.R")
```

    [1] FALSE

```r
file.path("mytest3.R")
```

    [1] "mytest3.R"

```r
file.path("folder1", "folder2")
```

    [1] "folder1/folder2"

```r
?dir.create
```

```r
dir.create(file.path('testdir2', 'testdir3'), recursive = TRUE)
```

```r
unlink('testdir2', recursive = TRUE)
```

```r
setwd(old.dir)
```

```r
1:20
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

```r
pi:10
```

    [1] 3.141593 4.141593 5.141593 6.141593 7.141593 8.141593 9.141593

```r
15:1
```

     [1] 15 14 13 12 11 10  9  8  7  6  5  4  3  2  1

```r
?':'
```

```r
seq(1,20)
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

```r
seq(0, 10, by=0.5)
```

     [1]  0.0  0.5  1.0  1.5  2.0  2.5  3.0  3.5  4.0  4.5  5.0  5.5  6.0  6.5  7.0
    [16]  7.5  8.0  8.5  9.0  9.5 10.0

```r
my_seq <- seq(5, 10, length=30)
```

```r
length(my_seq)
```

    [1] 30

```r
1:length(my_seq)
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
    [26] 26 27 28 29 30

```r
seq(along.with = my_seq)
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
    [26] 26 27 28 29 30

```r
seq_along(my_seq)
```

     [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25
    [26] 26 27 28 29 30

```r
rep(0, times=40)
```

     [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
    [39] 0 0

```r
rep(c(0, 1, 2), times = 10)
```

     [1] 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2

```r
rep(c(0, 1, 2), each = 10)
```

     [1] 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2

```r
num_vect <- c(0.5, 55, -10, 6)
```

```r
tf <- (num_vect < 1)
```

```r
tf <- num_vect < 1
```

```r
tf
```

    [1]  TRUE FALSE  TRUE FALSE

```r
num_vect >= 6
```

    [1] FALSE  TRUE FALSE  TRUE

```r
my_char <- c("My", "name", "is")
```

```r
my_char
```

    [1] "My"   "name" "is"

```r
paste(my_char, collapse = " ")
```

    [1] "My name is"

```r
my_name <- c(my_char, "Johnny")
```

```r
my_name
```

    [1] "My"     "name"   "is"     "Johnny"

```r
paste(my_name, collapse = " ")
```

    [1] "My name is Johnny"

```r
paste("Hello", "world!", sep = " ")
```

    [1] "Hello world!"

```r
paste(1:3, c("X", "Y", "Z"), sep = "")
```

    [1] "1X" "2Y" "3Z"

```r
paste(LETTERS, 1:4, sep = "-")
```

     [1] "A-1" "B-2" "C-3" "D-4" "E-1" "F-2" "G-3" "H-4" "I-1" "J-2" "K-3" "L-4"
    [13] "M-1" "N-2" "O-3" "P-4" "Q-1" "R-2" "S-3" "T-4" "U-1" "V-2" "W-3" "X-4"
    [25] "Y-1" "Z-2"

```r
x <- c(44, NA, 5, NA)
```

```r
x * 3
```

    [1] 132  NA  15  NA

```r
y <- rnorm(1000)
```

```r
 z <- rep(NA, 1000)
```

```r
my_data <- sample(c(y, z), 100)
```

```r
my_na <- is.na(my_data)
```

```r
my_na
```

      [1] FALSE  TRUE  TRUE FALSE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE  TRUE
     [13] FALSE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE FALSE FALSE  TRUE
     [25] FALSE  TRUE FALSE  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE
     [37]  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE
     [49] FALSE FALSE  TRUE FALSE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE FALSE
     [61]  TRUE FALSE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE
     [73]  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE  TRUE FALSE
     [85] FALSE FALSE FALSE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE
     [97]  TRUE FALSE  TRUE  TRUE

```r
my_data == NA
```

      [1] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
     [26] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
     [51] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
     [76] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA

```r
sum(my_na)
```

    [1] 43

```r
my_data
```

      [1]  0.683938830           NA           NA -1.288150726 -1.254294679
      [6]           NA -0.637524508           NA -1.375581461 -0.003722559
     [11]  1.189724626           NA -1.165861151           NA  0.554053743
     [16]  0.172681470 -0.467409109           NA           NA           NA
     [21]           NA  0.069948743 -1.305184570           NA  0.163614157
     [26]           NA  1.432424902           NA  1.014589577  0.107094722
     [31]           NA  0.854177905 -0.009797410 -0.193421132 -0.538611369
     [36]  0.758416048           NA           NA  0.039952478 -1.053142342
     [41]           NA  1.488231269 -0.810597571 -0.368142178           NA
     [46] -1.111302794           NA -0.374616905  0.229249349 -1.039323875
     [51]           NA -0.468277191           NA           NA  1.352816105
     [56]           NA -0.589900010 -0.586478029           NA -0.080160992
     [61]           NA  0.364938808           NA           NA  0.056643982
     [66]           NA -0.372447603  1.687266079           NA  0.734473431
     [71] -0.510726060  1.677047020           NA           NA -0.257289583
     [76]           NA           NA  0.528820330           NA  0.660159148
     [81]           NA           NA           NA -1.211711286  0.543710700
     [86] -1.850313387 -0.092931885           NA           NA -0.445347458
     [91]  0.517046829 -1.957800832 -1.312731670           NA -2.811232468
     [96]  0.099546294           NA  1.154939366           NA           NA

```r
0 / 0
```

    [1] NaN

```r
Inf - Inf
```

    [1] NaN

По окончании каждого из курсов также будет предложено получить
подтверждение прохождения (однако, для этого необходим специальный
токен)

![](./Images/4.png)

## Оценка результата

В результате работы была установлена библиотека swirl, а также были
пройдены 5 подкурсов в рамках обучения “R Programming: The basics of
programming in R”

## Вывод

Были изучены базовые команды и функции языка R - работа с переменными,
векторами, файлами, циклами и NA.
