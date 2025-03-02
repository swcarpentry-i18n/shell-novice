---
title: Navigating Files and Directories
teaching: 30
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Пояснити подібності та відмінності між файлом і каталогом.
- Перетворити абсолютний шлях у відносний і навпаки.
- Створити абсолютні та відносні шляхи, які ідентифікують певні файли та каталоги.
- Використати опції та аргументи для зміни поведінки команд у терміналі.
- Продемонструвати використання табуляції для автоматичного доповнення та пояснити його переваги.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I move around on my computer?
- How can I see what files and directories I have?
- How can I specify the location of a file or directory on my computer?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: instructor

Introducing and navigating the filesystem in the shell
(covered in [Navigating Files and Directories](02-filedir.md) section)
can be confusing. Ви можете відкрити термінал та графічний провідник файлів поруч, щоб учні могли бачити вміст і структуру файлів, коли вони використовують термінал для навігації системою.

::::::::::::::::::::::::::::::::::::::::::::::::::

Частина операційної системи, яка відповідає за роботу з файлами та каталогами, називається **файловою системою**.
It organizes our data into files,
which hold information,
and directories (also called 'folders'),
which hold files or other directories.

Для створення, перевірки, перейменування та видалення файлів і каталогів зазвичай використовується декілька команд.
Щоб розглянути їх, перейдемо до нашого відкритого вікна терміналу.

По-перше, дізнаймося, де ми знаходимося, запустивши команду `pwd` (англ. 'print working directory' - надрукувати робочий каталог). Каталоги подібні до _місцезнаходження_ - у будь-який момент, коли ми використовуємо термінал, ми знаходимося в одному місці, яке називається **поточним робочим каталогом**. Commands mostly read and write files in the
current working directory, i.e. 'here', so knowing where you are before running
a command is important. Команда `pwd` покаже вам, де ви знаходитесь:

```bash
$ pwd
```

```output
/Users/nelle
```

У наведеному прикладі комп'ютер відповів `/Users/nelle`, що є **домашнім каталогом** Неллі:

:::::::::::::::::::::::::::::::::::::::::  callout

## Варіації домашнього каталогу

Розташування домашнього каталогу виглядає по-різному в різних операційних системах.
В Linux воно може виглядати як `/home/nelle`, а у Windows воно буде схоже на `C:\Documents and Settings\nelle` чи `C:\Users\nelle`.
(Зауважте, що воно може виглядати дещо інакше для різних версій Windows.)
In future examples, we've used Mac output as the default - Linux and Windows
output may differ slightly but should be generally similar.

Ми також припустимо, що ваша команда `pwd` повертає вашу домашню директорію користувача.
If `pwd` returns something different, you may need to navigate there using `cd`
or some commands in this lesson will not work as written.
See [Exploring Other Directories](#exploring-other-directories) for more details
on the `cd` command.

::::::::::::::::::::::::::::::::::::::::::::::::::

Для того, щоб зрозуміти, що таке 'домашній каталог', розглянемо як організована файлова система в цілому.  For the
sake of this example, we'll be
illustrating the filesystem on our scientist Nelle's computer.  After this
illustration, you'll be learning commands to explore your own filesystem,
which will be constructed in a similar way, but not be exactly identical.

На комп’ютері Неллі файлова система виглядає так:

![](fig/filesystem.svg){alt='Файлова система складається з кореневого каталогу, який містить підкаталоги з назвами bin, data, users та tmp'}

Файлова система виглядає як перевернуте дерево.
Найвищим каталогом є **кореневий каталог**, який містить усе інше.
We refer to it using a slash character, `/`, on its own;
this character is the leading slash in `/Users/nelle`.

Усередині цього каталогу є кілька інших каталогів: `bin` (в якому зберігаються певні вбудовані програми), `data` (для різноманітних файлів даних), `Users` (де знаходяться особисті директорії користувачів), `tmp` (для файлів тимчасового зберігання) та інші.

Ми знаємо, що наш поточний робочий каталог `/Users/nelle` зберігається всередині каталогу `/Users`, тому що `/Users` є першою частиною його імені.
Відповідно, нам відомо, що каталог `/Users` зберігається всередині кореневої директорії `/`, бо його ім'я розпочинається з символу `/`.

:::::::::::::::::::::::::::::::::::::::::  callout

## Символи скісної риски

Зверніть увагу, що символ `/` має два значення.
Коли він з’являється на початку назви файлу чи каталогу, це посилання на кореневу директорію. Коли він використовується _всередині_ шляху, це лише роздільник.

::::::::::::::::::::::::::::::::::::::::::::::::::

Underneath `/Users`,
we find one directory for each user with an account on Nelle's machine,
her colleagues _imhotep_ and _larry_.

![](fig/home-directories.svg){alt='Як і інші каталоги, домашні каталоги є підкаталогами
"/Users", наприклад "/Users/imhotep", "/Users/larry" або "/Users/nelle"'}

The user _imhotep_'s files are stored in `/Users/imhotep`,
user _larry_'s in `/Users/larry`,
and Nelle's in `/Users/nelle`. Оскільки саме Неллі є користувачем у наших прикладах, тому ми отримуємо `/Users/nelle` як наш домашній каталог.
Typically, when you open a new command prompt, you will be in
your home directory to start.

Тепер розглянемо команду, яка дозволить нам бачити вміст нашої власної файлової системи.  Ми можемо побачити, що знаходиться у нашому домашньому каталозі, запустивши `ls`:

```bash
$ ls
```

```output
Applications Documents    Library      Music        Public
Desktop      Downloads    Movies       Pictures
```

(Знову ж таки, ваші результати можуть дещо відрізнятися залежно від вашої операційної системи та того, як ви налаштували свою файлову систему.)

`ls` друкує назви файлів і каталогів у поточному каталозі.
Ми можемо зробити його вивід більш зрозумілим за допомогою **опції** `-F`, яка вказує `ls` класифікувати вивід, додаючи маркер до імен файлів і каталогів, щоб вказати, що вони собою являють:

- a trailing `/` indicates that this is a directory
- символ `@` вказує на посилання
- символ `*` вказує на виконуваний файл

Залежно від налаштувань терміналу за замовчуванням, він також може використовувати кольори для позначення файлів та каталогів, щоб краще їх розрізняти.

```bash
$ ls -F
```

```output
Applications/ Documents/    Library/      Music/        Public/
Desktop/      Downloads/    Movies/       Pictures/
```

В наведеному прикладі ми бачимо, що наш домашній каталог містить лише **підкаталоги**.
Any names in the output that don't have a classification symbol
are **files** in the current working directory.

:::::::::::::::::::::::::::::::::::::::::  callout

## Clearing your terminal

Якщо екран стає занадто захаращеним, ви можете очистити термінал за допомогою команди `clear`. Ви все ще можете отримати доступ до попередніх команд за допомогою клавіш <kbd>↑</kbd> та <kbd>↓</kbd> для переміщення по рядках, або за допомогою прокрутки у вашому терміналі.

::::::::::::::::::::::::::::::::::::::::::::::::::

### Отримання допомоги

У `ls` є багато інших опцій. Існує два поширених способи дізнатися, як використовувати команду і які параметри вона приймає --- **залежно від вашого середовища, ви можете виявити, що працює лише один із цих способів:**

1. Ми можемо передати команді опцію `--help` (доступну в Linux і Git Bash), наприклад:

```bash
$ ls --help
```

2. We can read its manual with `man` (available on Linux and macOS):

```bash
$ man ls
```

Далі ми роздивимось обидва способи.

:::::::::::::::::::::::::::::::::::::::::  callout

## Довідка для вбудованих команд

Деякі команди вбудовано в оболонку Bash, а не існують як окремі програми у файловій системі. Одним із прикладів є команда `cd` (зміна каталогу).
Якщо після команди `man cd` ви отримуєте повідомлення на кшталт `No manual entry for cd`, спробуйте натомість `help cd`. За допомогою команди `help` ви можете отримати інформацію про використання [вбудованих команд Bash](https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins.html).

::::::::::::::::::::::::::::::::::::::::::::::::::

#### Опція \`--help'

Більшість команд bash і програм, написаних людьми для запуску з bash, підтримують опцію `--help`, яка виводить додаткову інформацію про те, як користуватися відповідною командою або програмою.

```bash
$ ls --help
```

```output
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if neither -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options, too.
  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
      --author               with -l, print the author of each file
  -b, --escape               print C-style escapes for nongraphic characters
      --block-size=SIZE      scale sizes by SIZE before printing them; e.g.,
                               '--block-size=M' prints sizes in units of
                               1,048,576 bytes; see SIZE format below
  -B, --ignore-backups       do not list implied entries ending with ~
  -c                         with -lt: sort by, and show, ctime (time of last
                               modification of file status information);
                               with -l: show ctime and sort by name;
                               otherwise: sort by ctime, newest first
  -C                         list entries by columns
      --color[=WHEN]         colorize the output; WHEN can be 'always' (default
                               if omitted), 'auto', or 'never'; more info below
  -d, --directory            list directories themselves, not their contents
  -D, --dired                generate output designed for Emacs' dired mode
  -f                         do not sort, enable -aU, disable -ls --color
  -F, --classify             append indicator (one of */=>@|) to entries
...        ...        ...
```

:::::::::::::::::::::::::::::::::::::::::  callout

### Коли використовувати короткі або довгі опції

Коли існують як короткі, так і довгі опції:

- Використовуйте коротку під час введення команд безпосередньо в термінал, щоб мінімізувати натискання клавіш і швидше виконувати завдання.
- Use the long option in scripts to provide clarity.
 It will be read many times and typed once.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Непідтримувані параметри командного рядка

Якщо ви спробуєте використати параметр, який не підтримується терміналом, `ls` та інші команди зазвичай виводитимуть повідомлення про помилку, схоже на:

```bash
$ ls -j
```

```error
ls: invalid option -- 'j'
Try 'ls --help' for more information.
```

::::::::::::::::::::::::::::::::::::::::::::::::::

#### Команда `man`

Інший спосіб дізнатися про `ls` - ввести

```bash
$ man ls
```

This command will turn your terminal into a page with a description
of the `ls` command and its options.

Для навігації сторінками `man` ви можете використовувати <kbd>↑</kbd> і <kbd>↓</kbd> для переміщення по рядках, або спробувати <kbd>b</kbd> і <kbd>Spacebar</kbd> для переходу вгору і вниз на цілу сторінку.
Для пошуку символу або слова на сторінках `man`, використовуйте клавішу <kbd>/</kbd> та слідом введіть символ або слово, яке ви шукаєте.
Іноді пошук може призвести до кількох результатів.
У такому випадку ви можете переміщатися між результатами за допомогою клавіш <kbd>N</kbd> (для переходу вперед) та <kbd>Shift</kbd>\+<kbd>N</kbd> (для переходу назад).

Щоб **вийти** зі сторінок `man`, натисніть <kbd>q</kbd>.

:::::::::::::::::::::::::::::::::::::::::  callout

## Сторінки з інструкціями в Інтернеті

Звісно, є й третій спосіб отримати доступ до довідки для команд: пошук в інтернеті за допомогою веббраузера.
Якщо ви скористаєтеся пошуком в Інтернеті, додання до запиту фрази `unix man page` дозволить отримати більш доречні результати.

GNU надає посилання на свої [посібники](http://www.gnu.org/manual/manual.html), зокрема на [основні утиліти GNU](http://www.gnu.org/software/coreutils/manual/coreutils.html), які охоплюють багато команд, представлених у цьому уроці.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Вивчення інших опцій `ls`

Ви також можете використовувати декілька опцій одночасно. Що робить команда `ls` при використанні з опцією `-l`? А якщо ви використовуєте `-l` та `-h` одночасно?

Деякі з результатів виконання команди стосуються властивостей, які ми не розглядаємо у цьому семінарі (наприклад, права доступу до файлів та їх власники), але решта все одно буде корисною.

:::::::::::::::  solution

## Розв'язок

Опція `-l` змушує `ls` використовувати довгий (англ. **l**ong) формат виводу, показуючи не лише назви файлів/директорій, але й додаткову інформацію, таку як розмір файлу і час його останньої модифікації. Якщо ви використовуєте як `-h`, так і `-l`, це зробить виведення розміру файлу у більш зрозумілому людині вигляді ("**h**uman readable"), тобто покаже щось на кшталт `5.3K` замість `5369`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Виведення у зворотному хронологічному порядку

За замовчуванням `ls` виводить вміст каталогу в алфавітному порядку за іменами елементів. Команда `ls -t` перелічує елементи за часом останньої зміни, а не за алфавітом. Команда `ls -r` виводить вміст каталогу у зворотному порядку.
Який файл буде показано останнім при комбінації опцій `-t` і `-r`?
Підказка: Вам потрібно скористатися опцією `-l`, щоб переглянути дати останніх змін.

:::::::::::::::  solution

## Розв'язання

При використанні `-rt` останній змінений файл є останнім у списку. Це може бути дуже корисним для пошуку ваших останніх редагувань або перевірки чи було створено новий вихідний файл.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

### Exploring Other Directories

Ми можемо використовувати `ls` не лише у поточному робочому каталозі, але й для виведення вмісту іншого каталогу.
Подивимося на наш каталог `Desktop` (робочий стіл), виконавши `ls -F Desktop`, тобто, команду `ls` з **опцією** `-F` і [**аргументом**][Arguments] `Desktop`.
Аргумент `Desktop` повідомляє `ls`, що ми хочемо отримати список чогось іншого, ніж наш поточний робочий каталог:

```bash
$ ls -F Desktop
```

```output
shell-lesson-data/
```

Зауважте, що якщо у вашому поточному робочому каталозі не існує каталогу з назвою `Desktop`, ця команда поверне помилку. Typically, a `Desktop` directory exists in your
home directory, which we assume is the current working directory of your bash shell.

Your output should be a list of all the files and sub-directories in your
Desktop directory, including the `shell-lesson-data` directory you downloaded at
the [setup for this lesson](../learners/setup.md). (On most systems, the
contents of the `Desktop` directory in the shell will show up as icons in a graphical
user interface behind all the open windows. Подивіться, чи це ваш випадок.)

Ієрархічна організація речей таким чином допомагає нам відстежувати нашу роботу. Хоча у нашому домашньому каталозі можна зберігати сотні файлів, так само як і сотні паперових документів на робочому столі, набагато легше знаходити речі, коли вони організовані у підкаталоги з розумними назвами.

Тепер, коли ми знаємо, що каталог `shell-lesson-data` знаходиться у каталозі Desktop, ми можемо зробити дві речі.

По-перше, ми можемо переглянути його вміст, використовуючи ту ж стратегію, що і раніше, передавши ім'я каталогу в `ls`:

```bash
$ ls -F Desktop/shell-lesson-data
```

```output
exercise-data/  north-pacific-gyre/
```

По-друге, ми можемо змінити наше місцезнаходження на інший каталог, щоб ми більше не знаходилися в нашому домашньому каталозі.

The command to change locations is `cd` followed by a
directory name to change our working directory.
`cd` означає 'змінити каталог' (англ. 'change directory'), що трохи вводить в оману.
The command doesn't change the directory;
it changes the shell's current working directory.
Іншими словами, вона змінює налаштування терміналу щодо того, в якому каталозі ми знаходимося.
Команда `cd` подібна до подвійного клацання по каталогу в графічному інтерфейсі, щоб потрапити до нього.

Припустимо, нам треба перейти до каталогу `exercise-data`, який ми бачили вище. Ми можемо скористатися наступною серією команд, щоб дістатися туди:

```bash
$ cd Desktop
$ cd shell-lesson-data
$ cd exercise-data
```

Ці команди перемістять нас з домашнього каталогу до Desktop, потім до `shell-lesson-data`, а потім до `exercise-data`.
Ви помітите, що команда `cd` нічого не виводить. Це нормально.
Багато команд терміналу нічого не виводять на екран після успішного виконання.
Але якщо ми виконаємо `pwd` після неї, то побачимо, що зараз ми знаходимося у `/Users/nelle/Desktop/shell-lesson-data/exercise-data`.

Тепер, якщо ми виконаємо команду `ls -F` без аргументів, вона виведе вміст `/Users/nelle/Desktop/shell-lesson-data/exercise-data`, тому що саме там ми зараз знаходимося:

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data/exercise-data
```

```bash
$ ls -F
```

```output
alkanes/  animal-counts/  creatures/  numbers.txt  writing/
```

We now know how to go down the directory tree (i.e. how to go into a subdirectory),
but how do we go up (i.e. how do we leave a directory and go into its parent directory)?
Ми можемо спробувати наступне:

```bash
$ cd shell-lesson-data
```

```error
-bash: cd: shell-lesson-data: No such file or directory
```

Але ми отримуємо помилку! Чому?

With our methods so far,
`cd` can only see sub-directories inside your current directory. Існують різні способи перегляду батьківських каталогів; ми почнемо з найпростішого.

У терміналі є скорочення для переходу на один рівень каталогу вгору. Це працює наступним чином:

```bash
$ cd ..
```

`..` - це спеціальне ім'я каталогу, що означає "каталог, що містить поточний", або більш стисло, **батько** поточного каталогу.
Звичайно, якщо ми запустимо `pwd` після виконання `cd ..`, ми знову у `/Users/nelle/Desktop/shell-lesson-data`:

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data
```

Спеціальний каталог `..` зазвичай не з'являється, коли ми запускаємо `ls`. Якщо ми хочемо побачити його, ми можемо додати опцію `-a` до `ls -F`:

```bash
$ ls -F -a
```

```output
./  ../  exercise-data/  north-pacific-gyre/
```

`-a` означає 'показати все' (англ. show all) (включно з прихованими файлами); ця опція змушує `ls` показувати нам імена файлів і каталогів, які починаються з `.`, наприклад, `..` (яке, якщо ми знаходимося у `/Users/nelle`, вказує на каталог `/Users`).
Як ви можете бачити, команда також показує ще один спеціальний каталог, який називається `.`, що означає 'поточний робочий каталог'.
Може здатися, що це дещо надлишково - мати для нього ім'я, але незабаром ми побачимо, як воно може бути використано.

Зауважте, що у більшості інструментів командного рядка можна комбінувати декілька параметрів за допомогою одного `-` і без пробілів між параметрами: `ls -F -a` є еквівалентним до `ls -Fa`.

:::::::::::::::::::::::::::::::::::::::::  callout

## Інші приховані файли

In addition to the hidden directories `..` and `.`, you may also see a file
called `.bash_profile`. Цей файл зазвичай містить конфігурацію терміналу. You may also see other files and directories beginning
with `.`. These are usually files and directories that are used to configure
different programs on your computer. Префікс `.` використовується для того, щоб ці конфігураційні файли не захаращували термінал, коли використовується стандартна команда `ls`.

::::::::::::::::::::::::::::::::::::::::::::::::::

Ці три команди є основними командами для навігації по файловій системі на вашому комп'ютері: `pwd`, `ls` і `cd`. Let's explore some variations on those commands. What happens
if you type `cd` on its own, without giving
a directory?

```bash
$ cd
```

How can you check what happened? Команда `pwd` дає нам відповідь!

```bash
$ pwd
```

```output
/Users/nelle
```

Виявляється, `cd` без аргументу поверне вас до домашнього каталогу, що дуже зручно, якщо ви загубилися у власній файловій системі.

Let's try returning to the `exercise-data` directory from before. Минулого разу ми використовували три команди, але насправді ми можемо поєднати перелік каталогів для переходу до каталогу `exercise-data` за один крок:

```bash
$ cd Desktop/shell-lesson-data/exercise-data
```

Переконайтеся, що ми перемістилися в потрібне місце, виконавши `pwd` і `ls -F`.

If we want to move up one level from the data directory, we could use `cd ..`.  Але існує інший спосіб переміщення до будь-якого каталогу, незалежно від вашого поточного розташування.

So far, when specifying directory names, or even a directory path (as above),
we have been using **relative paths**.  When you use a relative path with a command
like `ls` or `cd`, it tries to find that location from where we are,
rather than from the root of the file system.

However, it is possible to specify the **absolute path** to a directory by
including its entire path from the root directory, which is indicated by a
leading slash. The leading `/` tells the computer to follow the path from
the root of the file system, so it always refers to exactly one directory,
no matter where we are when we run the command.

Це дає змогу перейти до каталогу `shell-lesson-data` з будь-якого місця у файловій системі (у тому числі з каталогу `exercise-data`). Щоб знайти абсолютний шлях ми можемо скористатися `pwd`, а потім витягти потрібний нам фрагмент, щоб перейти до `shell-lesson-data`.

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data/exercise-data
```

```bash
$ cd /Users/nelle/Desktop/shell-lesson-data
```

Виконайте `pwd` і `ls -F`, щоб переконатися, що ми знаходимося в потрібному каталозі.

:::::::::::::::::::::::::::::::::::::::::  callout

## Ще два скорочення

Термінал інтерпретує символ тильди (`~`) на початку шляху як "домашній каталог поточного користувача". Наприклад, якщо домашнім каталогом користувача Неллі є каталог `/Users/nelle`, то `~/data` еквівалентно `/Users/nelle/data`. This only works if it is the first character in the
path; `here/there/~/elsewhere` is _not_ `here/there/Users/nelle/elsewhere`.

Іншим скороченням є символ `-` (тире). `cd` will translate `-` into
_the previous directory I was in_, which is faster than having to remember,
then type, the full path.  This is a _very_ efficient way of moving
_back and forth between two directories_ -- i.e. if you execute `cd -` twice,
you end up back in the starting directory.

The difference between `cd ..` and `cd -` is
that the former brings you _up_, while the latter brings you _back_.

***

Спробуйте!
Спочатку перейдіть до `~/Desktop/shell-lesson-data` (ви вже маєте бути там).

```bash
$ cd ~/Desktop/shell-lesson-data
```

Потім `cd` у каталог `exercise-data/creatures`

```bash
$ cd exercise-data/creatures
```

Тепер, якщо ви виконаєте

```bash
$ cd -
```

ви побачите, що повернулися до `~/Desktop/shell-lesson-data`.
Запустіть `cd -` ще раз і ви повернетесь до `~/Desktop/shell-lesson-data/exercise-data/creatures`

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Абсолютні та відносні шляхи

Starting from `/Users/nelle/data`,
which of the following commands could Nelle use to navigate to her home directory,
which is `/Users/nelle`?

1. `cd .`
2. `cd /`
3. `cd /home/nelle`
4. `cd ../..`
5. `cd ~`
6. `cd home`
7. `cd ~/data/..`
8. `cd`
9. `cd ..`

:::::::::::::::  solution

## Розв'язання

1. Ні: скорочення `.` означає поточний каталог.

2. Ні: скорочення `/` означає кореневий каталог.

3. No: Nelle's home directory is `/Users/nelle`.

4. No: this command goes up two levels, i.e. ends in `/Users`.

5. Yes: `~` stands for the user's home directory, in this case `/Users/nelle`.

6. Ні: ця команда виконає перехід до каталогу `home` у поточному каталозі, якщо він існує.

7. Так: надмірно складна, але правильна.

8. Yes: shortcut to go back to the user's home directory.

9. Yes: goes up one level.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Relative Path Resolution

Використовуючи наведену нижче схему файлової системи, якщо `pwd` показує `/Users/thing`, що покаже команда `ls -F ../backup`?

1. `../backup: No such file or directory`
2. `2012-12-01 2013-01-08 2013-01-27`
3. `2012-12-01/ 2013-01-08/ 2013-01-27/`
4. `original/ pnas_final/ pnas_sub/`

![](fig/filesystem-challenge.svg){alt='A directory tree below the Users directory where "/Users" contains the directories "backup" and "thing"; "/Users/backup" contains "original","pnas\_final" and "pnas\_sub"; "/Users/thing" contains "backup"; and"/Users/thing/backup" contains "2012-12-01", "2013-01-08" and"2013-01-27"'}

:::::::::::::::  solution

## Розв'язання

1. No: there _is_ a directory `backup` in `/Users`.

2. Ні: це вміст каталогу `Users/thing/backup`, але за допомогою `..` ми просили піднятися на один рівень вище.

3. No: see previous explanation.

4. Так: `../backup/` вказує на `/Users/backup/`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## `ls` Reading Comprehension

Using the filesystem diagram below,
if `pwd` displays `/Users/backup`,
and `-r` tells `ls` to display things in reverse order,
what command(s) will result in the following output:

```output
pnas_sub/ pnas_final/ original/
```

![](fig/filesystem-challenge.svg){alt='A directory tree below the Users directory where "/Users" contains the directories "backup" and "thing"; "/Users/backup" contains "original","pnas\_final" and "pnas\_sub"; "/Users/thing" contains "backup"; and"/Users/thing/backup" contains "2012-12-01", "2013-01-08" and"2013-01-27"'}

1. `ls pwd`
2. `ls -r -F`
3. `ls -r -F /Users/backup`

:::::::::::::::  solution

## Розв'язання

1. Ні: `pwd` не є назвою каталогу.

2. Yes: `ls` without directory argument lists files and directories
 in the current directory.

3. Yes: uses the absolute path explicitly.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## General Syntax of a Shell Command

Ми вже познайомилися з командами, опціями та аргументами, але, можливо, буде корисно формалізувати деяку термінологію.

Consider the command below as a general example of a command,
which we will dissect into its component parts:

```bash
$ ls -F /
```

![](fig/shell_command_syntax.svg){alt='Загальний синтаксис команди терміналу'}

`ls` is the **command**, with an **option** `-F` and an
**argument** `/`.
Ми вже зустрічалися з опціями, які починаються з одного тире (`-`), відомі як **короткі варіанти**, або двох тире (`--`), відомі як **довгі варіанти**.
\[Параметри] змінюють поведінку команди, а \[Аргументи] вказують команді, над чим вона має працювати (наприклад, над файлами й каталогами).
Sometimes options and arguments are referred to as **parameters**.
A command can be called with more than one option and more than one argument, but a
command doesn't always require an argument or an option.

You might sometimes see options being referred to as **switches** or **flags**,
especially for options that take no argument. In this lesson we will stick with
using the term _option_.

Кожна частина відокремлюється пробілами. Якщо ви пропустите пробіл між `ls` і `-F`, термінал шукатиме команду з назвою `ls-F`, якої не існує. Also, capitalization can be important.
For example, `ls -s` will display the size of files and directories alongside the names,
while `ls -S` will sort the files and directories by size, as shown below:

```bash
$ cd ~/Desktop/shell-lesson-data
$ ls -s exercise-data
```

```output
total 28
 4 animal-counts   4 creatures  12 numbers.txt   4 alkanes   4 writing
```

Note that the sizes returned by `ls -s` are in _blocks_.
Оскільки вони визначаються по-різному для різних операційних систем, ви можете отримати не такі значення, як у прикладі.

```bash
$ ls -S exercise-data
```

```output
animal-counts  creatures  alkanes  writing  numbers.txt
```

Зібравши все це разом, наша команда вище дасть нам список файлів і каталогів у кореневому каталозі `/`.
An example of the output you might get from the above command is given below:

```bash
$ ls -F /
```

```output
Applications/         System/
Library/              Users/
Network/              Volumes/
```

### Конвеєр Неллі: Організація файлів

Знаючи так багато про файли та каталоги, Неллі готова впорядкувати файли, які створить машина для аналізу білків.

She creates a directory called `north-pacific-gyre`
(to remind herself where the data came from),
which will contain the data files from the assay machine
and her data processing scripts.

Each of her physical samples is labelled according to her lab's convention
with a unique ten-character ID,
such as 'NENE01729A'.
This ID is what she used in her collection log
to record the location, time, depth, and other characteristics of the sample,
so she decides to use it within the filename of each data file.
Оскільки результат роботи аналізатора є звичайним текстом, вона назве свої файли `NENE01729A.txt`, `NENE01812A.txt` і так далі.
Усі 1520 файлів буде збережено в одному каталозі.

Тепер у її поточному каталозі `shell-lesson-data`, Нелл може побачити, які файли вона має за допомогою цієї команди:

```bash
$ ls north-pacific-gyre/
```

This command is a lot to type,
but she can let the shell do most of the work through what is called **tab completion**.
Якщо вона набере:

```bash
$ ls nor
```

and then presses <kbd>Tab</kbd> (the tab key on her keyboard),
the shell automatically completes the directory name for her:

```bash
$ ls north-pacific-gyre/
```

Pressing <kbd>Tab</kbd> again does nothing,
since there are multiple possibilities;
pressing <kbd>Tab</kbd> twice brings up a list of all the files.

If Nelle then presses <kbd>G</kbd> and then presses <kbd>Tab</kbd> again,
the shell will append 'goo' since all files that start with 'g' share
the first three characters 'goo'.

```bash
$ ls north-pacific-gyre/goo
```

To see all of those files, she can press <kbd>Tab</kbd> twice more.

```bash
ls north-pacific-gyre/goo goodiff.sh goostats.sh
```

This is called **tab completion**,
and we will see it in many other tools as we go on.

[Arguments]: https://swcarpentry.github.io/shell-novice/reference.html#argument

:::::::::::::::::::::::::::::::::::::::: keypoints

- Файлова система відповідає за керування інформацією на диску.
- Інформація зберігається у файлах, які зберігаються в каталогах (теках).
- Directories can also store other directories, which then form a directory tree.
- Команда `pwd` виводить поточний робочий каталог користувача.
- `ls [path]` prints a listing of a specific file or directory; `ls` on its own lists the current working directory.
- Команда `cd [шлях]` змінює поточний робочий каталог.
- Більшість команд приймають параметри, які починаються з одного символу `-`.
- Назви каталогів в шляху розділяються символами `/` в Unix, але `\\` в Windows.
- Символ `/` сам по собі є кореневим каталогом усієї файлової системи.
- Абсолютний шлях вказує на розташування від кореня файлової системи.
- Відносний шлях вказує на розташування, починаючи з поточного.
- `.` on its own means 'the current directory'; `..` means 'the directory above the current one'.

::::::::::::::::::::::::::::::::::::::::::::::::::


