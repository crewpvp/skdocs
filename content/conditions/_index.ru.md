+++
title = "Условные операторы"
archetype = "default"
url = "conditions"
weight = 5
+++

## Условные операторы
<gray>Даже у Нео был выбор</gray>

<hundred-empty-line></hundred-empty-line>

Имея сплошной код далеко не уедешь, иногда нужен выбор, при каких случаях свернуть в тот, или иной блок кода. Как раз в этом нам помогут условия. 
<fifty-empty-line></fifty-empty-line>
Синтакс условий в Skript выглядит следующим образом:
```
if %objects% %условный оператор% %objects%:
  #ваш код
```
Первый и третий аргумент (%objects%) - это то, что мы собираемся сравнивать, а %условным оператором% выступает критерий по которому мы сравниваем. 
<fifty-empty-line></fifty-empty-line>
Под условным оператором подразумеваются знаки, используемые в математических неравенствах, такие как: <, >, =
<fifty-empty-line></fifty-empty-line>
Скрипт позволяет использовать текст вместо символов, и если быть каноничным - лучше использовать именно текст: 
```
> - is greater than 
< - is less than 
= - is 
>= - is greater than or equal to 
<= - is less than or equal to
```
Это не весь возможный список используемых действий
Условие конечно же сработает если критерий внутри него будет удовлетворен, приведем примеры верных и не верных условий (не с точки зрения написания кода):
```
on load:
  if 1 is 1:
    broadcast "1 is 1"
    #будет выведено '1 is 1'
  if 2 is 1:
    broadcast "2 is 1"
    #условие не сработает, так как оно ложное
  if 2 is greater than 1:
    broadcast "2 > 1"
    #будет выведено '2 > 1'
```
Очевидно, что помимо литералов, в условии могут быть использованы идентификаторы:
```
on load:
  set {_var} to 1
  if {_var} is greater than or equal to 1:
    broadcast "%{_var}% is greater than or equal to 1"
    # будет выведено '1 is greater than or equal to 1'
```
Конструкцию описанную выше, можно расширить с помощью else: что означает 'иначе',
```
if %objects% %логический оператор% %objects%:
  #ваш код
else:
  #ваш код
Блок кода после else будет выполнен в том случае, если условие не верно, например:
on load:
  if 2 is 1:
    broadcast "2 is 1"
    #условие не сработает, так как оно ложное
  else:
    broadcast "2 is not 1"
    #но сработает блок else
```
Кроме этого, есть так же аналог конструкции swith case из других языков:
```
on load:
  if 2 is 1:
    broadcast "2 is 1"
    #условие не сработает, так как оно ложное
  else if 2 is 2:
    broadcast "2 is 2"
    #будет выведено '2 is 2'
```
Конструкция else if что-то вроде проверить еще что-то, если условие выше не верно, причем длина конструкции такого вида не имеет предела, можно бесконечно делать проверки:
```
on load: 
 set {_var} to 3
 if {_var} is 1:
    broadcast "2 is 1"
    #условие не сработает, так как оно ложное
  else if {_var} is 2:
    broadcast "%{_var}% is 2"
    #условие не сработает, так как оно ложное
  else if {_var} is 3:
    broadcast "%{_var}% is 3"
    #будет выведено '3 is 3'
  #else if ...
  else:
    broadcast "%{_var}% is undefined"
    #сработает только в том случае, если все, что выше не сработало
```
Но проверка будет завершена раньше, если какое-то из условий истинно.
Второй аргумент в условии можно сделать с отрицанием:
```
on load: 
  set {_var} to 3
  if {_var} is not 1:
    broadcast "%{_var}% is not 1"
    #будет выведено '3 is not 1'
```
В переводе это что-то типа 'если {\_var} не является 1, то выполнить: ...' Также, помимо not, можно дополнить условие другими булевыми операциями: and и or, что значит и и или соответственно:
```
on load:
  set {_var} to 3
    if {_var} is (2 or 3):
      broadcast "%{_var}% is 2 or 3"
      #будет выведено, так как 3 это 2 или 3, что удовлетворяет условию
on load:
  set {_var1} to 2
  set {_var2} to 3
  if ({_var1} and {_var2}) is (2 and 3):
    broadcast "%{_var1}% and %{_var2}% is 2 and 3"
    #будет выведено, так как список из {_var1} и {_var2} это 2 и 3, что удовлетворяет условию
```
Помимо базовых операторов сравнения, в языке присутствуют и другие, список всегда доступен по ссылке: https://docs.skriptlang.org/conditions.html 

Мы разберем лишь одно из них: contains, потому что оно ускорят работу со списками и текстом: 

Синтакс: 

Без отрицания:
```
if %inventories/texts/objects% contain[(s)] %item types/texts/objects%:
  #ваш код
```

С отрицанием:
```
if %inventories/texts/objects% (doesn't|does not|do not|don't) contain %item types/texts/objects%:
  #ваш код
```
Это может быть использовано при проверке текстовой переменной на содержание определенной последовательности символов:
```
on load:
  set {_var} to "Hello World!"
  if {_var} contains "Hello":
    broadcast "yes"
    #сработает, так как изначальный текст содержит в себе 'Hello'
Может быть использовано при работе со списком переменных:
on load:
  set {_var1} to 1
  set {_var2} to 5
  if {_var1},{_var2} contains 5:
    broadcast "Yes"
    #сработает, так как одна из двух переменных равняется 5
```
Не забывайте про производительность, большое количество сложных проверок -- ресурсо-затратная операция, процессоры на архитектурах х86 их х64 способны выполнять лишь 1 операцию за такт, то есть если в вашем условии стоит or или and, то это уже как минимум две операции.

При использовании конструкции else if, если вы можете представить в голове поток входящих данных и способны составить процентное соотношение вероятности выпадения каждого варианта, ставьте наиболее частые варианты раньше чем редкие, это сэкономит количество проверок при выполнении кода. 

Проверки булевых типов данных быстрее чем числовых, а числовых быстрее чем текстовых. 

Условие contains при проверке списка переменных, проверит каждую из входящих переменных, то есть совершит перебор, не забывайте это.


Считаю на этом ваше базовое понимание как устроены условия уже сложилось.