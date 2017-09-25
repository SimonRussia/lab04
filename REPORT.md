## Laboratory work IV

Данная лабораторная работа посвещена изучению систем автоматизации сборки проекта на примере **CMake**

```ShellSession
$ open https://cmake.org/
```

## Tasks

- [X] 1. Создать публичный репозиторий с названием **lab04** на сервисе **GitHub**
- [X] 2. Ознакомиться со ссылками учебного материала
- [X] 3. Выполнить инструкцию учебного материала
- [X] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ export GITHUB_USERNAME=<имя_пользователя>
```

>Подготовка к выполнению Лабораторной работы №4.
```ShellSession
$ # Копируем репозиторий Лаб. №3 в каталог Лаб. №4.
$ git clone https://github.com/${GITHUB_USERNAME}/lab03.git lab04
$ cd lab04
$ # Локально отключаемся от ветки Лаб. №3.
$ git remote remove origin
$ # Подключаемся к ветке Лаб. №4.
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab04.git
```

>CMAKE
```ShellSession 
$ g++ -I./include -std=c++11 -c sources/print.cpp
$ ls print.o
$ ar rvs print.a print.o
$ file print.a
$ g++ -I./include -std=c++11 -c examples/example1.cpp
$ ls example1.o
$ g++ example1.o print.a -o example1
$ ./example1 && echo
```

>CMAKE
```ShellSession
$ g++ -I./include -std=c++11 -c examples/example2.cpp
$ ls example2.o
$ g++ example2.o print.a -o example2
$ ./example2
$ cat log.txt && echo
```

>Удаляем файлы.
```ShellSession
$ # Стираем объектные файлы.
$ rm -rf example1.o example2.o print.o
$ # Стираем архив.
$ rm -rf print.a
$ # Стираем исполняемые файлы.
$ rm -rf example1 example2
$ # Стираем текстовый файл.
$ rm -rf log.txt
```

>Редактируем файл 'CMakeLists.txt'. _**(#1)**_
```ShellSession
$ cat > CMakeLists.txt <<EOF
$ # Проверка версии CMake. (Если версия установленой программы старее указаной, произайдёт аварийный выход).
cmake_minimum_required(VERSION 3.0)
$ # Название проекта
project(print)
EOF
```

>Редактируем файл 'CMakeLists.txt'. _**(#2)**_
```ShellSession
$ cat >> CMakeLists.txt <<EOF
$ # Установка переменной CMAKE_CXX_STANDARD со значением 11.
set(CMAKE_CXX_STANDARD 11)
$ # Установка переменной CMAKE_CXX_STANDARD_REQUIRED со значением ON.
set(CMAKE_CXX_STANDARD_REQUIRED ON)
EOF
```

>Редактируем файл 'CMakeLists.txt'.  _**(#3)**_
```ShellSession
$ cat >> CMakeLists.txt <<EOF
$ # Создание статической библиотеки с именем print.
add_library(print STATIC \${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
EOF
```

>Редактируем файл 'CMakeLists.txt'.  _**(#4)**_
```ShellSession
$ cat >> CMakeLists.txt <<EOF
$ # Добавляем путь к 'include' для заголовочных файлов.
include_directories(\${CMAKE_CURRENT_SOURCE_DIR}/include)
EOF
```

```ShellSession
$ cmake -H. -B_build
$ cmake --build _build
```

>Создает исполняемые файл.
```ShellSession
$ cat >> CMakeLists.txt <<EOF
$ # Создает исполняемый файл с именем example1.
add_executable(example1 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
$ # Создает исполняемый файл с именем example2.
add_executable(example2 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
EOF
```

>Линкуем программы с библиотекой.
```ShellSession
$ cat >> CMakeLists.txt <<EOF
$ # Линковка программ example с библиотекой print.
target_link_libraries(example1 print)
target_link_libraries(example2 print)
EOF
```


```ShellSession
$ cmake --build _build
$ cmake --build _build --target print
$ cmake --build _build --target example1
$ cmake --build _build --target example2
```

```ShellSession
$ ls -la _build/libprint.a
$ _build/example1 && echo
hello
$ _build/example2
$ cat log.txt && echo
hello
```

>Скачиваем файл 'CMakeLists.txt' из репозитория Лаб. №4.
```ShellSession
$ # Скачиваем содержимое репозитория Лаб. №4.
$ git clone https://github.com/tp-labs/lab04 tmp
$ # Переносим файл 'CMakeLists.txt' в основной каталог.
$ mv -f tmp/CMakeLists.txt .
$ # Стираем дерикторию 'tmp'
$ rm -rf tmp
```

>Настройки cmake проекта.
```ShellSession
$ # Выводим файл 'CMakeLists.txt' в стандартный вывод.
$ cat CMakeLists.txt
$ # -H. устанавливаем каталог в который сгенерируется файл 'CMakeLists.txt'.
$ # -B_build указывает директорию для собираемых файлов. !(Используется только в связке с -H).
$ # -D - заменяет команду 'set'. Пример: set(CMAKE_INSTALL_PREFIX _install).
$ cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
$ # --build _build создает бинарное дерево проекта.
$ # --target указывает необходимые для обработки цели. (В данном примере будет обработан target install)
$ # Если не указывать --target, то, по умолчанию, будут обработаны все target указанные в 'CMakeLists.txt'.
$ cmake --build _build --target install
#tree графически выводит в териминале структуру проекта.
$ tree _install
```

>Заключительный этап Лаб. №4.
```ShellSession
$ # Индексируем файл 'CMakeLists.txt'.
$ git add CMakeLists.txt
$ # Создаем 'commit'.
$ git commit -m"added CMakeLists.txt"
$ # Выгружаем локальную ветку в репозиторий Лаб. №4.
$ git push origin master
```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=04
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [Autotools](http://www.gnu.org/software/automake/manual/html_node/Autotools-Introduction.html)
- [CMake](https://cgold.readthedocs.io/en/latest/index.html)

```
Copyright (c) 2017 Братья Вершинины
```
