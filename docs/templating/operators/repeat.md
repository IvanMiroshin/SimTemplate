# repeat

Цикл repeat аналогичен циклу foreach. Отличие заключается в том, что repeat выполняет перебор итерацию текущего элемента DOM, а не его содержимого.

## **Синтаксис**

```text
repeat($expression as $value [~exception clear | none]);
```

**Переменные цикла:**

`$value.item` — возвращает значение текущего элемента массива $data.expression

`$value.key` — возвращает ключ текущего элемента массива $data.expression

`$value.index` — возвращает индекс текущего элемента массива $data.expression \(от 0 до count-1\)

`$value.number` — возвращает порядковый номер элемента массива $data.expression \(от 1 до count\)

**Обработка исключений:**

Ситуация, когда цикл не может быть выполнен `$data.expression != array` может быть обработанная параметром `~exception`:

1. `clear` — удалить элемент DOM \(используется по умолчанию\)
2. `none` — оставить элемент DOM без изменений

## Примеры использования

**Пример \#1** Вывод всех пользователей из массива `$data.user`:

Входные данные:

```php
Array
(
    [users] => Array
        (
            [0] => Alex
            [1] => William
            [2] => Daniel
        )
)
```

Шаблон:

```markup
<h1>Пользователи</h1>
<ul>
     <li data-sim="repeat($data.users as $user); content($user.item);">
          Пользователь
     </li>
</ul>​
```

Результат выполнения:

```markup
<h1>Пользователи</h1>
<ul>
    <li>Alex</li>
    <li>William</li>
    <li>Daniel</li>
</ul>
```

**Пример \#2** Обход `$data.user` с указанием исключения `clear`:

Входные данные:

```php
Array
(
    [users] => 'String, not array'
)
```

Шаблон:

```markup
<h1>Пользователи</h1>
<ul>
     <li data-sim="repeat($data.users as $use ~exception clear); content($user.item);">
          Пользователь 
     </li>
</ul>​
```

Результат выполнения:

```markup
<h1>Пользователи</h1>
<ul></ul>​
```

**Пример \#3** Обход `$data.user` с указанием исключения `none`:

Входные данные:

```php
Array
(
    [users] => 'String, not array'
)
```

Шаблон:

```markup
<h1>Пользователи</h1>
<ul>
     <li data-sim="repeat($data.users as $use ~exception clear); content($user.item);">
          Пользователь 
     </li>
</ul>
```

Результат выполнения:

```markup
<h1>Пользователи</h1>
<ul>
    <li></li>
</ul>​
```

