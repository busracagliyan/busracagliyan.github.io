---
layout: post
title:  "Command Operators"
date:   2024-08-16 15:07:16 +0300
categories: linux, command
---
Command operators used in the terminal are used to combine, direct, and execute commands under certain conditions. Here are the basic command operators and their functions:

### 1. ';' (Semicolon)

- The semicolon operator is used to execute multiple commands one after another. The commands are executed independently of each other, the next command is executed when the previous command finishes. This means that the success or failure of one command does not affect the execution of other commands.

- **Usage**
    ```bash
    comamnd1; command2; command3
    ```
        
    `command1`, `command2` and `command3` are executed in order. Each command executes independently of the previous one.

- **Example**
    ```bash
    echo "Hello, World!"; mkdir test; cd test
    ```
    
    ![image 1](/assets/post-command-operators/ss1.png)

### 2. '&' (Ampersand)

- This operator is used to run a command in the background so that other operations can be performed in the terminal.
  
- **Usage**
    ```bash
    command &
    ```
    
    `command` is run in the background.
  
- **Example**
    ```bash
    sleep 10 &
    ```
    
    ![image 2](/assets/post-command-operators/ss2.png)
      
    > The `fg` command is used to bring a background job to the foreground.

### 3. '&&' (AND)

- This operator executes the next command if the first command succeeds. If the first command fails, the next command is not executed.

- **Usage**
    ```bash
    command1 && command2
    ```
    If `command1` succeeds, `command2` is executed.
  
- **Example**
    ```bash
    pwd && ls
    ```
    ![image 3](/assets/post-command-operators/ss3.png)

### 4. '||' (OR)

- This operator executes the next command if the first command fails. If the first command succeeds, the next command is not executed.

- **Usage**
    ```bash
    command1 || command2
    ```
    If `command1` fails, `command2` is executed.
  
- **Example**
    ```bash
    pwd || ls
    ```
    ![image 4](/assets/post-command-operators/ss4.png)

### 5. '|' (PIPE)

- The pipe operator is used to use the output of one command as input to another command. This operator is often used to create chains of data processing.

- **Usage**
    ```bash
    command1 | command2
    ```
    The output of `command1` becomes the input of `command2`

- **Example**
    ```bash
    ls -l | grep test
    ```
    ![image 5](/assets/post-command-operators/ss5.png)

### 6. '!'

This command is used to re-run a command that was run in the past. Usage examples:

1. '**!number**'
    - Reruns a specific command number that was run in the past.

    - **Usage**
        ```bash
        !number
        ```
        
    - **Example**
        ```bash
        !12
        ```
        ![image 6.1](/assets/post-command-operators/ss6-1.png)
      
2. '**!!**'
    - Reruns the last executed command.
  
    - **Usage**
        ```bash
        !!
        ```

    - **Example**
        ```bash
        ls
        !!
        ```
        ![image 6.2](/assets/post-command-operators/ss6-2.png)

3. '**!string**'
    - Reruns the last command that started with `string`.

    - **Usage**
        ```bash
        !string
        ```
   
    - **Example**
        ```bash
        !echo
        ```
        ![image 6.3](/assets/post-command-operators/ss6-3.png)
      
4. '**!$**'
    - Reuses the last argument of the last executed command.

    - **Usage**
        ```bash
        command !$
        ```

    - **Example**
        ```bash
        echo "Hello, World!"
        vi !$
        ```
        ![image 6.4](/assets/post-command-operators/ss6-4.png)

### 7. '>', '>>', '<' (The Redirection Operators)

The Redirection Operators

1. '**>**'
    - This operator is used to redirect the output of a command to a file. If the file already exists, it overwrites the previous content.
    
    - **Usage**
        ```bash
        command > output_file
        ```
        The output of `command` is written to the file `output_file`. If the file already exists, its contents are deleted and rewritten.
    
    - **Example**
        ```bash
        echo "Hello, World!" > output_file
        ```
        ![image 7.1](/assets/post-command-operators/ss7-1.png)

2. '**>>**'
    - This operator appends the output of a command to a file. If the file does not exist, it is created; if it does, it is appended to the current content.
    
    - **Usage**
        ```bash
        command >> output_file
        ```
        The output of `command` is appended to the end of the file `output_file`.
    
    - **Example**
        ```bash
        echo "new line" >> output_file2
        echo "new line2" >> output_file2
        ```
        ![image 7.2](/assets/post-command-operators/ss7-2.png)

3. '**<**'
    - This operator is used to get the input of a command from a file.
    
    - **Usage**
        ```bash
        command < input_file
        ```
        The input of `command` is taken from the `input_file` file.
    
    - **Example**
        ```bash
        grep a < alphabet.txt
        ```
        ![image 7.3](/assets/post-command-operators/ss7-3.png)

### 8. '2>' (Redirecting Standard Error)

- This operator is used to redirect the error output of a command to a file. Unlike normal output, error messages are redirected with the `2>` operator.

- **Usage**
    ```bash
    command 2> error_file
    ```
    The error output of `command` is written to the file `error_file`
    
- **Example**
    ```bash
    ls -l output 2> /dev/null
    ```
    ![image 8](/assets/post-command-operators/ss8.png)
  
    > The `/dev/null` file is specifically used to prevent unwanted output or error messages.
