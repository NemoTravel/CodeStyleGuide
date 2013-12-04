# Code Style Guide v 1.0 #

## Что такое "хорошо" и что такое "плохо" ##

----

### Оглавление ###

1. Введение
2. Общие положения по коду (Общее для PHP и JavaScript)
3. Общие положения по комментированию кода
4. PHP
5. JavaScript
3. HTML
4. CSS + Stylus
5. Smarty
7. git

### Введение ###
Данный документ создан с единственной целью - формализовать код, сделать его единообразным, легкочитаемым, простым и эффективным.

**Внимание!** Данный документ содержит ненормативную лексику. Ее пришлось добавить исключительно в показательных целях, как пример того, что делать запрещено. Автор приносит свои извинения за это.

В этом документе указаны стандарты написания кода при разработке любого рода проектов. Он состоит из разделов, в свою очередь состоящих из правил. Различается три уровня правил: 

1. "**Необходимо**", "**обязательно**", "**требуется**", "**строго**" - ожидается обязательное исполнение указанного правила, за исключением отдельно описанных случаев
2. "**(не) рекомендуется**", "**(не)желательно**", "**разрешено**", "**допускается**"  - обязательное исполнение правила не ожидается, но правило рекомендовано к исполнению. Настоятельно рекомендуется указать комментарием, почему код противоречит правилу.
3. "**Зарпещено**", "**недопустимо**" - ожидается, что описанные подходы не будут применяться ни в каком виде

В случае, если осуществляется поддержка проекта, код которого не соответствует стандартам, описанным в документе, то: 

1. Переписанные части кода **должны** соответствовать стандартам, описанным в этом документе
2. Остальной код **разрешается** оставить как есть

----

### Общие положения по коду (Общее для PHP и JavaScript) ###

Кодировка - **строго** UTF-8 без [BOM](http://ru.wikipedia.org/wiki/%D0%9C%D0%B0%D1%80%D0%BA%D0%B5%D1%80_%D0%BF%D0%BE%D1%81%D0%BB%D0%B5%D0%B4%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D0%B8_%D0%B1%D0%B0%D0%B9%D1%82%D0%BE%D0%B2)

====

Перенос строки - **строго** Unix-style (LF)

====

**Не рекомендуется** писать строки больше 120-ти символов в длинну. Длинные конструкции рекомендуется разбивать на несколько строк с надлежащим форматированием.

----

#### Индентация и выравнивание ####

Идентация кода **строго обязательна**. Это означает: любой блок (несколько команд, следующих одна за другой) должен быть индентирован на одинаковую глубину. Глубина вложенного блока отличается от родительского ровно на один уровень.

*ПЛОХО: (Индентация отсутствует либо нелогична)*
```php
class SomeClass { 
private $foo;
public $bar;

public function process () {
$a = 0;
	$b = 1;
$this->foo = $this->bar;
}
}
```
*ПЛОХО: (вложенный блок индентируется на два уровня больше, чем родительский)*
```php
	if ($user->isJedi()) {
			GlobalForce::setForceDisturbance($user);
	}
```
*ХОРОШО:*
```php
class SomeClass { 
	private $foo;
	public $bar;
	
	public function process () {
		$a = 0;
		$b = 1;
		$this->foo = $this->bar;
	}
}
```
*ХОРОШО:*
```php
	if ($user->isJedi()) {
		GlobalForce::setForceDisturbance($user);
	}
```

====

Отступ для индентации кода - **строго** табулятор (Tab). (Некоторые интерпретаторы данного документа могут отображать Tab-ы пробелами)
См. [Lea Verou: Why tabs are clearly superior](http://lea.verou.me/2012/01/why-tabs-are-clearly-superior/)

====

**Рекомендуется** использовать Tab шириной в 4 пробела (Все IDE разрешают настраивать ширину Tab-а)

====

**Запрещено** использовать Tab для "выравнивания" кода:

*ПЛОХО: (Используются Tab-ы перед символами "=")*
```php
private $text			= 'abracadabra';
private $other_texts	= 'arbadacarba';
```
*ХОРОШО: (Используются пробелы)*
```php
private $text        = 'abracadabra';
private $other_texts = 'arbadacarba';
```

====

При [чейнинге методов](http://en.wikipedia.org/wiki/Method_chaining) **рекомендуется** сносить методы на следующую строку с индентацией на один уровень. Рекомендация становится **необходимостью**, если методов больше двух. При этом **разрешается** оставлять фильтрующую функцию на первой строке, если она одна.

*ПЛОХО:*
```javascript
$container.find('.js-something').show().removeClass('.js-disabled').data('someDataKey',someDataHere);
```
*ХОРОШО:*
```javascript
$container.find('.js-something')
	.show()
	.removeClass('.js-disabled')
	.data('someDataKey', someDataHere);
```

----

#### Константы и булевы переменные ####

Все константы **должны** записываться в верхнем регистре, смысловые слова разделяются символами подчеркивания 

*ПЛОХО:*
```php
define('maximum_punches_in_face',1000);
class SomeClass {
	const maximum = 1000;
}
```
*ХОРОШО:*
```php
define('MAXIMUM_PUNCHES_IN_FACE',1000);
class SomeClass {
	const MAXIMUM = 1000;
}
```
**Обоснование:** константы в коде "бросаются в глаза" и легко отличимы от переменных

====

Булевы и специальные типы данных записываются либо в вехнем либо в нижнем регистре. **Запрещается** смешивать регистры. **Рекомендуется** нижний регистр.
Это правило применяется к ключевым словам: ````true````, ````false````, ````null````, ````undefined````.

*ПЛОХО:*
```php
$isOK = False;
```
*ЕЩЕ ХУЖЕ:*
```php
$isOK = FaLsE;
```
*ХОРОШО:*
```php
$isOK = false;
$hasChildren = FALSE;
```

----

#### Именование переменных, функций и классов ####

Язык названий переменных/классов/функций и т. д. - **строго** английский.

*ПЛОХО:*
```javascript
var PeriodoEntrePulsaciones = 300;
var taimautNaAyaksZapros = 300;
```
*ХОРОШО:*
```javascript
var requestTimeout = 300;
```

====

Любое имя **должно** быть лаконичным, но понятным: имя должно описывать назначение переменной/функции/класса, чем короче это описание, тем лучше

*ПЛОХО:*
```javascript
var bnum = fv + bc,
    someAwesomeNumberThatMakesEverythingAwesome = 0;
```
*ХОРОШО:*
```javascript
var resultBlocksCount = fieldValue + baseCount,
    awesomeNumber = 0;
```

====

Имена классов и объектов-контроллеров (в JavaScript) **строго** [PascalCase (UpperCamelCase)](http://c2.com/cgi/wiki?PascalCase), **разрешено** использование нижней черты (````_````) в php и только там (autoloader может ориентироваться на этот символ для поиска требемого класса в файлах проекта).

*ПЛОХО:*
```javascript
var some_page_controlling_object = { /* snip */ };

var Some_Page_Controller_Object = { /* snip */ };

var somepagecontrollerobject = { /* snip */ };
```
*ХОРОШО:*
```javascript
var SomePageControllerObject = { /* snip */ };
```
```php
class AdminCore_SystemLanguages_AdminController { /* snip */ }
```

====

Имена функций и переменных - **строго** [CamelCase (lowerCamelCase)](http://c2.com/cgi/wiki?LowerCamelCase). Единственным исключением является случай, когда первое слово - аббревиатура

*ПЛОХО:*
```javascript
function do_something_awesome () { /* snip */ }

var XML_text = '';
```
*ХОРОШО:*
```javascript
function doSomethingAwesome () { /* snip */ }

var XMLText = '';
```

====

Имена геттеров и сеттеров **обязаны** начинаться с ````get```` и ````set```` соответственно

*ПЛОХО:*
```php
public function id()           { return $this->id; }
public function retrieveName() { return $this->name; }
```
*ХОРОШО:*
```php
public function getId()   { return $this->id; }
public function getName() { return $this->name; }
```

====

Односимвольные имена переменных **запрещены**. Единственным исключением являеется случай, когда переменная является итератором цикла

*ПЛОХО:*
```php
$t = time();
```
*ХОРОШО:*
```php
for ($i = 0, $c = count($elements); $i < c; $i++) { /* snip */ }
```

----

#### Форматирование кода ####

В логических, строковых и арифметических операциях, а также во время группировки скобками и присваивания, **обязательно** использование пробелов слева и справа от операндов. Исключения:
- Для логического отрицания отступ справа **запрещен**
- Конкатенацию **не рекомендуется** выделять пробелами 
- **Разрешается** не использовать внутренние боковые отступы внутри скобок

*ПЛОХО:*
```php
// Нет отступов у присваивания и символа +
$x=1+4;

// Нет отступов у скобки
$y = ($x * 3)+ 2;
 
// Лишний отступ у !
$z = ! $lambda; 
```
*ХОРОШО:*
```php
$x = 1 + 4;

$y = ($x * 3) + 2;

$z = !$lambda;
```

====

Форматирование конструкции ````switch```` **должно** подчиняться следующим правилам:
- ````case```` **должно** быть сдвинуто на один уровень относительно ````switch````
- код между````case```` и ````break```` **должен** быть сдвинут на один уровень относительно ````case````
- ````break```` настоятельно **рекомендуется** сдвигать на один уровень относительно ````case````

*ПЛОХО:*
```javascript
switch (forcePower) {
case 'weak':
itemModifier = '_whimsyweak';
break;
case 'normal':
itemModifier = '_normal';
break;
case 'strong':
itemModifier = '_superstrong';
break;
default:
itemModifier = '_none';
break;
}
```
*ХОРОШО:*
```javascript
switch (forcePower) {
	case 'weak':
		itemModifier = '_whimsyweak';
		break;
	case 'normal':
		itemModifier = '_normal';
		break;
	case 'strong':
		itemModifier = '_superstrong';
		break;
	default:
		itemModifier = '_none';
		break;
}
```

====

**Обязательно** использование пробелов при определении функций, методов, классов и в управляющих конструкциях типа ````for````, ````foreach````, ````if````, ````switch````, ````catch```` и так далее.
Тем не менее, **не рекомендуется** использовать пробелы в таких случаях:
- перед запятой при перечислении аргументов функции/метода
- после открывающей и перед закрывающей скобкой списка аргументов функции/метода
- после открывающей и перед закрывающей скобкой логического условия конструкции ````if````
- после открывающей и перед закрывающей скобкой списка аргументов конструкций ````for````, ````foreach````, ````switch````, ````catch```` и так далее

*ПЛОХО:*
```php
function makeMyDay($a,$b,$c){
	$return = 0;
	for($i = 1;$i < count($a);$i++){
		$return += $a[$i] * ($b + $c);
	}

	return $return;
}

class myDayMaker{
	public function checkMyDay($day){
		if($day){
			switch($day){
				case'today':
				case'tomorrow':
					return 1;
					break;
				default:
					return 0;
					break;
			}
		}
		
		return -1;
	}
}
```
*ХОРОШО:*
```php
function makeMyDay ($a, $b, $c){
	$return = 0;

	for ($i = 1; $i < count($a); $i++) {
		$return += $a[$i] * ($b + $c);
	}

	return $return;
}

class myDayMaker {
	public function checkMyDay ($day) {
		if ($day) {
			switch ($day) {
				case 'today':
				case 'tomorrow':
					return 1;
					break;
				default:
					return 0;
					break;
			}
		}
		
		return -1;
	}
}
```

====

**Должны** использоваться ["египетские скобки" (Стиль «K&R»)](http://ru.wikipedia.org/wiki/%D0%9E%D1%82%D1%81%D1%82%D1%83%D0%BF_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)).

====

Если скобки можно опустить, они **должны** быть.

*ПЛОХО:*
```javascript
if (Luke.usesForce()) DeathStar.explode();

if (Luke.usesForce())
	DeathStar.explode();
```
*ХОРОШО:*
```javascript
if (Luke.usesForce()) {
	DeathStar.explode();
}
```

====

В ````if ... else```` конструкциях, ````else```` **должно** быть на отдельной строке, ````else```` на одной строке с закрывающей фигурной скобкой **запрещено**

*ПЛОХО:*
```javascript
if (items.length > 0)
{
	items.push(getNewItem());
}else populateItems();
```
*ХОРОШО:*
```javascript
if (items.length > 0) {
	items.push(getNewItem());
}
else {
	populateItems();
}
```

====

**Допускается** "сворачивание" *простейших* геттеров/сеттеров в одну строку.

*ПЛОХО:*
```php
// Too much code is "hidden"
public function getChildren () { if ($this->hasChildren()) { return $this->children; } return array(); }
```
*ХОРОШО:*
```php
public function getChildren () { return $this->children; }
```

====

**Запрещено** использование логических операторов в символьном виде

*ПЛОХО:*
```smarty
{if $object->hasChildren() or $forceChildrenDisplay}
```
*ХОРОШО:* 
```smarty
{if $object->hasChildren() || $forceChildrenDisplay}
```

====

Сложные (более чем на 2 оператора) логические конструкции **должны** быть отформатированы

*ПЛОХО:*
```php
if ($isOK && ($user->isPriveleged() || $user->isRoot()) && count($result) > 0) {
	/* snip */
}
```
*ХОРОШО:*
```php
if (
	$isOK &&
	(
		$user->isPriveleged() ||
		$user->isRoot()
	) &&
	count($result) > 0
) {
	/* snip */
}
```

====

**Запрещено** начинать строку с логического оператора при форматировании сложных логических условий

*ПЛОХО:*
```php
if (
	$isOK 
	&& $user->isRoot()
	&& count($result) > 0
	&& count($categories) > 1
) {
	/* snip */
}
```
*ХОРОШО:*
```php
if (
	$isOK && 
	$user->isRoot() &&
	count($result) > 0 &&
	count($categories) > 1
) {
	/* snip */
}
```

====

**Запрещено** использование присваивания в логических выражениях

*ПЛОХО:*
```php
if ($arrCount = count($array)) {
	/* snip */
}
```
*ХОРОШО:*
```php
$arrCount = count($array);
if ($arrCount) {
	/* snip */
}
```

====

При инициализации ассоциативных массивов в PHP и объектов (````Object````) в JavaScript каждый элемент **должен** располагаться на отдельной строке.
**Разрешается** не применять это правило если массив/объект состоит из одного элемента и конструкция легкочитаема
Для линейных массивов (и просто массивов в JavaScript) **разрешается** указывать элементы в одну строку и/или разбивать их на несколько строк, больше чем по элементу на строку.
Также, настоятельно **рекомендуется** выравнивать значения в массиве/объекте для повышения читаемости

*ПЛОХО:*
```php
$basicData = array('name' => null, 'age' => 0, 'root_priveleges' => false);
```
```javascript
$element.someJQueryPlugin({some:'initialization',parameters:'here'});
```
*ХОРОШО:*
```php
$basicData = array(
	'name'            => null,
	'age'             => 0,
	'root_priveleges' => false
);
```
```javascript
$element.someJQueryPlugin({
	some       : 'initialization',
	parameters : 'here'
});

// Так тоже можно, но только аккуратно
$element.someJQueryPlugin({some: 'initialization'});
```

====

[Yoda conditions](http://ru.wikipedia.org/wiki/%D0%A3%D1%81%D0%BB%D0%BE%D0%B2%D0%B8%D1%8F_%D0%99%D0%BE%D0%B4%D1%8B) **рекомендуются** к применению:
```php
if ('use' == $the_force) {
    $victorious = You::will($be);
}
```

====

**Рекомендуется** вызовы функций с несколькими аргументами форматировать таким образом:

- Каждый аргумент располагается на своей строке
- Каждый аргумент индентирован на 1 уровень относительно уровня вызова функции
- Запятая ставится после аргумента и является последним символом в строке
- Открывающая скобка находится на одной строке с вызовом функции
- Закрывающая скобка находится на отдельной строке

*ПЛОХО:*
```php
someFunction($with,$a,$hella,$lot,$ofPossiblyLong,$argumentsNamesAndStuff);
```
*ХОРОШО:*
```php
someFunction(
	$with,
	$a,
	$hella,
	$lot,
	$ofPossiblyLong,
	$argumentsNamesAndStuff
);
```

----
#### Прочее ####

**Не рекомендуется** использовать ["магические числа"](http://ru.wikipedia.org/wiki/%D0%9C%D0%B0%D0%B3%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%BE%D0%B5_%D1%87%D0%B8%D1%81%D0%BB%D0%BE_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5))

*ПЛОХО:*
```javascript
if ($items.length > 6) {
	return;
}
```
*ХОРОШО:*
```javascript
// Now it's magic but later it could be passed here as a user-configured value
var maxItems = 6;

/* snip */

if ($items.length > maxItems) {
	return;
}
```

====

Строки настоятельно **рекомендуется** записывать в одинарных кавычках.

====

**Обязательно** использование конкатенации для записи длинных строк

*ПЛОХО:*
```javascript
var error = 'This is a soopah long error \
		that my soopah cool script trows on every occasion \
		because I\'m a soopah cool web developer and \
		I know how to do cool stuff';
```
*ХОРОШО:*
```javascript
var error = 'This is a soopah long error '+
		'that my soopah cool script trows on every occasion '+
		'because I\'m a soopah cool web developer and '+
		'I know how to do cool stuff';
```

====

Не полагайтесь на приведение типов: **не рекомендуется** пользоваться конструкциями вида
```php
if ($possiblyEmptyArray) { /* snip */ }
```
если переменная не заведомо [скалярна](http://php.net/manual/en/language.types.intro.php) для PHP или [примитивна](http://javascriptweblog.wordpress.com/2010/09/27/the-secret-life-of-javascript-primitives/) для JavaScript.

----

### Общие положения по комментированию кода ###

Язык комментариев - настоятельно **рекомендуется** английский.

====

Однострочные комментарии размещаются **строго** отдельной строкой с пустой строкой сверху. Единственным исключением является случай, когда комментарий вставляется перед ``` else``` или ``` elseif```. В таком случае пустая строка перед комментарием **запрещена**. Это же правило применяется и для комментирования HTML

*ПЛОХО:*
```php
$player->applyWeapon($cow); // Bad comment - not on separate line

$player->setWeapon($chainsaw);
// Bad comment - no empty line before
$player->applyWeapon($cow);

$player->setWeapon($chainsaw);

// Bad comment - empty line after

$player->applyWeapon($cow);

if ($success) {
	Do::something();
}

// Bad comment - unneeded empty line before
else {
	Do::somethingElse();
}
```
*ХОРОШО:*
```php
$player->setWeapon($chainsaw);

// Good comment - empty line before, no empty line after
$player->applyWeapon($cow);

if ($success) {
	Do::something();
}
// Good comment - no empty line before a comment to else/elseif statement
else {
	Do::somethingElse();
}
```

====

**Обязательна** документация кода по стандартам *PHPDoc* ([Документация](http://manual.phpdoc.org/HTMLframesConverter/default/)) и *JSDoc* ([Документация](http://usejsdoc.org/)).
Для HTML, CSS (*CSSDOC:* [Сайт](http://cssdoc.net/), [Примеры на Хабре](http://habrahabr.ru/post/87406/ "2")), XML и SQL документация **желательна**.

*ПЛОХО:*
```php
// This function does something good
// You can pass a receiver, index of goody goodness
// and a special magic boolean (not needed)
// It returns an instance of SomeGoodThing
function doSomethingGood ($receiver, $goodIndex, $recursive = true) {
	return new SomeGoodThing($receiver, $goodIndex, $recursive);
}
```
*ХОРОШО:*
```php
/**
 * This function does something good
 *
 * And here we describe what this function does in detail
 *
 * @param SomeEntity $receiver
 * @param int $goodIndex
 * @param bool $recursive
 *
 * @return SomeGoodThing
 */
function doSomethingGood ($receiver, $goodIndex, $recursive = true) {
	return new SomeGoodThing($receiver, $goodIndex, $recursive);
}
```
**Обоснование:** задокументированный код очень облегчает поддержку. Через месяц, разработчики уже не помнят, что конкретно делает тот или иной метод, и как.

====

**Обязательно** использование ````@return```` в документации к функции/методу если он возвращает что-либо

*ПРИМЕР:*
```php
class SomeClass {
	/**
	 * Returns an instance of self
	 * @return SomeClass
	 * /
	public static function getInstance () {
		return new self();
	}
}
```

====

Настоятельно **рекомендуется** использование ````@throws```` в документации к функции/методу, бросающим исключения

*ПРИМЕР:*
```php
/**
 * Some dummy description here. Disregard it.
 * @throws WrongValueException
 * @return bool
 * /
function checkValue ($value) {
	if (!is_object($value)) {
		throw new WrongValueException();
	}

	return $value->checkSelf();
}
```

====

Строжайше **запрещено** использовать ненормативную лексику в комментариях, исполняемом коде и всех прочих файлах, даже "зацензуренную"

*ПЛОХО:*
```smarty
{* Это – ублюдонский рендер неведомой ёбанной хуйни *}
{cms_render page="some_bad_page" capture="fuckshit"}
```
*ТАК ТОЖЕ ПЛОХО:*
```smarty
{* Это – уб**донский рендер неведомой ё*анной х**ни *}
{cms_render page="some_bad_page" capture="inline"}
```
*И ДАЖЕ ТАК ПЛОХО:*
```xml
<xmlelement name="shitface"/>
```
*ХОРОШО:*
```smarty
{* Это – рендер неизвестной мне страницы *}
{cms_render page="some_bad_page" capture="inline"}
```
```xml
<xmlelement name="badface"/>
```

====

Строжайше **запрещено** упоминание имен клиентов, их организаций и другой "чувствительной" информации (упоминания договоров, паспортных данных, коммерческих тайн, проектов в разработке и т. д.)

*ПЛОХО:*
```html
<!-- This was added on request by our client Anakin Skywalker as was written in his contract appendix #123 -->
```
**Обоснование:** Это по факту является нарушением NDA (Non-Disclosure Agreement).

Номера тикетов (задач в Redmine) в комментариях **разрешены**.

*ПРИМЕР:*
```php
// TODO implement this function when #123123 is resolved
```
**Обоснование:** сам номер тикета ничего не говорит, сам тикет увидят только те, кто имеет на это право. 

====

**Допускаются** "пасхальные яйца" в комментарих к коду, тем не менее, юмор должен быть сдержанным и обязательно соблюдение вышеописанных правил комментирования. **Рекомендуется** не злоупотреблять разрешением и не создавать непонятных большинству людей, либо слишком много "пасхалок".

*ПРИМЕР:*
```javascript
/**
 * Cookie monster - an object that deals with route cookies: creates one by DOM structure and saves.
 * Also provides a limited access to trip properties: type and segments data
 * @type {Object}
 */
/* Just a little bit of code vandalism
                .---. .---.
               :     : o   :    me want cookie!
           _..-:   o :     :-.._    /
       .-''  '  `---' `---' "   ``-.
     .'   "   '  "  .    "  . '  "  `.
    :   '.---.,,.,...,.,.,.,..---.  ' ;
    `. " `.                     .' " .'
     `.  '`.                   .' ' .'
      `.    `-._           _.-' "  .'  .----.
        `. "    '"--...--"'  . ' .'  .'  o   `.
        .'`-._'    " .     " _.-'`. :       o  :
      .'      ```--.....--'''    ' `:_ o       :
    .'    "     '         "     "   ; `.;";";";'
   ;         '       "       '     . ; .' ; ; ;
  ;     '         '       '   "    .'      .-'
  '  "     "   '      "           "    _.-'
*/
```

====

Использование комментариев
````TODO```` и ````FIXME```` настоятельно **рекомендуется**.

Применение:
- ````FIXME```` используется для указания на проблему
- ````TODO```` используется для указание на решение проблемы

*ПРИМЕР:*
```php
// FIXME this code sometimes throw an exception. Need to figure out why
```
```php
// TODO need to check for available slots here in order to avoid unexpected exception throwing
```

====

При комментировании кусков кода **обязательно** указание времени, причины и имени/корпоративной почты комментирующего. Ненужные куски кода **должны** удаляться, а не комментироваться.

*ПРИМЕР:*
```smarty
{* v.poopking 13.06.2013 07:40 : Commented out due to bugs in backend processing. Return when #123123 is fixed *}
{*<div class="some-class-name__here">
    {include file='some_template.tpl'}
</div>*}
```
**Обоснование:** закомментированный код будет удаляться. Чтобы этого не произошло стоит указывать причину, по которой код комментируется, и должен оставаться в файле.

----

### PHP ###

Строжайше **запрещено** использование конструкций типа ````$$variable````. Автор полагает, что это правило в объяснении не нуждается

====

Строжайше **запрещено** подавление ошибок через ````@````

====

Расширение php-файла **строго** ````.php```.

====

Первыми символом любого php-файла **должен** быть открывающий тег ````<?php````.

====

**Запрещено** использование PHP short tag (````<? /* snip */ ?>````  ````<?= /* snip */ ?>).
Хорошее объяснение [тут](http://programmers.stackexchange.com/questions/151661/is-it-bad-practice-to-use-tag-in-php#answer-151694).

====

Строжайше **запрещено** использование закрывающего PHP тега (````?>````)

====

**Запрещено** в рамках одного файла объявлять символы (классы, функции и т. д.) и исполнять логику

*ПЛОХО:*
```php
class SuperVillain { /* snip */ }

$magneto = new SuperVillain('Magneto');

try {
	$magneto->conquer($world);
}
catch (VillainException $e) {
	/* snip */
}
```
*ХОРОШО:*
```php
// Файл SuperVillain.php
class SuperVillain { /* snip */ }

// Файл index.php
try {
	$magneto->conquer($world);
}
catch (VillainException $e) {
	/* snip */
}
```

====

Каждый класс **должен** размещаться в отдельном файле, имя которого **должно** совпадать с именем класса. Единственным исключением является случай, когда в файле объявляются несколько очень тесно связанных между собой классов, например - класс DAO (Data Access Object) и исключения, которые использует только он.

====

Настоятельно **рекомендуется** использовать исключения (Exceptions) для сигнализации обо всех нештатных ситуациях.

*ПЛОХО:*
```php
	public static function logIn ($login, $password) {
		if (self::checkLoginAndPassword($login,$password)) {
			return null;
		}
		
		return new self();
	}
```
*ХОРОШО:*
```php
	public static function logIn ($login, $password) {
		if (self::checkLoginAndPassword($login,$password)) {
			throw new UserNotFoundException ();
		}
		
		return new self();
	}
```

====

Все классы-наследники класса ````Exception```` **должны** иметь имя, заканчивающееся на слово ````Exception````

====

Любые конфигурационные файлы **должны** иметь расширение ````.php````

====

Настоятельно **рекомендуется** использовать следующие параметры при разработке:
````
display_errors = On
display_startup_errors = On
error_reporting = -1
````
При этом код не должен вызывать ни одной ошибки (даже ````E_NOTICE````). **Разрешается** при выводе отключать отображение ````E_NOTICE````, но не более.

----

#### Циклы ####

Настоятельно **рекомендуется** использовать следующую конструкцию для циклов ```for```:
```php
for ($i = 0, $c = count($array); $i < $c; $i++) { /* snip */ }
```
**Обоснование:** ````count($array)```` выполняется только один раз и ее выполнение вписано в сам цикл, что есть удобно

====

Настоятельно **рекомендуется** использовать комментарии типа
```php
/**
 * @var SomeObject $object
 */
foreach ($objectsArray as $object) {
	$object->someMethid();
}
```
**Обоснование:** IDE "подхватит" ````$object```` как объект класса ````SomeObject````, что позволит использовать встроенный в IDE автокомплитер по полям/методам объекта.

----

#### Строки ####

Использование переменных внутри строки **запрещено**.

*ПЛОХО:*
```php
return "C'mon $name let's go party!";
```
*ТОЖЕ ПЛОХО:*
```php
return "C'mon {$user['name']} let's go party!";
```
*ХОРОШО:*
```php
return 'C\'mon '.$name.' let's go party!';
```

====

Если требуется принудительно вывести перенос строки (например - в отдельном скрипте, обрабатывающем запросы дугого сервера), **рекомендуется** использовать константу.

*ПРИМЕР:*
```php
define('EOL',"\r\n");

echo '42'.EOL;
```

----

#### Классы, методы и функции ####

Использование ````var```` **запрещено**.

====

**Обязательно** использование ключевого слова ````public```` даже там, где его можно опустить.

====

Использование [магических методов](http://php.net/manual/ru/language.oop5.magic.php) **не рекомендуется**

====

Если свойство или метод могут быть статическими, они **должны** быть статическими

====

Каждый класс **должен** быть разделен на такие "логические блоки":

- Блок констант класса
- Блок свойств класса
- Блок публичных методов
- Блок защищенных методов
- Блок Блок приватных методов

====

Использование [статических переменных](http://www.php.net/manual/en/language.variables.scope.php#example-104) в функциях **запрещено**

====

Использование ````global```` запрещено

====

Использование суперглобального массива ````$GLOBALS```` **запрещено**

====

Если метод/функция принимают объект как параметр, **обязательно** указание класса объекта

*ПЛОХО:*
```php
	public static function disturbForce ($jedi) {
		$ratio = $jedi->getForceStrength();
		/* snip */
	}
```
*ХОРОШО:*
```php
	public static function disturbForce (JediPerson $jedi) {
		$ratio = $jedi->getForceStrength();
		/* snip */
	}
```
**Подробнее:** [Type Hinting](http://www.php.net/manual/en/language.oop5.typehinting.php)

----

### JavaScript ###

Настоятельно **рекомендуется** использование [strict mode](http://habrahabr.ru/post/118666/)

====

**Обязательно** использование точки с запятой в конце каждой команды

*ПЛОХО:*
```javascript
i = 'work'
```
*ХОРОШО:*

```javascript
i = 'work but I\'m also correct';
```
====

Использование точки с запятой после закрывающей скобки блока **запрещено**

*ПЛОХО:*
```javascript
if (itemsStack.length) {
	/* snip */
};
```
*ХОРОШО:*

```javascript
if (itemsStack.length) {
	/* snip */
}
```

====

Объявление переменных **обязано** быть в начале области видимости. Если объявляется несколько переменных, то вторая и все последующие **должны** размещаться на отдельной строке, со сдвигом *на 4 пробела*, причем первыми **рекомендуется** указывать инициализированные переменные, а последними - неинициализированные.

*ПЛОХО:*
```javascript
var result, $element = $('.js-something');

/* snip */

var $parent = $element.parent('.js-container');
```
*ХОРОШО:*
```javascript
var $element = $('.js-something'),
    $parent = $element.parent('.js-container'),
    result;
```

====

Переменные, содержащие в себе jQuery-коллекцию **должны** начинаться с символа ````$````

====

**Не рекомендуется** использовать метод ````end()```` библиотеки jQuery.

*ПЛОХО:*
```javascript
$container
	.find('.js-somethingToHide')
		.hide()
		.addClass('.js-disabled')
	.end()
	.find('.js-somethingToShow')
		.show()
		.removeClass('.js-disabled');
```
*ХОРОШО:*
```javascript
$container.find('.js-somethingToHide')
	.hide()
	.addClass('.js-disabled')
	
$container.find('.js-somethingToShow')
	.show()
	.removeClass('.js-disabled');
```

====

**Запрещено** использовать выборки по чему-либо кроме классов с префиксом ````js-```` и их суперпозиций

*ПЛОХО:*
```javascript
$container.find('a').addClass('i-invisible');
$container.find('.csg-someClass').addClass('i-invisible');
$container.find('#someId').addClass('i-invisible');
```
*ХОРОШО:*
```javascript
$container.find('.js-someClass').addClass('i-invisible');
```

----

#### Объекты и массивы ####

Настоятельно **не рекомендуется** использовать ````new Array()```` и ````new Object()````, используйте сокращенную запись: ````[]```` и ````{}```` соотсетственно

*ПЛОХО:*
```javascript
var myArray = new Array(),
	myObject = new Object();
```
*ХОРОШО:*
```javascript
var myArray = [],
	myObject = {};
```

====

**Запрещено** оставлять запятую после последнего свойства объекта или элемента массива

*ПЛОХО:*
```javascript
var myArray = [1, 2, 3, 4,],
	myObject = {
		/* snip */
		lastProperty: 'abracadabra',
	};
```
*ХОРОШО:*

```javascript
var myArray = [1, 2, 3, 4],
	myObject = {
		/* snip */
		lastProperty: 'abracadabra'
	};
```
**Обоснование:** в объекте это может "уронить" InternetExplorer, в массиве - добавить нежелательный ````null```` еще одним элементом массива, причем последнее зависит от того, какой интерпретатор используется

====

Настоятельно **не рекомендуется** создавать свойства объекта, для записи которых приходится использовать кавычки. Исключением может быть случай, когда эти свойства *всегда* создаются и используются программно.

**Запрещено** оборачивать в кавычки свойства объектов, когда это не требуется. 

*ПЛОХО:*
```javascript
var fictionalChar = {
	'full-name': 'Donkey-Hot',
	'age': undefined
}
```
*ХОРОШО:*
```javascript
var fictionalChar = {
	fullName : 'Donkey-Hot',
	age      : undefined
}
```

====

**Запрещено** использовать квадратные скобки и строки для доступа к свойству объекта

*ПЛОХО:*
```javascript
this.options['someConfigurableHook'].call(this);
```
*ХОРОШО:*
```javascript
this.options.someConfigurableHook.call(this);
```

====

**Запрещено** использовать "коверканые" зарезервированные слова как названия свойств объекта, используйте читаемые синонимы

*ПЛОХО:*
```javascript
var something = {
	if: 'parameterName',
	klass: 'prefix-ds__bem_class'
};
```
*ХОРОШО:*
```javascript
var something = {
	condition: 'parameterName',
	addClass: 'prefix-ds__bem_class'
};
```

====

Для добавления или изменения элементов в массиве **необходимо** использовать методы ````push()````, ````pop()````, ````shift()````, ````unshift()```` и т. д.

*ПЛОХО:*
```javascript
someStack[someStack.length] = 'abracadabra';
```
*ХОРОШО:*
```javascript
someStack.push('new string');
```

====

При  итерации по свойствам объекта **обязательно** использование ````.hasOwnProperty()````

*ПЛОХО:*
```javascript
var tmp = {
	a: 1,
	b: 2,
	c: 3
};

for (var i in tmp) {
	console.log(i, tmp[i]);
}
```
*ХОРОШО:*
```javascript
var tmp = {
	a: 1,
	b: 2,
	c: 3
};

for (var i in tmp) {
	if (tmp.hasOwnProperty(i)) {
		console.log(i, tmp[i]);
	}
}
```

----

#### Функции ####

**Запрещено** объявлять переменную с именем ````arguments````.

**Обоснование:** читаем про [предопределенную локальную переменную](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/arguments)

====

Определять функции внутри логических блоков либо циклов **запрещено**.

----

#### События ####

Если возникает нужда передать данные через событие (большинство фреймворков позволяют передавать произвольные данные вместе с событиями), настоятельно **рекомендуется** использовать один объект, даже если передаваемых объектов несколько

*ПЛОХО:*
```javascript
$element.trigger('customEvent', some, data);
```
*ХОРОШО:*
```javascript
$element.trigger(
	'customEvent',
	{
		key  : some,
		data : data
	}
);
```

**Обоснование:** если потребуется передавать еще один объект, нужно будет просто добавить его обработку в требуемые обработчики, вместо того, чтобы добавлять еще один аргумент во все возможные 25

====

**Рекомендуется** использовать события и их обработчики, вместо вызова функций. При этом обработчикам событий **рекомендуется** получать все необходимые для себя данные через данные в самом событии.

*ПЛОХО:*
```javascript
function doSomething () {
	/* snip */
	doSomethingAdditional(some, parameters, here);
}
```
*ХОРОШО:*
```javascript
function doSomething () {
	/* snip */
	$element.trigger(
		'doneSomething',
		{
			some      : parameters,
			passed    : to,
			triggered : event
		}
	);
}
```
**Обоснование:** если потребуется "точечно" добавить функциональность, например - на одной странице из многих, намного проще и удобнее провесить еще один обработчик событий, чем переопределять "специально оставленную" функцию

----

#### Прочее ####

Имена "приватных" свойств **рекомендуется** начинать с ````_````

====

**Необходимо** всегда передавать второй параметр в функцию ````parseInt````

====

При создании прототипа объекта, **необходимо** *добавлять* методы в прототип, а не переписывать его

*ПЛОХО:*
```javascript
function SuperHero() {
  this.name;
}

SuperHero.prototype = {
	setName: function setName (name) {
		this.name = name;
	},
	
	getName: function getName () {
		return this.name;
	}
};
```
*ХОРОШО:*
```javascript
function SuperHero() {
  this.name;
}

SuperHero.prototype.setName = function setName (name) {
	this.name = name;
}
	
SuperHero.prototype.getName = function getName () {
	return this.name;
}
```
**Обоснование:** переписав прототип уничтожатся уже существующие в нем методы, делая наследование невозможным

----

### HTML ###

**Обязательно** корректное использование doctype во всех местах, где его можно применить. При этом используется ````<!DOCTYPE html>````

**Обоснование:** см. [презентацию Вадима Макеева](http://pepelsbey.net/pres/doctype/)

====

Тег ````<html>```` **обязан** иметь аттрибут ````lang````, если это возможно

====

Тег ````<head>```` **обязан** содержать необходимые метатеги, определяющие:

- Тип передаваемых данных (обычно - ````text/html; charset=UTF-8````)
- Кодировку страницы
- Заголовок страницы

====

Тег ````<head>```` **обязан** содержать подключение общих javascript-библиотек (например, jQuery) и css. **Запрещено** подключение общих библиотек и стилей в теле страницы

====

**Не рекомендуется** указывать аттрибут ````type```` для тегов ````link```` и ````script````, если значение равно значению по умолчанию (````type="text/css"```` и ````type="text/javascript"```` соответственно)

**Обоснование:** [Спецификация HTML 5](http://www.w3.org/html/wg/drafts/html/master/document-metadata.html) не требует указания типа данных, используя вышеуказанные значения как значения по умолчанию.

====

**Запрещено** использование тегов ````<style>```` и ````<script>```` для внедрения стилей или скриптов на страницу не через подключение соответствующего файла

*ПЛОХО:*
```html
<style>
	.csg-testClass {
		color: red;
	}
<style>
<script>
	var someVar = 'Some text';
</script>
```
*ХОРОШО:*
```html
<link rel="stylesheet" href="css_additional.css"/>
<script src="js_additional.js"/>
```

====

**Обязательно** закрывать HTML-теги, даже если это не требуется

*ПЛОХО:*
```html
<li>Some text here.
<li>Some new text here.
<li>You get the idea.
```
*ХОРОШО:*
```html
<li>Some text here. </li>
<li>Some new text here. </li>
<li>You get the idea. </li>
```

====

Названия тегов **должны** быть в нижнем регистре

*ПЛОХО:*
```html
<DIV class="prefix-subprefix-some__class">I'm a text!</DIV>
```
*ХОРОШО:*
```html
<div class="prefix-subprefix-some__class">I'm a text!</div>
```

====

Настоятельно **рекомендуется** использовать [семантические HTML-элементы](http://blogs.msdn.com/b/jennifer/archive/2011/08/01/html5-part-1-semantic-markup-and-page-layout.aspx). [W3CSchools](http://www.w3schools.com/html/html5_semantic_elements.asp)

====

**Запрещено** использовать inline-css и inline-javascript. Используйте классы.

*ПЛОХО:*
```html
<div style="color: red;" onclick="doSomething();">
```
*ХОРОШО:*
```html
<div class="prefix-some__class js-some__js__class">
```

====

**Обязательно** использование индентации для вложенных элементов.

====

Все вложенные элементы **обязаны** размещаться каждый - с новой строки. Единственным исключением из правила является ситуация, когда требуется исключить пробелы между элементами с ````display: inline-block;````

====

**Запрещено** использовать HTML-комментарии для исключения пробельных символов между элементами

====

**Не рекомендуется** использовать комментарии для обозначения конца какого-либо блока.

*ПЛОХО:*
```html
<div class="csg-some__class">
	<!-- snip -->
</div><!-- /.csg-some__class -->
```
*ХОРОШО:*
```html
<div class="csg-some__class">
	<!-- snip -->
</div>
```
**Обоснование:** классы меняются, добавляются или убираются, а комментарии править никто не будет. Более того, это увеличивает объем файла (даже если используются Smarty-комментарии) и значительно ухудшает читаемость кода.

----

#### Классы ####

Классы **обязаны** подчиняться следующим правилам именования a-la [BEM](http://ru.bem.info/):
```
themePrefix-[componentPrefix-]blockName[__blockName[__blockName[...]]][_modifier]
```
Где

- ````themePrefix-```` - префикс, говорящий о том, для какой темы оформления используется данный класс, либо имеющий одно из *специальных значений*: ````i-```` (общие и/или служебные стили) или ````js-```` невизуальный класс, существующий *исключительно* для обработки с помощью JavaScript. В данном руководстве используется префикс ````csg-````, относящийся к теме CodeStyleGuide
- ````componentPrefix-```` - префикс, определяющий, к какому компоненту относится данный класс
- ````blockName```` - название смыслового блока верстки
- ````_modifier```` - модификатор, обозначающий определенное *состояние* блока (````_selected````, ````_active````, ````_disabled```` и т. д.)

*ПРИМЕР:*
````
csg-news-newsList // Список новостей компонента news темы оформления air
csg-news-newsList__article // Новость в списке новостей компонента news темы оформления air
csg-news-newsList__article__header // Заголовок новости в списке новостей компонента news темы оформления air
csg-news-newsList__article__header_hot // Заголовок горячей новости в списке новостей компонента news темы оформления air
````

====

**Запрещено** использовать символы ````-```` и ````_```` в названиях смысловых блоков. Они заререзвированы как разделители

====

Названия смысловых блоков **должны** быть в camelCase.

*ПЛОХО:*
````
csg-news-newslist

csg-flights-flight__shortinfo__departureDate
```` 
*ХОРОШО:*
````
csg-news-newsList

csg-flights-flight__shortInfo__departureDate
````

----

### CSS + Stylus ###

**Обязательно** использование двоеточий после названия свойства

====

**Обязательно** использование точки с запятой после значения свойства

====

**Обязательно** использование фигурных скобок для выделения блока

====

Каждое свойство **должно** размещаться на отдельной строке 

====

Индентация **обязательна**

====

**Запрещено** вешать стили на что-либо кроме классов

====

**Запрещено** вешать стили на классы с префиксом ````js-````

====

**Не рекомендуется** использование ````float```` там, где можно обойтись ````display: inline-block;```` либо ````display: table-cell;````

----

#### Структура файлов ####

Все цвета, размеры и т. п. **должны** быть вынесены в отдельный файл ````_vars.styl````.

====

Стили, относящиеся к модулям и их крупным частям **должны** быть разнесены по файлам с человекопонятными названиями

*ПРИМЕР:*
````
news_newslist.styl
news_article.styl
````

====

Все подключаемые файлы **должны** лежать в папке ````css/blocks````

====

Основной .styl-файл, который будет компилироваться **должен** иметь имя ````style.styl````, содержать исключительно подключения других .styl-файлов с комментариями и располагаться в папке ````css/````

====

**Запрещено** подключать файлы куда-либо кроме ````style.styl````

====

**Запрещено** подключать файлы с расширением ````.css````

====

**Запрещено** вешать стили на один и тот-же класс в двух разных местах

====

**Не рекомендуется** использовать ````@extend```` от не-служебных классов

----

#### Компиляция stylus ####

Компиляцию stylus-а **необходимо** проводить с указанием ключей ````-c```` и ````--include-css````

----

### Smarty ###

Расширение файла шаблона - **строго** ````.tpl````

====

Все шаблоны **должны** размещаться в соответствующих папках темы и вложенной в нее папке компонента.

====

**Запрещено** явно указывать тему, из которой берется шаблон

*ПЛОХО:*
```smarty
{include file="../../themes/someTheme/some/path/to/template.tpl"}
```
*ХОРОШО:*
```smarty
{include file="some/path/to/template.tpl"}
```

====

В начале и конце файла **обязательно** указание специальных маркерных HTML-комментариев, говорящих о том, к какому компоненту относится файл, к какой теме оформления принадлежит и где находится

*ПРИМЕР:*
```html
<!-- BEGIN c:ComponentName t:ThemeName /some/path/to/template.tpl -->

<!-- snip -->

<!-- END c:ComponentName t:ThemeName /some/path/to/template.tpl -->
```

----

#### Модификаторы и функции ####

При создании модификатора **обязательно** указывать в комментариях примеры использования

====

**Рекомендуется** вместо модификаторов создавать функции, принимающие некоторое количество именованных параметров. Полное описание параметров **обязательно**

----

### git ###

Т. к. не выработан git-flow, данный раздел является обзорным, не может и не должен определять порядок работы с системой контроля версий git

====

При создании ветки **обязательно** указание номера тикета первыми символами, после которого идет краткое описание решаемой задачи

====

**Запрещено** использовать символ ````#```` в названии ветки

**Обоснование:** некоторые IDE жестоко бажат при работе с подобными ветками

*ПРИМЕР:* ````1234-authorization_refactor````

====

Каждый коммит **должен** содержать номер тикета, проблема котрого решается этим коммитом

====

**Не рекомендуется** коммитить решение нескольких проблем в рамках одного коммита

====

**Обязательно** указание хеша оригинального коммита при [cherry-pick](http://git-scm.com/docs/git-cherry-pick)-е

====

Если cherry-pick применяется к нескольким коммитам, решающим одну и ту-же проблему, настоятельно **рекомендуется** перед операцией [push](http://git-scm.com/docs/git-push) [аммендить коммиты](http://www.commandlinefu.com/commands/view/1249/add-forgotten-changes-to-the-last-git-commit), при этом сохранение всех хешей оригинальных коммитов **обязательно**