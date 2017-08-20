# dart-string-mask
A string formatter and validator based on masks

Port of https://github.com/the-darc/string-mask to Dart

## Features and bugs

Please file feature requests and bugs at the [issue tracker][tracker].

A string formatter and validator based on masks.

## INSTALLATION

**With pub.dartlang.org!**

```yaml
#dependencies:
#  string_mask: ^0.0.1
```

## SPECIAL MASK CHARACTERS

Character | Description
--- | ---
`0` | Any numbers
`9` | Any numbers (Optional)
`#` | Any numbers (recursive)
`A` | Any alphanumeric character
`a` | Any alphanumeric character (Optional) __Not implemented yet__
`S` | Any letter
`U` | Any letter (All lower case character will be mapped to uppercase)
`L` | Any letter (All upper case character will be mapped to lowercase)
`$` | Escape character, used to escape any of the special formatting characters.

### Special characters types

 - **Optional characters:** Used to parse characters that cold exist in the source string or not. See [Date and time](#date-and-time).

 - **Recursive characters:** Used to parse patterns that repeat in the end or in the start of the source string. See [Two decimal number with thousands separators](#two-decimal-number-with-thousands-separators)

> _Note: Any character of the mask positioned after a recursive character will be handled as a non special character._

## USAGE

 **Use it creating an mask instance with the StringMask contructor:**

```dart
/**
 * - optionsObject parameter is optional in the constructor
 * - apply will return the a masked string value
 * - validate will return `true` if the string matchs the mask
 */
var mask = new StringMask('some mask', options: new MaskOptions()); //optionsObject is optional
var maskedValue = mask.apply('some value string');
var isValid = mask.validate('some value string to validate');
```

**Or by the static interface:**

```dart
/**
 * - optionsObject parameter is optional in all methods
 * - apply will return the a masked string value
 * - validate will return `true` if the string matchs the mask
 * - process will return a object: {result: <maskedValue>, valid: <isValid>}
 */
var maskedValue = StringMask.apply_('some value string', 'some mask', optionsObject); 
var isValid = StringMask.validate_('some value string', 'some mask', optionsObject);
var result = StringMask.process_('some value string', 'some mask', optionsObject);
```

### Some masks examples

#### Number

```dart
    var maskOptions = new MaskOptions()
      ..reverse = true;

    var formatter = new StringMask("#0", options: maskOptions);
    var result = formatter.apply('123'); // 123
```

#### Two decimal number with thousands separators

```dart
    var maskOptions = new MaskOptions()
      ..reverse = true;

    var formatter = new StringMask('#.##0,00', options: maskOptions);
    var result = formatter.apply('100123456'); // 1.001.234,56
    var result2 = formatter.apply('6'); // 0,06
```

#### Phone number

```dart
    var formatter = new StringMask('+00 (00) 0000-0000');
    var result = formatter.apply('553122222222'); // +55 (31) 2222-2222
```

#### Percentage

```dart
    var maskOptions = new MaskOptions()
      ..reverse = true;

    var formatter = new StringMask('#.##0,00', options: maskOptions);
    var result = formatter.apply('001'); // 0,01%
```

#### Brazilian CPF number

```dart
    var formatter = new StringMask('000.000.000-00');
    var result = formatter.apply('12965815620'); // 129.658.156-20
```

#### Date and time

```dart
    var formatter = new StringMask('90/90/9900');
    var result = formatter.apply('1187'); // 1/1/87
```

#### Convert Case

```dart
    var formatter = new StringMask('UUUUUUUUUUUUU');
    var result = formatter.apply('To Upper Case'); // TO UPPER CASE
```

```dart
    var formatter = new StringMask('LLLLLLLLLLLLL');
    var result = formatter.apply('To Lower Case'); // to lower case
```

#### International Bank Number

```Dart
    var formatter = new StringMask('UUAA AAAA AAAA AAAA AAAA AAAA AAA');
    var result = formatter.apply('FR761111BBBB69410000AA33222');
	// result: FR76 1111 BBBB 6941 0000 AA33 222
```

## CONTRIBUTING

We'd love for you to contribute to our source code! We just ask to: 

 - Write tests for the new feature or bug fix that you are solving
 - Ensure all tests pass before send the pull-request (Use: `$ gulp pre-push`)
 - Use commit messages following the commit conventions of [angular.js Git Commit Guidelines](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#commit)
 - Pull requests will not be merged if:
   - has not unit tests
   - reduce the code coverage
   - not passing in the `$gulp pre-push` task

## LICENSE

Copyright (c) 2016 Daniel Campos

Licensed under the MIT license.
  
  
