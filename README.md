# Working-with-files-and-folders-in-R

Working with files and folders in R, In this tutorial, we are going to cover how to work with files and folders in R.

Working with the current directory, Unless you specify it otherwise, all documents can be studied and stored in the operating directory.

Therefore, the primary element you want to understand is the way to get and set up your operating directory.
1. working directory

If you want to get the working directory then use

getwd()

2. set the working directory

If you want to set the working directory then

setwd("D:/ FolderName")

Suppose if you want to create a subfolder under the current directory you can choose the paste command and can set the working directory.

setwd(paste0(getwd(), "/SubFolderName"))

If you are using RStudio then press Ctrl + Shift + H and choose the desired directory.
3. List of files

Suppose if you want to identify the list of files in a particular folder then you can choose list.files().

For example list files in a specific folder

list.files (path = "D:/RStudio/Foldername/")

You can get the files from a browsed folder also, simply use

list.files(path = choose.dir())

Checking if a file or folder exists


4. File Exists

Suppose if you want to identify the rawdata.csv file that exists in the working directory then

file.exists("rawdata.csv")

5. Directory Creation

If you want to create a new directory then dir.create() will be helpful.

Imagine if you want to check if the folder “Images” exists in the current directory, if not creates a new directory.

ifelse(!dir.exists("Images"), dir.create("Images"), "Folder exists already")

If you mention recursive=TRUE then can identify all files within the subfolders

list.files(recursive = TRUE)

file_access(), file_exists(), dir_exists(), link_exists(): Query for existence and access permissions
6. Fullname

Suppose if you want to get the full name (path and file name) of each file then use

list.files(full.name = TRUE)


7. Blank File

If you want to create a blank file then

file.create("new_text.txt")
file.create("new_word.docx")
file.create("new_csv.csv")

dir_create(), link_create(): Create files, directories, or links

You can make use of sapply and can create n number of files.

N=10

sapply(paste0("file", 1:N, ".csv"), file.create)

Working with files and folders in R
8. Change File

file_chmod(): Change file permissions

file_chown(): Change owner or group of a file
9. Move File

Most of we want to copy the files from one folder to another folder, so file.copy will be useful for this.

file.copy("D:/RStudio/source_file_tocopy.txt", "D:/RStudio/NewFolder/")

The above command will copy the file from one location to another with the same file name and if you mention the specified name accordingly will change the file name.

The list of the files within any sub-folder you want to capture then make use recursive.

dir_copy(), link_copy(): Copy files, directories or links

list.files("D:/path/to/somewhere/else", recursive = TRUE)

If the folder contains huge number of files, then will leads to time lag to execute the command.

Suppose if you want to get the fullnames then,

list.files("D:/path/to/somewhere/else", full.names = TRUE, recursive = TRUE)

10. Pattern

Imagine if you want list out only csv files then, then you can make use of pattern.

list.files(pattern = ".csv")

list all CSV files recursively through each sub-folder

list.files(pattern = ".csv", recursive = TRUE)

Suppose if you want to read all CSV files from a particular folder or current working directory.

ClubbedFile <- lapply(list.files(pattern = ".csv"), read.csv)

11. File Snapshot

You can make use of file snapshot to get a file snapshot of the current directory

snapshot <- fileSnapshot()

fileSnapshot returns a list, which here we will just call “snapshot”. The most useful piece of information can be garnered from this by referencing “info”:

So we can easily capture the following information

size indicates the size of the file

isdir indicates is file a directory? ==> TRUE or FALSE

mode indicates the file permissions in octal

mtime indicates the last modified timestamp

ctime indicates time stamp created

atime indicates time stamp last accessed

exe indicates type of executable (or “no” if not an executable)


12. File info

file.info also similar to fileSnapshot, except that it returns a single record of information corresponding to an input file.

file.info("myfile.csv")

file.ctime:- If you want to get just the created timestamp of a file, call file.ctime:

file.mtime:- Getting the last modified timestamp is similar to above, except we use file.mtime:
13. Unlink File

Obviously, if we’re dealing with lots of files then we need to delete some files then unlink or file.remove functions will be more helpful.

unlink("myfile.csv")
file.remove("myfile.csv")

Delete a directory, you need to add recursive = TRUE

unlink("some_directory", recursive = TRUE)

file_delete(), dir_delete(), link_delete(): Delete files, directories, or links
14. Basename

Getting the base name of a file can be done using the basename function:

basename("D:/path/to/file.txt")

The above code will return “file.txt”


15. Directory name

How to get the directory name of a file

dirname("D:/path/to/file.txt")

This will return “D:/path/to”
Working with files and folders in R
16. File Extension

How to get a file’s extension

library(tools)
file_ext("D:/path/to/file.txt") # returns "txt"
file_ext("C:/path/to/file.csv") # returns "csv"

17. Open File

To open, or launch, a file, use the shell.exec or file.show functions:

shell.exec("D:/path/to/file/file.txt")

file.show to launch a file

file.show("D:/path/to/file/ file.txt")

These functions will be very helpful when you generating a greater number of files and see the results.

How to open a file selection window

file.choose()

Running this command will return the name of the file selected by the user.
18. Filestrings

How to move a file

library(filesstrings)
file.move("D:/path/to/file/some_file.txt", "D:/some/other/path")

Here, the first argument is the name of the file you want to move and the second argument is the destination directory.

19. Path Manipulation

path(), path_wd(): Construct path to a file or directory

file_temp(), path_temp(): Create names for temporary files

path_expand(), path_expand_r(), path_home(), path_home_r(): Finding the User Home Directory

path_file() path_dir() path_ext() path_ext_remove() path_ext_set(): Manipulate file paths

path_file() returns the filename portion of the path,

path_dir() returns the directory portion,

path_ext() returns the last extension (if any) for a path,

path_ext_remove() removes the last extension and returns the rest of the path,

path_ext_set() replaces the extension with a new extension. If there is no existing extension the new extension is appended.

path_filter(): Filter paths

path_split: splits paths into parts.

path_join: joins parts together. The inverse of path_split(). See path() to concatenate vectorized strings into a path.

path_abs: returns a normalized, absolute version of a path.

path_norm: eliminates . references and rationalizes up-level .. references, so A/./B and A/foo/../B both become A/B, but ../B is not changed. If one of the paths is a symbolic link, this may change the meaning of the path, so consider using path_real() instead.

path_rel: computes the path relative to the start path, which can be either an absolute or relative path.

path_common: finds the common parts of two (or more) paths.

path_has_parent: determine if a path has a given parent. path_common: finds the common parts of two (or more) paths.

path_has_parent: determine if a path has a given parent.

More path related examples refer here
20. Help

is_file(), is_dir(), is_link(): Functions to test for file types
