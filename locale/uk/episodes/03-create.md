---
title: Робота з файлами та каталогами
teaching: 30
exercises: 20
---

::::::::::::::::::::::::::::::::::::::: objectives

- Створити ієрархію каталогів, яка відповідає заданій схемі.
- Створити файли в цій ієрархії за допомогою редактора або шляхом копіювання та перейменування файлів, що вже існують.
- Видалити, скопіювати та перемістити вказані файли та/або каталоги.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Як я можу створювати, копіювати та видаляти файли і каталоги?
- Як я можу редагувати файли?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Створення каталогів

Тепер ми знаємо, як досліджувати файли та каталоги, але як їх створювати?

In this episode we will learn about creating and moving files and directories,
using the `exercise-data/writing` directory as an example.

### Крок перший: подивіться, де ми знаходимося і що вже маємо

Ми все ще маємо бути у каталозі `shell-lesson-data` на Робочому столі (англ. Desktop), що ми можемо перевірити за допомогою:

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data
```

Далі ми перейдемо до каталогу `exercise-data/writing` і подивимося, що у ньому міститься:

```bash
$ cd exercise-data/writing/
$ ls -F
```

```output
haiku.txt LittleWomen.txt
```

### Створення каталогу

Створимо новий каталог з назвою `thesis` за допомогою команди `mkdir thesis` (яка не має виводу):

```bash
$ mkdir thesis
```

Як ви можете здогадатися з її назви, команда `mkdir` означає 'зробити каталог' (англ. 'make directory').
Оскільки `thesis` є відносним шляхом
(тобто не має початкової косої риски, як `/what/ever/thesis`),
новий каталог буде створено у поточному робочому каталозі:

```bash
$ ls -F
```

```output
haiku.txt  LittleWomen.txt  thesis/
```

Оскільки ми щойно створили каталог `thesis`, у ньому ще нічого немає:

```bash
$ ls -F thesis
```

Note that `mkdir` is not limited to creating single directories one at a time.
Параметр `-p` дозволяє команді `mkdir` створювати каталог із вкладеними підкаталогами за одну операцію:

```bash
$ mkdir -p ../project/data ../project/results
```

The `-R` option to the `ls` command will list all nested subdirectories within a directory.
Let's use `ls -FR` to recursively list the new directory hierarchy we just created in the
`project` directory:

```bash
$ ls -FR ../project
```

```output
../project/:
data/  results/

../project/data:

../project/results:
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Два способи зробити одне й те саме

Використання терміналу для створення каталогу нічим не відрізняється від використання файлового провідника.
If you open the current directory using your operating system's graphical file explorer,
the `thesis` directory will appear there too.
While the shell and the file explorer are two different ways of interacting with the files,
the files and directories themselves are the same.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Good names for files and directories

Complicated names of files and directories can make your life painful
when working on the command line. Here we provide a few useful
tips for the names of your files and directories.

1. Не використовуйте пробіли.

Spaces can make a name more meaningful,
but since spaces are used to separate arguments on the command line
it is better to avoid them in names of files and directories.
Ви можете використовувати `-` або `_` (наприклад, `north-pacific-gyre/` замість `north pacific gyre/`).
Щоб перевірити це, спробуйте набрати `mkdir north pacific gyre` і подивіться, який каталог (або каталоги!)
буде створено при перевірці за допомогою `ls -F`.

2. Не починайте назву з `-` (тире).

Команди розглядають назви, що починаються з `-`, як опції.

3. Використовуйте літери, цифри, `.` (крапка), `-` (тире) і `_` (підкреслення).

Багато інших символів мають особливе значення у командному рядку.
We will learn about some of these during this lesson.
There are special characters that can cause your command to not work as
expected and can even result in data loss.

If you need to refer to names of files or directories that have spaces
or other special characters, you should surround the name in single
[quotes](https://www.gnu.org/software/bash/manual/html_node/Quoting.html) (`''`).

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  instructor

Учні іноді можуть потрапити в пастку текстових редакторів командного рядка, таких як Vim, Emacs або Nano. Closing the terminal emulator and opening
a new one can be frustrating as learners will have to navigate to the
correct folder again. Для пом'якшення цієї проблеми ми радимо викладачам використовувати той самий текстовий редактор, що й учні під час семінарів (у більшості випадків Nano).

::::::::::::::::::::::::::::::::::::::::::::::::::

### Створення текстового файлу

Let's change our working directory to `thesis` using `cd`,
then run a text editor called Nano to create a file called `draft.txt`:

```bash
$ cd thesis
$ nano draft.txt
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Який редактор?

When we say, '`nano` is a text editor' we really do mean 'text'. Він може працювати лише з простими символьними даними, а не з таблицями, зображеннями чи будь-якими іншими зручними для людини даними. We use it in examples because it is one of the
least complex text editors. However, because of this trait, it may
not be powerful enough or flexible enough for the work you need to do
after this workshop. У системах Unix (таких як Linux та macOS), багато програмістів використовують [Emacs] (https://www.gnu.org/software/emacs/) або [Vim](https://www.vim.org/) (обидва вимагають більше часу на вивчення), або графічний редактор, такий як [Gedit](https://projects.gnome.org/gedit/). On Windows, you may wish to
use [Notepad++](https://notepad-plus-plus.org/).  Windows also has a built-in
editor called `notepad` that can be run from the command line in the same
way as `nano` for the purposes of this lesson.

Незалежно від того, яким редактором ви користуєтеся, вам потрібно знати, де він шукає і зберігає файли. If you start it from the shell, it will (probably)
use your current working directory as its default location. If you use
your computer's start menu, it may want to save files in your Desktop or
Documents directory instead. Ви можете змінити це, перейшовши до іншого каталогу під час першого виконання команди "Зберегти як...".

::::::::::::::::::::::::::::::::::::::::::::::::::

Let's type in a few lines of text.

![](fig/nano-screenshot.png){alt="screenshot of nano text editor in action with the text It's not publish or perish any more, it's share and thrive"}

Після того, як ми будемо задоволені нашим текстом, ми можемо натиснути <kbd>Ctrl</kbd>\+<kbd>O</kbd> (натисніть клавішу <kbd>Ctrl</kbd> or <kbd>Control</kbd> і, утримуючи її, натиснути клавішу <kbd>O</kbd>), щоб записати наші дані на диск. Нас запитають, до якого файлу ми хочемо зберегти дані. Натисніть клавішу <kbd>Return</kbd>, щоб прийняти запропоновану за замовчуванням назву `draft.txt`.

Once our file is saved, we can use <kbd>Ctrl</kbd>\+<kbd>X</kbd> to quit the editor and
return to the shell.

:::::::::::::::::::::::::::::::::::::::::  callout

## Control, Ctrl, or ^ Key

The Control key is also called the 'Ctrl' key. There are various ways
in which using the Control key may be described. For example, you may
see an instruction to press the <kbd>Control</kbd> key and, while holding it down,
press the <kbd>X</kbd> key, described as any of:

- `Control-X`
- `Control+X`
- `Ctrl-C`
- `Ctrl+X`
- `^X`
- `C-x`

У nano, у нижній частині екрана ви побачите `^G Отримати довідку ^O Вивести на екран`.
This means that you can use `Control-G` to get help and `Control-O` to save your
file.

::::::::::::::::::::::::::::::::::::::::::::::::::

Після завершення роботи команда `nano` не залишає жодних даних на екрані, але `ls` тепер показує, що ми створили файл з назвою `draft.txt`:

```bash
$ ls
```

```output
draft.txt
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Створення файлів іншим способом

Ми побачили, як створювати текстові файли за допомогою редактора `nano`.
Тепер спробуйте виконати наступну команду:

```bash
$ touch my_file.txt
```

1. Що зробила команда `touch`?
   When you look at your current directory using the GUI file explorer,
   does the file show up?

2. Use `ls -l` to inspect the files.  How large is `my_file.txt`?

3. When might you want to create a file this way?

:::::::::::::::  solution

## Solution

1. The `touch` command generates a new file called `my_file.txt` in
   your current directory.  You
   can observe this newly generated file by typing `ls` at the
   command line prompt.  `my_file.txt` can also be viewed in your
   GUI file explorer.

2. When you inspect the file with `ls -l`, note that the size of
   `my_file.txt` is 0 bytes.  In other words, it contains no data.
   If you open `my_file.txt` using your text editor it is blank.

3. Some programs do not generate output files themselves, but
   instead require that empty files have already been generated.
   When the program is run, it searches for an existing file to
   populate with its output.  The touch command allows you to
   efficiently generate a blank text file to be used by such
   programs.

:::::::::::::::::::::::::

To avoid confusion later on,
we suggest removing the file you've just created before proceeding with the rest
of the episode, otherwise future outputs may vary from those given in the lesson.
To do this, use the following command:

```bash
$ rm my_file.txt
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## What's In A Name?

You may have noticed that all of Nelle's files are named 'something dot
something', and in this part of the lesson, we always used the extension
`.txt`.  This is just a convention; we can call a file `mythesis` or
almost anything else we want. However, most people use two-part names
most of the time to help them (and their programs) tell different kinds
of files apart. The second part of such a name is called the
**filename extension** and indicates
what type of data the file holds: `.txt` signals a plain text file, `.pdf`
indicates a PDF document, `.cfg` is a configuration file full of parameters
for some program or other, `.png` is a PNG image, and so on.

This is just a convention, albeit an important one. Files merely contain
bytes; it's up to us and our programs to interpret those bytes
according to the rules for plain text files, PDF documents, configuration
files, images, and so on.

Naming a PNG image of a whale as `whale.mp3` doesn't somehow
magically turn it into a recording of whale song, though it _might_
cause the operating system to associate the file with a music player
program. In this case, if someone double-clicked `whale.mp3` in a file
explorer program, the music player will automatically (and erroneously)
attempt to open the `whale.mp3` file.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Moving files and directories

Returning to the `shell-lesson-data/exercise-data/writing` directory,

```bash
$ cd ~/Desktop/shell-lesson-data/exercise-data/writing
```

In our `thesis` directory we have a file `draft.txt`
which isn't a particularly informative name,
so let's change the file's name using `mv`,
which is short for 'move':

```bash
$ mv thesis/draft.txt thesis/quotes.txt
```

The first argument tells `mv` what we're 'moving',
while the second is where it's to go.
In this case,
we're moving `thesis/draft.txt` to `thesis/quotes.txt`,
which has the same effect as renaming the file.
Sure enough,
`ls` shows us that `thesis` now contains one file called `quotes.txt`:

```bash
$ ls thesis
```

```output
quotes.txt
```

One must be careful when specifying the target file name, since `mv` will
silently overwrite any existing file with the same name, which could
lead to data loss. By default, `mv` will not ask for confirmation before overwriting files.
However, an additional option, `mv -i` (or `mv --interactive`), will cause `mv` to request
such confirmation.

Note that `mv` also works on directories.

Let's move `quotes.txt` into the current working directory.
We use `mv` once again,
but this time we'll use just the name of a directory as the second argument
to tell `mv` that we want to keep the filename
but put the file somewhere new.
(This is why the command is called 'move'.)
In this case,
the directory name we use is the special directory name `.` that we mentioned earlier.

```bash
$ mv thesis/quotes.txt .
```

The effect is to move the file from the directory it was in to the current working directory.
`ls` now shows us that `thesis` is empty:

```bash
$ ls thesis
```

```output
$
```

Alternatively, we can confirm the file `quotes.txt` is no longer present in the `thesis` directory
by explicitly trying to list it:

```bash
$ ls thesis/quotes.txt
```

```error
ls: cannot access 'thesis/quotes.txt': No such file or directory
```

`ls` with a filename or directory as an argument only lists the requested file or directory.
If the file given as the argument doesn't exist, the shell returns an error as we saw above.
We can use this to see that `quotes.txt` is now present in our current directory:

```bash
$ ls quotes.txt
```

```output
quotes.txt
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Moving Files to a new folder

After running the following commands,
Jamie realizes that she put the files `sucrose.dat` and `maltose.dat` into the wrong folder.
The files should have been placed in the `raw` folder.

```bash
$ ls -F
 analyzed/ raw/
$ ls -F analyzed
fructose.dat glucose.dat maltose.dat sucrose.dat
$ cd analyzed
```

Fill in the blanks to move these files to the `raw/` folder
(i.e. the one she forgot to put them in)

```bash
$ mv sucrose.dat maltose.dat ____/____
```

:::::::::::::::  solution

## Solution

```bash
$ mv sucrose.dat maltose.dat ../raw
```

Recall that `..` refers to the parent directory (i.e. one above the current directory)
and that `.` refers to the current directory.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Copying files and directories

The `cp` command works very much like `mv`,
except it copies a file instead of moving it.
We can check that it did the right thing using `ls`
with two paths as arguments --- like most Unix commands,
`ls` can be given multiple paths at once:

```bash
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt
```

```output
quotes.txt   thesis/quotations.txt
```

We can also copy a directory and all its contents by using the
[recursive](https://en.wikipedia.org/wiki/Recursion) option `-r`,
e.g. to back up a directory:

```bash
$ cp -r thesis thesis_backup
```

We can check the result by listing the contents of both the `thesis` and `thesis_backup` directory:

```bash
$ ls thesis thesis_backup
```

```output
thesis:
quotations.txt

thesis_backup:
quotations.txt
```

It is important to include the `-r` flag. If you want to copy a directory and you omit this option
you will see a message that the directory has been omitted because `-r not specified`.

```bash
$ cp thesis thesis_backup
cp: -r not specified; omitting directory 'thesis'
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Renaming Files

Suppose that you created a plain-text file in your current directory to contain a list of the
statistical tests you will need to do to analyze your data, and named it `statstics.txt`

After creating and saving this file you realize you misspelled the filename! You want to
correct the mistake, which of the following commands could you use to do so?

1. `cp statstics.txt statistics.txt`
2. `mv statstics.txt statistics.txt`
3. `mv statstics.txt .`
4. `cp statstics.txt .`

:::::::::::::::  solution

## Solution

1. No.  While this would create a file with the correct name,
   the incorrectly named file still exists in the directory
   and would need to be deleted.
2. Yes, this would work to rename the file.
3. No, the period(.) indicates where to move the file, but does not provide a new file name;
   identical file names
   cannot be created.
4. No, the period(.) indicates where to copy the file, but does not provide a new file name;
   identical file names cannot be created.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Moving and Copying

What is the output of the closing `ls` command in the sequence shown below?

```bash
$ pwd
```

```output
/Users/jamie/data
```

```bash
$ ls
```

```output
proteins.dat
```

```bash
$ mkdir recombined
$ mv proteins.dat recombined/
$ cp recombined/proteins.dat ../proteins-saved.dat
$ ls
```

1. `proteins-saved.dat recombined`
2. `recombined`
3. `proteins.dat recombined`
4. `proteins-saved.dat`

:::::::::::::::  solution

## Solution

We start in the `/Users/jamie/data` directory, and create a new folder called `recombined`.
The second line moves (`mv`) the file `proteins.dat` to the new folder (`recombined`).
The third line makes a copy of the file we just moved.
The tricky part here is where the file was copied to.
Recall that `..` means 'go up a level', so the copied file is now in `/Users/jamie`.
Notice that `..` is interpreted with respect to the current working
directory, **not** with respect to the location of the file being copied.
So, the only thing that will show using ls (in `/Users/jamie/data`) is the recombined folder.

1. No, see explanation above.  `proteins-saved.dat` is located at `/Users/jamie`
2. Yes
3. No, see explanation above.  `proteins.dat` is located at `/Users/jamie/data/recombined`
4. No, see explanation above.  `proteins-saved.dat` is located at `/Users/jamie`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Removing files and directories

Returning to the `shell-lesson-data/exercise-data/writing` directory,
let's tidy up this directory by removing the `quotes.txt` file we created.
The Unix command we'll use for this is `rm` (short for 'remove'):

```bash
$ rm quotes.txt
```

We can confirm the file has gone using `ls`:

```bash
$ ls quotes.txt
```

```error
ls: cannot access 'quotes.txt': No such file or directory
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Deleting Is Forever

The Unix shell doesn't have a trash bin that we can recover deleted
files from (though most graphical interfaces to Unix do).  Instead,
when we delete files, they are unlinked from the file system so that
their storage space on disk can be recycled. Tools for finding and
recovering deleted files do exist, but there's no guarantee they'll
work in any particular situation, since the computer may recycle the
file's disk space right away.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Using `rm` Safely

What happens when we execute `rm -i thesis_backup/quotations.txt`?
Why would we want this protection when using `rm`?

:::::::::::::::  solution

## Solution

```output
rm: remove regular file 'thesis_backup/quotations.txt'? y
```

The `-i` option will prompt before (every) removal (use <kbd>Y</kbd> to confirm deletion
or <kbd>N</kbd> to keep the file).
The Unix shell doesn't have a trash bin, so all the files removed will disappear forever.
By using the `-i` option, we have the chance to check that we are deleting only the files
that we want to remove.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

If we try to remove the `thesis` directory using `rm thesis`,
we get an error message:

```bash
$ rm thesis
```

```error
rm: cannot remove 'thesis': Is a directory
```

This happens because `rm` by default only works on files, not directories.

`rm` can remove a directory _and all its contents_ if we use the
recursive option `-r`, and it will do so _without any confirmation prompts_:

```bash
$ rm -r thesis
```

Given that there is no way to retrieve files deleted using the shell,
`rm -r` _should be used with great caution_
(you might consider adding the interactive option `rm -r -i`).

## Operations with multiple files and directories

Oftentimes one needs to copy or move several files at once.
This can be done by providing a list of individual filenames,
or specifying a naming pattern using wildcards. Wildcards are
special characters that can be used to represent unknown characters
or sets of characters when navigating the Unix file system.

:::::::::::::::::::::::::::::::::::::::  challenge

## Copy with Multiple Filenames

For this exercise, you can test the commands in the `shell-lesson-data/exercise-data` directory.

In the example below, what does `cp` do when given several filenames and a directory name?

```bash
$ mkdir backup
$ cp creatures/minotaur.dat creatures/unicorn.dat backup/
```

In the example below, what does `cp` do when given three or more file names?

```bash
$ cd creatures
$ ls -F
```

```output
basilisk.dat  minotaur.dat  unicorn.dat
```

```bash
$ cp minotaur.dat unicorn.dat basilisk.dat
```

:::::::::::::::  solution

## Solution

If given more than one file name followed by a directory name
(i.e. the destination directory must be the last argument),
`cp` copies the files to the named directory.

If given three file names, `cp` throws an error such as the one below,
because it is expecting a directory name as the last argument.

```error
cp: target 'basilisk.dat' is not a directory
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

### Using wildcards for accessing multiple files at once

:::::::::::::::::::::::::::::::::::::::::  callout

## Wildcards

`*` is a **wildcard**, which represents zero or more other characters.
Let's consider the `shell-lesson-data/exercise-data/alkanes` directory:
`*.pdb` represents `ethane.pdb`, `propane.pdb`, and every
file that ends with '.pdb'. On the other hand, `p*.pdb` only represents
`pentane.pdb` and `propane.pdb`, because the 'p' at the front can only
represent filenames that begin with the letter 'p'.

`?` is also a wildcard, but it represents exactly one character.
So `?ethane.pdb` could represent `methane.pdb` whereas
`*ethane.pdb` represents both `ethane.pdb` and `methane.pdb`.

Wildcards can be used in combination with each other. For example,
`???ane.pdb` indicates three characters followed by `ane.pdb`,
giving `cubane.pdb  ethane.pdb  octane.pdb`.

When the shell sees a wildcard, it expands the wildcard to create a
list of matching filenames _before_ running the preceding command.
As an exception, if a wildcard expression does not match
any file, Bash will pass the expression as an argument to the command
as it is. For example, typing `ls *.pdf` in the `alkanes` directory
(which contains only files with names ending with `.pdb`) results in
an error message that there is no file called `*.pdf`.
However, generally commands like `wc` and `ls` see the lists of
file names matching these expressions, but not the wildcards
themselves. It is the shell, not the other programs, that expands
the wildcards.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## List filenames matching a pattern

When run in the `alkanes` directory, which `ls` command(s) will
produce this output?

`ethane.pdb   methane.pdb`

1. `ls *t*ane.pdb`
2. `ls *t?ne.*`
3. `ls *t??ne.pdb`
4. `ls ethane.*`

:::::::::::::::  solution

## Solution

The solution is `3.`

`1.` shows all files whose names contain zero or more characters (`*`)
followed by the letter `t`,
then zero or more characters (`*`) followed by `ane.pdb`.
This gives `ethane.pdb  methane.pdb  octane.pdb  pentane.pdb`.

`2.` shows all files whose names start with zero or more characters (`*`) followed by
the letter `t`,
then a single character (`?`), then `ne.` followed by zero or more characters (`*`).
This will give us `octane.pdb` and `pentane.pdb` but doesn't match anything
which ends in `thane.pdb`.

`3.` fixes the problems of option 2 by matching two characters (`??`) between `t` and `ne`.
This is the solution.

`4.` only shows files starting with `ethane.`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## More on Wildcards

Sam has a directory containing calibration data, datasets, and descriptions of
the datasets:

```bash
.
├── 2015-10-23-calibration.txt
├── 2015-10-23-dataset1.txt
├── 2015-10-23-dataset2.txt
├── 2015-10-23-dataset_overview.txt
├── 2015-10-26-calibration.txt
├── 2015-10-26-dataset1.txt
├── 2015-10-26-dataset2.txt
├── 2015-10-26-dataset_overview.txt
├── 2015-11-23-calibration.txt
├── 2015-11-23-dataset1.txt
├── 2015-11-23-dataset2.txt
├── 2015-11-23-dataset_overview.txt
├── backup
│   ├── calibration
│   └── datasets
└── send_to_bob
    ├── all_datasets_created_on_a_23rd
    └── all_november_files
```

Before heading off to another field trip, she wants to back up her data and
send some datasets to her colleague Bob. Sam uses the following commands
to get the job done:

```bash
$ cp *dataset* backup/datasets
$ cp ____calibration____ backup/calibration
$ cp 2015-____-____ send_to_bob/all_november_files/
$ cp ____ send_to_bob/all_datasets_created_on_a_23rd/
```

Help Sam by filling in the blanks.

The resulting directory structure should look like this

```bash
.
├── 2015-10-23-calibration.txt
├── 2015-10-23-dataset1.txt
├── 2015-10-23-dataset2.txt
├── 2015-10-23-dataset_overview.txt
├── 2015-10-26-calibration.txt
├── 2015-10-26-dataset1.txt
├── 2015-10-26-dataset2.txt
├── 2015-10-26-dataset_overview.txt
├── 2015-11-23-calibration.txt
├── 2015-11-23-dataset1.txt
├── 2015-11-23-dataset2.txt
├── 2015-11-23-dataset_overview.txt
├── backup
│   ├── calibration
│   │   ├── 2015-10-23-calibration.txt
│   │   ├── 2015-10-26-calibration.txt
│   │   └── 2015-11-23-calibration.txt
│   └── datasets
│       ├── 2015-10-23-dataset1.txt
│       ├── 2015-10-23-dataset2.txt
│       ├── 2015-10-23-dataset_overview.txt
│       ├── 2015-10-26-dataset1.txt
│       ├── 2015-10-26-dataset2.txt
│       ├── 2015-10-26-dataset_overview.txt
│       ├── 2015-11-23-dataset1.txt
│       ├── 2015-11-23-dataset2.txt
│       └── 2015-11-23-dataset_overview.txt
└── send_to_bob
    ├── all_datasets_created_on_a_23rd
    │   ├── 2015-10-23-dataset1.txt
    │   ├── 2015-10-23-dataset2.txt
    │   ├── 2015-10-23-dataset_overview.txt
    │   ├── 2015-11-23-dataset1.txt
    │   ├── 2015-11-23-dataset2.txt
    │   └── 2015-11-23-dataset_overview.txt
    └── all_november_files
        ├── 2015-11-23-calibration.txt
        ├── 2015-11-23-dataset1.txt
        ├── 2015-11-23-dataset2.txt
        └── 2015-11-23-dataset_overview.txt
```

:::::::::::::::  solution

## Solution

```bash
$ cp *calibration.txt backup/calibration
$ cp 2015-11-* send_to_bob/all_november_files/
$ cp *-23-dataset* send_to_bob/all_datasets_created_on_a_23rd/
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Organizing Directories and Files

Jamie is working on a project, and she sees that her files aren't very well
organized:

```bash
$ ls -F
```

```output
analyzed/  fructose.dat    raw/   sucrose.dat
```

The `fructose.dat` and `sucrose.dat` files contain output from her data
analysis. What command(s) covered in this lesson does she need to run
so that the commands below will produce the output shown?

```bash
$ ls -F
```

```output
analyzed/   raw/
```

```bash
$ ls analyzed
```

```output
fructose.dat    sucrose.dat
```

:::::::::::::::  solution

## Solution

```bash
mv *.dat analyzed
```

Jamie needs to move her files `fructose.dat` and `sucrose.dat` to the `analyzed` directory.
The shell will expand \*.dat to match all .dat files in the current directory.
The `mv` command then moves the list of .dat files to the 'analyzed' directory.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Reproduce a folder structure

You're starting a new experiment and would like to duplicate the directory
structure from your previous experiment so you can add new data.

Assume that the previous experiment is in a folder called `2016-05-18`,
which contains a `data` folder that in turn contains folders named `raw` and
`processed` that contain data files.  The goal is to copy the folder structure
of the `2016-05-18` folder into a folder called `2016-05-20`
so that your final directory structure looks like this:

```output
2016-05-20/
└── data
   ├── processed
   └── raw
```

Which of the following set of commands would achieve this objective?
What would the other commands do?

```bash
$ mkdir 2016-05-20
$ mkdir 2016-05-20/data
$ mkdir 2016-05-20/data/processed
$ mkdir 2016-05-20/data/raw
```

```bash
$ mkdir 2016-05-20
$ cd 2016-05-20
$ mkdir data
$ cd data
$ mkdir raw processed
```

```bash
$ mkdir 2016-05-20/data/raw
$ mkdir 2016-05-20/data/processed
```

```bash
$ mkdir -p 2016-05-20/data/raw
$ mkdir -p 2016-05-20/data/processed
```

```bash
$ mkdir 2016-05-20
$ cd 2016-05-20
$ mkdir data
$ mkdir raw processed
```

:::::::::::::::  solution

## Solution

The first two sets of commands achieve this objective.
The first set uses relative paths to create the top-level directory before
the subdirectories.

The third set of commands will give an error because the default behavior of `mkdir`
won't create a subdirectory of a non-existent directory:
the intermediate level folders must be created first.

The fourth set of commands achieve this objective. Remember, the `-p` option,
followed by a path of one or more
directories, will cause `mkdir` to create any intermediate subdirectories as required.

The final set of commands generates the 'raw' and 'processed' directories at the same level
as the 'data' directory.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- `cp [old] [new]` copies a file.
- `mkdir [path]` creates a new directory.
- `mv [old] [new]` moves (renames) a file or directory.
- `rm [path]` removes (deletes) a file.
- `*` matches zero or more characters in a filename, so `*.txt` matches all files ending in `.txt`.
- `?` matches any single character in a filename, so `?.txt` matches `a.txt` but not `any.txt`.
- Use of the Control key may be described in many ways, including `Ctrl-X`, `Control-X`, and `^X`.
- The shell does not have a trash bin: once something is deleted, it's really gone.
- Most files' names are `something.extension`. The extension isn't required, and doesn't guarantee anything, but is normally used to indicate the type of data in the file.
- Depending on the type of work you do, you may need a more powerful text editor than Nano.

::::::::::::::::::::::::::::::::::::::::::::::::::
