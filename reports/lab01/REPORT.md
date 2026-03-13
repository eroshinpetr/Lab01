# Отчет по лабораторной работе №1
**Тема:** Изучение утилит для разработки проектов  
**Выполнил:** Eroshin Petr IU8-21  
**Дата выполнения:** 04.03.2026  
**Среда выполнения:** Linux (Ubuntu) на VirtualBox  
**Репозиторий с файлами:** https://github.com/eroshinpetr/lab01

## 1. Выполнение туториала

### 1.1. Настройка переменных окружения
```bash
export GITHUB_USERNAME=eroshinpetr
export GIST_TOKEN=ghp_XXXXX   # токен скрыт
alias edit=nano

1.2. Создание структуры директорий
mkdir -p ${GITHUB_USERNAME}/workspace
cd ${GITHUB_USERNAME}/workspace
mkdir -p workspace/tasks/ workspace/projects/ workspace/reports/
cd workspace

1.3. Установка Node.js
wget https://nodejs.org/dist/v6.11.5/node-v6.11.5-linux-x64.tar.xz
tar -xf node-v6.11.5-linux-x64.tar.xz
rm -rf node-v6.11.5-linux-x64.tar.xz
mv node-v6.11.5-linux-x64 node
export PATH=${PATH}:`pwd`/node/bin

1.4. Создание скрипта activate
mkdir scripts
cat > scripts/activate <<EOF
export PATH=\${PATH}:`pwd`/node/bin
EOF
source scripts/activate

1.5. Установка gist
gem install gist
(umask 0077 && echo ${GIST_TOKEN} > ~/.gist)

1.6. Клонирование лабораторной работы
export LAB_NUMBER=01
git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
mkdir -p reports/lab${LAB_NUMBER}
cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
cd reports/lab${LAB_NUMBER}


2. Домашнее задание

2.1. Скачивание и распаковка Boost
cd ~
wget https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz
tar -xzf boost_1_69_0.tar.gz
mv boost_1_69_0 ~/boost_1_69_0
cd ~/boost_1_69_0
**Результат:** Архив успешно скачан (размер ~107 МБ) и распакован. Создана директория `~/boost_1_69_0`.

2.2. Подсчёт файлов
Без учёта вложенных директорий:

find . -maxdepth 1 -type f | wc -l
Вывод: 16

С учётом вложенных директорий:
find . -type f | wc -l
Вывод: 62110

Заголовочные файлы (.h, .hpp, .hxx):
find . -type f \( -name "*.h" -o -name "*.hpp" -o -name "*.hxx" \) | wc -l
Вывод: 15208

Файлы .cpp:
find . -type f -name "*.cpp" | wc -l
Вывод: 13789

Остальные файлы:
find . -type f ! \( -name "*.h" -o -name "*.hpp" -o -name "*.hxx" -o -name "*.cpp" \) | wc -l
Вывод: 33113

2.3. Поиск файла any.hpp
find . -name "any.hpp" -type f
Полный список сохранён в файле any_list.txt.

2.4. Поиск упоминаний boost::asio
grep -r "boost::asio" . | wc -l
Вывод: 17424

Полный список упоминаний сохранён в файле asio_list.txt.

2.5. Компиляция Boost
./bootstrap.sh
./b2
Лог компиляции сохранён в файле compilation.log.

2.6. Перенос статических библиотек
mkdir -p ~/boost-libs
cp ~/boost-install/lib/*.a ~/boost-libs/
**Результат:** Все статические библиотеки успешно скопированы в `~/boost-libs`. Размер каждого файла записан в [`lib_sizes.txt`](https://github.com/eroshinpetr/Lab01/blob/main/reports/lab01/lib_sizes.txt), топ-10 самых тяжёлых — в [`top10.txt`](https://github.com/eroshinpetr/Lab01/blob/main/reports/lab01/top10.txt).

2.7. Размер каждого файла в ~/boost-libs
du -sh ~/boost-libs/*
Полный список размеров сохранён в lib_sizes.txt.

2.8. Топ-10 самых тяжёлых файлов
du -sh ~/boost-libs/* | sort -rh | head -10

Вывод:
4.5M    libboost_wave.a
2.7M    libboost_regex.a
2.7M    libboost_math_tr1l.a
2.7M    libboost_math_tr1.a
2.6M    libboost_math_tr1f.a
2.3M    libboost_unit_test_framework.a
2.3M    libboost_test_exec_monitor.a
2.0M    libboost_locale.a
1.6M    libboost_program_options.a
1.2M    libboost_serialization.a

Полный список сохранён в top10.txt.
