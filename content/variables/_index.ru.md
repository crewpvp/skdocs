+++
title = "Переменные"
archetype = "default"
url = "variables"
weight = 4
+++

## Переменные
<gray>Где, как и зачем хранить данные?</gray>

<hundred-empty-line></hundred-empty-line>

Переменные есть практически во всех языках программирования (индентификаторы), они необходимы чтобы запоминать какую-либо информацию, в основном она хранится только в оперативной памяти, но в Skript'е можно хранить их и на диске (учитывайте, что любая переменная - занимает память, и хранить что-то долгосрочное, допустим данные игроков, там - не стоит), проблема же оперативной памяти в том, что после выключения сервера - данные просто пропадут.
<fifty-empty-line></fifty-empty-line>
Перейдем к сути. Skript - слабо типизированный язык, то есть при объявлении переменной, нам не нужно указывать ее тип (число это, или текст, или еще что-либо)
<fifty-empty-line></fifty-empty-line>
Синтакс переменной: **<gray>{название}</gray>**
<fifty-empty-line></fifty-empty-line>
Области видимости переменной:

> -- Глобальная, с сохранением на диск\
> -- Глобальная без сохранения на диск (только в оперативной памяти)\
> -- Локальная (только в оперативной памяти) 

Чтобы объяснить интерпретатору, какую именно переменную мы создаем, нужно в начале названия дописать определенный символ:

-- Для локальной переменной используется символ **\"<gray><font style = "font-size: 2rem">_</font></gray>\"** (нижнее подчеркивание), например {\_var}

-- Для глобальной переменной, с сохранением на диск -- никаких символов не используется

-- Для глобальной переменной, без сохранения на диск, нам необходимо исправить конфиг плагина Skript по директории **/plugins/Skript/config.sk**
<fifty-empty-line></fifty-empty-line>
это:

```
default:
    type: CSV
    pattern: .*
    file: ./plugins/Skript/variables.csv
    backup interval: 2 hours
```
исправить на это:
```
default:
    type: CSV
    pattern: (?!-).*
    file: ./plugins/Skript/variables.csv
    backup interval: 2 hours
```

После этого исправления -- переменная не будет сохранятся на диск, если в начале ее названия есть символ \"<gray>**-**</gray>\", например **{-var}**
<fifty-empty-line></fifty-empty-line>
Теперь разъясним какие отличия у глобальных и локальных переменных:
<fifty-empty-line></fifty-empty-line>
Глобальные можно изменять и получать их значение в любом блоке кода, даже если он в другом файле.
<fifty-empty-line></fifty-empty-line>
Локальные же можно изменять и получать их значения только в том событии, в котором они используются, причем после окончания выполнения кода в событии они будут автоматически удалены, поэтому в основном, там где не нужно взаимодействие разных событий используются именно они.
В Skript есть большое количество типов данных связанных с игровыми аспектами minecraft, их описание можно найти на странице типов в документации: <font style = "font-size: 2rem">**Я ТАК ПОНИМАЮ ЗДЕСЬ НУЖНА ССЫЛКА НА https://docs.skriptlang.org/expressions.html**</font>
<fifty-empty-line></fifty-empty-line>

### Использование переменных
В этой части мы будем работать только с базовыми типами, которые есть во многих языках - текст, число и булевый тип (содержащий в себе только true или false)
<fifty-empty-line></fifty-empty-line>
Переменная считается не объявленной до тех пор, пока мы не присвоим ей какое-то значение.\
Как присвоить значение? Для этого используется выражение: **set <gray>%objects%</gray> to <gray>%objects%</gray>**\
В дословном переводе получится что-то вроде этого: **установить <gray>%что-то%</gray> на <gray>%что-то%</gray>** 
### Локальные переменные и текстовый тип данных

Основываясь на прошлом уроке, попробуем поместить текст 'Hello World!' во внутрь какой-нибудь переменной: **set <gray>{\_var}</gray> to <gray>\"Hello World!\"</gray>**\
Данной строкой мы поместили в локальную переменную <gray>{\_var}</gray> текст <gray>Hello World!</gray>
<fifty-empty-line></fifty-empty-line>
Теперь в выражении вывода мы можем заменить наш текст, на переменную:
```
on load:
  set {_var} to "Hello World!"
  broadcast {_var}
```
Перезагрузим скрипт и увидим, что результат аналогичный, что и с кодом до этого. 
<fifty-empty-line></fifty-empty-line>
Кроме этого вам скорее всего хотелось бы узнать, как можно соединить две переменные в тексте, или преобразовать переменную с любым типом в текст:
<fifty-empty-line></fifty-empty-line>
Для того нам необходимо вписать переменную в двойные кавычки и заключить эту переменную между %, вот так "%{\_var}%"\
Причем внутри кавычек мы можем использовать любое количество переменных. 
<fifty-empty-line></fifty-empty-line>
Изменим наш прошлый код на этот:
```
on load:
  set {_var} to "Hello World!"
  broadcast "%{_var}%, %{_var}%"
```
Перезагрузив скрипт, мы должны увидеть в чате <gray>\'Hello World!, Hello World!\'</gray> (если всё выполнено верно)
<fifty-empty-line></fifty-empty-line>
Можно удалять переменные при помощи выражения: **delete <gray>%objects%</gray>**, где аргумент это идентификатор.
<fifty-empty-line></fifty-empty-line>
Приготовьтесь к взрыву мозга: для названия переменной можно использовать значение другой переменной:
```
on load:
  set {_var} to "var2"
  set {_%{_var}%} to "Hello World!"
  broadcast "%{_%{_var}%}%, %{_var2}%"
```
Пояснение кода написанного выше:\
Создается переменная с текстом **\'var2\'**, после чего - создается переменная, в название которой мы помещаем текстовое значение из переменной **{\_var}** и задаем ей значение \'Hello World!\', затем выводим значение **{\_var2}** в чат (в обоих вариантах будет одно и то же)

### Глобальные переменные

Теперь поговорим насчет глобальных переменных. Для демонстрации их в действии нам необходимо второе событие. Возьмем **\'on break\'**, это событие которое вызывается, когда игрок ломает блок.
```
on load:
  set {-var} to "Hello World!"
on break:
  broadcast "%{-var}%"
```
Так как глобальные работают во всех блоках кода -- в данном коде, при загрузке, создается глобальная переменная **{-var}**, с текстом \'Hello World!\', и при разрушении блока игроком **{-var}** выведется в чат.
<fifty-empty-line></fifty-empty-line>

### Числовой тип данных
Вернемся к типам данных: числа в отличии от текста, пишутся без кавычек, например: **set {\_var} to 2** 
<fifty-empty-line></fifty-empty-line>
Кроме того, чтобы задать значение числа в переменную, мы можем использовать математические операции **сложение, вычитание, умножение, деление**, а так же другие числовые переменные
<fifty-empty-line></fifty-empty-line>
Для примера попробуем рассчитать квадрат числа 64 и выведем его в чат:
```
on load:
  set {_var} to 64*64
  broadcast "%{_var}%"
```
Если все верно, в чат будет выведено число 4096

{{% notice style="info" title="Важное про использование выражений" %}}
На самом деле внутри **% %** в кавычках мы можем использовать выражения, математические операции и так далее
```
on load:
  set {_var} to 64
  broadcast "%{_var}*{_var}%"
```
Тоже выведет нам число 4096, но в переменной {\_var} все еще будет 64, но на выводе мы перемножаем ее саму на себя. 
{{% /notice %}}
Интерпретатор не запрещает нам использовать математические операции с другими типами данных, просто на выходе мы можем получить сомнительный результат, который может не удовлетворять нашим требованиям. 
<fifty-empty-line></fifty-empty-line>
Математические операции поддерживают выражения для более удобной работы:\
**`add %number% to %number%` и `remove %number% from %number%`**
<fifty-empty-line></fifty-empty-line>
Где первое: добавляет ко второму аргументу - первый аргумент, причем второй аргумент - обязательно переменная, а первый может быть литералом (числом) и переменной (идентификатором).\
Второе: делает тоже самое, но вместо увеличения - уменьшает
<fifty-empty-line></fifty-empty-line>
Даже если переменная не задана, но было использовано выражение **add**, добавляемое число прибавится к нулю и значение запишется в переменную
```
on load:
  add 64 to {_var}
  broadcast "%{_var}*{_var}%"
```
Результатом будет всё то же число: 4096

### Булев тип данных
Булев тип занимает минимальное количество оперативной памяти, ведь сам он по себе содержит по сути true (1, истина) или false (0, ложь), и используется в основном для проверки чего-либо.
<fifty-empty-line></fifty-empty-line>
Теперь создадим переменную данного типа: **set {_var} to true** или **set {_var} to false**

{{% notice style="note" title="Глоссарий" %}}
> Компилятор -- это программа, которая переводит текст, написанный на языке программирования, в набор машинных кодов (то есть в язык, который понимает компьютер)

> Интерпретатор -- программа, выполняющая интерпретацию. Интерпретация — построчный анализ, обработка и выполнение исходного кода программы или запроса.

> Литерал -- прямой текст, число

> Идентификатор -- компонент языка, выражение, переменная

> Аргумент -- в данном контексте -- какие-то данные поступающие в функцию, выражение
{{% /notice %}}
