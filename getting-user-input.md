# Getting User Input

## Setup

Create a new Python script named `morse_code.py`.

Copy the incomplete `output_morse_code` function and add it to the beginning of your file. This function will take the message as an argument and output the message on the LED and buzzer, and will not return anything.

```py
def output_morse_code(message):
    # Code to output message in morse code goes here
```

For testing purposes, implement the `output_morse_code` function so that it prints out the message for now.

## Input Loop

At the end of the file, create a loop that runs forever. Inside the loop,

* Ask the user to input a message
* Call the `output_morse_code` function with the message the user entered

## Testing

Before going further, make sure that your input code is working. Run your program and input a message. Make sure the message is printed out. Also make sure you get asked to input a message again, and that it is also printed. Stop your program when you are finished testing.

If the program doesn't do what you expect it to, there may be a problem in your code. Identify and fix any problems, then run your program again to check if the problem has been fixed.

