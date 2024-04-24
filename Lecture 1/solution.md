# Lecture 1 The Shell


1. For this course, you need to be using a Unix shell like Bash or ZSH. If you are on Linux or macOS, you don’t have to do anything special. If you are on Windows, you need to make sure you are not running cmd.exe or PowerShell; you can use Windows Subsystem for Linux or a Linux virtual machine to use Unix-style command-line tools. To make sure you’re running an appropriate shell, you can try the command echo $SHELL. If it says something like /bin/bash or /usr/bin/zsh, that means you’re running the right program.

    ```shell
    cd Lecture\ 1 
    echo $SHELL
    ```

2. Create a new directory called missing under /tmp.

    ```shell
    mkdir tmp
    cd tmp
    mkdir missing
    ```

3. Look up the touch program. The man program is your friend.

    ```shell
    man touch
    ```

4. Use touch to create a new file called semester in missing.

    ```shell
    cd missing
    touch semester
    ```

5. Write the following into that file, one line at a time:

    ```shell
    #!/bin/sh
    curl --head --silent https://missing.csail.mit.edu
    ```

    The first line might be tricky to get working. It’s helpful to know that # starts a comment in Bash, and ! has a special meaning even within double-quoted (") strings. Bash treats single-quoted strings (') differently: they will do the trick in this case. See the Bash quoting manual page for more information.

6. Try to execute the file, i.e. type the path to the script (./semester) into your shell and press enter. Understand why it doesn’t work by consulting the output of ls (hint: look at the permission bits of the file).

    ```shell
    ./semester
    ls -l
    -rw-r--r--  1 XdpCs  staff  0 Apr 24 22:29 semester
    ```

    semester does not have execute permission.

7. Run the command by explicitly starting the sh interpreter, and giving it the file semester as the first argument, i.e. sh semester. Why does this work, while ./semester didn’t?

    ```shell
    sh ./semester
    ```

    sh is a POSIX-compliant command interpreter. It reads and interprets commands from the file within the current shell without needing the file to have execute permission.

8. Look up the chmod program (e.g. use man chmod).

    ```shell
    man chmod
    ```

9. Use chmod to make it possible to run the command ./semester rather than having to type sh semester. How does your shell know that the file is supposed to be interpreted using sh? See this page on the shebang line for more information.

    ```shell
    chmod u+x
    ./semester
    ```

10. Use | and > to write the “last modified” date output by semester into a file called last-modified.txt in your home directory.

    ```shell
    date -r semester | cat > last-modified.txt
    ```

    The echo command does not read from standard input, so we just use the cat command.

11. Write a command that reads out your laptop battery’s power level or your desktop machine’s CPU temperature from /sys. Note: if you’re a macOS user, your OS doesn’t have sysfs, so you can skip this exercise.

    I'm  a macOS user.
