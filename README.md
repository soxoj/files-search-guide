# Guide to searching in different file types

The goal of this guide is to describe tools for search and for simplification of search for text information in the most of popular files and databases.
The guide is applicable for searching in breaches of various formats (archive big text files, csv/sql), documents (pdf, xls/x, doc/x)
and in specialized databases (1C, Cronos, etc.).

[Russian version](./README-RU.md) | English version

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
  - [1c-database-converter (1C)](#1c)

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

`-C number` - print `number` lines of context surrounding each match

`-i` - case-insensitive search: search on the `Target` and `target` words will found `TARGET`

`-R` - recursive search: the tool will scan all the nested directories (you can use * as the name of file)

`-a` - treat all files as text files, use in case of the error `Binary file (standard input) matches`

Example of `grep` usage:

`grep -iR target dumps/*` - search on the word `target` (case-insensitive) throuhg all the text files in the directory `dumps`

## Documents

### xlsxgrep

It will be best to convert `XLSX` files to `CSV` and use `grep` for the search or just use tool`xlsxgrep`.

Usage example:

`xlsxgrep target -H -N -r dumps/*`

## Archives

- [ ] TODO: link to a universal script for search through the all types of archives

### zgrep

It will be best to use `zgrep` for searching in archives .gz and .tgz.

The tool is a direct analogue of `grep` except for the following:
- the recursive mode `-R` is not supported
- the tool can search both through text files and thtough archives

Example of `zgrep` usage:

`zgrep -ia target dumps/*` - search on the word `target` (case-insensitive) throuhg all the text files and through gz-archives un the directory `dumps`

### 7zip

It will be best to use `7zip` unpacking tool with `grep` to search through 7z archives:

Usage example:

`7z x archive.7z -so | grep ...`

`7zip` also can work with other types of archives.

### unrar

It will be best to use `unrar` unpacking tool with `grep` to searcg through the rar archives:

Usage example:

`unrar p archive.rar | grep ...`

## Databases

### cronodump

There is a popular database software and file format `Cronos` in Russia. It will be best to use an appropriate version of official client (Cronos, CronosPlus, CronosPro) or you can just convert database to a CSV file with the tool [cronodump](https://github.com/alephdata/cronodump):

```
git clone https://github.com/alephdata/cronodump && cd cronodump
python3 setup.py install
croconvert --csv cronos_db_directory/

# a new directory will be created 
ls cronodump-2022-04-25-02-53-57-293000
БТК.csv  Files-FL

grep ...
```

### 1C

There is a popular software 1C in Russia. 1C uses its own file formats: .1CD, .efd and others. You can use [onec_dtools](https://github.com/Infactum/onec_dtools) to write your custom script to extract all the data from 1C database or use [1c-database-converter](https://github.com/soxoj/1c-database-converter) to convert database to a CSV files.

```
./run.py 8-2-14.1CD
Target: 8-2-14.1CD
Results found: 1
1) Out Dir: 8-2-14.1CD_csv
File Type: 1CD
Status: Exported content of 1CD file

------------------------------
Total found: 1
```