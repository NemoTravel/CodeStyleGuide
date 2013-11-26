# Code Style Guide v 1.0 #

## Что такое "хорошо" и что такое "плохо" ##

### Оглавление ###

1. Введение
2. Общие положения по коду (Общее для PHP и JavaScript)
3. Общие положения по комментированию кода
4. PHP
5. JavaScript
3. HTML
4. CSS + Stylus
5. Smarty
6. Сторонние фронтенд-библиотеки и инструмент
8. SQL
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

### Общие положения по коду (Общее для PHP и JavaScript) ###

Кодировка - **строго** UTF-8

Перенос строки - **строго** Unix-style (LF)

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

Отступ для индентации кода - **строго** табулятор (Tab). (Некоторые интерпретаторы данного документа могут отображать Tab-ы пробелами)
См. 

**Рекомендуется** использовать Tab шириной в 4 пробела (Все IDE разрешают настраивать ширину Tab-а)

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

#### Константы и булевы переменные ####

Все константы **должны** записываться в верхнем регистре
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

#### Именование переменных, функций и классов ####

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

Односимвольные имена переменных **запрещены**. Единственным исключением являеется случай, когда переменная является итератором цикла
*ПЛОХО:*
```php
$t = time();
```
*ХОРОШО:*
```php
for ($i = 0, $c = count($elements); $i < c; $i++) { /* snip */ }
```

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

**Должны** использоваться ["египетские скобки" (Стиль «K&R»)](http://ru.wikipedia.org/wiki/%D0%9E%D1%82%D1%81%D1%82%D1%83%D0%BF_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)).

Если скобки можно опустить, они **должны** быть.

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

**Допускается** "сворачивание" простейших геттеров/сеттеров в одну строку.
*ПЛОХО:*
```php
// Too much code is "hidden"
public function getChildren () { if ($this->hasChildren()) { return $this->children; } return array(); }
```
*ХОРОШО:*
```php
public function getChildren () { return $this->children; }
```

**Запрещено** использование логических операторов в символьном виде
*ПЛОХО:*
```smarty
{if $object->hasChildren() or $forceChildrenDisplay}
```
*ХОРОШО:* 
```smarty
{if $object->hasChildren() || $forceChildrenDisplay}
```

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

[Yoda conditions](http://ru.wikipedia.org/wiki/%D0%A3%D1%81%D0%BB%D0%BE%D0%B2%D0%B8%D1%8F_%D0%99%D0%BE%D0%B4%D1%8B) **рекомендуются** к применению:
```php
if ('use' == $the_force) {
    $victorious = You::will($be);
}
```

### Общие положения по комментированию кода ###

Язык комментариев - настоятельно **рекомендуется** английский.

Однострочные комментарии размещаются **строго** отдельной строкой с пустой строкой сверху. Единственным исключением является случай, когда комментарий вставляется перед ``` else``` или ``` elseif```. В таком случае пустая строка перед комментарием **запрещена**.
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

**Обязательно** использование ````@return```` для функций/методов, возвращающих значение

Настоятельно **рекомендуется** использование ````@throws```` в документации к функции/методу, бросающим исключения

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

**Допускаются** "пасхальные яйца" в комментарих к коду, тем не менее, юмор должен быть сдержанным и обязательно соблюдение вышеописанных правил комментирования.
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

Использование комментариев
````TODO```` и ````FIXME```` настоятельно **рекомендуется**.
Применение:
````FIXME```` используется для указания на проблему
````TODO```` используется для указание на решение проблемы
*ПРИМЕР:*
```php
// FIXME this code sometimes throw an exception. Need to figure out why
```
```php
// TODO need to check for available slots here in order to avoid unexpected exception throwing
```

При комментировании кусков кода **обязательно** указание времени, причины и имени/корпоративной почты комментирующего. Ненужные куски кода **должны** удаляться, а не комментироваться.
*ПРИМЕР:*
```smarty
{* v.poopking 13.06.2013 07:40 : Commented out due to bugs in backend processing. Return when #123123 is fixed *}
{*<div class="some-class-name__here">
    {include file='some_template.tpl'}
</div>*}
```
**Обоснование:** закомментированный код будет удаляться. Чтобы этого не произошло стоит указывать причину, по которой код комментируется, и должен оставаться в файле.

### PHP ###

Строжайше **запрещено** использование конструкций типа ````$$variable````. Автор полагает, что это правило в объяснении не нуждается

**Запрещено** использование PHP short tag (````<? /* snip */ ?>````  ````<?= /* snip */ ?>).
Хорошее объяснение [тут](http://programmers.stackexchange.com/questions/151661/is-it-bad-practice-to-use-tag-in-php#answer-151694).

Строжайше **запрещено** использование закрывающего PHP тега (````?>````)

#### Циклы ####

Настоятельно **рекомендуется** использовать следующую конструкцию для циклов ```for```:
```php
for ($i = 0, $c = count($array); $i < $c; $i++) { /* snip */ }
```
**Обоснование:** ````count($array)```` выполняется только один раз и ее выполнение вписано в сам цикл, что есть удобно

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

#### Приведение типов ####

Не полагайтесь на приведение типов: **не рекомендуется** пользоваться конструкциями вида
```php
if ($possiblyEmptyArray) { /* snip */ }
```
если переменная не заведомо булева.