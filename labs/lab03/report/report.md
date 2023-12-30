---
## Front matter
title: "Отчет по лабораторной работе №3"
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
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы
Целью работы является освоение процедуры оформления отчетов с помощью легковесного языка разметки Markdown.


# Выполнение лабораторной работы
1. Откройте терминал (рис. @fig:001).

![Открытый терминал](image/1.png){#fig:001 width=90%}

2. Перейдите в каталог курса сформированный при выполнении лабораторной работы №2: cd ~/work/study/2023-2024/"Архитектура компьютера"/arch-pc/ (рис. @fig:002).

![Переход в каталог курса](image/2.png){#fig:002 width=90%}

Обновите локальный репозиторий, скачав изменения из удаленного репозитория с помощью команды git pull (рис. @fig:003).

![Обновление локального репозитория](image/3.png){#fig:003 width=90%}
 
3. Перейдите в каталог с шаблоном отчета по лабораторной работе № 3
cd ~/work/study/2023-2024/"Архитектура компьютера"/arch-pc/labs/lab03/report (рис. @fig:004).

![Переход в каталог с шаблоном отчета](image/4.png){#fig:004 width=90%}

4. Проведите компиляцию шаблона с использованием Makefile. Для этого введите команду make (рис. @fig:005).

![Компиляция шаблона отчета](image/5.png){#fig:005 width=90%}

При успешной компиляции должны сгенерироваться файлы report.pdf и report.docx (рис. @fig:006). Откройте и проверьте корректность полученных файлов.

![Сгенерированные файлы](image/6.png){#fig:006 width=90%}

5. Удалите полученный файлы с использованием Makefile. Для этого введите команду make clean (рис. @fig:007).

![Удаление полученных файлов](image/7.png){#fig:007 width=90%}

Проверьте, что после этой команды файлы report.pdf и report.docx были удалены (рис. @fig:008).

![Файлы удалены](image/8.png){#fig:008 width=90%}

6. Откройте файл report.md c помощью любого текстового редактора, например gedit (рис. @fig:009).

![Открытие report.md с помощью gedit](image/9.png){#fig:009 width=90%}

Внимательно изучите структуру этого файла (рис. @fig:010).

![Структура файла](image/10.png){#fig:010 width=90%}

# Выполнение заданий для самостоятельной работы
1. В соответствующем каталоге сделайте отчёт по лабораторной работе № 2 в формате Markdown. В качестве отчёта необходимо предоставить отчёты в 3 форматах: pdf, docx
и md (рис. @fig:011, @fig:012).

![Отчёт по лабораторной работе № 2 в 3 форматах](image/11.png){#fig:011 width=90%}

![Отчёт по лабораторной работе № 2 в в формате Markdown](image/12.png){#fig:012 width=90%}

# Выводы
В ходе выполнения лабораторной работы я освоила процедуры оформления отчетов с помощью легковесного языка разметки Markdown.


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
16. Таненбаум Э., Бос Х. Современные операционные системы. — 4-е изд. — СПб. : Питер,
2015. — 1120 с. — (Классика Computer Science).

