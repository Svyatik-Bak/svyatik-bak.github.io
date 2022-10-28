# Як відтворювати WAV файли в C за допомогою WinAPI
Сьогодні я покажу як відтворювати WAV в C, не довго тягтиму

Ось код:
````
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
````
# Основна функція
Почнемо з основою функції: ```int wmain(int argc, wchar_t *argv[])```
Назва функції wmain тут не просто так, все це зроблено так, тому що другий аргумент функції це "wchar_t",
а у звичайній функції main аргумент має бути типу "char", але нам потрібен саме wchar_t, інакше буде попередження

```warning: passing argument 1 of 'PlaySoundW' from incompatible pointer type [-Wincompatible-pointer-types]```
А виникає воно через те, що "char" це ASCII, а метод "PlaySoundW" використовує UNICODE, якщо ви все-таки хочете використовувати ASCII
то потрібно цей метод замінити на "PlaySoundA". Якщо у вас виникли проблеми з компілюванням, то спробуйте додати аргумент ```-municode```
якщо ви використовуєте MinGW.
# if (argc > 1)
Наступна частина програми ```if (argc > 1)``` може здатися на перший погляд не зрозумілою, але давайте розберемося в цьому,
"argc" означає кількість аргументів, і коли ви запускаєте програму завжди є один аргумент (скоріше за все це сама програма), і якщо аргументів більше
чим 1, то має запуститися те, що йде в дужках, в іншому випадку піде те, що в дужках в else, для того щоб цього не сталося потрібно запустити програму
з аргументом, а сам аргумент це файл, який буде відтворювати програму.
# Як скомпілювати?
Я використовую цю команду ```gcc saund.c -o saund.exe -municode -lwinmm```
# Де завантажити?
[Завантажити репозиторію](https://github.com/Svyatik-Bak/saund/archive/refs/heads/main.zip)

[Переглянути репозиторію](https://github.com/Svyatik-Bak/saund)

[Подивитися код у браузері](https://svyatik-bak.github.io/saund/saund.txt)
