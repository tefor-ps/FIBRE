# Welcome to the site of the file-sytem based image database (fsdb) of TEFOr Paris-Saclay

## Disclaimer
The projects of this group are under active development and therefore is provided “AS IS”, without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages or other liability, whether in an action of contract, tort or otherwise, arising from, out of or in connection with the software or the use or other dealings in the software.


## Introduction
This repo was conceived for collaborative developent of the 'file-system based image database (fsdb)' of TEFOR Paris-Saclay, an application which facilitates the data management and accessibility of heavy image data on linux storage servers.

## Installation
The fsdb has a modular structure which allows to install only the wanted functionalities. 
Absolutely necessary are:
- [fsdb-install](https://gitlab.com/tefor/fsdb/fsdb-install), which is organizing the installation of the fsdb.
- [fsdb-core](https://gitlab.com/tefor/fsdb/fsdb-core), which is providing the scafolding of all fsdb functionalities.
- [fsdb-janitor](https://gitlab.com/tefor/fsdb/fsdb-janitor), which is keeping the body of data within the fsdb up-to-date.

Optionally can be installed:
- [fsdb-archiver](https://gitlab.com/tefor/fsdb/fsdb-archiver), which is managing the compression and export of data into a cold (offline) archive.
- [fsdb-secDataGeneration](https://gitlab.com/tefor/fsdb/fsdb-sdg), which generates lightweight representations of the raw data to facilitate browsing and screening.
- [fsdb-registration](https://gitlab.com/tefor/fsdb/fsdb-registration), which is implementing selected functionalities of [ANTs](https://stnava.github.io/ANTs/) into the fsdb.


