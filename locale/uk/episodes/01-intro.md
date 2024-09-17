---
title: Знайомство з терміналом
teaching: 5
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Пояснити, як термінал пов'язаний з клавіатурою, екраном, операційною системою та програмами користувача.
- Пояснити, коли та чому інтерфейси командного рядка слід використовувати замість графічних інтерфейсів.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What is a command shell and why would I use one?

::::::::::::::::::::::::::::::::::::::::::::::::::

### Попередні знання

Люди та комп’ютери зазвичай взаємодіють багатьма різними способами, наприклад за допомогою клавіатури та миші, сенсорного екрану або системи розпізнавання мови.
Найбільш поширений спосіб взаємодії з персональними комп’ютерами називається графічний інтерфейс користувача (GUI - graphical user interface).
За допомогою такого інтерфейсу ми надаємо комп’ютеру інструкції, обираючи дію у меню за допомогою миші.

Хоча візуальна допомога графічного інтерфейсу користувача робить інтуїтивним його вивчення,
такий спосіб надсилання інструкцій до комп'ютера дуже погано масштабується.
Уявіть наступну задачу:
для бібліографічного пошуку вам необхідно скопіювати третій рядок з тисячі вхідних файлів з тисячі
різних директорій та вставити усе це в один файл.
Using a GUI, you would not only be clicking at your desk for several hours,
but you could potentially also commit an error in the process of completing this repetitive task.
Саме тут ми й скористаємося перевагами терміналу Unix.
The Unix shell is both a **command-line interface** (CLI) and a scripting language,
allowing such repetitive tasks to be done automatically and fast.
With the proper commands, the shell can repeat tasks with or without some modification
as many times as we want.
З використанням терміналу приклад задачі з бібліографічним пошуком може бути вирішений за секунди.

### Термінал

Термінал - це програма, де користувач може вводити команди.
With the shell, it's possible to invoke complicated programs like climate modeling software
or simple commands that create an empty directory with only one line of code.
Найбільш популярним терміналом є Bash (the Bourne Again SHell, який отримав таку назву, тому що був розроблений на основі терміналу, написаного Стівеном Борном).
Bash is the default shell on most modern implementations of Unix and in most packages that provide
Unix-like tools for Windows.
Note that 'Git Bash' is a piece of software that enables Windows users to use a Bash like interface
when interacting with Git.

Using the shell will take some effort and some time to learn.
У той час як графічний інтерфейс надає вам можливість вибору, команди терміналу не надаються автоматично, тому вам доведеться вивчити кілька команд, як нову лексику у мові, яку ви вивчаєте.
However, unlike a spoken language, a small number of "words" (i.e. commands) gets you a long way,
and we'll cover those essential few today.

Граматика терміналу дозволяє комбінувати наявні інструменти у потужні конвеєри та автоматично обробляти великі обсяги даних. Sequences of
commands can be written into a _script_, improving the reproducibility of
workflows.

In addition, the command line is often the easiest way to interact with remote machines
and supercomputers.
Familiarity with the shell is near essential to run a variety of specialized tools and resources
including high-performance computing systems.
Оскільки кластери та хмарні обчислювальні системи стають все більш популярними для обробки наукових даних, вміння взаємодіяти з терміналом стає необхідною навичкою.
We can build on the command-line skills covered here
to tackle a wide range of scientific questions and computational challenges.

Отже, почнемо.

When the shell is first opened, you are presented with a **prompt**,
indicating that the shell is waiting for input.

```bash
$
```

The shell typically uses `$ ` as the prompt, but may use a different symbol.
In the examples for this lesson, we'll show the prompt as `$ `.
Most importantly, _do not type the prompt_ when typing commands.
Треба вводити тільки команди, що йдуть за ним.
Це правило діє як на цих уроках, так і на уроках з інших джерел.
Also note that after you type a command, you have to press the <kbd>Enter</kbd> key to execute it.

The prompt is followed by a **text cursor**, a character that indicates the position where your
typing will appear.
Курсор зазвичай блимає або є суцільним блоком, але він також може бути підкресленням або вертикальною рискою.
Ви могли його бачити, наприклад, в текстових редакторах.

Зверніть увагу, що ваш запит може виглядати дещо інакше. Зокрема, більшість популярних середовищ оболонки за замовчуванням вказують ваше ім'я користувача та ім'я хоста перед '$'. Такий запит може виглядати так, наприклад:

```bash
nelle@localhost $
```

The prompt might even include more than this. Do not worry if your prompt is not
just a short `$ `. This lesson does not depend on this additional information and it
should also not get in your way. The only important item to focus on is the `$ `
character itself and we will see later why.

So let's try our first command, `ls`, which is short for listing.
Ця команда покаже зміст поточного каталогу:

```bash
$ ls
```

```output
Desktop     Downloads   Movies      Pictures
Documents   Library     Music       Public
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Команду не знайдено

If the shell can't find a program whose name is the command you typed, it
will print an error message such as:

```bash
$ ks
```

```output
ks: command not found
```

This might happen if the command was mis-typed or if the program corresponding to that command
is not installed.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Конвеєр Неллі: Типова Проблема

Nelle Nemo, a marine biologist,
has just returned from a six-month survey of the
[North Pacific Gyre](https://en.wikipedia.org/wiki/North_Pacific_Gyre),
where she has been sampling gelatinous marine life in the
[Great Pacific Garbage Patch](https://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch).
She has 1520 samples that she's run through an assay machine to measure the relative abundance
of 300 proteins.
Їй потрібно запустити ці 1520 файлів через уявну програму `goostats.sh`, яку вона успадкувала.
In addition to this huge task, she has to write up results by the end of the month, so her paper
can appear in a special issue of _Aquatic Goo Letters_.

If Nelle chooses to run `goostats.sh` by hand using a GUI,
she'll have to select and open a file 1520 times.
Якщо обробка одного файлу програмою `goostats.sh` триватиме 30 секунд, загальний процес вимагатиме більше ніж 12 годин уваги Неллі.
With the shell, Nelle can instead assign her computer this mundane task while she focuses
her attention on writing her paper.

У наступних кількох уроках будуть розглянуті шляхи, яким чином Неллі може цього досягти.
More specifically,
the lessons explain how she can use a command shell to run the `goostats.sh` program,
using loops to automate the repetitive steps of entering file names,
so that her computer can work while she writes her paper.

As a bonus,
once she has put a processing pipeline together,
she will be able to use it again whenever she collects more data.

Для того, щоб досягти своєї мети, Неллі необхідно знати, як:

- перейти до файла/каталогу
- створити файл/каталог
- перевірити довжину файлу
- з'єднати команди разом
- отримати набір файлів
- iterate over files
- запустити скрипт, що містить розроблений нею конвеєр

:::::::::::::::::::::::::::::::::::::::: keypoints

- Термінал - це програма, основним призначенням якої є читання команд і запуск інших програм.
- У цьому уроці використовується Bash. Це термінал за замовчуванням у багатьох реалізаціях Unix.
- Програми можна запускати у Bash шляхом введення команд у вікні командного рядка.
- Основними перевагами терміналу є високе співвідношення кількості дій до кількості натискань клавіш, підтримка автоматизації повторюваних завдань,
  а також можливість доступу до віддалених машин.
- A significant challenge when using the shell can be knowing what commands need to be run and how to run them.

::::::::::::::::::::::::::::::::::::::::::::::::::
