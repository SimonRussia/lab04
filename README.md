## Laboratory work III

**Отчет:** Овчаров Анисим (ИУ8-33)


## Tasks

- [X] 1. Создать публичный репозиторий с названием **lab03** и с лиценцией **MIT**
- [X] 2. Ознакомиться со ссылками учебного материала
- [X] 3. Выполнить инструкцию учебного материала
- [X] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ #Командой export создаем новую переменную командной оболочки и экспортируем ее, тем самым, делаем ее доступной для других процессов, которые могут быть запущены из этого интерпретатора.
$ export GITHUB_USERNAME=SimonRussia #Создаем переменную для имени пользователя в GitHub.
$ export GITHUB_EMAIL=git.streisand@gmail.com #Создаем переменную для e-mail пользователя в GitHub.
$ alias edit=<nano|vi|vim|subl>
```

```ShellSession
$ #Связка команд для создания каталога и перехода в него.
$ mkdir lab03 && cd lab03
$ #Создаем Git-репозиторий.
$ git init
$ #Добавляем глобальные параметры:
$ #Имя пользователя в GitHub.
$ git config --global user.name ${GITHUB_USERNAME}
$ #E-mail пользователя в GitHub.
$ git config --global user.email ${GITHUB_EMAIL}
$ #Открывает редактор для внесения изменений в файл конфигураций.
$ #В нем увидим добавленные выше параметры, и можем внести изменения или добавить другие параметры, непосредственно в самом файле .gitconfig.
$ git config -e --global
$ #Подключает укзанные ветви для их отслеживание и работы с ними.
$ #origin указывает именно на УДАЛЕННУЮ ветвь master, а не на ту, которая находится в рабочем дереве.
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab03
$ #Объединение в текущую ветвь удаленной ветви.
$ #Копируем содержимое удаленной ветви в локальную.
$ git pull origin master
$ #Создаем файл README.md
$ touch README.md
$ #Отображает пути и файлы в рабочем дереве, которые отличаются от удаленных.
$ #Красный цвет - изменения не подтверждены.
$ #Зеленые цвет - подтвержденные изменения.
$ git status
$ #Добавляет изменения из рабочего дерева в удаленное.
$ git add README.md
$ #Сохраняет внесенные изменения, добавляет сопровождающее сообщение.
$ git commit -m"added README.md"
$ #Обновляет удаленные ссылки, используя локальные ссылки, при отправке объектов из рабочего дерева.
$ git push origin master
```

Добавить на сервисе **GitHub** в репозитории **lab03** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
```

```ShellSession
$ #Снова копируем содержимое локальной ветви.
$ #В частности созанный на сайте файл (.gitignore).
$ git pull origin master
$ #Просмотрим журналы (историю) фиксаций.
$ git log
```

```ShellSession
$ #Создаем локальные каталоги.
$ mkdir sources
$ mkdir include
$ mkdir examples
$ #Создаем 4 файлы и добавляем в них код.
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out) {
  out << text;
}

void print(const std::string& text, std::ofstream& out) {
  out << text;
}
EOF
```

```ShellSession
$ cat > include/print.hpp <<EOF
#include <string>
#include <fstream>
#include <iostream>

void print(const std::string& text, std::ostream& out = std::cout);
void print(const std::string& text, std::ofstream& out);
EOF
```

```ShellSession
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv) {
  print("hello");
}
EOF
```

```ShellSession
$ cat > examples/example2.cpp <<EOF
#include <fstream>
#include <print.hpp>

int main(int argc, char** argv) {
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```ShellSession
$ #Редактируем файл README.md.
$ edit README.md
```

```ShellSession
$ #Проверяем состояние.
$ #Отображается список файлов помеченных красным.
$ git status
$ #Данной командой мы индексируем все созданные нами файлы и каталоги.
$ git add .
$ #Подтверждаем внесенные изменения.
$ #После подтверждения, еще раз проверяем состояние.
$ #Теперь все файлы помечены зеленым цветом.
$ git commit -m"added sources"
$ #Выгружаем все наши файлы и каталоги в локальный репозиторий.
$ git push origin master
```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=03
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2017 Братья Вершинины
```
