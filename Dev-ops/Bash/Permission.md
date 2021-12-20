# Permisstion

## List files with permissions 

To list all file/directory with full information:

```sh
ls -l
```

The result will have the following format:

```txt
drwxrwx--x join join ............ 
^ ^  ^  ^   ^    ^
| |  |  |   |    The group
| |  |  |   The owner 
| |  | Permission of every other users
| |  Permission of group of the file
|Permission of owner of the file
The type, can be file(-), directory (d) or link (l), etc
```

## Permission explains

| | File | Directory |
|-|---| --- |
|Read (r)| User can read file's content | User can see what inside the directory |
|Write (w)| User can modify the file| User can delete, rename, create files, directory inside the directory|
|Execute (x)| User can execute the file | Are you allow to enter the directory? </br> Eg: If you want to access a file inside /usr/bin, you must have execute permission on /,/user and /user/bin|
