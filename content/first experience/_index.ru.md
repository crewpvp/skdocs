+++
title = "Проба пера"
archetype = "default"
url = "tryfirst"
weight = 3
+++

## Проба пера
<gray>Не под ребро</gray>

<hundred-empty-line></hundred-empty-line>

После того как вы установили плагин на свой сервер, внутри папки /plugins/ будет создана папка /Skript/. В ней находятся ваши собственные скрипты, сохраненные переменные и настройки самого плагина. Сейчас нас не совсем интересуют настройки и переменные, хранящиеся в таблице .csv, поэтому попробуем перейти сразу к написанию чего-либо (а зачем медлить?)

### Шаг №1
<fifty-empty-line></fifty-empty-line>
Выберем текстовый редактор.
<fifty-empty-line></fifty-empty-line>
Чтобы начать создавать код своими умелыми ручками нам необходим текстовый редактор.
<fifty-empty-line></fifty-empty-line>
Если у вас уже есть любимый - используйте его (Microsoft Word не подойдёт), но если нет - возьмите любой из списка ниже:

{{% big-link url="https://www.sublimetext.com/" icon="fa-solid fa-link" %}}**Sublimetext <gray>(windows, linux, mac)</gray>**{{% /big-link %}}

{{% big-link url="https://code.visualstudio.com/" icon="fa-solid fa-link" %}}**Visualstudio <gray>(windows, linux, mac)</gray>**{{% /big-link %}}

{{% big-link url="https://notepad-plus-plus.org/downloads/" icon="fa-solid fa-link" %}}**Notepad++ <gray>(windows)</gray>**{{% /big-link %}}

### Шаг №2
<fifty-empty-line></fifty-empty-line>
Создадим файл, где мы будем воплощать IT-художества.
<fifty-empty-line></fifty-empty-line>
Заходим в директорию **/plugins/Skript/scripts/**, создаем внутри файл (название не важно, но постарайтесь использовать только латиницу и цифры) с расширением **.sk** - Например **myfirstscript.sk** 
<fifty-empty-line></fifty-empty-line>
Теперь откройте файл в текстовом редакторе.

### Шаг №3
<fifty-empty-line></fifty-empty-line>
Перейдём к воплощению IT-художеств.
<fifty-empty-line></fifty-empty-line>
Skript -- это событийно-ориентированный язык, то есть, чтобы что-то выполнилось, должно произойти какое-то событие. Под событием имеется ввиду действие пользователя или самого сервера, так вот начало нашего блока кода должно начинаться с необходимого нам события.
<fifty-empty-line></fifty-empty-line>
Структура блока кода в Skript:
```
%название события или описание функции%:
  <- #Обязательный отступ после ':', из-за него интерпретатор 
     #понимает внутри какого блока мы работаем
  ваш код...
```
Отступом может быть 2 пробела, 4 пробела или 1 нажатие клавиши TAB. В одном файле не могут быть использованы разные виды отступов. Выберите тот, который удобен именно вам.
<fifty-empty-line></fifty-empty-line>
Отступы используются не только при объявлении функций или использования события, но вам пока что об этом знать рано, поймете в процессе чтения данной документации
<fifty-empty-line></fifty-empty-line>
В данном примере мы возьмем простое и понятное событие '**on load**', которое происходит при загрузке файла скрипта, в котором  находится данное событие. 

```
on load:
  здесь будет наш код...
```

Теперь мы можем добавить выражение для вывода текста для всех, это выражение **broadcast**\
Синтакс этого выражения: <gray>**broadcast %objects% [(to|in) %worlds%]**</gray>
<fifty-empty-line></fifty-empty-line>
Немного разберем как в документации пишется синтакс:

> Все что заключено в проценты <gray>**% %**</gray> обозначает тип данных который может использоваться в выражении (в нашем случае это тип Object, что обозначает абсолютно любой тип данных

> Внутри <gray>**% %**</gray> так же может присутствовать символ /, он используется для перечисления определенных типов внутри выражения, которые могут быть к нему применены

> Все что заключено в квадратные скобки <gray>**[ ]**</gray> означает, что это не обязательная часть выражения, она может быть, а может не быть (на усмотрение разработчика) (в нашем случае, можно дополнительно указать в каких мирах конкретно нужно выводить сообщение)

> Скобки <gray>**( )**</gray> используются для изменения приоритета (объединения в один блок), словно в математике, сначала будет считываться то, что внутри, а только потом все, что вне

> Знак <gray>**|**</gray> означает ИЛИ (в нашем случае "(<gray>to</gray>|<gray>in</gray>)" в скобки взяты два слова <gray>to</gray> и <gray>in</gray>, между ними |, следовательно при написании можно использовать как broadcast %objects% in %worlds% или broadcast %objects% to %worlds%, оба варианта будут рабочими в коде)

Теперь мы можем попробовать вывести какой-то текст на сервере:

```
on load:
  broadcast "Hello World!"
```

{{% notice style="info" title="Важное про служебные символы" %}}
Текст в языке Skript пишется внутри двойных кавычек ("text"), кроме этого если в тексте надо будет написать служебный символ, например кавычки, их придется удвоить\
(\"Пример: \"\" \"\" \", означает текст Пример: \" \")
{{% /notice %}}

Так же, в Skript, можно писать комментарии - те участки кода, которые будут пропускаться при запуске файла скрипта. Обычно их используют для пояснений, что делает та или иная часть программы, для заметок и другого. Комментарий обозначается решеткой в начале строки \'#\'
<fifty-empty-line></fifty-empty-line>
Например:
```
#Код ниже передает привет миру при запуске этого скрипта
on load:
  broadcast "Hello World!"
```

### Шаг №4
Теперь изучим основные команды плагина Skript.
<fifty-empty-line></fifty-empty-line>
Главная команда: **/skript** или просто **/sk**
<fifty-empty-line></fifty-empty-line>
Подкоманды:
<fifty-empty-line></fifty-empty-line>
**/skript reload <gray>(</gray><green>путь до скрипта</green><gray>|</gray><green>config</green><gray>|</gray><green>all</green><gray>)</gray>** -- перезагружает определенный файл, конфиг или все сразу 
<fifty-empty-line></fifty-empty-line>
**/skript enable <gray>(</gray><green>путь до скрипта</green><gray>|</gray><green>all</green><gray>)</gray>** -- включает определенный скрипт или все сразу 
<fifty-empty-line></fifty-empty-line>
**/skript disable <gray>(</gray><green>путь до скрипта</green><gray>|</gray><green>all</green><gray>)</gray>** -- отключает определенный скрипт или все сразу 
<fifty-empty-line></fifty-empty-line>
**/skript info** -- выводит информацию о плагине и текущих установленных дополнениях 
<fifty-empty-line></fifty-empty-line>
**/skript update** -- проверяет наличие новых версий плагина 
<fifty-empty-line></fifty-empty-line>
**/skript help** -- пишет то, что было описано выше 

{{% notice style="info" title="Важное про выключение скриптов" %}}
Скрипт не будет загруждаться, если первый символ его названия '-', такой скрипт считается выключенным, причем если он уже был загружен в память, переименование скрипта не выключит его, нужно будет написать команду **/sk disable НазваниеСкрипта** 
{{% /notice %}}

Кроме этого вы можете включать и выключать целые директории со скриптами. Например у нас есть есть некая папка **/main/**, в которой находятся файлы скрипта, мы можем быстро включить, выключить или перезагрузить их просто указав директорию: **/sk reload main/**

### Шаг №5

Теперь перезагрузим созданный нами файл: **/sk reload НазваниеСкрипта**\
<fifty-empty-line></fifty-empty-line>
<font style = "font-size: 1.6rem"> Если вы выполнили все шаги верно -- в чат напишется 'Hello World!' </font>

{{% notice style="note" title="Глоссарий" %}}
> Переменные -- зарезервированная область памяти в которых хранится какая-либо информация

> Событийно-ориентированное программирование -- парадигма программирования, в которой выполнение программы определяется событиями - действиями пользователя, сообщениями других программ и потоков, событиями операционной системы.

> IT (Information Technology) -- информационные технологии
{{% /notice %}}