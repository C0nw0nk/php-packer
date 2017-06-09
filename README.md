php-packer
==========

A PHP version of Packer, JavaScript obfuscation library originally created by Dean Edwards, ported to PHP by Nicolas Martin.
Packed for composer and slightly extended by Thomas Lutz.

## Installation

Simply run `composer require tholu/php-packer`.

## Usage (slightly changed from previous used implementation!)

```php
<?php
require 'vendor/autoload.php';

$js = file_get_contents('test.js');

/*
 * params of the constructor :
 * $script:           the JavaScript to pack, string.
 * $encoding:         level of encoding, int or string :
 *                    0,10,62,95 or 'None', 'Numeric', 'Normal', 'High ASCII'.
 *                    default: 62 ('Normal').
 * $fastDecode:       include the fast decoder in the packed result, boolean.
 *                    default: true.
 * $specialChars:     if you have flagged your private and local variables
 *                    in the script, boolean.
 *                    default: false.
 * $removeSemicolons: whether to remove semicolons from the source script.
 *                    default: true.
 */

// $packer = new Tholu\Packer\Packer($script, $encoding, $fastDecode, $specialChars, $removeSemicolons, $encryptionKey);
$packer = new Tholu\Packer\Packer($js, 'Normal', true, false, true, 'SOMEKEY');
$packed_js = $packer->pack();
echo $packed_js;

// Define the following variable before running the unpacking script
// var UNPACK_KEY = 'SOMEKEY';
```


## Encryption

Define the following variable before running the unpacking script. Encryption key is ```WEB``` by default, and is automatically added if ```UNPACK_KEY``` is undefined.

Encryption is not secured, and is used to hide variable names or the nature of the script.

```var UNPACK_KEY = 'SOMEKEY';```
