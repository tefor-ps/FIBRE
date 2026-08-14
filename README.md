# fsdb - file system based database

## An introduction
The fsdb organizes the transfer and management of (multidimensional) image data sets from their image acquisition machines (IAS) to the centralized storage server. It can be run directly on the storage server (if it is strong enough) or on a separate compute server, which is connected to the storeage server. 

Following our own need and that of our collaborators (our focus lies on the analysis of heavy image data like collections of high resolution 3D confocal stacks) we developed the fsdb as a hands-off data management system for heavy image data. 

Our solution for accessibility of big data is based on __secondary data__, which represent the original data in the form of small (light-weight) derivatives.   

The fsdb is organizing the raw data together with their secondary data strictly by file name in a well structured automatically generated file tree structure. This allows access to all data without a database-specific tools and facilitates working/screening/analyzing of the data with any tool of choice.

The structure of the file system used by the fsdb is defined in the .scripts.config file, which is dynamically generated in the fsdb's core scripts' directory. A more detailed description of this file can be found in the dedicated documentation [below](#scriptsconfig).



# Installation of the fsdb

We are offering two methods for the installation of the fsdb. Both are guiding you through the installation and give you the opportunity to decide, which part of the installtion you want to run - or not. 

## Automatic install

The easiest for a stright-forward (de-novo) installation of the fsdb is to clone the repository [fsdb-install](https://gitlab.com/tefor/fsdb/fsdb-install/) and run the install-fsdb.sh
```
git clone https://gitlab.com/tefor/fsdb/fsdb-install/-/tree/main
cd ./fsdb-install
sudo bash install-fsdb.sh
```

## Manual install

For a manual installation please download the `initializeFsdb.sh` from the [*install* directory](https://gitlab.com/tefor/fsdb/fsdb-core/-/tree/main/install) of the [fsdb-core](https://gitlab.com/tefor/fsdb/fsdb-core/) module and run the necessary scripts in a terminal using sudo.
```
sudo bash [path to your download directory]/initializeFsdb.sh
```
This will install all necessary Unix tools, download the rest of the fsdb and guide you through the process of installing and configuring your fsdb instance.   

For an update or repair of a pre-existing installation of the fsdb you can run the script `installFsdb.sh` from the local *install* directory. 
```
sudo bash [path to your local installation]/install/installFsdb.sh
```
This will update the scripts of fsdb (from its [gitlab repo](https://gitlab.com/tefor/fsdb)) and guide you through the updating process.   

While the fsdb is designed to run in the background (non-interactive) on a Linux server it can - with some limitation - also be run in the 'Windows Subsystem for Linux' (wsl2). However, this use-case was very little tested on our and therefore is not recommended.

# Installation of individual modules
The fsdb has a modular structure which allows to install only the wanted functionalities. 
Absolutely necessary are:
- [fsdb-install](https://gitlab.com/tefor/fsdb/fsdb-install), which is organizing the installation of the fsdb.
- [fsdb-core](https://gitlab.com/tefor/fsdb/fsdb-core), which is providing the scafolding of all fsdb functionalities.
- [fsdb-janitor](https://gitlab.com/tefor/fsdb/fsdb-janitor), which is keeping the body of data within the fsdb up-to-date.
- [fsdb-sdg](https://gitlab.com/tefor/fsdb/fsdb-sdg), which generates lightweight representations of the raw data (secData) to facilitate browsing and screening.

Optionally can be installed:
- [fsdb-archiver](https://gitlab.com/tefor/fsdb/fsdb-archiver), which is managing the compression and export of data into a cold (offline) archive.
- [fsdb-registration](https://gitlab.com/tefor/fsdb/fsdb-registration), which is implementing selected functionalities of [ANTs](https://stnava.github.io/ANTs/) into the fsdb.

# Preparation of the image acquisition systems (IAS)

The image acquisition systems (IAS), serviced by the fsdb need to make the storage location of the images for the fsdb accessible to the fsdb-server. As most IAS run windows as operating system please refer to the microsoft article [File sharing over a network in Windows](https://support.microsoft.com/en-us/windows/file-sharing-over-a-network-in-windows-b58704b2-f53a-4b82-7bc1-80f9994725bf#ID0EBD&ID0EBD) for the details. For security reasons we suggest to share access to this directory exclusivly with an account you create for this task on the IAS (e.g., datarobot).    
The following information of the IAS will be needed during the setup of the fsdb to facilitate the automatic file transfer:
- IP address of the IAS
- (shared) name of the shared directory
- name of the account used to access above shared directory
- password of above acount

## File sharing for the fsdb 

On your IAS 
- create a new account to use for the file sharing. 
  - Ensure, that the account name does not contain white-spaces.
- make a note of the password of the new account.

For the root-directory of the storage partition of your IAS
- follow the [online documentation](https://support.microsoft.com/en-us/windows/file-sharing-over-a-network-in-windows-b58704b2-f53a-4b82-7bc1-80f9994725bf#ID0EBD&ID0EBD)on how to created shared directories.
- share the root-directory of the storage partition of your IAS with the newly created account.
  - grant the new account read/write permissions, so it can also clean-up the storage of the microscope.
  
For reasons of hard disk space management we suggest to structure the storage partition of your IAS as follows
IAS (computer)
- storage (partition or hard drive) <- make this a shared directory
  - user1 (*)
  - user2 (*)
  - user3 (*)
  - ...
  
(*) the names of these directories need to be listed under USER in the configuration of the fsdb (see below).
(**) 


# Disclaimer
The projects of this group are under active development and therefore is provided “AS IS”, without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages or other liability, whether in an action of contract, tort or otherwise, arising from, out of or in connection with the software or the use or other dealings in the software.