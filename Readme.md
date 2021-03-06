Библиотека расчета координат кадра
==================================

Как пользоваться?
-----------------

Для работы потребуется установить СMake версии 3.12 или выше. При установке
разрешить исталлятору добавить cmake.exe в PATH хотя бы для текущего
пользователя (иначе каждый раз придется прописывать полный путь до cmake.exe,
что явно не очень удобно).

Первым делом нужно сконфигурировать проект и создать проектные файлы (Solution в
случае Visual Studio, make-файлы для gcc и т.д.).

Для этого нужно:

1. Создать папку сборки, в которую попадут сгенерированные файлы. Имя может быть произвольное, для простоты пусть будет "build". Перейти в неё.

    ```
    mkdir build
    cd build
    ```

    *Например, если на моей машине исходные файлы проекта в папке D:/Develop/Koord_kadra, то я создам соотвествующую папку D:/Build/Koord_kadra*

2. Запустить **cmake** из этой папки и сгенерировать файлы проекта
    ```
    cmake -G "название_генератора" -DCMAKE_INSTALL_PREFIX="путь_к_папке_установки" "путь_к_исходникам"
    ```
    *Папка установки - это папка, в которой после сборки будут лежать файлы, готовые для передачи другим разработчикам.*

    На моей машине это выглядит так:
    ```
    cmake -G "Visual Studio 15 2017 Win64" -DCMAKE_INSTALL_PREFIX="D:/Deploy/Koord_kadra" "D:/Develop/Koord_kadra"
    ```
    *Список доступных имен генераторов для текущей платформы можно получить через вызвов cmake --help*

3. Все, можно работать.

В случае Visual Studio просто открываешь созданный solution и работаешь как обычно. В нем будут 2 проекта: библиотека и тестовое приложение.

Как поделиться собранной библиотекой с другими?
-----------------------------------------------

После того, как библиотека собрана и протестирована, нужно сделать следующее:

1. Вызвать цель INSTALL (в случае Visual Studio - правый клик на ней в Solution Exlorer, кликнуть в выпадающем меню Build).

    Можно то же самое сделать из консоли (из папки сборки):
    ```
    cmake --build . --target INSTALL --config Release
    ```

2. Все, если сборка прошла без ошибок - в папке установки появятся все необходмые файлы. Эту папку целиком нужно передать другим разработчикам.