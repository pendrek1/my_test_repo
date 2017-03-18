# IPK Project 1

## NAME
ftrest - client program
ftrestd - server program

## SYNOPSIS
ftrest COMMAND REMOTE-PATH \[LOCAL-PATH\]
ftrestd \[-r ROOT-FOLDER\] \[-p PORT\]

## DESCRIPTION
While server program **ftrestd** is running, client **ftrest** can execute
a **COMMAND** (meaning it can send request and server executes).

**COMMAND**
    Accepted values are get, put, rem, lst, mkd, rmd

**get**
    Get file from server specified by **REMOTE-PATH**. Save the file
    to current working directory or as **LOCAL-PATH** if set.

**put**
    Put file specified by **LOCAL-PATH** on server to **REMOTE-PATH**.
    **LOCAL-PATH** is not optional with put!

**rem**
    Remove file on server specified by **REMOTE-PATH**.
    **LOCAL-PATH** is not used with rem.

**lst**
    Get list of content of folder on server secified by **REMOTE-PATH**.
    **LOCAL-PATH** is not used with lst.

**mkd**
    Make new directory on server specified by **REMOTE-PATH**.
    **LOCAL-PATH** is not used with lst.

**rmd**
    Make new directory on server specified by **REMOTE-PATH**.
    **LOCAL-PATH** is not used with lst.

**REMOTE-PATH**
Must have exact form: *http://hostname:port/user/path*
Must contin all mentioned parts!
Only port is optional. Default port number is 6677.

**LOCAL-PATH**
    Normal absolute or relative path to a file.

## OPTIONS
Following options can be used only for server program **ftrestd**.

**-r ROOT-FOLDER**
    Set root folder for server. Root folder must contain user folders.
    If not set, current working directory is default.

**-p PORT**
    Set number of port on which server will be listening.
    If not set, port number 6677 is default.

## ERRORS
If happens some error, which is fata and program cannot continue, program 
write error message and terminate. If program can run on, write just warning
and continue.

#### Server errors
Server errors happen mostly right after turning server program on.
If there is some fail in connection with client or in client data,
sever only send error response to client, write warning and wait
for new connection.

#### Client errors
There can be errors or warnings, that came from client itself
(bad arguments, bad path, connection fail...)
Also there can be errors received from server.
Errors from server can be following:

**Not a directory**
    **REMOTE-PATH** should refer to a directory but refering to some other
    type of object.
    Commands: **lst**, **rmd**, **mkd** (parent not a dir), **put** (parent not a dir)

**Directory not found**
    Directory with **REMOTE-PATH** was not found.
    Commands: **lst**, **rmd**, **mkd** (parent not found), **put** (parent not found)

**Directory not empty**
    Directory with **REMOTE-PATH** is not empty. Contains some objects.
    Commands: **rmd**

**Already exists**
    **REMOTE-PATH** refers to existing object, so that cannot be created.
    Commands: **put**, **mkd**

**Not a file**
    **REMOTE-PATH** should refer to a file but refering to some other
    type of object.
    Commands: **del**, **get**.

**File not found**
    File with **REMOTE-PATH** was not found.
    Commands: **del**, **get**.

**User account not found**
    User specified by **REMOTE-PATH** does not exist on server.
    Commands: *all*

**Unknown error**
    Other causes of error caught by server.
    Commands: *all*

## AUTOR
Written by Antonin Vlach

## COPYRIGTH
Writen as a project at Faculty of Information Technologies of Brno
University of technology. Written in 2017 in my second year of bachelor
studies.
    
## SEE ALSO
[Task](https://wis.fit.vutbr.cz/FIT/st/course-sl.php?id=610264&item=62126) of the project.
IPK - computer comunications and networks. Course's [synopsis]()
