# Guide to searching in different file types

The goal of this guide is to describe tools for search and for simplification of search for text information in the most of popular files and databases.
The guide is applicable for searching in breaches of various formats (archive big text files, csv/sql), documents (pdf, xls/x, doc/x)
and in specialized databases (1C, Cronos, etc.).

## Contents

- [Universal search](#universal-search)
  - [dnGrep](#dngrep)
- [Text files](#text-files)
  - [grep](#grep)
- [Documents](#documents)
  - [xlsxgrep](#xlsxgrep)
- [Archives](#archives)
  - [zgrep](#zgrep)
  - [7zip](#7zip)
  - [unrar](#unrar)
- [Databases](#databases)
  - [cronodump (Cronos)](#cronodump)
  - [onec_dtools (1C)](#onec_dtools)

## Universal search

### dnGrep

[dnGrep](http://dngrep.github.io/) - a universal tool with graphical user interface for Windows, that can do search through text files, documents,
PDF and in the most popular formats of artchives. Regular expressions and recursive search in the directories are supported. Extra capatibilities: Windows Explorer integration!

Despite on some problems with visualization of search and fails with big archives dnGrep looks like the most perspective tool for mass search in text files.

![image](https://github.com/dnGrep/dnGrep/wiki/Images/grep-main.png)

## Text files

### grep

Unix tool `grep` is the standard of the searchers. You should only pass two parameters: search pattern and file, and the tool searches lines that match the pattern. The pattern can be a simple string (for example, phone number or email address).

`grep` is used by other utilities (or just its syntax), so let's consider some main arguments:

`-A number` - print `number` lines of context after each match

`-B number` - print `number` lines of context before each match

`-С number` - print `number` lines of context surrounding each match

`-i` - регистронезависимый поиск, только при этом режиме поиск по `Target` и `target` найдёт строку "TARGET"

`-R` - рекурсивный поиск, в этом режиме утилита сможет искать во всех вложенных директориях (для поиска по любым файлам в текущей достаточно указать * вместо названия файла)

`-a` - воспринимать все файлы как текстовые, использовать при ошибке `Двоичный файл (стандартный ввод) совпадает`

Пример поиска в текстовом файле:

`grep -iR target dumps/*` - будет произведён поиск по слову `target` во всех регистрах во всех текстовых файлах в директории `dumps`

## Documents

### xlsxgrep

Для поиска в документах XLSX можно использовать либо `grep`, предварительно сконвертировав таблицу в CSV, либо использовать утилиту
`xlsxgrep`. Пример поиска:

`xlsxgrep target -H -N -r dumps/*`

## Archives

- [ ] Написать универсальный скрипт для поиска во всех типах архивов

### zgrep

Для поиска в архивах .gz, .tgz можно использовать утилиту `zgrep`.

Использование аналогично обычному `grep`, за исключением следующих особенностей:
- режим рекурсивного поиска `-R` не поддерживается
- наряду с архивами утилита также может искать по текстовым файлам

`zgrep -ia target dumps/*` - будет произведён поиск по слову `target` во всех регистрах во всех текстовых файлах и gz-архивах в директории `dumps`

### 7zip

Для поиска в архивах `7zip` можно использовать соответствующую утилиту для полной распаковки в цепочке с `grep`:

`7z x archive.7z -so | grep ...`

`7zip` также умеет работать со многими другими типами архивов.

### unrar

Для поиска в архивах `rar` можно использовать соответствующую утилиту для полной распаковки в цепочке с `grep`:

`unrar p archive.rar | grep ...`

## Databases

### cronodump

Для популярного в России формата баз данных Cronos следует использовать либо соответствующую версию клиента (Cronos, CronosPlus, CronosPro)
либо можно сконвертировать базу в формат таблицы CSV с помощью утилиты [cronodump](https://github.com/alephdata/cronodump):

```
git clone https://github.com/alephdata/cronodump && cd cronodump
python3 setup.py install
croconvert --csv cronos_db_directory/

# будет создана новая директория c файлами
ls cronodump-2022-04-25-02-53-57-293000
БТК.csv  Files-FL

grep ...
```

### onec_dtools

Для анализа файлов баз данных 1C можно использовать скрипты на основе утилиты [onec_dtools](https://github.com/Infactum/onec_dtools),
позволяющие вытащить все текстовые строки и бинарные данные из базы любого формата.

- [ ] Написать скрипт для конвертации 1Cv8.CD в CSV
