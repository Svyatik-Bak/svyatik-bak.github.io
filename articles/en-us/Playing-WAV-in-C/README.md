# How to play WAV files in C using WinAPI
Today I will show you how to play WAV in C, I won't delay.

Here is the code:
```
#include <windows.h>
#include <stdio.h>

int wmain(int argc, wchar_t *argv[])
{
    if (args > 1)
    {
    PlaySoundW(argv[1],NULL,SND_SYNC | SND_LOOP | SND_FILENAME);
    return 0;
    }
    else
    {
       wprintf(L"Error: One argument expected.\n");
       wprintf(L"saund.exe <filename>\n");
       wprintf(L"You can only play .wav file\n");
       return 1;
    }
}
```
# Main function
Let's start with the main function: ```int wmain(int argc, wchar_t *argv[])```
The name of the wmain function is not just there, it's all done so because the second argument to the function is "wchar_t",
and in the regular main function, the argument must be of type "char", but we need exactly wchar_t, otherwise there will be a warning

```warning: passing argument 1 of 'PlaySoundW' from incompatible pointer type [-Wincompatible-pointer-types]```
And it occurs because "char" is ASCII, and the ```PlaySoundW``` method uses UNICODE, if you still want to use ASCII
then you need to replace this method with ```PlaySoundA```. If you're having trouble compiling, try adding the ```-municode``` argument
if you are using MinGW.
# if (args > 1)
The next part of the program ```if (argc > 1)``` may not seem clear at first glance, but let's understand it,
"argc" stands for the number of arguments, and when you run the program there is always one argument (probably the program itself), and if there are more arguments
than 1, then what goes in brackets should start, in other cases what goes in brackets in else, in order for this not to happen, you need to run the program
with an argument, and the argument itself is the file that the program will play.
# How to compile?
I use this command ```gcc saund.c -o saund.exe -municode -lwinmm```
# Where can I download?
[Download repository](https://github.com/Svyatik-Bak/saund/archive/refs/heads/main.zip)

[View repository](https://github.com/Svyatik-Bak/saund)

[View code in browser](https://svyatik-bak.github.io/saund/saund.txt)
