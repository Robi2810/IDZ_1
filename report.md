# Архитектура вычислительных систем
## Индивидуальное домашнее задание №1
### Вариант 14

### Вишняков Родион Сергеевич 
##### группа БПИ213
###### 16 октября 2022 г.
[![Typing SVG](https://readme-typing-svg.herokuapp.com?color=%2336BCF7&lines=Faculty+of+Computer+science+student)](https://git.io/typing-svg)


Задание: Сформировать массив B из элементов массива A заменой всех отрицательных значений на максимум из массива A.

### Отчёт
![img](/p1.png)

### 4 балла
•	Приведено решение задачи на C.

Код находится в файле main.c
Далее в командную строку вводим данные команды для получения искомого ассемблерского файла, а также исполняемого файла.


$gcc -O0 -Wall -fno-asynchronous-unwind-tables main.c -o main


$gcc -O0 -Wall -fno-asynchronous-unwind-tables -S main.c -o main.s


$gcc main.s -o

Лишние макросы были убраны за счёт использования аргументов командной строки. 

`gcc -masm=intel -fno-asynchronous-unwind-tables -fno-jump-tables -fno-stack-protector -fno-exceptions -S main.c`

Необходимые комментарии находятся в main.s


Файл | Тест           | Результат | Соотвествие 
-----------|----------------|:---------:|------------:
main.c     | 1 -1 -1 1 1    | 1 1 1 1 1 |        True | 
main.s     | 1 -1 -1 1 1    | 1 1 1 1 1 |        True |
main.c     | 3 -3 4 -5 6	   | 3 6 4 6 6 |       True      |
main.s     | 3 -3 4 -5 6    | 3 6 4 6 6 |       True      |
main.c     | 1 -2 -3 -4 9	  | 1 9 9 9 9 |      True       |
main.s     | 1 -2 -3 -4 9	  | 1 9 9 9 9 |     True        |
main.c     | 1 -1 -1 -1 -1	 | 1 1 1 1 1 |      True       |
main.s     | 1 -1 -1 -1 -1	  | 1 1 1 1 1 |     True        |


Представлено полное тестовое покрытие, дающее одинаковый результат на обоих программах.
После тестирования программ можно сделать вывод, что работа программы является корректной и эквивалентной.


Для проверки ввести команды:
#### gcc main.s
#### gcc ./a.out

### 5	баллов
В дополнение к требованиям на предыдущую оценку

•	В реализованной программе я использовал функции с передачей данных через параметры.
![img](/p2.png)

Измененная программа была сохранена в файле main2.c

Функциональность:


input_max() - получает на вход размер массива N и указатель на массив в которые будут заполняться данные. При выполнении этой функции мы получаем массив и функция возвращает максимальное число среди элементов массива.


out_put() - получает на вход размер массива N и указатель на массив, который необходимо напечатать.


task() - получает на вход указатель на начальный массив и массив, в который будет записываться результат, количество элементов в массиве и максимальный элемент из изначального массива.


Комментарии:
В ассемблерскую программу при вызову функций были добавлены комментарии, которые описывают передачу фактических параметров и перенос возвращаемого результат, в случае когда функция ничего не возвращает был добавлен комментарий (void )
В этой программе не использовались формальные параметры.

### 6 баллов
В дополнение к требованиям на предыдущую оценку
Я сделал рефакторинг программы на ассемблере за счет максимального использования регистров процессора. Измененная программа сохранена в файле “main2-refactored.s”. В основном были использованы регистры: r12, r13, r14, r15. В процессе рефакторинга соотвественно были изменены команды (например movl -> movq), а также были изменены регистры, которые контактировали с “новыми” регистрами (например: movl eax, -24(%rbp) -> movq rax, r12).
Также были добавлены комментарии, которые поясняют использование регистров в соответсвии с переменными из исходной программы на С.

Файл | Тест           | Результат | Соотвествие
-----------|----------------|:---------:|------------:
main2.c     | 1 -1 -1 1 1    | 1 1 1 1 1 |        True | 
main2.s     | 1 -1 -1 1 1    | 1 1 1 1 1 |        True |
main2-refactored.s     | 1 -1 -1 1 1	   | 1 1 1 1 1 |       True      |
main2.c     | 3 -3 4 -5 6    | 3 6 4 6 6 |       True      |
main.s     | 3 -3 4 -5 6	   | 3 6 4 6 6 |      True       |
main2-refactored.s       | 3 -3 4 -5 6	   | 3 6 4 6 6 |     True        |
main.c     | 1 -2 -3 -4 9	  | 1 9 9 9 9 |      True       |
main.s     | 1 -2 -3 -4 9	  | 1 9 9 9 9 |     True        |
main2-refactored.s     | 1 -2 -3 -4 9	  | 1 9 9 9 9 |     True        |

Представлено полное тестовое покрытие, дающее одинаковый результат на всех программах.


Для проверки ввести команды:
#### gcc main2-refactored.s
#### gcc ./a.out

### 7 баллов
В дополнение к требованиям на предыдущую оценку

Реализация программы на ассемблере, полученной после рефакторинга, в виде двух единиц компиляции (2-1.s & 2-2.s).
Я разделил код ассемблера на файл с функциями и файл с main. Далее скомпилировал полученные файлы и запустил файлы с исходными данными и файла для вывода результатов с использованием аргументов командной строки.


Для проверки ввести команды:
#### gcc 2-1.s 2-2.s
#### gcc ./a.out


![img](/p3.png)
Далее я переделал файл Си, чтобы он брал и записывал данные из вводимых в командную строку файлов. (int argc, char * argv[]) измененная программа была сохранена под названием “main3.c”
После чего эта программа была скопилирована в main3.s и разделена на файлы 3-1.s и 3-2.s, в которых были функции и main соответсвенно.


Для проверки ввести команды:
#### gcc 3-1.s 3-2.s
#### gcc ./a.out input.txt output.txt


![img](/p4.png)

### 8 баллов
В дополнение к требованиям на предыдущую оценку

В программу была добавлена функция генератора случайных наборов данных, расширяющих возможности тестирования, а также подключение генератора к программе с выбором в командной строке варианта ввода данных. (./a.out -r).
Также было реализовано расширение анализа командной строки для выбора способа порождения исходных данных.
#### if argv[1] == "-r") -> rand_ma
#### else -> input.txt output.txt
Также модификация программы на C и программы на ассемблере, полученной после рефакторинга, для проведения сравнения на производительность.
#### start = time(NULL)
#### end = time(NULL)
#### difftime(end, start)
Для замедления работы до секунды, я постввил цикл на 10000 повторов в функции task, также поставил больший диапазон генерирования рандомных чисел и увеличил количество элементов в массиве.
### Все изменения были записаны в файл main4.c
![img](/p5.png)

После чего провел несколько вариантов тестовых прогонов.
#### Пришел к выводу, что программа после рефакторинга работает быстрее.
### 9 баллов
![img](/p6.png)
