# Lec 02

Linux Commands:

1. ssh: secure shell&#x20;
2. pwd: print working directory (folder)&#x20;
3. Is: list all the file in the directory. (-l long listing) (ls -lh human readable) (a flag - list all files, hidden file as well).
4. touch: creates a empty file. # touch example.txt&#x20;
5. nano/vim/emacs: editor.&#x20;
6. apt: install app  # apt install emacs-nox
7. wget: download file to vm. (# wget url)
8. mv - move. can use to rename # mv oldname newname.&#x20;
9. cp - copy. copy files.&#x20;
10. scp: - copy between vm and local. # scp user@ip:\~/source destination or switch dest and source
11. cat: read in the content and output it. (print content)
12. head/tail: - show the first 10 lines of file/show the last 10 lines of the file. (head -n lines - show number of line. tail -f - f means follow. &#x20;
13. mkdir: make directory. (# mkdir data)
14. man: shows the manual of a command (# man ls) (# use / to search)&#x20;
15. cd: change directory. (. is this direcotry) (.. - parent directory)&#x20;
16. sudo/su: root. use as root user. /su - siwtch user, su root (default = root).  (you can do sudo su - switch to root).&#x20;
17. chmod: # chmod WHO+WHAT  chmod o+r secret.txt (-r) took away read
18. python3: run python ptrogram.
19. which: - where is python3(or other) installed on computer.
20. echo: print things.
21. \|: pipe - connect output of one process to input of the next.
22. \>: redirection. A > output.txt - redirect of stdout to output.txt
23. \>>: append to file if exists (not replace like >)
24. &>: standard error, and stdout both redirection.
25. wc: world count - how many world typed (ctrld to exit out) line, world,character
26. grep: - search # grep worldtosearch  #-v inverse search case insensitive grep -i madison.
27. find: find looks at directory. dump everything in a directory.&#x20;
28. &: Async. runs in background and get output immediagtely
29. ps: ps - list processes. # flags: ps a (all user on vm) ps ax (everything, not just shell).&#x20;
30. kill: kill process. # kill PID . (can find pid using grep).  (flg - kill -9 ( most strong), level 1-9).&#x20;
31. pkill: #pkill Name - process name. Kill a program. e.g pkill python3
32. htop: show process running, resources (CPU, memory)
33. df: storage and capacity.  #df - h human readable.  #df -h . 25G disk.&#x20;
34. du: information about how much space in different places. #du -hs summary. -hs ./\*&#x20;
35. Isof:  # list open "files" . (use for networks)  #sudo lsof -i tcp (tcp) -P ( port number)

Notes:

Shell - program with a loop, ask from prompt and run command.

ssh: secure shell

ctrl r - reverse search.&#x20;

use sudo apt update before install.

ctrl+c kills a process

in ls -l . the first is - if the file is a file, if it is a d, then it is a directory.

The first colomn tells who owns the file. Second tells the group who own the file. 3 levels.

3 groups of 3 letters. rwx. # rwx = read write execute

Can use Pathlib (library) with reproducible path

First line  on file - tells which program to use, how to execute.

(p1 - which bash) #! - top line

PATH variable. in bash, environment variable start with $. #$PATH.&#x20;



## Lec 03

pipe operate on stdin and stdout.&#x20;

To connect two program, A | B. stdout of A -> stdin of B.

![](<../../.gitbook/assets/image (1).png>)

stderr -> for things like warning that shouldn't be chained. (straight to screen) (stack trace go to stderr).&#x20;



Redirection: Process to file.  A >output.txt. (can redirect from stdout or stderr)&#x20;
