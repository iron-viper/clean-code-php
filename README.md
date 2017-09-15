# Чистый код на PHP

## Содержание

  1. [Введение](#Введение)
  2. [Переменные](#Переменные)
     * [Используйте значимые и произносимые имена переменных](#Используйте-значимые-и-произносимые-имена-переменных)
     * [Для одного типа переменных используйте единый словарь](#Для-одного-типа-переменных-используйте-единый-словарь)
     * [Используйте имена, по которым удобно искать (часть 1)](#Используйте-имена-по-которым-удобно-искать-часть-1)
     * [Используйте имена, по которым удобно искать (часть 2)](#Используйте-имена-по-которым-удобно-искать-часть-2)
     * [Используйте пояснительные переменные](#Используйте-пояснительные-переменные)
     * [Избегайте глубоких вложений (часть 1)](#Избегайте-глубоких-вложений-часть-1)
     * [Избегайте глубоких вложений (часть 2)](#Избегайте-глубоких-вложений-часть-2)
     * [Избегайте ментального сопоставления](#Избегайте-ментального-сопоставления)
     * [Не добавляйте ненужный контекст](#Не-добавляйте-ненужный-контекст)
     * [Вместо сокращённых или условных используйте аргументы по умолчанию](#Вместо-сокращённых-или-условных-используйте-аргументы-по-умолчанию)
  3. [Функции](#Функции)
     * [Аргументы функций (в идеале два или меньше)](#Аргументы-функций-в-идеале-два-или-меньше)
     * [Функции должны делать что-то одно](#Функции-должны-делать-что-то-одно)
     * [Имена функций должны быть говорящими](#Имена-функций-должны-быть-говорящими)
     * [Функции должны быть лишь одним уровнем абстракции](#Функции-должны-быть-лишь-одним-уровнем-абстракции)
     * [Не используйте флаги в качестве параметров функций](#Не-используйте-флаги-в-качестве-параметров-функций)
     * [Избегайте побочных эффектов](#Избегайте-побочных-эффектов)
     * [Не пишите в глобальные функции](#Не-пишите-в-глобальные-функции)
     * [Не используйте шаблон Одиночка (Singleton)](#Не-используйте-шаблон-Одиночка-singleton)
     * [Инкапсулирование условных выражений](#Инкапсулирование-условных-выражений)
     * [Избегайте негативных условных выражений](#Избегайте-негативных-условных-выражений)
     * [Избегайте условных выражений](#Избегайте-условных-выражений)
     * [Избегайте проверки типов (часть 1))](#Избегайте-проверки-типов-часть-1)
     * [Избегайте проверки типов (часть 2)](#Избегайте-проверки-типов-часть-2)
     * [Убирайте мёртвый код](#Убирайте-мёртвый-код)
  4. [Объекты и структуры данных](#Объекты-и-структуры-данных)
     * [Используйте инкапсуляцию объектов](#Используйте-инкапсуляцию-объектов)
     * [У объектов должны быть private/protected компоненты](#У-объектов-должны-быть-privateprotected-компоненты)
  5. [Классы](#Классы)
     * [Композиция лучше наследования](#Композиция-лучше-наследования)
     * [Избегать Текучий интерфейс (Fluent interface)](#Избегать-Текучий-интерфейс-fluent-interface)
  6. [SOLID](#solid)
     * [Принцип единственной ответственности (Single Responsibility Principle, SRP)](#Принцип-единственной-ответственности-single-responsibility-principle-srp)
     * [Принцип открытости/закрытости (Open/Closed Principle, OCP)](#Принцип-открытостизакрытости-openclosed-principle-ocp)
     * [Принцип подстановки Барбары Лисков (Liskov Substitution Principle, LSP)](#Принцип-подстановки-Барбары-Лисков-liskov-substitution-principle-lsp)
     * [Принцип разделения интерфейса (Interface Segregation Principle, ISP)](#Принцип-разделения-интерфейса-interface-segregation-principle-isp)
     * [Принцип инверсии зависимостей (Dependency Inversion Principle, DIP)](#Принцип-инверсии-зависимостей-dependency-inversion-principle-dip)
  7. [Не повторяйся (Don’t repeat yourself, DRY)](#Не-повторяйся-dont-repeat-yourself-dry)
  8. [Переводы](#Переводы)

## Введение

Это принципы разработки ПО, взятые из книги [*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) Роберта Мартина и адаптированные для PHP. Это руководство не по стилям программирования, а по созданию читабельного, многократно используемого и пригодного для рефакторинга кода на PHP.

Не каждый из этих принципов должен строго соблюдаться, и ещё с меньшим количеством все будут согласны. Это лишь рекомендации, не более, но все они кодифицированы в многолетнем коллективном опыте автора *Clean Code*.

Вдохновленный [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)

## Переменные

### Используйте значимые и произносимые имена переменных

**Плохо:**

```php
$ymdstr = $moment->format('y-m-d');
```

**Хорошо:**

```php
$currentDate = $moment->format('y-m-d');
```

**[⬆ вернуться к началу](#Содержание)**

### Для одного типа переменных используйте единый словарь

**Плохо:**

```php
getUserInfo();
getUserData();
getUserRecord();
getUserProfile();
```

**Хорошо:**

```php
getUser();
```

**[⬆ вернуться к началу](#Содержание)**

### Используйте имена, по которым удобно искать (часть 1)

Мы прочитаем больше кода, чем когда-либо напишем. Поэтому важно писать такой код, который будет читабелен и удобен для поиска. Но давая переменным имена, бесполезные для понимания нашей программы, мы мешаем будущим читателям. Используйте такие имена, по которым удобно искать.

**Плохо:**

```php
// What the heck is 448 for?
$result = $serializer->serialize($data, 448);
```

**Хорошо:**

```php
$json = $serializer->serialize($data, JSON_UNESCAPED_SLASHES | JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE);
```

### Используйте имена, по которым удобно искать (часть 2)

**Плохо:**

```php
// What the heck is 4 for?
if ($user->access & 4) {
    // ...
}
```

**Хорошо:**

```php
class User
{
    const ACCESS_READ = 1;
    const ACCESS_CREATE = 2;
    const ACCESS_UPDATE = 4;
    const ACCESS_DELETE = 8;
}

if ($user->access & User::ACCESS_UPDATE) {
    // do edit ...
}
```

**[⬆ вернуться к началу](#Содержание)**

### Используйте пояснительные переменные

**Плохо:**

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches[1], $matches[2]);
```

**Лучше:**

Так лучше, но мы всё ещё сильно зависим от регулярного выражения.

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/';
preg_match($cityZipCodeRegex, $address, $matches);

[, $city, $zipCode] = $matches;
saveCityZipCode($city, $zipCode);
```

**Хорошо:**

С помощью именования подпаттернов снижаем зависимость от регулярного выражения.

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,\\]+[,\\\s]+(?<city>.+?)\s*(?<zipCode>\d{5})?$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches['city'], $matches['zipCode']);
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте глубоких вложений (часть 1)

Слишком много `if/else` утверждений может сделать ваш код трудно сопровождаемым. Явное лучше, неявного.

**Плохо:**

```php
function isShopOpen($day): bool
{
    if ($day) {
        if (is_string($day)) {
            $day = strtolower($day);
            if ($day === 'friday') {
                return true;
            } elseif ($day === 'saturday') {
                return true;
            } elseif ($day === 'sunday') {
                return true;
            } else {
                return false;
            }
        } else {
            return false;
        }
    } else {
        return false;
    }
}
```

**Хорошо:**

```php
function isShopOpen(string $day): bool
{
    if (empty($day)) {
        return false;
    }

    $openingDays = [
        'friday', 'saturday', 'sunday'
    ];

    return in_array(strtolower($day), $openingDays);
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте глубоких вложений (часть 2)

**Плохо:**

```php
function fibonacci(int $n)
{
    if ($n < 50) {
        if ($n !== 0) {
            if ($n !== 1) {
                return fibonacci($n - 1) + fibonacci($n - 2);
            } else {
                return 1;
            }
        } else {
            return 0;
        }
    } else {
        return 'Not supported';
    }
}
```

**Хорошо:**

```php
function fibonacci(int $n): int
{
    if ($n === 0) {
        return 0;
    }

    if ($n === 1) {
        return 1;
    }

    if ($n > 50) {
        throw new \Exception('Not supported');
    }

    return fibonacci($n - 1) + fibonacci($n - 2);
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте ментального сопоставления

Не заставляйте тех, кто будет читать ваш код, переводить значения переменных. Лучше писать явно, чем неявно.

**Плохо:**

```php
$l = ['Austin', 'New York', 'San Francisco'];

for ($i = 0; $i < count($l); $i++) {
    $li = $l[$i];
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    // Wait, what is `$li` for again?
    dispatch($li);
}
```

**Хорошо:**

```php
$locations = ['Austin', 'New York', 'San Francisco'];

foreach ($locations as $location) {
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    dispatch($location);
}
```

**[⬆ вернуться к началу](#Содержание)**

### Не добавляйте ненужный контекст

Если имя вашего класса/объекта с чем-то у вас ассоциируется, не проецируйте эту ассоциацию на имя переменной.

**Плохо:**

```php
class Car
{
    public $carMake;
    public $carModel;
    public $carColor;

    //...
}
```

**Хорошо:**

```php
class Car
{
    public $make;
    public $model;
    public $color;

    //...
}
```

**[⬆ вернуться к началу](#Содержание)**

### Вместо сокращённых или условных используйте аргументы по умолчанию

**Не хорошо:**

Это не хорошо потому, что переменная `$breweryName` может быть `NULL`.

```php
function createMicrobrewery($breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```

**Лучше:**

Это решение мение понятно, чем предыдущая версия, но лучше контролирует значение переменной.

```php
function createMicrobrewery($name = null): void
{
    $breweryName = $name ?: 'Hipster Brew Co.';
    // ...
}
```

**Хорошо:**

Если вы используете только PHP 7+, то вы можете использовать [контроль типов](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration) и быть увереным, что переменная `$breweryName` никогда не будет `NULL`.

```php
function createMicrobrewery(string $breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```

**[⬆ вернуться к началу](#Содержание)**

## Функции

### Аргументы функций (в идеале два или меньше)

Крайне важно ограничивать количество параметров функций, потому что это упрощает тестирование. Больше трёх аргументов ведёт к "комбинаторному взрыву", когда вам нужно протестировать кучу разных случаев применительно к каждому аргументу.

Идеальный вариант — вообще без аргументов. Один-два тоже нормально, но трёх нужно избегать. Если их получается больше, то нужно объединять, чтобы уменьшить количество. Обычно если у вас больше двух аргументов, то функция делает слишком много. В тех случаях, когда это не так, чаще всего в качестве аргумента достаточно использовать более высокоуровневый объект.

**Плохо:**

```php
function createMenu(string $title, string $body, string $buttonText, bool $cancellable): void
{
    // ...
}
```

**Хорошо:**

```php
class MenuConfig
{
    public $title;
    public $body;
    public $buttonText;
    public $cancellable = false;
}

$config = new MenuConfig();
$config->title = 'Foo';
$config->body = 'Bar';
$config->buttonText = 'Baz';
$config->cancellable = true;

function createMenu(MenuConfig $config): void
{
    // ...
}
```

**[⬆ вернуться к началу](#Содержание)**

### Функции должны делать что-то одно

Это, безусловно, самое важное правило в разработке ПО. Когда функции делают больше одной вещи, их труднее составлять, тестировать и обосновывать. А если вы можете наделить функции только какими-то одиночными действиями, то их будет легче рефакторить, а ваш код станет гораздо чище. Даже если вы не будете следовать никакой другой рекомендации, кроме этой, то всё равно опередите многих других разработчиков.

**Плохо:**

```php
function emailClients(array $clients): void
{
    foreach ($clients as $client) {
        $clientRecord = $db->find($client);
        if ($clientRecord->isActive()) {
            email($client);
        }
    }
}
```

**Хорошо:**

```php
function emailClients(array $clients): void
{
    $activeClients = activeClients($clients);
    array_walk($activeClients, 'email');
}

function activeClients(array $clients): array
{
    return array_filter($clients, 'isClientActive');
}

function isClientActive(int $client): bool
{
    $clientRecord = $db->find($client);

    return $clientRecord->isActive();
}
```

**[⬆ вернуться к началу](#Содержание)**

### Имена функций должны быть говорящими

**Плохо:**

```php
class Email
{
    //...

    public function handle(): void
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// What is this? A handle for the message? Are we writing to a file now?
$message->handle();
```

**Хорошо:**

```php
class Email 
{
    //...

    public function send(): void
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// Clear and obvious
$message->send();
```

**[⬆ вернуться к началу](#Содержание)**

### Функции должны быть лишь одним уровнем абстракции

Если у вас несколько уровней абстракции, то на функцию возложено слишком много задач. Разбиение функций позволяет многократно использовать код и облегчает тестирование.

**Плохо:**

```php
function parseBetterJSAlternative(string $code): void
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            // ...
        }
    }

    $ast = [];
    foreach ($tokens as $token) {
        // lex...
    }

    foreach ($ast as $node) {
        // parse...
    }
}
```

**Тоже плохо:**

Мы выполнили некоторые функции, но функция `parseBetterJSAlternative()` все еще очень сложна и не тестируема.

```php
function tokenize(string $code): array
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            $tokens[] = /* ... */;
        }
    }

    return $tokens;
}

function lexer(array $tokens): array
{
    $ast = [];
    foreach ($tokens as $token) {
        $ast[] = /* ... */;
    }

    return $ast;
}

function parseBetterJSAlternative(string $code): void
{
    $tokens = tokenize($code);
    $ast = lexer($tokens);
    foreach ($ast as $node) {
        // parse...
    }
}
```

**Хорошо:**

Лучшим решением является вынесение всех зависимостей из функции `parseBetterJSAlternative()`.

```php
class Tokenizer
{
    public function tokenize(string $code): array
    {
        $regexes = [
            // ...
        ];

        $statements = explode(' ', $code);
        $tokens = [];
        foreach ($regexes as $regex) {
            foreach ($statements as $statement) {
                $tokens[] = /* ... */;
            }
        }

        return $tokens;
    }
}

class Lexer
{
    public function lexify(array $tokens): array
    {
        $ast = [];
        foreach ($tokens as $token) {
            $ast[] = /* ... */;
        }

        return $ast;
    }
}

class BetterJSAlternative
{
    private $tokenizer;
    private $lexer;

    public function __construct(Tokenizer $tokenizer, Lexer $lexer)
    {
        $this->tokenizer = $tokenizer;
        $this->lexer = $lexer;
    }

    public function parse(string $code): void
    {
        $tokens = $this->tokenizer->tokenize($code);
        $ast = $this->lexer->lexify($tokens);
        foreach ($ast as $node) {
            // parse...
        }
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

### Не используйте флаги в качестве параметров функций

Флаги говорят вашим пользователям, что функции делают больше одной вещи. А они должны делать что-то одно. Разделяйте свои функции, если они идут по разным ветвям кода в соответствии с булевой логикой.

**Плохо:**

```php
function createFile(string $name, bool $temp = false): void
{
    if ($temp) {
        touch('./temp/'.$name);
    } else {
        touch($name);
    }
}
```

**Хорошо:**

```php
function createFile(string $name): void
{
    touch($name);
}

function createTempFile(string $name): void
{
    touch('./temp/'.$name);
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте побочных эффектов

Функция может привносить побочные эффекты, если она не только получает значение и возвращает другое значение/значения, но и делает что-то ещё. Побочным эффектом может быть запись в файл, изменение глобальной переменной или случайная отправка всех ваших денег незнакомому человеку.

Но иногда побочные эффекты бывают нужны. Например, та же запись в файл. Лучше делать это централизованно. Не выбирайте несколько функций и классов, которые пишут в какой-то один файл, используйте для этого единый сервис. Единственный.

Главная задача — избежать распространённых ошибок вроде общего состояния для нескольких объектов без какой-либо структуры; использования изменяемых типов данных, которые могут быть чем-то перезаписаны; отсутствия централизованной обработки побочных эффектов. Если вы сможете это сделать, то будете счастливее подавляющего большинства других программистов.

**Плохо:**

```php
// Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
$name = 'Ryan McDermott';

function splitIntoFirstAndLastName(): void
{
    global $name;

    $name = explode(' ', $name);
}

splitIntoFirstAndLastName();

var_dump($name); // ['Ryan', 'McDermott'];
```

**Хорошо:**

```php
function splitIntoFirstAndLastName(string $name): array
{
    return explode(' ', $name);
}

$name = 'Ryan McDermott';
$newName = splitIntoFirstAndLastName($name);

var_dump($name); // 'Ryan McDermott';
var_dump($newName); // ['Ryan', 'McDermott'];
```

**[⬆ вернуться к началу](#Содержание)**

### Не пишите в глобальные функции

Засорение глобалами — дурная привычка в любом языке, потому что вы можете конфликтовать с другой библиотекой, а пользователи вашего API не будут об этом знать, пока не получат исключение в production. Приведу пример: вам нужен конфигурационный массив. Вы пишете глобальную функцию вроде `config()`, но она может конфликтовать с другой библиотекой, пытающейся делать то же самое.

**Плохо:**

```php
function config(): array
{
    return  [
        'foo' => 'bar',
    ]
}
```

**Хорошо:**

```php
class Configuration
{
    private $configuration = [];

    public function __construct(array $configuration)
    {
        $this->configuration = $configuration;
    }

    public function get(string $key): ?string
    {
        return isset($this->configuration[$key]) ? $this->configuration[$key] : null;
    }
}
```

Загрузите конфигурацию и создайте экземпляр класса `Configuration`.

```php
$configuration = new Configuration([
    'foo' => 'bar',
]);
```

И теперь вы должны использовать экземпляр класса `Configuration` в своем приложении.

**[⬆ вернуться к началу](#Содержание)**

### Не используйте шаблон Одиночка (Singleton)

Шаблон проектирования Одиночка (Singleton) является [антипаттерном](https://ru.wikipedia.org/wiki/Одиночка_(шаблон_проектирования)). Перефразируем Brian Button:

1. Как правило, одиночки используются в качестве **глобального экземпляра**, почему это так плохо? Потому, что вы **скрываете зависимости вашего приложения** в своем коде, вместо того, чтобы сделать их явными через интерфейсы. Сделать что-то глобальным, чтобы избежать его распространения - это [чем-то попахивает](https://ru.wikipedia.org/wiki/Код_с_запашком).
2. Одиночки нарушают принцип [единой ответственности](#Принцип-единственной-ответственности-single-responsibility-principle-srp): в силу того, что **они контролируют собственное создание и жизненный цикл**.
3. Одиночки по своей сути приводят к тому, что код получается тесно [связанным](https://ru.wikipedia.org/wiki/Зацепление (программирование)). Это во многих случаях **затрудняет его тестирование**.
4. Одиночки несут состояние на протяжении всей жизни приложения. Еще один удар по тестированию, **так как вы можете столкнуться с ситуацией, когда необходимо закончить тесты**, что является большим нет для модульных тестов. Зачем? Потому что каждый модульный тест должен быть независимым от другого.

[Misko Hevery](http://misko.hevery.com/about/) также очень хорошо разбирается в [корне проблемы](http://misko.hevery.com/2008/08/25/root-cause-of-singletons/).

**Плохо:**

```php
class DBConnection
{
    private static $instance;

    private function __construct(string $dsn)
    {
        // ...
    }

    public static function getInstance(): DBConnection
    {
        if (self::$instance === null) {
            self::$instance = new self();
        }

        return self::$instance;
    }

    // ...
}

$singleton = DBConnection::getInstance();
```

**Хорошо:**

```php
class DBConnection
{
    public function __construct(string $dsn)
    {
        // ...
    }

     // ...
}
```

Создайте экземпляр класса `DBConnection` и настройте его с помощью [DSN](http://php.net/manual/en/pdo.construct.php#refsect1-pdo.construct-parameters).

```php
$connection = new DBConnection($dsn);
```

И теперь вы должны использовать экземпляр класса `DBConnection` в своем приложении.

**[⬆ вернуться к началу](#Содержание)**

### Инкапсулирование условных выражений

**Плохо:**

```php
if ($article->state === 'published') {
    // ...
}
```

**Хорошо:**

```php
if ($article->isPublished()) {
    // ...
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте негативных условных выражений

**Плохо:**

```php
function isDOMNodeNotPresent(\DOMNode $node): bool
{
    // ...
}

if (!isDOMNodeNotPresent($node))
{
    // ...
}
```

**Хорошо:**

```php
function isDOMNodePresent(\DOMNode $node): bool
{
    // ...
}

if (isDOMNodePresent($node)) {
    // ...
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте условных выражений

Наверно, это кажется невозможным. Впервые это услышав, многие говорят: "Как я смогу что-либо сделать без выражения `if`?" Второй распространённый вопрос: "Ну, это прекрасно, но зачем мне это?" Ответ заключается в рассмотренном выше правиле чистого кода: функция должна делать что-то одно. Если у вас есть классы и функции, содержащие выражение `if`, то тем самым вы говорите своим пользователям, что функция делает больше одной вещи. Не забывайте — нужно оставить что-то одно.

**Плохо:**

```php
class Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        switch ($this->type) {
            case '777':
                return $this->getMaxAltitude() - $this->getPassengerCount();
            case 'Air Force One':
                return $this->getMaxAltitude();
            case 'Cessna':
                return $this->getMaxAltitude() - $this->getFuelExpenditure();
        }
    }
}
```

**Хорошо:**

```php
interface Airplane
{
    // ...

    public function getCruisingAltitude(): int;
}

class Boeing777 implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getPassengerCount();
    }
}

class AirForceOne implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude();
    }
}

class Cessna implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getFuelExpenditure();
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте проверки типов (часть 1)

PHP не типизирован, т. е. ваши функции могут принимать аргументы любых типов. Иногда такая свобода даже мешает и возникает соблазн выполнять проверку типов в функциях. Но есть много способов этого избежать. Первое, что нужно учитывать, это согласованные API.

**Плохо:**

```php
function travelToTexas($vehicle): void
{
    if ($vehicle instanceof Bicycle) {
        $vehicle->peddleTo(new Location('texas'));
    } elseif ($vehicle instanceof Car) {
        $vehicle->driveTo(new Location('texas'));
    }
}
```

**Хорошо:**

```php
function travelToTexas(Traveler $vehicle): void
{
    $vehicle->travelTo(new Location('texas'));
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегайте проверки типов (часть 2)

Если вы работаете с базовыми примитивами (вроде строковых, целочисленных) и массивами, то не можете использовать полиморфизм. Но если кажется, что вам всё ещё нужна проверка типов и вы используете PHP 7+, то примените [объявление типов](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration) или строгий режим (strict mode). Это даст вам статичную типизацию поверх стандартного PHP-синтаксиса. Проблема ручной проверки типов в том, что её качественное выполнение подразумевает такое многословие, что полученная искусственная "типобезопасность" не компенсирует потери читабельности кода. Сохраняйте чистоту своего PHP, пишите хорошие тесты и проводите качественные ревизии кода. Или делайте всё это, но со строгим объявлением PHP-типов или в строгом режиме.

**Плохо:**

```php
function combine($val1, $val2): int
{
    if (!is_numeric($val1) || !is_numeric($val2)) {
        throw new \Exception('Must be of type Number');
    }

    return $val1 + $val2;
}
```

**Хорошо:**

```php
function combine(int $val1, int $val2): int
{
    return $val1 + $val2;
}
```

**[⬆ вернуться к началу](#Содержание)**

### Убирайте мёртвый код

Он плох так же, как и дублирующий код. Не нужно держать его в кодовой базе. Если что-то не вызывается, избавьтесь от этого! Если что, мёртвый код можно будет достать из истории версий.

**Плохо:**

```php
function oldRequestModule(string $url): void
{
    // ...
}

function newRequestModule(string $url): void
{
    // ...
}

$request = newRequestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**Хорошо:**

```php
function requestModule(string $url): void
{
    // ...
}

$request = requestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**[⬆ вернуться к началу](#Содержание)**


## Объекты и структуры данных

### Используйте инкапсуляцию объектов

В PHP можно задать для методов ключевые слова `public`, `protected` и `private`. С их помощью вы будете управлять изменением свойств объекта.

* Если вам нужно не только получать свойство объекта, то необязательно находить и менять каждый метод чтения (accessor) в кодовой базе.
* Благодаря `set` проще добавить валидацию.
* Можно инкапсулировать внутреннее представление.
* С помощью геттеров и сеттеров легко добавлять журналирование и обработку ошибок.
* При наследовании такого класса вы можете переопределить функциональность по умолчанию.
* Вы можете лениво загружать свойства объекта, например получая их с сервера.

Также это часть принципа [Открытости/Закрытости](#Принцип-открытостизакрытости-openclosed-principle-ocp), входящего в набор объектно ориентированных принципов проектирования.

**Плохо:**

```php
class BankAccount
{
    public $balance = 1000;
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->balance -= 100;
```

**Хорошо:**

```php
class BankAccount
{
    private $balance;

    public function __construct(int $balance = 1000)
    {
      $this->balance = $balance;
    }

    public function withdrawBalance(int $amount): void
    {
        if ($amount > $this->balance) {
            throw new \Exception('Amount greater than available balance.');
        }

        $this->balance -= $amount;
    }

    public function depositBalance(int $amount): void
    {
        $this->balance += $amount;
    }

    public function getBalance(): int
    {
        return $this->balance;
    }
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->withdrawBalance($shoesPrice);

// Get balance
$balance = $bankAccount->getBalance();
```

**[⬆ вернуться к началу](#Содержание)**

### У объектов должны быть private/protected компоненты

**Плохо:**

```php
class Employee
{
    public $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }
}

$employee = new Employee('John Doe');
echo 'Employee name: '.$employee->name; // Employee name: John Doe
```

**Хорошо:**

```php
class Employee
{
    private $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    public function getName(): string
    {
        return $this->name;
    }
}

$employee = new Employee('John Doe');
echo 'Employee name: '.$employee->getName(); // Employee name: John Doe
```

**[⬆ вернуться к началу](#Содержание)**

## Классы

### Композиция лучше наследования

Как говорится в известной книге "[*Шаблоны проектирования*](https://en.wikipedia.org/wiki/Design_Patterns)" Банды четырёх, по мере возможности нужно выбирать композицию, а не наследование. Есть много хороших причин использовать как наследование, так и композицию. Главная цель этой максимы заключается в том, если вы инстинктивно склоняетесь к наследованию, то постарайтесь представить, может ли композиция лучше решить вашу задачу. В каких-то случаях это действительно более подходящий вариант.

Вы спросите: "А когда лучше выбирать наследование?" Всё зависит от конкретной задачи, но можно ориентироваться на этот список ситуаций, когда наследование предпочтительнее композиции:

1. Ваше наследование — это взаимосвязь is-a, а не has-a. Пример: Человек → Животное vs. Пользователь → Детали пользователя (UserDetails).
2. Вы можете повторно использовать код из базовых классов. (Люди могут двигаться, как животные.)
3. Вы хотите внести глобальные изменения в производные классы, изменив базовый класс. (Изменение расхода калорий у животных во время движения.)

**Плохо:**

```php
class Employee 
{
    private $name;
    private $email;

    public function __construct(string $name, string $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    // ...
}

// Bad because Employees "have" tax data. 
// EmployeeTaxData is not a type of Employee

class EmployeeTaxData extends Employee 
{
    private $ssn;
    private $salary;
    
    public function __construct(string $name, string $email, string $ssn, string $salary)
    {
        parent::__construct($name, $email);

        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}
```

**Хорошо:**

```php
class EmployeeTaxData 
{
    private $ssn;
    private $salary;

    public function __construct(string $ssn, string $salary)
    {
        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}

class Employee 
{
    private $name;
    private $email;
    private $taxData;

    public function __construct(string $name, string $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    public function setTaxData(string $ssn, string $salary)
    {
        $this->taxData = new EmployeeTaxData($ssn, $salary);
    }

    // ...
}
```

**[⬆ вернуться к началу](#Содержание)**

### Избегать Текучий интерфейс (Fluent interface)

[Текучий интерфейс (Fluent interface)](https://ru.wikipedia.org/wiki/Fluent_interface) - это объектно-ориентированный API, целью которого является улучшение читабельности исходного кода с помощью [Цепочки методов (Method chaining)](https://en.wikipedia.org/wiki/Method_chaining).

Хотя могут быть некоторые случаи в которых этот шаблон уменьшает многословность кода (например, [PHPUnit Mock Builder](https://phpunit.de/manual/current/en/test-doubles.html) или [Doctrine Query Builder](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/query-builder.html)), но чаще всего это происходит с некоторыми издержками:

1. Нарушение [Инкапсуляции](https://ru.wikipedia.org/wiki/Инкапсуляция_(программирование))
2. Нарушение [Декораторов](https://ru.wikipedia.org/wiki/Декоратор_(шаблон_проектирования))
3. Затрудняет [мокинг (mock)](https://ru.wikipedia.org/wiki/Mock-объект) в тестах
4. Осложняет чтение diff коммитов

Для получения дополнительной информации вы можете прочитать [сообщение в блоге](https://ocramius.github.io/blog/fluent-interfaces-are-evil/), написанное [Marco Pivetta](https://github.com/Ocramius).

**Плохо:**

```php
class Car
{
    private $make = 'Honda';
    private $model = 'Accord';
    private $color = 'white';

    public function setMake(string $make): self
    {
        $this->make = $make;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function setModel(string $model): self
    {
        $this->model = $model;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function setColor(string $color): self
    {
        $this->color = $color;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function dump(): void
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = (new Car())
  ->setColor('pink')
  ->setMake('Ford')
  ->setModel('F-150')
  ->dump();
```

**Хорошо:**

```php
class Car
{
    private $make = 'Honda';
    private $model = 'Accord';
    private $color = 'white';

    public function setMake(string $make): void
    {
        $this->make = $make;
    }

    public function setModel(string $model): void
    {
        $this->model = $model;
    }

    public function setColor(string $color): void
    {
        $this->color = $color;
    }

    public function dump(): void
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = new Car();
$car->setColor('pink');
$car->setMake('Ford');
$car->setModel('F-150');
$car->dump();
```

**[⬆ вернуться к началу](#Содержание)**

## SOLID

**SOLID** - это мнемонический акроним, введенный Michael Feathers для первых пяти принципов объектно-ориентированного программирования и дизайна, описанных Robert Martin.

 * [S: Принцип единственной ответственности (Single Responsibility Principle, SRP)](#Принцип-единственной-ответственности-single-responsibility-principle-srp)
 * [O: Принцип открытости/закрытости (Open/Closed Principle, OCP)](#Принцип-открытостизакрытости-openclosed-principle-ocp)
 * [L: Принцип подстановки Барбары Лисков (Liskov Substitution Principle, LSP)](#Принцип-подстановки-Барбары-Лисков-liskov-substitution-principle-lsp)
 * [I: Принцип разделения интерфейса (Interface Segregation Principle, ISP)](#Принцип-разделения-интерфейса-interface-segregation-principle-isp)
 * [D: Принцип инверсии зависимостей (Dependency Inversion Principle, DIP)](#Принцип-инверсии-зависимостей-dependency-inversion-principle-dip)

### Принцип единственной ответственности (Single Responsibility Principle, SRP)

Как говорится в книге Clean Code: "Для изменения класса никогда не должно быть более одной причины". Порой заманчиво набить класс всевозможной функциональностью, как мы это делаем с сумками и рюкзаками, которые разрешается взять в качестве ручной клади в самолёт. Проблема в том, что ваш класс не будет концептуально связанным (conceptually cohesive), и поэтому возникнет много причин изменить его. Важно минимизировать количество случаев, когда вам нужно изменять класс. А важно потому, что когда в классе избыток функциональности и вам нужно поменять её часть, то может быть трудно понять, как это отразится на зависимых модулях в кодовой базе.

**Плохо:**

```php
class UserSettings
{
    private $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }

    public function changeSettings(array $settings): void
    {
        if ($this->verifyCredentials()) {
            // ...
        }
    }

    private function verifyCredentials(): bool
    {
        // ...
    }
}
```

**Хорошо:**

```php
class UserAuth 
{
    private $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }
    
    public function verifyCredentials(): bool
    {
        // ...
    }
}

class UserSettings 
{
    private $user;
    private $auth;

    public function __construct(User $user) 
    {
        $this->user = $user;
        $this->auth = new UserAuth($user);
    }

    public function changeSettings(array $settings): void
    {
        if ($this->auth->verifyCredentials()) {
            // ...
        }
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

### Принцип открытости/закрытости (Open/Closed Principle, OCP)

Как сказал Bertrand Meyer: "Программные сущности (классы, модули, функции и т. д.) должны быть открыты для расширения, но закрыты для модифицирования". Что это означает? Позвольте пользователям добавлять новую функциональность без изменения кода.

**Плохо:**

```php
abstract class Adapter
{
    protected $name;

    public function getName(): string
    {
        return $this->name;
    }
}

class AjaxAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'ajaxAdapter';
    }
}

class NodeAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'nodeAdapter';
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch(string $url): Promise
    {
        $adapterName = $this->adapter->getName();

        if ($adapterName === 'ajaxAdapter') {
            return $this->makeAjaxCall($url);
        } elseif ($adapterName === 'httpNodeAdapter') {
            return $this->makeHttpCall($url);
        }
    }

    private function makeAjaxCall(string $url): Promise
    {
        // request and return promise
    }

    private function makeHttpCall(string $url): Promise
    {
        // request and return promise
    }
}
```

**Хорошо:**

```php
interface Adapter
{
    public function request(string $url): Promise;
}

class AjaxAdapter implements Adapter
{
    public function request(string $url): Promise
    {
        // request and return promise
    }
}

class NodeAdapter implements Adapter
{
    public function request(string $url): Promise
    {
        // request and return promise
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch(string $url): Promise
    {
        return $this->adapter->request($url);
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

### Принцип подстановки Барбары Лисков (Liskov Substitution Principle, LSP)

За этим пугающим термином скрывается очень простая идея. Формальное определение: "Если S — это подтип Т, то объекты типа Т могут быть заменены объектами типа S (например, вместо объектов типа Т можно подставить объекты типа S) без изменения каких-либо свойств программы (корректность, задачи и т. д.)". Ещё более пугающее определение.

Можно объяснить проще: если у вас есть родительский и дочерний классы, тогда они могут быть взаимозаменяемы без получения некорректных результатов. Рассмотрим классический пример с квадратом и прямоугольником. С точки зрения математики квадрат — это прямоугольник, но если смоделировать эту взаимосвязь is-a посредством наследования, то у вас будут проблемы.

**Плохо:**

```php
class Rectangle
{
    protected $width = 0;
    protected $height = 0;

    public function render(int $area): void
    {
        // ...
    }

    public function setWidth(int $width): void
    {
        $this->width = $width;
    }

    public function setHeight(int $height): void
    {
        $this->height = $height;
    }

    public function getArea(): int
    {
        return $this->width * $this->height;
    }
}

class Square extends Rectangle
{
    public function setWidth(int $width): void
    {
        $this->width = $this->height = $width;
    }

    public function setHeight(int $height): void
    {
        $this->width = $this->height = $height;
    }
}

function renderLargeRectangles(Rectangle $rectangles): void
{
    foreach ($rectangles as $rectangle) {
        $rectangle->setWidth(4);
        $rectangle->setHeight(5);
        $area = $rectangle->getArea(); // Плохо: Will return 25 for Square. Should be 20.
        $rectangle->render($area);
    }
}

$rectangles = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles($rectangles);
```

**Хорошо:**

```php
abstract class Shape
{
    protected $width = 0;
    protected $height = 0;

    abstract public function getArea(): int;

    public function render(int $area): void
    {
        // ...
    }
}

class Rectangle extends Shape
{
    public function setWidth(int $width): void
    {
        $this->width = $width;
    }

    public function setHeight(int $height): void
    {
        $this->height = $height;
    }

    public function getArea(): int
    {
        return $this->width * $this->height;
    }
}

class Square extends Shape
{
    private $length = 0;

    public function setLength(int $length): void
    {
        $this->length = $length;
    }

    public function getArea(): int
    {
        return pow($this->length, 2);
    }
}

function renderLargeRectangles(Shape $rectangles): void
{
    foreach ($rectangles as $rectangle) {
        if ($rectangle instanceof Square) {
            $rectangle->setLength(5);
        } elseif ($rectangle instanceof Rectangle) {
            $rectangle->setWidth(4);
            $rectangle->setHeight(5);
        }

        $area = $rectangle->getArea(); 
        $rectangle->render($area);
    }
}

$shapes = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles($shapes);
```

**[⬆ вернуться к началу](#Содержание)**

### Принцип разделения интерфейса (Interface Segregation Principle, ISP)

Согласно ISP, "Клиенты не должны зависеть от интерфейсов, которые не используют".

Хороший пример демонстрации принципа: классы, для которых требуются большие объекты настроек (settings objects). Рекомендуется не требовать от клиентов настраивать много параметров, потому что по большей части они им не нужны. Если сделать их опциональными, то это поможет избежать раздутости интерфейса.

**Плохо:**

```php
interface Employee
{
    public function work(): void;

    public function eat(): void;
}

class Human implements Employee
{
    public function work(): void
    {
        // ....working
    }

    public function eat(): void
    {
        // ...... eating in lunch break
    }
}

class Robot implements Employee
{
    public function work(): void
    {
        //.... working much more
    }

    public function eat(): void
    {
        //.... robot can't eat, but it must implement this method
    }
}
```

**Хорошо:**

Not every worker is an employee, but every employee is an worker.

```php
interface Workable
{
    public function work(): void;
}

interface Feedable
{
    public function eat(): void;
}

interface Employee extends Feedable, Workable
{
}

class Human implements Employee
{
    public function work(): void
    {
        // ....working
    }

    public function eat(): void
    {
        //.... eating in lunch break
    }
}

// robot can only work
class Robot implements Workable
{
    public function work(): void
    {
        // ....working
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

### Принцип инверсии зависимостей (Dependency Inversion Principle, DIP)

Этот принцип гласит:

1. Высокоуровневые модули не должны зависеть от низкоуровневых. Оба вида должны зависеть от абстракций.
2. Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций.

Сначала это может быть трудным для понимания, но если вы работали с PHP-фреймворками (вроде Symfony), то уже встречались с реализацией этого принципа в виде инъекции зависимости (Dependency Injection, DI). Однако эти принципы не идентичны, DI ограждает высокоуровневые модули от деталей своих низкоуровневых модулей и их настройки. Это может быть сделано посредством DI. Огромное преимущество в том, что снижается сцепление (coupling) между модулями. Сцепление — очень плохой шаблон разработки, затрудняющий рефакторинг кода.

**Плохо:**

```php
class Employee
{
    public function work(): void
    {
        // ....working
    }
}

class Robot extends Employee
{
    public function work(): void
    {
        //.... working much more
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage(): void
    {
        $this->employee->work();
    }
}
```

**Хорошо:**

```php
interface Employee
{
    public function work(): void;
}

class Human implements Employee
{
    public function work(): void
    {
        // ....working
    }
}

class Robot implements Employee
{
    public function work(): void
    {
        //.... working much more
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage(): void
    {
        $this->employee->work();
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

## Не повторяйся (Don’t repeat yourself, DRY)

Постарайтесь соблюдать принцип [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself).

Старайтесь полностью избавиться от дублирующего кода. Он плох тем, что если вам нужно менять логику, то это придётся делать в нескольких местах.

Представьте, что вы владеете ресторанчиком и отслеживаете, есть ли продукты: помидоры, лук, чеснок, специи и т. д. Если у вас несколько списков с содержимым холодильников, то вам придётся обновлять их все, когда вы готовите какое-то блюдо. А если список один, то и вносить изменения придётся только в него.

Зачастую дублирующий код возникает потому, что вы делаете две и более вещи, у которых много общего. Но небольшая разница между ними заставляет вас писать несколько функций, и те по большей части делают одно и то же. Удаление дублирующего кода означает, что вы создаёте абстракцию, которая может обрабатывать все различия с помощью единственной функции/модуля/класса.

Правильный выбор абстракции критически важен, поэтому нужно следовать принципам SOLID, описанным в разделе "[Классы](#Классы)". Плохие абстракции могут оказаться хуже дублирующего кода, так что будьте осторожны! Но если можете написать хорошие, то делайте это! Не повторяйтесь, иначе окажется, что при каждом изменении вам нужно обновлять код в нескольких местах.

**Плохо:**

```php
function showDeveloperList(array $developers): void
{
    foreach ($developers as $developer) {
        $expectedSalary = $developer->calculateExpectedSalary();
        $experience = $developer->getExperience();
        $githubLink = $developer->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}

function showManagerList(array $managers): void
{
    foreach ($managers as $manager) {
        $expectedSalary = $manager->calculateExpectedSalary();
        $experience = $manager->getExperience();
        $githubLink = $manager->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}
```

**Хорошо:**

```php
function showList(array $employees): void
{
    foreach ($employees as $employee) {
        $expectedSalary = $employee->calculateExpectedSalary();
        $experience = $employee->getExperience();
        $githubLink = $employee->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}
```

**Очень хорошо:**

Лучше использовать компактную версию кода.

```php
function showList(array $employees): void
{
    foreach ($employees as $employee) {
        render([
            $employee->calculateExpectedSalary(),
            $employee->getExperience(),
            $employee->getGithubLink()
        ]);
    }
}
```

**[⬆ вернуться к началу](#Содержание)**

## Переводы

На других языках:

 * ![en](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/United-Kingdom.png) **Английский:**
   * [jupeter/clean-code-php](https://github.com/jupeter/clean-code-php)
 * ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Китайский:**
   * [yangweijie/clean-code-php](https://github.com/yangweijie/clean-code-php)
   * [php-cpm/clean-code-php](https://github.com/php-cpm/clean-code-php)
 * ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Русский:**
   * [peter-gribanov/clean-code-php](https://github.com/peter-gribanov/clean-code-php)

**[⬆ вернуться к началу](#Содержание)**
