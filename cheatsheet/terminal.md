# Terminal Command Cheatsheet

- [INTRO TO BASH/Terminal](https://www.youtube.com/watch?v=snOP94q34V4&list=PLY6oTPmKnKbYjGEm9nLowExbgkI-epIgg&index=6&t=1083s)

## Bash Commands

| Purpose | Command |
|---------|---------|
| print working directory | `pwd` |
| show all files in current directory | `ls -la` |
| create a file | `touch filename` |
| create a folder | `mkdir foldername`|
| go into folder from current directory | `cd foldername` |
| go into parent folder from current directory | `cd ..` |
| go back to home folder | `cd ~` |
| Print Contents of File | `cat filename` |
| Remove a folder | `rm -rf foldername` |
| move a file | `mv currentfile newlocation`  |
| copy a file | `cp currentfile copylocation` |
| Kill a Port | `sudo kill -9 $(sudo lsof -t -i:3000)` |

## Powershell Commands

| Purpose | Command |
|---------|---------|
| print working directory | `Get-Location` |
| show files in director | `dir` |
| create a file | `New-Item -Path . -Name "testfile1.txt" -ItemType "file" -Value "This is a text string."` |
| create a folder | `New-Item -Path . -Name "logfiles" -ItemType "directory"`|
| go into folder from current directory | `cd foldername` |
| go into parent folder from current directory | `cd ..` |
| Print Contents of File | `cat filename` |
| Remove a folder | `del foldername` |
| move a file | `Move-Item -Path C:\test.txt -Destination E:\Temp\tst.txt`  |
| copy a file | `Copy-Item "C:\Wabash\Logfiles\mar1604.log.txt" -Destination "C:\Presentation"` |
| Kill a Port | `netstat -ano | findstr :PORT_NUMBER` & `taskkill /PID PORT_NUMBER /F` |

<hr>

## File Paths

- ` ./` path starting from current folder
- `../` path starting from parent folder
- `~/` path starting from home folder
- `/` path starting from root folder

## Exiting Nano and VIM (terminal text editors)
- nano: `ctrl + x`
- vim: `:wq`