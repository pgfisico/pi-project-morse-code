# Converting to Morse Code

## Background

Morse code is a method to transmit text as a series of on and off signals. Each character has a specific morse code signal, made up of dots and dashes. A space does not have a signal, it is represented by a defined period of time when no signals are transmitted. Dots and dashes correspond to different on times, with the dot representing on for a short amount of time and the dash representing on for a long amount of time.

For this project, we will use International Morse Code, as defined by the [International Telecommunication Union Recommendation M.1677-1](https://www.itu.int/dms_pubrec/itu-r/rec/m/R-REC-M.1677-1-200910-I!!PDF-E.pdf). The recommendation lists the mapping of characters to international morse code signals.

To make it easier for you to decode morse code, print out this diagram.

![](/assets/Dichotomic Morse Code.png)

When you are receiving morse code, start with your finger at the top of the tree on the circle labelled "Start". When you receive a dot, move your finger to the left along the dotted line to the next circle. When you receive a dash, move your finger to the right along the dashed line to the next circle. Once the signal is finished, the character your finger is on is the character you received. For example, if you receive a dot and then a dash, you would move your finger from start to "E" when you hear the dot, and then from "E" to "A" when you hear the dash. Your finger has stopped on the letter "A", which has the morse code signal "-.".

Note that the most commonly used characters in English intentionally have shorter morse code signals. You can see this visually in the diagram - the characters with shorter signals are higher in the tree.

## Mapping Characters to Signals

To map characters to signals, copy and paste the following dictionary at the top of your file. In Python, a dictionary allows the programmer to associate keys to values. In the `CHARACTER_TO_MORSE_CODE` dictionary below, the keys are the characters and the values are the morse code signals. For example, the line `'a': '.-',` maps the key `a` to the value `.-`. This dictionary is based on international morse code, and you will use it to convert the message to morse code signals in the next step.

```py
CHARACTER_TO_MORSE_CODE = {
    'a': '.-',
    'b': '-...',
    'c': '-.-.',
    'd': '-..',
    'e': '.',
    'f': '..-.',
    'g': '--.',
    'h': '....',
    'i': '..',
    'j': '.---',
    'k': '-.-',
    'l': '.-..',
    'm': '--',
    'n': '-.',
    'o': '---',
    'p': '.--.',
    'q': '--.-',
    'r': '.-.',
    's': '...',
    't': '-',
    'u': '..-',
    'v': '...-',
    'w': '.--',
    'x': '-..-',
    'y': '-.--',
    'z': '--..',
    '1': '.----',
    '2': '..---',
    '3': '...--',
    '4': '....-',
    '5': '.....',
    '6': '-....',
    '7': '--...',
    '8': '---..',
    '9': '----.',
    '0': '-----',
    '.': '.-.-.-',
    ',': '--..--',
    ':': '---...',
    '?': '..--..',
    "'": '.----.',
    '-': '-....-',
    '/': '-..-.',
    '(': '-.--.',
    ')': '-.--.-',
    '"': '.-..-.',
    '=': '-...-',
    '+': '.-.-.',
    '@': '.--.-.'
}
```

Above the `output_morse_code` function and below the `CHARACTER_TO_MORSE_CODE` dictionary, copy the incomplete `output_morse_code_signal` function. It requires a single argument named `signal`. This function will take the signal as an argument and output the signal on the LED and buzzer. It will not return anything.

```py
def output_morse_code_signal(signal):
    # Code to output morse code signal to the LED and buzzer goes here
```

For testing purposes, implement the `output_morse_code_signal` function so that it prints out the signal for now.

You now need to update the `output_morse_code` function to get the signal. You may have noticed that the `CHARACTER_TO_MORSE_CODE` dictionary only has entries for lowercase letters. Morse code makes no distinction between uppercase and lowercase letters, so the signal is the same for `A` and `a`. Since the user may input a message that has a mix of uppercase and lowercase letters, you need to change all the letters to lowercase so that they can be found in the dictionary. To change a string to lowercase, use the `lower` function. This function can be called on a string variable named `var`, by writing `var.lower()`. Below is the Python documentation for the `lower` function.

> `str.lower()`  
> Return a copy of the string with all the cased characters converted to lowercase.
>
> The lowercasing algorithm used is described in section 3.13 of the Unicode Standard.

Once you have a lowercase version of the message, remove the printing code from the `output_morse_code` function and replace it with the following incomplete loop. This loop goes through every character in the lowercase message, and will be used to convert the characters into morse code signals. Note that it assumes that the lowercase version of the message is stored in a variable named `lowercase_message`. Make sure to change it if you have used a different variable.

```py
for character in lowercase_message:
    # Code to convert characters in a message into morse code signals goes here
```

Complete the loop so that for each `character`, the program does the following.
* If `character` is a space, print "SPACE"
* Otherwise, get the signal from the dictionary
  * If the signal is not in the dictionary, print an error message that includes the character whose signal was not found
  * Otherwise, call the `output_morse_code_signal` function with the signal for the character

To get a signal from the `CHARACTER_TO_MORSE_CODE` dictionary, use the following dictionary function.

```py
CHARACTER_TO_MORSE_CODE.get(character)
```

The `get` function will return the signal if the character was found in the dictionary, or `None` if it was not. `None` is a special value in Python which is often used to indicate the absence of a value.

In order to check if the value of a variable is `None`, use the following. You don't need to worry about what the `is` operator does in Python for now, but note that it is not the same thing as checking if values are equal.

```py
if variable is None:
    # Your code here
```

## Testing

Before going further, make sure that your message conversion code is working. Run your program and input a message. Make sure the message contains at least one uppercase letter, one space, and one character that is not in the `CHARACTER_TO_MORSE_CODE` dictionary so that you test all possible cases in your code. Check that the printed signals are correct using the morse code tree or the ITU recommendation from above.

If the program doesn't do what you expect it to, there may be a problem in your code. Identify and fix any problems, then run your program again to check if the problem has been fixed.