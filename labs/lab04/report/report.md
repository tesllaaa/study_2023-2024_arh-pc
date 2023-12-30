---
## Front matter
title: "Отчет по лабораторной работе №4"
subtitle: "дисциплина: Архитектура компьютера"
author: "Михайлова Регина Алексеевна"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Освоение процедуры компиляции и сборки программ, написанных на ассемблере NASM.


# Выполнение лабораторной работы

1. Рассмотрим пример простой программы на языке ассемблера NASM. Традиционно первая
программа выводит приветственное сообщение Hello world! на экран.
Создадим каталог для работы с программами на языке ассемблера NASM (рис. @fig:001, @fig:002):
mkdir -p ~/work/arch-pc/lab04

![Создание каталога](image/1.png){#fig:001 width=90%}

![Созданный каталог](image/2.png){#fig:002 width=90%}

Перейдем в созданный каталог (рис. @fig:003):
cd ~/work/arch-pc/lab04

![Переход в созданный каталог](image/3.png){#fig:003 width=90%}

Создадим текстовый файл с именем hello.asm (рис. @fig:004, @fig:005):
touch hello.asm

![Создание файла hello.asm](image/4.png){#fig:004 width=90%}

![Созданный файл hello.asm](image/5.png){#fig:005 width=90%}

Откроем этот файл с помощью любого текстового редактора, например, gedit (рис. @fig:006):
gedit hello.asm

![Открытие файла hello.asm](image/6.png){#fig:006 width=90%}

и введем в него следующий текст:
```NASM
; hello.asm
SECTION .data ; Начало секции данных
hello: DB 'Hello world!',10 ; 'Hello world!' плюс
; символ перевода строки
helloLen: EQU $-hello ; Длина строки hello
SECTION .text ; Начало секции кода
GLOBAL _start
_start: ; Точка входа в программу
mov eax,4 ; Системный вызов для записи (sys_write)
mov ebx,1 ; Описатель файла '1' - стандартный вывод
mov ecx,hello ; Адрес строки hello в ecx
mov edx,helloLen ; Размер строки hello
int 80h ; Вызов ядра
mov eax,1 ; Системный вызов для выхода (sys_exit)
mov ebx,0 ; Выход с кодом возврата '0' (без ошибок)
int 80h ; Вызов ядра
```

2. NASM превращает текст программы в объектный код. Например, для компиляции приве-
дённого выше текста программы «Hello World» (рис. @fig:007) необходимо написать:
nasm -f elf hello.asm

![Компиляция программы «Hello World»](image/7.png){#fig:007 width=90%}

Если текст программы набран без ошибок, то транслятор преобразует текст программы
из файла hello.asm в объектный код, который запишется в файл hello.o. Таким образом,
имена всех файлов получаются из имени входного файла и расширения по умолчанию.
При наличии ошибок объектный файл не создаётся, а после запуска транслятора появятся
сообщения об ошибках или предупреждения.
С помощью команды ls проверим, что объектный файл был создан (рис. @fig:008).

![hello.o успешно создан](image/8.png){#fig:008 width=90%}

3. Полный вариант командной строки nasm выглядит следующим образом:
nasm [-@ косвенный_файл_настроек] [-o объектный_файл] [-f формат_объектного_файла] [-l листинг] [параметры...] [--] исходный_файл

Выполним следующую команду (рис. @fig:009):
nasm -o obj.o -f elf -g -l list.lst hello.asm

![Компиляция hello.asm в obj.o](image/9.png){#fig:009 width=90%}

Данная команда скомпилирует исходный файл hello.asm в obj.o (опция -o позволяет
задать имя объектного файла, в данном случае obj.o), при этом формат выходного файла
будет elf, и в него будут включены символы для отладки (опция -g), кроме того, будет создан
файл листинга list.lst (опция -l).
С помощью команды ls проверим, что файлы были созданы (рис. @fig:010)

![obj.o и list.lst успешно созданы](image/10.png){#fig:010 width=90%}

4. Чтобы получить исполняемую программу, объектный файл необходимо передать на обработку компоновщику (рис. @fig:011):
ld -m elf_i386 hello.o -o hello
С помощью команды ls проверим, что исполняемый файл hello был создан (рис. @fig:011).

![Передача объектного файла компоновщику](image/11.png){#fig:011 width=90%}


Выполним следующую команду (рис. @fig:012):
ld -m elf_i386 obj.o -o main

Исполняемый файл будет иметь имя main (рис. @fig:012)

![Создание файла main](image/12.png){#fig:012 width=90%}

5. Запустить на выполнение созданный исполняемый файл (рис. @fig:013), находящийся в текущем каталоге,
можно, набрав в командной строке:
./hello

![Исполняемый файл успешно выполнен](image/13.png){#fig:013 width=90%}

# Выполнение заданий для самостоятельной работы
1. В каталоге ~/work/arch-pc/lab04 с помощью команды cp создадим копию файла
hello.asm с именем lab4.asm (рис. @fig:014), после чего копия файла будет успешно создана (рис. @fig:015)

![Копирование файла](image/14.png){#fig:014 width=90%}

![Копия файла создана](image/15.png){#fig:015 width=90%}


2. С помощью текстового редактора внесем изменения в текст программы в
файле lab4.asm так, чтобы вместо Hello world! на экран выводилась строка с
фамилией и именем:

```NASM
SECTION .data 
name: DB 'Mikhaylova Regina',10
nameLen: EQU $-name

SECTION .text 
GLOBAL _start

_start: 
mov eax,4 
mov ebx,1 
mov ecx,name 
mov edx,nameLen 
int 80h 
mov eax,1 
mov ebx,0 
int 80h 
```
3. Оттранслируем полученный текст программы lab4.asm в объектный файл (рис. @fig:016). Выполним
компоновку объектного файла (рис. @fig:017) и запустим получившийся исполняемый файл  (рис. @fig:018).

![Преобразование в объектный файл](image/16.png){#fig:016 width=90%}

![Компоновка объектного файла](image/17.png){#fig:017 width=90%}

![Запуск исполняемого файла](image/18.png){#fig:018 width=90%}


# Вывод

В ходе лабораторной работы я освоила процедуры компиляции и сборки программ, написанных на ассемблере NASM.

# Список литературы

1. GDB: The GNU Project Debugger. — URL: https://www.gnu.org/software/gdb/.
2. GNU Bash Manual. — 2016. — URL: https://www.gnu.org/software/bash/manual/.
3. Midnight Commander Development Center. — 2021. — URL: https://midnight-commander.
org/.
4. NASM Assembly Language Tutorials. — 2021. — URL: https://asmtutor.com/.
5. Newham C. Learning the bash Shell: Unix Shell Programming. — O’Reilly Media, 2005. —
354 с. — (In a Nutshell). — ISBN 0596009658. — URL: http://www.amazon.com/Learning-
bash-Shell-Programming-Nutshell/dp/0596009658.
6. Robbins A. Bash Pocket Reference. — O’Reilly Media, 2016. — 156 с. — ISBN 978-1491941591.
7. The NASM documentation. — 2021. — URL: https://www.nasm.us/docs.php.
8. Zarrelli G. Mastering Bash. — Packt Publishing, 2017. — 502 с. — ISBN 9781784396879.
9. Колдаев В. Д., Лупин С. А. Архитектура ЭВМ. — М. : Форум, 2018.
10. Куляс О. Л., Никитин К. А. Курс программирования на ASSEMBLER. — М. : Солон-Пресс,
2017.
11. Новожилов О. П. Архитектура ЭВМ и систем. — М. : Юрайт, 2016.
12. Расширенный ассемблер: NASM. — 2021. — URL: https://www.opennet.ru/docs/RUS/nasm/.
13. Робачевский А., Немнюгин С., Стесик О. Операционная система UNIX. — 2-е изд. — БХВ-
Петербург, 2010. — 656 с. — ISBN 978-5-94157-538-1.
14. Столяров А. Программирование на языке ассемблера NASM для ОС Unix. — 2-е изд. —
М. : МАКС Пресс, 2011. — URL: http://www.stolyarov.info/books/asm_unix.
15. Таненбаум Э. Архитектура компьютера. — 6-е изд. — СПб. : Питер, 2013. — 874 с. —
(Классика Computer Science).
16. Таненбаум Э., Бос Х. Современные операционные системы. — 4-е изд. — СПб. : Питер, 2015. — 1120 с. — (Классика Computer Science).

