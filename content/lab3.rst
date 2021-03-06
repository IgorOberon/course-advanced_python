Адреса и указатели. Ввод данных в С. Адресная арифметика.
#########################################################

:date: 2018-09-17 07:06
:summary: Адреса и указатели. Ввод данных в С. Адресная арифметика
:status: published
:published: yes

.. default-role:: code

.. contents:: Содержание

Введение
==================

    Рассмотрим следующий пример программы на языке **C**.

.. _APP:

    Программа APP

.. code-block:: c

        #include <stdio.h>
        
        void three_sort(int a, int b, int c); // function declaration

        int main()
        {
                int a, b, c;
                
                a = 150; b = 200; c = 100;

                three_sort(a, b, c);

                printf("%d %d %d\n", a, b, c);
                return 0;
        }

        void three_sort(int a, int b, int c)
        {
            int tmp;
            if (a > b){
                tmp = a;
                a = b;
                b = tmp;
            }
            if (b > c){
                tmp = b;
                b = c;
                c = tmp;
            }
            if (a > b){
                tmp = a;
                a = b;
                b = tmp;
            }
        }

По изначальной задумке — процедура **three_sort()** должна отсортировать значения **a**, **b** и **c** по возрастанию, после чего программа выведет их на экран.


Упражнение №1
-------------

Скомпилируйте и выполните данную программу, посмотрите на результат.

Адреса и указатели
==================

Как вы могли увидеть — результат работы программы отличается от задуманного. Всё дело в том, что переменные **a**, **b** и **c** являются локальными как для главной функции (**main**) так и для процедуры (**three_sort**). Таким образом переменные внутри функции (**three_sort**) хранят лишь копии значений основной программы (**main**), а их изменение не приводит к изменению «оригинальных». Для исправления данной программы, необходимо использовать **указатели**.

**Типизированный указатель** или **указатель на ◯** — это переменная, хранящая адрес оперативной памяти, где располагаться данные типа ◯.

**Нетипизированный указатель** — указатель на **void** (``void *p``).

Для работы с указателем (на примере **int**) необходимо:

+------------------------------------+----------------------------+--------------------+-------------------------+
|              Описание              |          Действие          |       Пример       |         описание        |
+====================================+============================+====================+=========================+
| Описать переменную,                | Использовать префикс ***** | ``int *a, b;``     | **a** — указатель;      |
| как указатель на ◯                 | перед именем переменной    |                    | **b** — нет             |
+------------------------------------+----------------------------+--------------------+-------------------------+
| Присвоить адрес переменной         | Использовать префикс **&** | ``a = &b;``        | теперь **a** содержит   |
| указанного типа или       **NULL** | перед именем переменной    |                    | адрес **b**             |
| (указатель в никуда)               | со значением               |                    |                         |
+------------------------------------+----------------------------+--------------------+-------------------------+
| Получить/изменить значение,        | Использовать префикс ***** | ``*a = b * (*a);`` | значение, хранящееся    |
| хранящееся, по адресу              |                            |                    | по адресу **a**, равно  |
|                                    |                            |                    | **b**, умноженному на   |
|                                    |                            |                    | значение, хранящееся по |
|                                    |                            |                    | адресу **a**            |
+------------------------------------+----------------------------+--------------------+-------------------------+

В качестве примера, рассмотрим следующую программу:

.. code-block:: c

        #include <stdio.h>

        void inc_two(int *a); // function declaration

        int main()
        {
                int a = 1;         // set a to 1
                inc_two(&a);       // a = 3
                printf("%d\n", a); // print a
                return 0;
        }

        void inc_two(int *a)
        {
                *a = *a + 2;  // increase external value by 2
        }

Картина переменных получается следующая:


.. raw:: html

        <svg version="1.1" id="Слой_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
             viewBox="0 0 684 425" xml:space="preserve">
        <style type="text/css">
            .st0{fill:#F0F0FF;}
            .st1{fill:#FFFFFF;stroke:#000000;stroke-miterlimit:10;}
            .st2{fill:#293AA0;}
            .st3{fill:#FFFFFF;}
            .st4{font-family:'Arial';}
            .st5{font-size:40px;}
            .st6{font-size:36px;}
            .st7{fill:#293A00;fill-opacity:0.5;stroke:#000000;stroke-miterlimit:10;}
            .st8{fill:none;stroke:#000000;stroke-width:3;stroke-miterlimit:10;}
        </style>
        <g>
            <rect x="0.5" y="0.5" class="st0" width="683" height="424"/>
            <path d="M683,1v423H1V1H683 M684,0H0v425h684V0L684,0z"/>
        </g>
        <g>
            <rect x="51.6" y="144.7" class="st1" width="250" height="100"/>
            <rect x="51.6" y="294.7" class="st1" width="250" height="100"/>
            <g>
                <rect x="52.1" y="145.2" class="st2" width="249" height="49"/>
                <path d="M300.6,145.7v48h-248v-48H300.6 M301.6,144.7h-250v50h250V144.7L301.6,144.7z"/>
            </g>
            <g>
                <rect x="52.1" y="295.7" class="st2" width="249" height="49"/>
                <path d="M300.6,296.2v48h-248v-48H300.6 M301.6,295.2h-250v50h250V295.2L301.6,295.2z"/>
            </g>
            <text transform="matrix(1 0 0 1 133.2755 181.4805)" class="st3 st4 st5">main</text>
            <text transform="matrix(1 0 0 1 115.5935 330.3064)" class="st3 st4 st6">inc_two</text>
            <text transform="matrix(1 0 0 1 165.5018 226.4805)" class="st4 st5">a</text>
            <text transform="matrix(1 0 0 1 166.6143 375.3064)" class="st4 st6">a</text>
            <rect x="382.6" y="144.7" class="st1" width="250" height="100"/>
            <rect x="382.6" y="294.7" class="st1" width="250" height="100"/>
            <g>
                <rect x="383.1" y="145.2" class="st2" width="249" height="49"/>
                <path d="M631.6,145.7v48h-248v-48H631.6 M632.6,144.7h-250v50h250V144.7L632.6,144.7z"/>
            </g>
            <g>
                <rect x="383.1" y="295.7" class="st2" width="249" height="49"/>
                <path d="M631.6,296.2v48h-248v-48H631.6 M632.6,295.2h-250v50h250V295.2L632.6,295.2z"/>
            </g>
            <text transform="matrix(1 0 0 1 464.275 181.4805)" class="st3 st4 st5">main</text>
            <text transform="matrix(1 0 0 1 446.5935 330.3064)" class="st3 st4 st6">inc_two</text>
            <text transform="matrix(1 0 0 1 496.5018 226.4805)" class="st4 st5">a</text>
            <text transform="matrix(1 0 0 1 497.6143 375.3064)" class="st4 st6">a</text>
            <text transform="matrix(1 0 0 1 79.3594 63.7402)"><tspan x="0" y="0" class="st4 st5">До вызова</tspan><tspan x="5" y="48" class="st4 st5">inc_two(a)</tspan></text>
            <text transform="matrix(1 0 0 1 346.2383 63.7402)"><tspan x="0" y="0" class="st4 st5">Во время работы</tspan><tspan x="69.1" y="48" class="st4 st5">inc_two(a)</tspan></text>
            <rect x="51.5" y="295.5" class="st7" width="250" height="99"/>
        </g>
        <g>
            <g>
                <path class="st8" d="M524.1,370.2c-11-79-259.2-152-155.2-157.3"/>
                <g>
                    
                        <ellipse transform="matrix(0.9966 -8.191825e-02 8.191825e-02 0.9966 -28.5386 44.1714)" cx="524" cy="369.9" rx="5.6" ry="5.6"/>
                </g>
                <g>
                    <path d="M382.5,212.5c-6.3,2.6-14.1,6.8-18.9,11.3l3.6-10.8l-4.2-10.6C368,206.5,376,210.3,382.5,212.5z"/>
                </g>
            </g>
        </g>
        </svg>


То есть, при вызове функции **inc_two**, переменна **a** содержит адрес, где располагается переменная **a** функции **main**. Благодаря этому функция может изменить значение «внешней» переменной.

Примечание: ``int **a`` — *указатель на указатель на целое число.*

Упражнение №2
-------------

Исправьте программу APP_.

Ввод данных в **C**
===================

Для ввода данных в языке **C** присутствует функция **scanf(<формат строка>, <адреса переменных>)**. **Формат строка** — полностью соответствует первому параметру функции **printf()**. **Адреса переменных** — адреса, куда **scanf()** будет сохранять результаты чтения данных с клавиатуры.

Пример использования:

Программа app_scan.c

.. code-block:: c

        #include <stdio.h>

        int main()
        {
            int day, month, year;
            printf("Get data: ");

            // give scanf addresses of day, month and year, with format (split numbers by "/") 
            scanf("%d/%d/%d", &day, &month, &year);

            printf("Result: %02d.%02d.%04d\n", day, month, year);
            return 0;
        }

.. code-block:: text

        $ gcc -o app_scan app_scan.c
        $ ./app_scan
        Get data: 1/12/1922
        Result: 01.12.1922

Упражнение №3
-------------

Скомпилируйте и запустите программу выше.

Упражнение №4
-------------

Добавьте в программу APP_ ввод **a**, **b** и **c** с клавиатуры **через запятую**. Попробуйте ввести начальные данные через пробел или через перевод строки.

***** Сделайте так, чтобы можно было использовать любой из трёх видов ввода.

Адресная арифметика
===================

Поскольку адрес в оперативной памяти — всего лишь число, то с указателями можно проводить арифметические операции.

Для наглядного объяснения рассмотрим программу:

.. code-block:: c

        #include <stdio.h>
        #include <stdint.h>  // to use integer with defined size

        int main()
        {
                int32_t a;  // 4-bytes integer
                int8_t *b;  // pointer to 1-byte integer
                int16_t *c; // pointer to 2-byte integer

                a = 0x12345678;
                b = (int8_t *)&a;
                c = (int16_t *)&a;

                printf("+--------+----------------+-----------+-----------+\n");
                printf("| Byte N |    Address     | Dec value | Hex value |\n");
                printf("+--------+----------------+-----------+-----------+\n");
                for (int i = 0; i < 4; ++i){
                    printf("| %6d | %p | %9d | 0x%07x |\n", i+1, b, *b, *b);
                    b += 1;
                }
                printf("+--------+----------------+-----------+-----------+\n");

                for (int i = 0; i < 2; ++i){
                    printf("| %6d | %p | %9d | 0x%07x |\n", i+1, c, *c, *c);;
                    c += 1;
                }
                printf("+--------+----------------+-----------+-----------+\n");
                printf("Base value: addrecc - %p, dec - %d, hex - 0x%x\n", &a, a, a);
                return 0;
        }

Возможный вариант результата работы программы:

.. code-block:: text
        
        +--------+----------------+-----------+-----------+
        | Byte N |    Address     | Dec value | Hex value |
        +--------+----------------+-----------+-----------+
        |      1 | 0x7fffce658fdc |       120 | 0x0000078 |
        |      2 | 0x7fffce658fdd |        86 | 0x0000056 |
        |      3 | 0x7fffce658fde |        52 | 0x0000034 |
        |      4 | 0x7fffce658fdf |        18 | 0x0000012 |
        +--------+----------------+-----------+-----------+
        |      1 | 0x7fffce658fdc |     22136 | 0x0005678 |
        |      2 | 0x7fffce658fde |      4660 | 0x0001234 |
        +--------+----------------+-----------+-----------+
        Base value: address - 0x7fffce658fdc, dec - 305419896, hex - 0x12345678

Как можно видеть: сначала и **b** и **c** указывали на туда, где располагается **a** (0x7fffce658fdc). После операции, увеличивающей адрес на 1, **b** стал указывать на следующий байт (0x7fffce658fdd), а вот **c** - нет. **c** начал указывать на адрес 0x7fffce658fde, который больше начального на 2.

Причина различного поведения заключается в том, что **a** — строго четырёхбайтное целое число (``int32_t`` из ``<stdint.h>``), **b** — указывает на однобайтовое число а **c** — на двухбайтное. Таким образом операция увеличения на единицу (``◯ += 1;`` или ``◯ += 1;`` или же ``◯++;``) переводит указатель на следующее значение соответствующего типа в оперативной памяти. Именно по этому адрес **b** увеличивается каждый раз на единицу, а у **c** — на двойку.

Рисунок ниже показывает внутреннее представление четырёхбайтного целого числа в случае little-endian порядка байт. Подробнее `тут`__

__ https://ru.wikipedia.org/wiki/Порядок_байтов


.. raw:: html
        
        <svg version="1.1" id="Слой_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
             viewBox="0 0 450 300" style="enable-background:new 0 0 450 300;" xml:space="preserve">
        <style type="text/css">
            .stt0{fill:#F0F0FF;}
            .stt1{font-family:'Arial';}
            .stt2{font-size:21px;}
            .stt3{fill:none;stroke:#000000;stroke-width:2;stroke-miterlimit:10;}
            .stt4{fill:none;}
            .stt5{font-family:'Courier New', 'Courier';}
        </style>
        <g>
            <rect x="0.5" y="0.5" class="stt0" width="449" height="299"/>
            <path d="M449,1v298H1V1H449 M450,0H0v300h450V0L450,0z"/>
        </g>
        <text transform="matrix(1 0 0 1 206.3275 43.1013)" class="stt1 stt2">Dec</text>
        <text transform="matrix(1 0 0 1 355.6558 43.1013)" class="stt1 stt2">Hex</text>
        <text transform="matrix(1 0 0 1 45.2329 120.1015)" class="stt1 stt2">4 Byte</text>
        <text transform="matrix(1 0 0 1 45.2329 196.4614)" class="stt1 stt2">2 Byte</text>
        <text transform="matrix(1 0 0 1 45.2329 271.1816)" class="stt1 stt2">1 Byte</text>
        <g>
            <line class="stt3" x1="296" y1="0" x2="296" y2="300"/>
        </g>
        <line class="stt3" x1="0" y1="225" x2="450" y2="225"/>
        <line class="stt3" x1="4.2" y1="0" x2="445.8" y2="0"/>
        <g>
            <line class="stt3" x1="0" y1="75" x2="450" y2="75"/>
            <line class="stt3" x1="0" y1="150" x2="450" y2="150"/>
        </g>
        <line class="stt3" x1="131" y1="0" x2="131" y2="300"/>
        <line class="stt4" x1="0" y1="0" x2="0" y2="300"/>
        <text transform="matrix(1 0 0 1 157.2908 117.6128)" class="stt5 stt2">305419896</text>
        <text transform="matrix(1 0 0 1 322.9204 117.6128)" class="stt5 stt2">12345678</text>
        <text transform="matrix(1 0 0 1 150.9897 193.9724)" class="stt5 stt2">22136 4660</text>
        <text transform="matrix(1 0 0 1 138.3877 269.6926)" class="stt5 stt2">120 86 52 18</text>
        <text transform="matrix(1 0 0 1 316.6187 193.9724)" class="stt5 stt2">5678 1234</text>
        <text transform="matrix(1 0 0 1 304.0171 269.6926)" class="stt5 stt2">78 56 34 12</text>
        </svg>


Упражнение №5
-------------

На вход подаётся последовательность целых чисел, заканчивающаяся нулём.

Вывести: максимальное, минимальное, количество чисел, сумму, произведение, максимальное чётное число или -1, если такого нет.

Упражнение №6
-------------

Написать функцию ``swap(a, b)``, которая будет менять местами значения переданных переменных. Переменные могут быть целыми числами или числами с плавающей точкой.

Для выполнения данного упражнения используйте то, что функции с разными сигнатурами (отличающиеся или именем или количеством параметров или типами передаваемых данных) воспринимаются как разные при использовании компилятора **g++** вместо **gcc**. Или же то, что **float** занимает 4 байта памяти (как и ``int32_t``);

Упражнение №7
-------------

Измените процедуру в приложении APP_ так, чтобы можно было сортировать не только три, но и два значения.

Для выполнения упражнения необходимо использовать задание параметра по умолчанию (в декларации процедуры сделать описание типа ``int c = 0``). Тогда в случае задания только двух параметров третий будет равен заранее определённому значению (**NULL**) и использовать компилятор **g++**, или просто требовать (но уже от программиста) задание ненужного параметра, как **NULL** для третьего (дополнительного) параметра.