---
title: Поля
description: Поля используются для генерации вывода шаблона формы заполнения и редактирования
extends: _layouts.documentation.ru
section: main
---

Поля используются для генерации вывода шаблона формы заполнения и редактирования


> Не стесняйтесь добавлять свои поля, например, для использования удобного редактора для вас или любых компонентов.
 
 
## Input


![Input](https://orchid.software/assets/img/ui/input.png)

Является одним из разносторонних элементов формы и позволяет создавать разные части интерфейса и обеспечивать взаимодействие с пользователем. Главным образом предназначен для создания текстовых полей.
 
Пример записи:
```php
Input::make()
    ->type('text')
    ->name('place')
    ->max(255)
    ->required()
    ->title('Name Articles')
    ->help('Article title');
``` 
 

> Заметьте многие параметры такие как `max`,`required`,`title`,`help`,`vertical`,`horizontal`; и многие другие, доступны почти каждым `полям` системы и являются не обязательными
 
 
 
## Wysiwyg


![Wysing](https://orchid.software/assets/img/ui/wysing.png)

Визуальный редактор в котором содержание отображается в процессе редактирования и 
выглядит максимально близко похожим на конечный результат.
Редактор позволяет вставлять рисунки, таблицы, указывать стили оформления текста, видео.
 
Пример записи:
```php
TinyMCE::make()
    ->name('body')
    ->required()
    ->title('Name Articles')
    ->help('Article title')
    ->theme('inlite');
``` 
Для отображения в редакторе верхней панели и меню, в котором доступны функции полноэкранного режима и просмотр html кода, нужно установить атрибут `theme('modern')`.
 
## Markdown

![Markdown](https://orchid.software/assets/img/ui/markdown.png)
![Markdown2](https://orchid.software/assets/img/ui/markdown2.png)

Редактор для облегчённого языка разметки,
 созданный с целью написания максимально читаемого и удобного для правки текста,
  но пригодного для преобразования в языки для продвинутых публикаций
 
Пример записи:
```php
SimpleMDE::make()
    ->name('body')
    ->title('О чём вы хотите рассказать?')
```  
 
## Picture
 
Позволяет загружать изображение и обрезать до нужного формата 


Пример записи:
```php
Picture::make()
    ->name('picture')
    ->width(500)
    ->height(300);
```  
           
       
## Datetime
 
![Datatime](https://orchid.software/assets/img/ui/datatime.png) 
 
Позволяет выбрать дату и время


Пример записи:
```php
DateTimer::make('open')
    ->title('Opening date');
```           

Разрешить прямой ввод:

```php
DateTimer::make('open')
    ->title('Opening date')
    ->allowInput();
```           

Формат данных:

```php
DateTimer::make('open')
    ->title('Opening date')
    ->format('Y-m-d');
```

Пример, для отображения в 24-ом формате:

```php
DateTimer::make('open')
    ->title('Opening date')
    ->format24hr();
```

Календарь со временем:

```php
DateTimer::make('open')
    ->title('Opening time')
    ->enableTime();
```

Выбор только времени:

```php
DateTimer::make('open')
    ->title('Opening time')
    ->noCalendar()
    ->format('h:i K');
```

           
## Checkbox
 
Элемент графического пользовательского интерфейса, позволяющий пользователю управлять параметром с двумя состояниями — ☑ включено и ☐ выключено.


Пример записи:
```php
CheckBox::make()
    ->name('free')
    ->value(1)
    ->title('Free')
    ->placeholder('Event for free')
    ->help('Event for free');
```           

## Code
 
Поле для записи программного кода с возможностью подсветки

![Code](https://orchid.software/assets/img/ui/code.png)


Пример записи:
```php
Code::make()
    ->name('block')
    ->title('Code Block')
    ->help('Simple web editor');
```    



## Textarea
 
Поле `textarea` представляет собой элемент формы для создания области, в которую можно вводить несколько строк текста. 
В отличие от тега `input` в текстовом поле допустимо делать переносы строк сохраняются при отправке данных на сервер.

Пример записи:
```php
TextArea::make()
    ->name('description')
    ->max(255)
    ->rows(5)
    ->required()
    ->title('Short description');
```    


## Select

Простой выбор из списка массива:

```php
Select::make()
    ->options([
        'index'   => 'Index',
        'noindex' => 'No index',
    ])
    ->name('select')
    ->title('Select tags')
    ->help('Allow search bots to index');
```

Работа с источником:

```php
Select::make('user')
    ->fromModel(User::class, 'email')
```

Источник с условием:
```php
Select::make('user')
    ->fromQuery(User::where('balance', '!=', '0'), 'email'),
```

Изменение ключа:
```php
Select::make('user')
    ->fromModel(User::class, 'email', 'uuid')
```

Возможны ситуации когда необходимо добавить некоторое значение которое означает, что поле не выбрано, 
для этого можно использовать метод `empty`:

```php
// Для массива
Select::make('user')
    ->options([
        1  => 'Пункт 1',
        2  => 'Пункт 2',
    ])
   ->empty('Не выбрано');

// Для источника
Select::make('user')
    ->fromModel(User::class, 'name')
    ->empty('Не выбрано');
```

> **Обратите внимание**, что `empty` вызывается позднее заполняющих методов, иначе добавленое значение будет перезаписано

Метод `empty` так же принимает и второй аргумент отвечающий за значение:

```php
Select::make('user')
    ->options([
        1  => 'Пункт 1',
        2  => 'Пункт 2',
    ])
   ->empty('Не выбрано', 0);
```


## Mask
 
Маска для ввода значений к тегу input. 
Отлично подходит если значения должны быть записаны в стандартном виде, например ИНН или номер телефона

Пример записи:
```php
Input::make()
    ->type('text')
    ->name('phone')
    ->mask('(999) 999-9999')
    ->title('Phone')
    ->help('Number Phone');
```   

В маску можно передавать json с параметрами, например:


```php
Input::make()
    ->type('text')
    ->name('price')
    ->mask([
     'mask' => '999 999 999.99',
     'numericInput' => true
    ])
    ->title('Стоимость');
```   

```php
Input::make()
    ->type('text')
    ->name('price')
    ->mask([
        'alias' => 'currency',
        'prefix' => ' ',
        'groupSeparator' => ' ',
        'digitsOptional' => true,
    ])
    ->title('Стоимость');
```   

Все доступные параметры *Inputmask* можно посмотреть [здесь](https://github.com/RobinHerbots/Inputmask#options)


## Отношения

Поля отношения могут подгружать динамические данные, это хорошее решение, если вам нужны связи.

```php
Relation::make('idea')
    ->fromModel(Idea::class, 'name')
    ->title('Выберите свою идею'),
```

Для модификации загрузки можно использовать указание на `scope` модели,
например, взять только активные:

```php
namespace App;

use Illuminate\Database\Eloquent\Model;

class Idea extends Model
{

    /**
     * @param Builder $query
     *
     * @return Builder
     */
    public function scopeActive(Builder $query)
    {
        return $query->where('active', true);
    }
}
```

```php
Relation::make('idea')
    ->fromModel(Idea::class, 'name')
    ->applyScope('active')
    ->title('Выберите свою идею'),
```


## Кнопка/Ссылка

В определенных случаях необходимо добавить кнопку для вызова модального окна, простую ссылку или добавить кнопку 
отправки формы в конце экрана. 
Для таких случаев существует поле `Button`. Поле `Button` не может иметь какого либо 
значения и не передается при сохранении. Оно может быть использовано для вызова модального окна определенного на экране
и для добавления простой ссылки в форме.

Пример использования с модальным окном `addNewPayment` добавленного ранее на экран: 

```php
Button::make()
    ->title('Add Payment')
    ->modal('addNewPayment')
    ->icon('icon-wallet')
    ->right()
```

Пример использования с ссылкой:

```php
Button::make()
    ->title('Google It!')
    ->type(Button::LINK)
    ->link('http://google.com');
```

Пример использования с методом:

```php
Button::make()
    ->title('Google It!')
    ->method('goToGoogle');
```

Доступные модификаторы:

* `modal('modalName')` - создает кнопку вызывающую модальное окно с именем `modalName` в рамках текущего экрана
* `right()` - Позиционирования элемента по правому краю экрана
* `block()` - Позиционирование элемента по всей ширине экрана
* `class('class-names')` - переписывает стандартные классы для кнопки
* `link('url')` - добавляет ссылку для кнопки. Игнорируется при заданном modal
* `method('methodName')` - при клике форма будет отправлена на заданный метод в рамках текущего экрана
* `title('Click Me!')` - задает название текущей кнопки
* `icon('icon-wallet)` - задает иконку для кнопки
 


## Модификация

Можно определить модификацию значения или других параметров с помощью магического метода `modify` добавив к этому
атрибут который необходимо переопределить:

```php
Input::make()
    ->type('text')
    ->name('name')
    ->modifyValue(function ($value) {
        return strtoupper($value);
    })
```

Это позволяет создавать «вычисленные поля».

