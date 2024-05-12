###Данная страница предназначена для документации





###Состав команды:
Воробьева К.Н.: разработка абстрактного синтаксического дерева и парсера
Чирикова П.С.: разработка интерпретатора
Шукайло Е.А.: написание примеров программ и документации





В нашем языке мы реализовали такие функции как:

* Именованные переменные (`let`)
* Рекурсия
* Ленивое вычисление
* Функции
* Замыкания




## Функциональные особенности нашего языка:

Именованные переменные: Мы внедрили возможность именования переменных для более удобной работы с данными.

Рекурсия: Реализована возможность рекурсивных вызовов функций, что позволяет функциям вызывать сами себя для решения задач.

Ленивые вычисления: Добавлена поддержка ленивых вычислений, оптимизирующих производительность путем вычисления значений только по мере необходимости.

Функции и замыкания: Функции стали неотъемлемой частью языка, позволяя абстрагировать повторяющиеся операции, а замыкания придают гибкость, позволяя функциям запоминать и манипулировать окружением, в котором они были созданы.

## Основные возможности:

Загрузка кода программы из файла и интерактивный интерпретатор REPL: Добавлена возможность загрузки кода из файлов и интерактивного взаимодействия с интерпретатором, облегчая процесс разработки и отладки.

## Математические выражения:

Математические операции: Поддерживаются основные математические операции: сложение, вычитание, умножение и деление. Операции всегда окружаются круглыми скобками, аргументы обрабатываются соответствующим образом в зависимости от количества переданных значений.

#### Примеры

``` 
  (+ 1 2) # 3

  (- 7) # -6
  
  (/ 2) # 0.5
  
  (* 1 2 3 4 5) # 120
```

### Булевые выражения

Поддерживаемые булевые операции - `&, |` - аналоги `and` и `or` соответственно. Они работают по тому же принципу, что и математические операции. Если аргументов один, возвращается значение этого аргумента. Булевые константы `true` и `false` записываются в коде программы с маленькой буквы без кавычек.

#### Примеры

``` 
  (& true 0) # false

  (| false (< 1 2)) # true
```

### Строковые литералы
Строковые литералы объявляются как последовательность символов, заключенных в двойные кавычки. Если строка не заключена в кавычки, она будет распознана как название переменной или функции.

#### Пример
```
  ("string") # вернётся строка string
```

### Операторы отношения

Поддерживаются операторы - `>, <, =`. Они являются бинарными и принимают на вход не более двух аргументов, возвращая булевое значение. Операции сравнения могут выполняться как между строками, так и между числами. 

#### Примеры

``` 
  (< 1.0 2.0) # true

  (> 2.7 4.2) # false
  
  (= "a" "b") # false
```

### Именованные переменные

Именованные переменные создаются с помощью синтаксиса `(let id Expr)`. Значение Expr будет вычислено только при необходимости, то есть в операциях, возвращающих значение. Здесь id - строка без кавычек.

#### Примеры

``` 
  (let id 1) # переменная id будет иметь значение 1
  
  (let id2 (+ 1 2)) # переменная id2 будет иметь значение OP(+, [1,2]), которое будет вычислено, например, в выражении (+ id2 1)
```

### Условные выражения

Условные выражения создаются с помощью синтаксиса `(if Expr then Expr else Expr)`, где ветвь `else` может быть опущена. При вызове будет оценено значение `cond` (булевое или приводимое к булевому значению), стоящее после `if`. Значения ветвей не оцениваются сразу.

#### Пример

``` 
  (if true then 1 else 2) # 1.0
```

### Функции

Функции создаются с помощью синтаксиса `(makefun function_name { arg1 arg2 } Expr )`. У функции может не быть аргументов. Аргументы функции и `function_name` - строки без кавычек. При вызове функции происходит проверка количества аргументов и их сопоставление - первый переданный сопоставляется с именем первого аргумента функции и так далее. За счёт замыканий любая функция может стать рекурсивной.

#### Примеры

``` 
  (let id 1)
  
  (makefun id_1 {arg_1 arg_2 } ( + arg_1 arg_2 id )) # функция с именем id_1 создана. Она содержит словарь уже объявленных переменных, в котором есть переменная id
  
  (id_1 1 2) # 4
  
  ((makefun id_1 {a} (if (> a 1) then ((print a) (id_1 (- a 1))) else \"function ended\")) (id_1 5)) # рекурсивная функция, которая выводит значения от 5 до 2, а потом завершается строкой "function ended"

```

### Комментарии 

`#` - строчный комментарий - содержимое до конца строки игнорируется.

`@...@` - комментарий от символа до символа - содержимое между символами игнорируется, включая переносы строк. 

#### Примеры

``` 
  (+ 1 @ 1 2 3 @ 4) # 5
  
  (if true then 1) # комментарий к строке
```

### Функция печати 

Для вывода переменных можно использовать функцию `print`. Возможные типы значений для вывода - численный, строковый и булевой (вычисленные значения).

#### Примеры

``` 
  (print 1) # выведет 1
  
  ((let id 1) (print id)) # выведет также 1
```
