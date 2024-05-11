# The Ultimate Guide to Cross-Format File Search

The goal of this guide is to describe tools for search and for simplification of search for text information in the most of popular files and databases.

It could benefit journalistic investigations, work with large volumes of data like [document leaks](https://ddosecrets.com/wiki/Distributed_Denial_of_Secrets) and eDiscovery.

The guide is applicable for searching in breaches of various formats (archive big text files, csv/sql), documents (pdf, xls/x, doc/x)
and in specialized databases (1C, Cronos, etc.).

English version | [Russian version](./README-RU.md)

## Contents

- [Universal search](#universal-search)
  - [Datashare](#datashare)
  - [dnGrep](#dngrep)
  - [AstroGrep](#astrogrep)
  - [Pinpoint](#pinpoint)
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

### Datashare

[Datashare](https://datashare.icij.org/) - a multi-OS platform from ICIJ designed for sharing large datasets of documents, particularly among researchers and journalists.

It allows you to search pdfs, images, texts, spreadsheets, slides and much more. 

![image](https://datashare.icij.org/assets/screenshot-extract-1734cb41.png)

### dnGrep

[dnGrep](http://dngrep.github.io/) - a tool with a graphical user interface for Windows, that can search through text files, documents,
PDF and in the most popular formats of archives. Regular expressions and recursive searches in the directories are supported. Extra capabilities: Windows Explorer integration!

Despite some problems with the visualization of search and fails with big archives dnGrep looks like the most perspective tool for mass search in text files.

![image](https://github.com/dnGrep/dnGrep/wiki/Images/grep-main.png)

### AstroGrep

[AstroGrep](https://astrogrep.sourceforge.net/) - a tool with a graphical user interface for Windows that enables users to perform text searches across multiple files, making it particularly useful for those who need to manage large sets of documents. It supports various file formats and offers a user-friendly interface.

The main advantages of AstroGrep include its ability to provide quick results from text searches within a vast array of files. Additionally, AstroGrep highlights the searched terms within the files, which simplifies the process of reviewing search results. It also includes useful functionalities like regular expression matching, which allows for more complex and precise searches.

However, AstroGrep primarily focuses on text searches, so its utility is restricted to textual data and does not extend to searches within Excel documents, archives, image or audio files. 

![image](https://astrogrep.sourceforge.net/pics/ss_main_new.png)

### Pinpoint

[Google Pinpoint](https://journaliststudio.google.com/pinpoint/about/) - a Cloud tool designed to help journalists manage large volumes of information.
It supports various file types including documents (converts almost everything to PDF), images, and audio files, and integrates with Google Drive for efficient data management. The tool enhances research efficiency by enabling quick searches through extensive datasets.

The advantages of Pinpoint include robust search capabilities that save time by simplifying the data review process. It also supports collaborative work, allowing multiple users to work on the same project simultaneously. 

However, as a cloud-based tool, it requires a stable internet connection.

![image](https://storage.googleapis.com/support-kms-prod/dBrMUtT6Ywj9XltPawwCMGkvjfVyQIaJ7zwX)

## Text files

### grep

Unix tool `grep` is the standard of the searchers. You should only pass two parameters: search pattern and file, and the tool searches lines that match the pattern. The pattern can be a simple string (for example, a phone number or email address).

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
