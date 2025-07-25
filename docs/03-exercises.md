



# Running Programs

:::{.notice}

Following is based on the “SciServer Essentials 2.0” image described in Ch 2. Setup Compute

:::

## Learning objectives

- Run a UNIX command

- Wrap a command in a Bash script with `#!`

- Make a Bash script executable


## Run a command

- Start a terminal

![](03-exercises_files/figure-docx//1Covg_bpPYGKnTVbOjX_FkGgWHBG6VwdEySKbpZNwqKo_g36ef0094ecf_0_0.png){width=100%}

- Run the `ls -l` command to list files (the `-l` is a command line argument that instructs the `ls` program to modify its operation so that longer details are provided about each file)

![](03-exercises_files/figure-docx//1Covg_bpPYGKnTVbOjX_FkGgWHBG6VwdEySKbpZNwqKo_g36ef0094ecf_0_8.png){width=100%}

- Run `echo "Hello, World!"` to print text to the terminal

![](03-exercises_files/figure-docx//1Covg_bpPYGKnTVbOjX_FkGgWHBG6VwdEySKbpZNwqKo_g36ef0094ecf_1_0.png){width=100%}

## Wrap a command in a Bash

- Create Text File

![](03-exercises_files/figure-docx//1Covg_bpPYGKnTVbOjX_FkGgWHBG6VwdEySKbpZNwqKo_g36ef0094ecf_0_29.png){width=100%}

- Write your first Bash script

![](03-exercises_files/figure-docx//1Covg_bpPYGKnTVbOjX_FkGgWHBG6VwdEySKbpZNwqKo_g36ef0094ecf_0_40.png){width=100%}


- Run `00-hello.sh`

![](03-exercises_files/figure-docx//1Covg_bpPYGKnTVbOjX_FkGgWHBG6VwdEySKbpZNwqKo_g36ef0094ecf_0_45.png){width=100%}


Congratulations! You have just:

- Created a Bash script that prints "Hello, World!" to the terminal


# Hello, World!

## Learning objectives

- Understand how to run Python scripts from the command line

## Hello, World! example

- Follow the steps from the ***SciServer*** lesson
    
    - Login to SciServer and start a new jupyter notebook

    - Start a new terminal session
    

- Create a new file named `01-helloworld.py` using the text editor and write the following code:

    ```python
    #!/usr/bin/env python3
    print("Hello, World!")
    ```

- Save the file and make it executable:

    ```bash
    chmod +x 01-helloworld.py
    ```

- In the terminal, run the script by typing:

    ```bash
    ./01-helloworld.py
    ```

- You should see the output:

   ```
   Hello, World!
   ```

Congratulations! You have just:

- Created a Python script that prints "Hello, World!" to the terminal

- Made the script executable

- Ran the script from the command line

# Command line arguments

## Printing All Command Line Arguments

- Let's make our Python scripts interactive by accepting input from the command line. Create a new file called `02-arguments.py` and type:

    ```python
    #!/usr/bin/env python3

    import sys

    print(sys.argv)
    ```

- Save the file and make it executable:

    ```bash
    chmod +x 02-arguments.py
    ```

- Now run it directly with some arguments:

    ```bash
    ./02-arguments.py hello world 123
    ```

    You'll see output like `['./02-arguments.py', 'hello', 'world', '123']`

The `sys` module provide access to the system-specific parameter. The variable `sys.argv` contains all command line arguments passed to your script, including the script name itself as the first element.


## Understanding Lists

Lists in Python are ordered collections of items enclosed in square brackets, like `[1, 2, 3]` or `["apple", "banana"]`. Lists can contain different types of data and are accessed by the position (index), starting from 0. For example, `my_list[0]` gets the first item, `my_list[1]` gets the second item, and so in.


## Accessing Specific Arguments

- Lets modify our script to print just the second command line argument:

    ```python
    #!/usr/bin/env python3

    import sys

    print("Script name:", sys.argv[0])
    print("First argument:", sys.argv[1])
    ```

- Run it with: `./02-arguments.py hello`

    This prints:

    ```bash
    Script name: ./02-arguments.py
    First argument: hello
    ```

    Notice how `sys.argv[0]` is always the script name, so the first actual argument is at index 1

    ***Warning***: If you don't provide enough arguments, Python will crash with an "IndexError". We'll learn to handle this with `if` statements later

## Arguments Are Strings

Command line arguments are always strings, even if they look like numbers. 

- Update `02-arguments.py`

    ```python
    #!/usr/bin/env python3

    import sys

    # This won't work as expected
    result = sys.argv[1] + sys.argv[2]
    print("Without conversion:", result)

    # Convert strings to integers first
    num1 = int(sys.argv[1])
    num2 = int(sys.argv[2])
    print("With conversion:", num1 + num2)
    ```

- Run it with: `./02-arguments.py 5 3`

    Output:

    ```bash
    Without conversion: 53
    With conversion: 8
    ```

Without conversion, Python concatenates the strings "5" and "3" into "53". The `int()` function converts string representations of numbers into actual integers that can be used in mathematical operations.

Congratulations! You have just:

- Created a Python script that accepts command line arguments

- Accessed specific arguments using `sys.argv`


# Parsing files line by line

## Create a Test File

- Let's create a simple text file called `sample.txt` using the Jupyter text editor

    The file should contain the following lines:

    ```
    apple
    banana
    cherry
    date

    ```

## File Streams in Python

A file stream is like a pipeline that lets you read data from a file one piece at a time. The most common way to open a file is using the `open()` function.

- Create a new Python script called `03-files.py`

    ```python
    #!/usr/bin/env python3

    import sys

    my_file = open( sys.argv[1] )
    print(my_file)

    ```

- Save it and make it executable

    ```bash
    chmod +x 03-files.py
    ``` 

- Run the script with the file name as an argument

    ```bash
    ./03-files.py sample.txt
    ``` 

    This will print something like

    ```bash
    <_io.TextIOWrapper name='sample1.txt' mode='r' encoding='UTF-8'>
    ```

As you can see, the `print()` function can't print the file content directly. This output just indicates the file `sample1.txt` is opened in read mode (`'r'`) with UTF-8 encoding.

## `for` loops

To read the file and print each line, we can use a `for` loop. 

- Update `03-files.py`:

    ```python
    #!/usr/bin/env python3

    import sys

    my_file = open(sys.argv[1])

    # for iterates through files
    for my_line in my_file:
        # objects have methods
        my_line = my_line.rstrip("\n")
        print( my_line )

    my_file.close()
    ```

- Save it and run the script again

    ```bash
    ./03-files.py sample1.txt
    ```

    This will print each line of the file without extra spaces or newlines

    ```bash
    apple
    banana
    cherry
    date
    ```

Congratulations! You have just:

- Created a Python script that reads a file 

- Used a `for` loop to iterate through each line in the file

- Printed each line without extra spaces or newlines


# head.py

# grep.py

# cut.py
