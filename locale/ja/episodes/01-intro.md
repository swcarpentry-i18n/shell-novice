---
title: シェルの紹介
teaching: 5
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- シェルがキーボード、画面、オペレーティングシステム、およびユーザーのプログラムとどのように関係しているかを説明する
- グラフィカルインターフェイスの代わりにコマンドラインインターフェイスを使用する場合と理由を説明する

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- コマンドシェルとは何ですか？それを使う利点は何ですか？

::::::::::::::::::::::::::::::::::::::::::::::::::

### 背景

Humans and computers commonly interact in many different ways, such as through a keyboard and mouse,
touch screen interfaces, or using speech recognition systems.
The most widely used way to interact with personal computers is called a
**graphical user interface** (GUI).
With a GUI, we give instructions by clicking a mouse and using menu-driven interactions.

While the visual aid of a GUI makes it intuitive to learn,
this way of delivering instructions to a computer scales very poorly.
Imagine the following task:
for a literature search, you have to copy the third line of one thousand text files in one thousand
different directories and paste it into a single file.
Using a GUI, you would not only be clicking at your desk for several hours,
but you could potentially also commit an error in the process of completing this repetitive task.
This is where we take advantage of the Unix shell.
The Unix shell is both a **command-line interface** (CLI) and a scripting language,
allowing such repetitive tasks to be done automatically and fast.
With the proper commands, the shell can repeat tasks with or without some modification
as many times as we want.
Using the shell, the task in the literature example can be accomplished in seconds.

### シェル

The shell is a program where users can type commands.
With the shell, it's possible to invoke complicated programs like climate modeling software
or simple commands that create an empty directory with only one line of code.
最も人気のある Unix シェルは、Bash、Bourne Again SHell です (これは Stephen Bourne によって書かれたシェルから派生したものであるためそう呼ばれています)。
Bash はほとんどの最新の Unix の搭載されたもののデフォルトシェルであり、 Windows 用の Unix のようなツールを提供するほとんどのパッケージで使われています。
Note that 'Git Bash' is a piece of software that enables Windows users to use a Bash like interface
when interacting with Git.

Using the shell will take some effort and some time to learn.
While a GUI presents you with choices to select, CLI choices are not automatically presented to you,
so you must learn a few commands like new vocabulary in a language you're studying.
However, unlike a spoken language, a small number of "words" (i.e. commands) gets you a long way,
and we'll cover those essential few today.

The grammar of a shell allows you to combine existing tools into powerful
pipelines and handle large volumes of data automatically. Sequences of
commands can be written into a _script_, improving the reproducibility of
workflows.

さらに、リモートマシンやスーパーコンピュータとやりとりするには、コマンドラインが最も簡単な方法であることが多いです。
高性能コンピュータシステムなどの多様な特殊なリソースやツールを実行するにはシェルに精通していることはほぼ必須です。
クラスターやクラウドコンピューティングシステムが科学的なデータクランチングのために普及するにつれ、 シェルによってやりとりできるということは必須のスキルになってきています。
ここで取り扱うコマンドラインのスキルを手にいれることで、 幅広く科学的な問題や計算機上の課題に取り組むことができます。

Let's get started.

When the shell is first opened, you are presented with a **prompt**,
indicating that the shell is waiting for input.

```bash
$
```

The shell typically uses `$ ` as the prompt, but may use a different symbol.
In the examples for this lesson, we'll show the prompt as `$ `.
Most importantly, _do not type the prompt_ when typing commands.
Only type the command that follows the prompt.
This rule applies both in these lessons and in lessons from other sources.
Also note that after you type a command, you have to press the <kbd>Enter</kbd> key to execute it.

The prompt is followed by a **text cursor**, a character that indicates the position where your
typing will appear.
The cursor is usually a flashing or solid block, but it can also be an underscore or a pipe.
You may have seen it in a text editor program, for example.

Note that your prompt might look a little different. In particular, most popular shell
environments by default put your user name and the host name before the `$`. Such
a prompt might look like, e.g.:

```bash
nelle@localhost $
```

The prompt might even include more than this. Do not worry if your prompt is not
just a short `$ `. This lesson does not depend on this additional information and it
should also not get in your way. The only important item to focus on is the `$ `
character itself and we will see later why.

So let's try our first command, `ls`, which is short for listing.
This command will list the contents of the current directory:

```bash
$ ls
```

```output
Desktop     Downloads   Movies      Pictures
Documents   Library     Music       Public
```

:::::::::::::::::::::::::::::::::::::::::  callout

## コマンドが見つからないとき

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

## Nelle's Pipeline: A Typical Problem

Nelle Nemo, a marine biologist,
has just returned from a six-month survey of the
[North Pacific Gyre](https://en.wikipedia.org/wiki/North_Pacific_Gyre),
where she has been sampling gelatinous marine life in the
[Great Pacific Garbage Patch](https://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch).
She has 1520 samples that she's run through an assay machine to measure the relative abundance
of 300 proteins.
She needs to run these 1520 files through an imaginary program called `goostats.sh`.
In addition to this huge task, she has to write up results by the end of the month, so her paper
can appear in a special issue of _Aquatic Goo Letters_.

If Nelle chooses to run `goostats.sh` by hand using a GUI,
she'll have to select and open a file 1520 times.
If `goostats.sh` takes 30 seconds to run each file, the whole process will take more than 12 hours
of Nelle's attention.
With the shell, Nelle can instead assign her computer this mundane task while she focuses
her attention on writing her paper.

The next few lessons will explore the ways Nelle can achieve this.
More specifically,
the lessons explain how she can use a command shell to run the `goostats.sh` program,
using loops to automate the repetitive steps of entering file names,
so that her computer can work while she writes her paper.

As a bonus,
once she has put a processing pipeline together,
she will be able to use it again whenever she collects more data.

In order to achieve her task, Nelle needs to know how to:

- navigate to a file/directory
- create a file/directory
- check the length of a file
- chain commands together
- retrieve a set of files
- iterate over files
- run a shell script containing her pipeline

:::::::::::::::::::::::::::::::::::::::: keypoints

- A shell is a program whose primary purpose is to read commands and run other programs.
- This lesson uses Bash, the default shell in many implementations of Unix.
- Programs can be run in Bash by entering commands at the command-line prompt.
- The shell's main advantages are its high action-to-keystroke ratio, its support for automating repetitive tasks, and its capacity to access networked machines.
- A significant challenge when using the shell can be knowing what commands need to be run and how to run them.

::::::::::::::::::::::::::::::::::::::::::::::::::