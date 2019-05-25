## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [ ] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [ ] 3. Ознакомиться со ссылками учебного материала
- [ ] 4. Выполнить инструкцию учебного материала
- [ ] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
#Создание наших переменных для гита
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
#Выбор редактора текста (в моем случае это нано)
$ alias edit=<nano|vi|vim|subl>
```

```ShellSession
#Переход в папку workspace
$ cd ${GITHUB_USERNAME}/workspace
#Активация скриптов
$ source scripts/activate
```

```ShellSession
#Создание папки
$ mkdir ~/.config
#Записываем информацию в файл (с помощью cat)
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
#Настроеваем протокол для гита
$ git config --global hub.protocol https
```

```ShellSession
#Создаем и автоматически переходим в папку
$ mkdir projects/lab02 && cd projects/lab02
#Создаем пустой репозиторий
$ git init
#Настраеваем гит( а именно вводим имя пользователя и пароль)
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global
#Подключение к удаленному репозиторию
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
#Добавляем ветку мастер (в иных случаях функция обновляет ветку)
$ git pull origin master
#Создаем файл
$ touch README.md
#Проверяем статус
$ git status
#Добавляем файл в гит
$ git add README.md
#Оставляем свой коммит
$ git commit -m"added README.md"
#Пушим наш файл
$ git push origin master
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
.idea/
```

```ShellSession
#Обновляем ветку
$ git pull origin master
#Смотрим историю изменений
$ git log
```

```ShellSession
#Создаем папки
$ mkdir sources
$ mkdir include
$ mkdir examples
#Создаем файлы и вводим нужные данные
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```ShellSession
#Создаем файлы и вводим нужные данные
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```ShellSession
#Создаем файлы и вводим нужные данные
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```ShellSession
#Создаем файлы и вводим нужные данные
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```ShellSession
#Редактируем файлы
$ edit README.md
```

```ShellSession
#Пушим в гит , то что изменили
$ git status
$ git add .
$ git commit -m"added sources"
$ git push origin master
```

## Report

```ShellSession
#Переход в папку labs
$ cd ~/workspace/labs/
#Создаем переменную
$ export LAB_NUMBER=02
#Клонируем репозиторий в папку
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
#Создаем папку
$ mkdir reports/lab${LAB_NUMBER}
#Копируем файлы в эту папку
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
#Переходим в нее
$ cd reports/lab${LAB_NUMBER}
#Редактируем файл и отправляем его на гист
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
4. Добавьте этот файл в локальную копию репозитория.
5. Закоммитьте изменения с *осмысленным* сообщением.
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
8. Запуште изменения в удалёный репозиторий.
9. Проверьте, что история коммитов доступна в удалёный репозитории.
```ShellSession
#ниже представлен листинг программы , 1-3 пункты сделал на гитхабе.
$ git init
$ touch hello_world.cpp
$ git add hello_world.cpp
$ git commit -m "[my first commit]"
$ git log
$ git clone https://github.com/TurboFen/Homework.git
$ git add . 
$ git commit -m "modified program"
$ git push origin master
$ cd Homework
$ git push origin master
$ git commit -m "my modified program"
$ git add hello_world.cpp
$ git commit -m "my modified program"
$ git push origin master

```
### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
3. **commit**, **push** локальную ветку в удалённый репозиторий.
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.
```ShellSession
$ git checkout -b patch1
$ git add hello_world.cpp
$ git commit -m "my new modified program"
$ git push origin patch1
$ git add hello_world.cpp
$ git commit -m "pull request modify"
$ git push origin patch1
#Удаление удаленной ветки
$ git push origin --delete patch1
$ git pull origin master
$ git checkout master
$ git pull origin master
#Удаление локальной ветки
$ git branch -d patch1
```
### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
7. Сделайте *force push* в ветку `patch2`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.
```ShellSession
$ git checkout -b patch2
#Установка и применение текстового редактора
$ sudo apt install clang-format
$ clang-format -style=Mozilla hello_world.cpp > task3.cpp
$ mv task3.cpp hello_word.cpp
$ git add helo_world.cpp
$ git commit -m "change for clang-format"
$ git pull origin patch2
$ git checkout master
#Ниже я разбирался с устранением конфликта в пул реквесте и последней операцией некоторые репозитории удалились но в интернете пишут что это  нормально
$ git pull origin patch2
$ git checkout patch2
$ git pull origin master
$ git add hello_world.cpp
$ git commit -m "try to rebase"
$ git push origin patch2
$ git pull origin patch2
$ git rebase master
$ git push --force origin master
```
## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2019 The ISC Authors
```
