# Как воспроизводить WAV файлы в C с помощью WinAPI
Сегодня я покажу как воспроизводить WAV в C, не буду долго тянуть

Вот код:
```
#include <windows.h>
#include <stdio.h>

int wmain(int argc, wchar_t *argv[])
{
    if (argc > 1)
    {
    PlaySoundW(argv[1],NULL,SND_SYNC | SND_LOOP | SND_FILENAME);
    return 0;
    }
    else
    {
       wprintf(L"Error: One argument expected.\n");
       wprintf(L"saund.exe <file name>\n");
       wprintf(L"You can play only .wav file\n");
       return 1;
    }
}
```
# Основная функция
Начнём с основой функции: ```int wmain(int argc, wchar_t *argv[])```
Название функции wmain здесь не просто так, всё это сделанно так потому что второй аргумент функции это "wchar_t",
а в обычной функции main аргумент должен быть типа "char", но нам нужен именно wchar_t, иначе будет предупреждение

```warning: passing argument 1 of 'PlaySoundW' from incompatible pointer type [-Wincompatible-pointer-types]```
А возникает оно из-за того что "char" это ASCII, а метод ```PlaySoundW``` использует UNICODE, если вы всё таки хотите использувать ASCII
то нужно этот метод заменить на ```PlaySoundA```. Если у вас возникли проблемы с компилированием, то попробуйте добавить аргумент ```-municode```
если вы используете MinGW.
# if (argc > 1)
Следуйщая часть программы ```if (argc > 1)``` может показатся на первый взгляд не понятной, но давайте разберёмся в этом, 
"argc" обозначает количество аргументов, и когда вы запускаете программу всегда есть один аргумент (скорее всего это сама программа), и если аргументов больше
чем 1, то должно запустится то что идёт в скобках, в другом случаи пойдёт то что в скобках в else, для того что бы этого не случилось нужно запустить программу
с аргументом, а сам аргумент это файл который будет воспроизводить программа.
# Как скомпилировать?
Я использую эту команду ```gcc saund.c -o saund.exe -municode -lwinmm```
# Где скачать?
[Скачать репозиторию](https://github.com/Svyatik-Bak/saund/archive/refs/heads/main.zip)

[Просмотреть репозиторию](https://github.com/Svyatik-Bak/saund)

[Просмотеть код в браузере](https://svyatik-bak.github.io/saund/saund.txt)
