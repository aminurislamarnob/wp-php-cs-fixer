# PHP CS Fixer: WordPress fixers

A set of custom fixers for [PHP CS Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer), specially for WordPress. This is the modified version of [tareq1988/wp-php-cs-fixer](https://github.com/tareq1988/wp-php-cs-fixer) which is made by Tareq Hasan, Founder & CTO of weDevs.

### What is php-cs-fixer?

The [php-cs-fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer) or [PHP Coding Standards Fixer](https://cs.symfony.com/) is an awesome tool created by the super awesome people at [Symfony](https://symfony.com/).

It helps your PHP code/repository to follow a certain coding standard defined by you team.

### What are WordPress Fixers?

WordPress uses a bit different coding standard from the rest of the world. It doesn't follow PSR standards yet.

The aim of this WordPress specific fixers is to allow WordPress developers to standardize their code according to the [WordPress Coding Standard](https://make.wordpress.org/core/handbook/best-practices/coding-standards/php/).

#### Available Fixers

1. **Space Inside Parenthesis**: This fixer ensures that when defining functions, if/else blocks, or control structures which have parenthesis, a space after the starting parenthesis and before the ending parenthesis exists. Rule name: `AiArnob/space_inside_parenthesis`.
2. **Blank Line After Class Opening**: PSR standards have the class opening brace on a new line, WordPress follows the same line standard. This ensures after the opening brace, one blank line exists (equals to two `\n`). Rule name: `AiArnob/blank_line_after_class_opening`.

## Installation
PHP CS Fixer: PHP CS fixers can be installed by running(as dev dependency):
```bash
composer require friendsofphp/php-cs-fixer
```

WP PHP CS Fixer: custom fixers can be installed by running:

```bash
composer require --dev aminurislamarnob/wp-php-cs-fixer
```

## Other Settings
Add the below packages to composer.json file inside `"require-dev": {}`
```bash
"wp-coding-standards/wpcs": "dev-master",
"phpcompatibility/php-compatibility": "*",
"phpcompatibility/phpcompatibility-wp": "*",
"dealerdirect/phpcodesniffer-composer-installer": "^0.7"
``` 

Add the below config to composer.json file inside `"config": {}`
```bash
"allow-plugins": {
    "dealerdirect/phpcodesniffer-composer-installer": true
}
```
***Finally you need to run the command `composer update` to install dependency packages.***

## Usage
Create file (`.php-cs-fixer.php`) to your plugin directory and copy paste the below code to the file:

```diff
<?php
// add the custom fixers
require_once __DIR__ . '/vendor/aminurislamarnob/wp-php-cs-fixer/loader.php';

$finder = PhpCsFixer\Finder::create()
    ->exclude('node_modules')
    ->exclude('vendors')
    ->in( __DIR__ )
;

$config = new PhpCsFixer\Config();
$config
    ->registerCustomFixers([
        new AiArnob\Fixer\SpaceInsideParenthesisFixer(),
        new AiArnob\Fixer\BlankLineAfterClassOpeningFixer()
    ])
    ->setRiskyAllowed(true)
    ->setUsingCache(false)
    ->setRules( AiArnob\Fixer\Fixer::rules() )
    ->setFinder( $finder )
;

return $config;
```

### Fix by Run Command
Upon configuring everything, run `php-cs-fixer fix` from the commandline.
