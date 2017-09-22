# Outputting to the LED

## Setup

At the top of the file, import `LED` from the GPIO module.

```py
from gpiozero import LED
```

After the `CHARACTER_TO_MORSE_CODE` dictionary, setup your LED with the pin number that you connected it to when building your circuit.

```py
led = LED(0) # Change the pin number to match your circuit
```

## Morse Code Timings

The dot and dash have different time lengths in morse code. There are also defined periods of times are used between characters and words to separate them from each other. All morse code timings are defined in terms of the length of a dot.

* A dash is equal to three dots
* The space between signals forming the same character is equal to one dot
* The space between two characters is equal to three dots
* The space between two words is equal to seven dots

Morse code however is not usually described in terms of the length of dot, but the number of words per minute. Since every word has a different number of letters and every letter has a different signal, the number of words per minute is usually in terms of a word that takes an average length of time to transmit using morse code. A commonly used word for defining the number of words per minute is "Paris". Using the word "Paris" as the reference point, you can use the following formula to convert words per minute to the length of a dot.

> `time = 1.2 / wpm`
>
> Where
>
> * `time` is the duration of a dot, in seconds
> * `wpm` is the number of words per minute

Above the `CHARACTER_TO_MORSE_CODE` dictionary, define the following timing constants that you will use to output messages in morse code.

```py
WORDS_PER_MINUTE = # Pick a value. 5 words per minute might be a good starting point
DOT_TIME_SECONDS = # Use the above information to calculate this value using WORDS_PER_MINUTE
DASH_TIME_SECONDS = # Use the above information to calculate this value using DOT_TIME_SECONDS
SIGNAL_SPACE_TIME_SECONDS = # Use the above information to calculate this value using DOT_TIME_SECONDS
CHARACTER_SPACE_TIME_SECONDS = # Use the above information to calculate this value using DOT_TIME_SECONDS
WORD_SPACE_TIME_SECONDS = # Use the above information to calculate this value using DOT_TIME_SECONDS
```

By defining the constants this way, you can change how fast your program outputs morse code by only changing the value of `WORDS_PER_MINUTE`. The formulas will take care of calculating all the other constants based on the number of words per minute.

## Outputting Morse Code

Remove the printing code from the `output_morse_code_signal` function and replace it with a loop that goes through every character in the signal. For each character, the program should do the following.

* If the character is a dot, turn the LED on for `DOT_TIME_SECONDS`, then turn it off
* If the character is a dash, turn the LED on for `DASH_TIME_SECONDS`, then turn it off
* Wait `SIGNAL_SPACE_TIME_SECONDS`

In order to wait, recall the `sleep` function from the `time` module. To use it, add the following import to the top of your file.

```py
from time import sleep
```

In the `output_morse_code` function, replace the printing of "SPACE" with code that waits `WORD_SPACE_TIME_SECONDS`. Also add code to wait `CHARACTER_SPACE_TIME_SECONDS` after the `output_morse_code` function calls the `output_morse_code_signal` function.

## Using the Program

Run your program and enter a message and see if it outputs the message in morse code as expected. If the program doesn't do what you expect it to, there may be a problem in your circuit or code. Identify and fix any problems, then run your program again to check if the problem has been fixed. Remember that you can adjust the value of `WORDS_PER_MINUTE` to speed up or slow down the morse code output.

Try getting someone else to type in a message and see if you can interpret the morse code using the morse code tree.

### Making the Timings Accurate

Depending on the way you wrote your code, it's likely that your code makes the character space time and word space time longer than they should be in some circumstances. For example, consider the program is outputting the message "SOS". Your program might do something like the following.

```
Dot
Wait SIGNAL_SPACE_TIME_SECONDS
Dot
Wait SIGNAL_SPACE_TIME_SECONDS
Dot
Wait SIGNAL_SPACE_TIME_SECONDS

Wait CHARACTER_SPACE_TIME_SECONDS

Dash
Wait SIGNAL_SPACE_TIME_SECONDS
Dash
Wait SIGNAL_SPACE_TIME_SECONDS
Dash
Wait SIGNAL_SPACE_TIME_SECONDS

Wait CHARACTER_SPACE_TIME_SECONDS

Dot
Wait SIGNAL_SPACE_TIME_SECONDS
Dot
Wait SIGNAL_SPACE_TIME_SECONDS
Dot
Wait SIGNAL_SPACE_TIME_SECONDS
```

Note that the length of the character space time is actually `SIGNAL_SPACE_TIME_SECONDS + CHARACTER_SPACE_TIME_SECONDS` in this example. A similar problem could happen with the word space time. There are several ways to fix the program so it follows the timings more precisely, some using more advanced Python knowledge and some using what you already know.

It is not required that you fix the program, however consider trying to fix it if you would like an extra challenge once the code is working. Note that the inaccurate timings may not be perceptible to a person because the time difference is small \(Try calculating the difference for yourself\). The difference becomes even smaller as you increase the number of words per minute, and the `sleep` function may already be inaccurate with very small times.