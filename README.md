# Практика 1. Инструменты разработки программного обеспечения

[![Build Status](https://travis-ci.org/Itseez-NNSU-SummerSchool2015/practice1-devtools.svg)](https://travis-ci.org/Itseez-NNSU-SummerSchool2015/practice1-devtools)

## Цели

__Цель данной работы__ - реализовать набор простых фильтров, а именно фильтра 
сглаживания посредством вычисления среднего по окрестности, линейного фильтра 
с произвольным ядром, медианного фильтра, горизонтального фильтра Собеля. 
В задаче предполагается, что задана двумерная матрица с элементами типа 
`unsigned char`. Также для некоторых фильтров имеется размер ядра, либо само 
ядро фильтра, которое используется для вычисления линейной свертки. По существу 
ядро также является двумерной матрицей.

Проект представляет собой инфраструктуру для проведения практики по освоению
следующих инструментов разработки:

  - Система контроля версий [Git](https://git-scm.com/book/en/v2).
  - [Google Test Framework](https://code.google.com/p/googletest).
  - Утилита [CMake](http://www.cmake.org) для сборки исходных кодов.

## Общая структура проекта

Структура проекта:

  - `3rdparty` - библиотека Google Test.
  - `include` - директория для размещения заголовочных файлов.
  - `samples` - директория для размещения демо-приложений.
  - `src` - директория с исходными кодами.
  - `test` - директория с тестами.
  - `.gitignore` - перечень файлов, игнорируемых Git.
  - `.travis.yml` - конфигурационный файл для системы автоматического 
     тестирования Travis-CI.
  - `CMakeLists.txt` - корневой файл для сборки проекта с помощью CMake.
  - `README.md` - информация о проекте, которую вы сейчас читаете.

В проекте содержатся следующие модули:

  - Общий модуль `matrix` (`./include/matrix.hpp`, `./src/matrix.cpp`),
    содержащий простейшую реализацию класса матриц. Предполагается, что он не
    редактируется при реализации фильтров.
  - Модуль `filters`( `./include/filters.hpp`, `./src/filters_opencv.cpp`, 
    `./src/filters_fabrics.cpp`), содержащий объявление абстрактного класса
    фильтров (`filters.hpp`) и его наследника, который реализует перечисленные
    фильтры средствами библиотеки OpenCV (`filters_opencv.cpp`), а также метод
    создания конкретной реализации класса фильтров (`filters_fabrics.cpp`).
  - Тесты для класса матриц и фильтров (`matrix_test.cpp`, `filters_test.cpp`).
  - Пример использования фильтра (`matrix_sample.cpp`).

## Задачи

__Основные задачи__:

  1. Разработать программную реализацию сглаживания посредством вычисления 
     среднего по окрестности. 
  2. Реализовать линейный фильтр с произвольным ядром. 
  3. Разработать реализацию медианного фильтра.
  4. Реализовать горизонтальный фильтр Собеля.

__Дополнительные задачи__:
  1. Расширить реализацию класса матриц следующими операциями и тестами к ним:
     1. Транспонирование матрицы.
     2. Умножение матриц (в виде перегрузки операции).
     3. Поэлементные операции сложения и вычитания (в виде перегрузки операции).
     4. Методы инициализации фиксированной константой, инициализация единичной 
        матрицы, инициализация диагональной матрицы с фиксированной константой.
     5. Вычисление детерминанта.
  2. Расширить программную реализацию вертикальным фильтром Собеля и 
     морфологическими операциями эрозии и дилатации.

## Общие инструкции по работе с Git

В данном разделе описана типичная последовательность действий, которую 
необходимо выполнить перед тем, как начать работать с проектом. Далее 
для определенности используется репозиторий practice1-devtools.

  1. Создать аккаунт на [github.com](https://github.com), если такой
     отсутствует. Для определенности обозначим аккаунт `github-account`.

  2. Сделать fork репозитория
     <https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools> (в
     терминологии Git upstream-репозиторий) к себе в личный профиль с названием
     github-account. В результате будет создана копия репозитория с названием
     <https://github.com/github-account/practice1-devtools>
     (origin-репозиторий).

  3. Клонировать [origin][origin] репозиторий к себе на локальный компьютер,
     воспользовавшись следующей командой:

  ```
  $ git clone https://github.com/github-account/practice1-devtools
  ```

  4. Перейти в директорию practice1-devtools:

  ```
  $ cd ./practice1-devtools
  ```

  5. Настроить адрес upstream-репозитория (потребуется при обновлении локальной 
     версии репозитория):

  ```
  $ git remote add upstream https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools
  ```

  6. Настроить имя пользователя, из под которого будут выполняться все операции
     с репозиторием Git:

  ```
  $ git config --global user.name "github-account"
  ```

  Примечание: если не выполнить указанную операцию при попытке размещения изменений
  на сервер потребуется вводить ваш `gihub-account` (появится сообщение, приведенное ниже).
  ```
  warning: push.default is unset; its implicit value is changing in
  Git 2.0 from 'matching' to 'simple'. To squelch this message
  and maintain the current behavior after the default changes, use:

    git config --global push.default matching

  To squelch this message and adopt the new behavior now, use:

    git config --global push.default simple

  When push.default is set to 'matching', git will push local branches
  to the remote branches that already exist with the same name.

  In Git 2.0, Git will default to the more conservative 'simple'
  behavior, which only pushes the current branch to the corresponding
  remote branch that 'git pull' uses to update the current branch.

  See 'git help config' and search for 'push.default' for further information.
  (the 'simple' mode was introduced in Git 1.7.11. Use the similar mode
  'current' instead of 'simple' if you sometimes use older versions of Git)

  Username for 'https://github.com': github-account
  Password for 'https://github-account@github.com':
  ```

Когда сделан форк репозитория у вас создается по умолчанию единственная ветка 
master. Тем не менее, при решении независимых задач следует создавать рабочие 
ветки. Далее показаны основные команды для управления ветками на примере ветки
`filter-implementation`.

  1. Получить список веток:
  
  ```
  $ git branch [-v]
  # [-v] - список с информацией о последних коммитах
  ```

  2. Создать ветку:

  ```
  $ git branch filter-implementation
  ```

  3. Создать ветку `filter-implementation` и перейти в нее:

  ```
  $ git checkout [-b] filter-implementation
  # [-b] - создание и переход в ветку <branch_name>
  ```
  4. Удалить ветку в локальном репозитории:

  ```
  $ git branch -d <branch_name>
  ```

  5. Удалить ветку на сервере:

  ```
  $ git push [remotename] :[branch]
  ```

При работе с файлами в ветке необходимо управлять изменениями. Далее приведен
перечень основных команд в предположении, что текущей рабочей веткой 
является `filter-implementation`.

  1. Получить список текущих изменений:
  
  ```
  $ git status
  ```
  
  2. Пометить файл как добавленный в текущую ветку репозитория (файл будет
     добавлен после выполнения команды `commit`):
  
  ```
  $ git add [<file_name>]
  # <file_name> - название файла для добавления в commit
    если вместо имени указан символ *, то будут добавлены все новые файлы, 
    не совпадающие с масками, указанными в .gitignore
  ```

  3. Добавить изменения в текущую ветку локального репозитория:

  ```  
  $ git commit [-m "<message_to_commit>"] [-a]
  # [-a] - автоматически добавляет изменения для существующих на сервере файлов
    без выполнения команды git add
  # [--amend] - перезаписывает последний коммит (используется, если не забыты
    изменения)
  ```

  4. Разместить изменения, которые были добавлены в локальный репозиторий 
     с помощью команды `commit`:

  ```
  $ git push origin [filter-implementation]
  ```

  5. Удалить файлы или директории (!без опции -f для файлов, состояния 
     которых совпадают с состояниям на сервере):

  ```
  $ git rm [-f] [--cached]
  # [-f] - принудительное удаление (файла с измененным состоянием)
  # [--cached] - удаление файлов на сервере, но не в локальной директории
  ```

  6. Переименовать файлы (или 3 команды: `mv`, `git rm`, `git add`):

  ```
  $ git mv <file_from> <file_to>
  ```

Когда в проекте работает несколько человек, то вполне естественная ситуация -
необходимость слияния изменений и разрешение конфликтов.

  1. Слияние (вариант 1):

  ```
  $ git merge upstream/master - слияние изменений из ветки upstream в master
  $ git merge master - слияние изменений из ветки master в текущую ветку
  ```

  2. Слияние (вариант 2):

  ```
  $ git checkout <branch_name> - переход в ветку <branch_name> (при необходимости)
  $ git rebase <base_branch> [<branch_name>] - слияние изменений из ветки <base_branch> в ветку <branch_name>
  $ git checkout <base_branch>
  $ git merge <branch_name>
  ```

  3. Инструмент для разрешения конфликтов:

  ```
  $ git mergetool
  ```

## Сборка проекта с помощью CMake и Microsoft Visual Studio

В данном разделе описана типичная последовательность действий, которую 
необходимо выполнить для сборки проекта с использованием утилиты CMake и 
Microsoft Visual Studio. Далее для определенности выполняется сборка проекта 
из репозитория practice1-devtools.
  1. Рядом с директорией `practice1-devtools` создайте
     `practice1-devtools-build`. В новой директории будут размещены файлы
     решения и проектов, сгенерированные с помощью CMake.

     ```
     $ cd ..
     $ mkdir practice1-devtools-build
     ```

  2. Перейдите в директорию `practice1-devtools-build`:

     ```
     $ cd ./practice1-devtools-build
     ```

  3. Сгенерируйте файлы решения и проектов с помощью утилиты CMake. Для этого
     можно воспользоваться графическим приложением, входящим в состав
     утилиты, либо выполнить следующую команду:

  ```
  $ cmake -DOpenCV_DIR="<OpenCVConfig.cmake-path>" -G <generator-name> <path-to-practice1-devtools>
  # <OpenCVConfig.cmake-path> - директория, в которой установлена 
    библиотека OpenCV и расположен файл OpenCVConfig.cmake
  # <generator-name> - название генератора, в случае тестовой
    инфраструктуры участников школы может быть "Visual Studio 10 Win64"
    (если в командной строке набрать cmake без параметров, то можно просмотреть
    список доступных генераторов)
  # <path-to-practice1-devtools> - путь до директории
    practice1-devtools, где лежат исходные коды проекта (если предыдущие действия
    выполнены корректно, то это директория`../practice1-devtools`)
  ```

  Примечание: после запуска утилиты CMake на экране появятся сообщения, приведенные
  ниже.

  ```
  -- The C compiler identification is MSVC 16.0.30319.1
  -- The CXX compiler identification is MSVC 16.0.30319.1
  -- Check for working C compiler using: Visual Studio 10 Win64
  -- Check for working C compiler using: Visual Studio 10 Win64 -- works
  -- Detecting C compiler ABI info
  -- Detecting C compiler ABI info - done
  -- Check for working CXX compiler using: Visual Studio 10 Win64
  -- Check for working CXX compiler using: Visual Studio 10 Win64 -- works
  -- Detecting CXX compiler ABI info
  -- Detecting CXX compiler ABI info - done
  -- OpenCV ARCH: x64
  -- OpenCV RUNTIME: vc10
  -- OpenCV STATIC: OFF
  -- Found OpenCV 2.4.11 in c:/OpenCV-2.4.11/opencv/build/x64/vc10/lib
  -- You might need to add c:\OpenCV-2.4.11\opencv\build\x64\vc10\bin to your PATH to be able to run your applications.
  --
  -- General configuration for practice1
  -- ======================================
  --
  --    Configuration:        Release
  --    OpenCV build path:    c:\OpenCV-2.4.11\opencv\build
  --
  -- Configuring done
  -- Generating done
  -- Build files have been written to: C:/Users/ss2015/Documents/GitHub/practice1-devtools
  ```

  4. Откройте сгенерированный файл решения `practice1.sln`.
  5. Нажмите правой кнопкой мыши по проекту `ALL_BUILD` и выберите пункт
     `Rebuild` контекстного меню, чтобы собрать решение. В результате все
     бинарные файлы будут размещены в директории
     `practice1-devtools-build/bin`.
  6. Для запуска приложения и тестов откройте командную строку (`cmd.exe` в `Пуск`)
     и перейдите в директорию с бинарными файлами, используя команду `cd`.
  7. Можно запустить приложение с примером использования матриц. Возможное сообщение 
     при запуске: `The program can't start because
     opencv_imgproc2411d.dll is missing from your computer. Try reinstalling
     the program to fix this problem.`. Решение 1: скопировать 
     соответствующую библиотеку из `C:\openCV-2.4.11\opencv\build\x64\vcX\bin`
     (`vcX` - версия Visual Studio, принимает значения `vc10`, `vc11`, `vc12`)
     к бинарным файлам проекта. Потребуется три таких библиотеки 
     `opencv_core2411d.dll`, `opencv_highgui2411d.dll`, `opencv_imgproc2411d.dll`.
     Решение 2: добавить путь `C:\openCV-2.4.11\opencv\build\x64\vcX\bin`
     (не забудьте заменить `vcX` на правильную версию Visual Studio)
     в переменную окружения `PATH`.
  8. По аналогии следует запустить тесты. В результате прохождения тестов
     появится список тестов и статус подобно тому, что показан ниже.

  ```
  [==========] Running 16 tests from 2 test cases.
  [----------] Global test environment set-up.
  [----------] 5 tests from Matrix
  [ RUN      ] Matrix.matrix_can_set_zeros
  [       OK ] Matrix.matrix_can_set_zeros (0 ms)
  [ RUN      ] Matrix.matrix_can_set_ones
  [       OK ] Matrix.matrix_can_set_ones (0 ms)
  [ RUN      ] Matrix.comparator_returns_true_on_equal_matrices
  [       OK ] Matrix.comparator_returns_true_on_equal_matrices (0 ms)
  [ RUN      ] Matrix.comparator_returns_false_on_non_equal_matrices
  [       OK ] Matrix.comparator_returns_false_on_non_equal_matrices (0 ms)
  [ RUN      ] Matrix.copy_ctor_works
  [       OK ] Matrix.copy_ctor_works (1 ms)
  [----------] 5 tests from Matrix (4 ms total)

  [----------] 11 tests from Instance/FiltersTest
  [ RUN      ] Instance/FiltersTest.box_filter_on_zero_mat/0
  [       OK ] Instance/FiltersTest.box_filter_on_zero_mat/0 (0 ms)
  [ RUN      ] Instance/FiltersTest.box_filter_on_ones_mat/0
  [       OK ] Instance/FiltersTest.box_filter_on_ones_mat/0 (0 ms)
  [ RUN      ] Instance/FiltersTest.box_filter_on_correct_mat/0
  [       OK ] Instance/FiltersTest.box_filter_on_correct_mat/0 (26 ms)
  [ RUN      ] Instance/FiltersTest.filter2d_on_zero_mat/0
  [       OK ] Instance/FiltersTest.filter2d_on_zero_mat/0 (0 ms)
  [ RUN      ] Instance/FiltersTest.filter2d_on_ones_mat/0
  [       OK ] Instance/FiltersTest.filter2d_on_ones_mat/0 (0 ms)
  [ RUN      ] Instance/FiltersTest.filter2d_on_correct_mat/0
  [       OK ] Instance/FiltersTest.filter2d_on_correct_mat/0 (23 ms)
  [ RUN      ] Instance/FiltersTest.median_on_zero_mat/0
  [       OK ] Instance/FiltersTest.median_on_zero_mat/0 (0 ms)
  [ RUN      ] Instance/FiltersTest.median_on_correct_mat/0
  [       OK ] Instance/FiltersTest.median_on_correct_mat/0 (25 ms)
  [ RUN      ] Instance/FiltersTest.SobelOx_on_zero_mat/0
  [       OK ] Instance/FiltersTest.SobelOx_on_zero_mat/0 (0 ms)
  [ RUN      ] Instance/FiltersTest.SobelOx_on_ones_mat/0
  [       OK ] Instance/FiltersTest.SobelOx_on_ones_mat/0 (0 ms)
  [ RUN      ] Instance/FiltersTest.sobel_ox_on_correct_mat/0
  [       OK ] Instance/FiltersTest.sobel_ox_on_correct_mat/0 (30 ms)
  [----------] 11 tests from Instance/FiltersTest (112 ms total)

  [----------] Global test environment tear-down
  [==========] 16 tests from 2 test cases ran. (120 ms total)
  [  PASSED  ] 16 tests.
  ```

__Примечание:__ генератор проекта должен совпадать с версией Visual Studio, которая
использовалась при сборке OpenCV. В пакете OpenCV доступны библиотеки, собранные
под VS 2010, 2012, 2013.

## Общая последовательность действий

  1. Сделать форк upstream-репозитория.
  2. Клонировать origin-репозиторий к себе на локальную машину (раздел 
     [Общие инструкции по работе с Git](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Общие-инструкции-по-работе-с-git)).
  3. Собрать проект и проверить его работоспособность, запустив тесты и пример
     (раздел [Сборка проекта с помощью 
     CMake и MS VS](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Сборка-проекта-с-помощью-cmake-и-microsoft-visual-studio)).
  4. Создать рабочую ветку для размещения реализаций фильтров (раздел 
     [Общие инструкции по работе с Git](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Общие-инструкции-по-работе-с-git)).
  5. Создать собственного наследника `FiltersSurname` от абстрактного класса фильтров.
  6. Реализовать последовательно все чисто виртуальные методы базового класса -
     методы фильтрации, перечисленные в разделе 
     [Основные задачи](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Задачи).
  7. При реализации каждого фильтра следует пересобрать проект и проверить 
     работоспособность тестов. Изменения необходимо постоянно фиксировать, выкладывая
     в рабочую ветку на сервер (раздел 
     [Общие инструкции по работе с Git](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Общие-инструкции-по-работе-с-git)).
  8. Сделать Pull Request в репозиторий upstream.
  9. Выбрать и решить одну из задач списка 
     [Дополнительные задачи](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Задачи).
     Необходимо проконтролировать, чтобы задача не была выбрана другими 
     участниками школы. В противном случае, в основной репозиторий попадет
     первая полностью готовая реализация.

## Детальная инструкция по выполнению работы

  1. Сделать форк upstream-репозитория.
     1. Открыть в браузере upstream-репозиторий 
        <https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools>.
     2. В правом верхем углу нажать кнопку `Fork`.
     3. Выбрать в качестве организации, куда направить форк, организацию, 
        соответствующую вашему аккаунту @github-account.
  2. Клонировать origin-репозиторий к себе на локальную машину.
     1. Открыть командную строку Git Bash (или Git Shell в зависимости от того,
        какой git-клиент установлен на вашей машине). Для этого необходимо найти
        соответствующий ярлык на рабочем столе или в меню "Пуск".
     2. Воспользоваться перечнем инструкций, описанных в разделе
        [Общие инструкции по работе с Git](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Общие-инструкции-по-работе-с-git)).
  3. Собрать проект и проверить его работоспособность, запустив тесты и пример.
     1. Воспользоваться инструкцией по сборке и запуску, описанной в разделе 
        [Сборка проекта с помощью CMake и MS VS](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Сборка-проекта-с-помощью-cmake-и-microsoft-visual-studio)).
     2. Чтобы проверить работоспособность тестов, достаточно запустить
        `practice1_test.exe` и `matrix_sample.exe`. Если все тесты "зеленые", 
        то можно двигаться дальше.
  
  ```
  cd practice1-devtools-build/bin
  ./practice1_test.exe
  ./matrix_sample.exe
  ```
  
  4. Создать рабочую ветку и перейти в нее для размещения реализаций фильтров 
     (подробный перечень инструкций в разделе 
     [Общие инструкции по работе с Git](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Общие-инструкции-по-работе-с-git)).
  5. Создать собственного наследника `FiltersSurname` от абстрактного класса фильтров.
     1. Создать файл `filters_YOUR_NAME.cpp` (файл с реализацией в файловой системе)
        для собственных реализаций фильтров. 
     2. В качестве шаблона необходимо воспользоваться `filters_opencv.cpp`. 
     3. Не забудьте после создания файла в файловой системе запустить еще 
        раз CMake, чтобы подцепить их в решение.
     4. В файл `filters.hpp` необходимо добавить в `enum FILTERS_IMPLEMENTATIONS`
        значение, соответствующее вашей реализации фильтра. Назовите его
        согласно вашей фамилии `YOUR_NAME`. Указанное перечисление используется
        при прогоне одних и тех же тестов на всех реализациях класса фильтров.
     5. В файле `filters_fabrics.cpp` объявите функцию 
       `Filters* createFiltersYourName()`. Данная функция будет использована
        при создании объекта класса с вашей реализации фильтров.
     6. В функции `Filters* createFilters(FILTERS_IMPLEMENTATIONS impl)` (файл
       `filters_fabrics.cpp`) необходимо добавить еще одну ветку у оператора-
        переключателя `switch`, по которой будет проходить исполнение программы,
        если создан объект класса фильтров `YOUR_NAME`.
     7. В файл `filters_YOUR_NAME.cpp` необходимо поместить реализацию функции
        создания объекта класса фильтров с вашей реализацией 
        `Filters* createFiltersYourName()`. Указание: для примера можно
        воспользоваться аналогичной функцией в файле `filters_opencv.cpp`.
  6. Реализовать последовательно все чисто виртуальные методы базового класса -
     методы фильтрации, перечисленные в разделе 
     [Основные задачи](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Задачи).
  7. При реализации каждого фильтра следует пересобрать проект и проверить 
     работоспособность тестов. Прототипы методов фильтрации изменять нельзя!
     Изменения необходимо постоянно фиксировать, выкладывая в рабочую
     ветку на сервер (разделы 
     [Общие инструкции по работе с Git](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Общие-инструкции-по-работе-с-git),
     [Сборка проекта с помощью CMake и MS VS](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Сборка-проекта-с-помощью-cmake-и-microsoft-visual-studio)).
  8. Разработать пример использования фильтра.
     1. Создать файл `filter_sample_SURNAME.cpp`.
     2. В качестве шаблона следует использовать `matrix_sample.cpp`.
  9. Собрать проект и проверить работоспособность разработанного примера
     использования собственных фильтров (раздел
     [Сборка проекта с помощью CMake и MS VS](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Сборка-проекта-с-помощью-cmake-и-microsoft-visual-studio))
  10. Сделать Pull Request в репозиторий upstream, чтобы проверить
      работоспособность тестов на Travis-CI и позволить преподавателям
      сделать ревью Вашего кода.
  11. Выбрать и решить одну из задач списка 
     [Дополнительные задачи](https://github.com/Itseez-NNSU-SummerSchool2015/practice1-devtools#Задачи).
     Необходимо проконтролировать, чтобы задача не была выбрана другими 
     участниками школы. В противном случае, в основной репозиторий попадет
     первая полностью готовая реализация.

<!-- LINKS -->

[origin]: https://github.com/github-account/practice1-devtools
