1) Сначала скачиваю исходники
2) Устанавливаю cmake
3) Создаем CMakeLists.txt
```
cmake_minimum_required(VERSION 3.4)
add_library(formatter STATIC formatter.h formatter.cpp)
```
4) настраиваю репозиторию сборки
```
cmake ~/workspace/projects/lab03/formatter_lib/
```
5) Запускаю саму сборку командой make
6) Библиотека собрана


Второе задание

1) Копирую библиотеку из предыдущего задания в наш текущий проект
2) Создаю CMakeLists.txt
```
cmake_minimum_required(VERSION 3.4)
project(formatter_ex)
include_directories(formatter_lib)
add_subdirectory(formatter_lib)
add_library(formatter_ex STATIC formatter_ex.h formatter_ex.cpp)
target_link_libraries(formatter_ex formatter)
```

3) Командами include_directories(formatter_lib) и add_subdirectory(formatter_lib) мы подключаю библиотеку из предыдущего задания
4) Этой командой: target_link_libraries(formatter_ex formatter) мы активирую подключенную библиотеку
5) Союираю пронкт командой make
6) Проект собран


Задание 3

Приложение hello_world

1) Переношу все нужные библиотеки в папку проекта
2) Создаю CMakeLists.txt
```
cmake_minimum_required(VERSION 3.4)
project(hello_world)
include_directories(formatter_ex_lib)
add_subdirectory(formatter_ex_lib)
add_executable(hello_world hello_world.cpp)
target_link_libraries(hello_world formatter_ex)
```
3) строчка: project(hello_world) задает название проекта
4) Собираю проект
5) Запускаю полученное приложение:
world 
-------------------------
hello, world!
----------------------


Приложение Solver

1) В этот раз нужно добавить две библиотеки
2) Копирую их в текущую директорию
3) Для библиотеки Sover я еще не писала CMakeLists.txt
4) Пишу его сейчас:
```
cmake_minimum_required(VERSION 3.4)
add_library(formatter STATIC formatter.h formatter.cpp)
```
5) Дальше нужно написать основной симэйк:
```
cmake_minimum_required(VERSION 3.4)
project(solver)
add_executable(solver equation.cpp)
include_directories(formatter_ex_lib)
add_subdirectory(formatter_ex_lib)
include_directories(solver_lib)
add_subdirectory(solver_lib)
target_link_libraries(solver formatter_ex)
```
6) Тут я подключила обе библиотеки
7) При попытке собрать проект g++ начал ругаться на неизвестную функцию sqrtf, пришлось мне добавть строчку #include<math.h> в исходники библиотеки solve. Иначе не программа отказывалась собираться
8) Запустила только что собранное приложение:

1  
1
1
-------------------------
error: discriminant < 0
-------------------------

9) Видимо приложение считало корни квадратного уравнения
