Прежде всего прочел статью "The TTY demystified" http://www.linusakesson.net/programming/tty/, которая немного помогла и дала какую-то общую архитектуру понятия терминала. Я ее представляю так:

```
ВВОД
|Keyboard|
--sends->
|Motherboard|
--changes some bytes in RAM->
|CPU|
--triggers interrupt->
|Kernel|
--sends keycode or scancode?->
|TTY driver| или может сначала |Keyboard driver|
--sends escape sequence?->
|Shell (bash)|
Здесь какой-то микс из понятий readline, terminfo, termcap, shopt и т.п. Не понятно кто за что отвечает.


ВЫВОД
как работает вывод мне не ясно, предположительно в случае с X-ами:
|Shell|
--chars or image->
|X server|
--...->
|GPU|
--...->
|Monitor|

КОНЕЦ
Однако вывод меня очень интересует в режиме “VGA” text-mode/virtual console/tty
```

Итого, хотелось бы понял это дело в приведенном примере выше. Вначале, на уровне концепции, затем на уровне древа процессов, затем на уровне какими командами и файлами управлять/настраивать “терминальную среду”. Например (поправьте если неправ):
- Прочесть текущие возможности терминала можно с помощью: `tput property`
- Узнать какой файл терминала используются для ввода: `tty`
- Узнать какойл файл терминала используются другими процессами: `ps l`
- Изменить параметры некого line discipline прикрепленного к устройству ввода (напр. /dev/tty2 или /dev/pts/2 в случае с Х): stty -F /dev/X property value
- Настройки readline библиотеки, которую используют многие TUI приложения, включая bash можно изменить в: `.inputrc` или в самом `.bashrc`
- Сменить параметры цвета можно: ?
- и т.д.

Так же задавал еще такой вопрос: https://unix.stackexchange.com/questions/459581/linux-vt-supports-8-colors-but-there-are-actual-16-distict-ones-why-is-so-that (возможно имеет смысл сказать об этом)
