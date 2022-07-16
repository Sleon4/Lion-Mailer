# Lion-Mailer
## Library created for easy email sending based on [PHPMailer](https://github.com/PHPMailer/PHPMailer).

[![Latest Stable Version](http://poser.pugx.org/lion-framework/lion-mailer/v)](https://packagist.org/packages/lion-framework/lion-mailer) [![Total Downloads](http://poser.pugx.org/lion-framework/lion-mailer/downloads)](https://packagist.org/packages/lion-framework/lion-mailer) [![License](http://poser.pugx.org/lion-framework/lion-mailer/license)](https://packagist.org/packages/lion-framework/lion-mailer) [![PHP Version Require](http://poser.pugx.org/lion-framework/lion-mailer/require/php)](https://packagist.org/packages/lion-framework/lion-mailer)

## Install
```shell
composer require lion-framework/lion-mailer
```

## Usage
```php
require_once("vendor/autoload.php");

use LionMailer\Mailer;
use LionMailer\DataMailer\Attach;

Mailer::init([
	'info' => [
		'debug' => 0,
		'host' => 'smtp.example',
		'port' => 0,
		'email' => "example@example.com",
		'user_name' => "example - user",
		'password' => "--example--",
		'encryption' => false // true for ssl, false for tls
	]
]);

$request = Mailer::send(
	Attach::newAttach(
		['example@gmail.com', 'User - Dev'], // addAdress
		['example2@gmail.com', 'User - Reply to'],  // addReplyTo
		null, // addCC
		null, // addBCC
		null // addAttachment
	),
	Mailer::newInfo(
		'example', // subject
		'example', // body
		'example' // alt body
	)
);

var_dump($request);

// or

$request = Mailer::send(
	Attach::newAttach(
		['example@gmail.com', 'User - Dev'], // addAdress
		['example2@gmail.com', 'User - Reply to'],  // addReplyTo
		null, // addCC
		null, // addBCC
		[$file], // addAttachment - optional: [$file, 'namefile.ext']
	),
	Mailer::newInfo(
		'example', // subject
		'example', // body
		'example' // alt body
	)
);

var_dump($request);
```

### 1. INSTRUCTIONS
The mailer class must be initialized using the init function and its respective parameters, debug 0 indicates that no type of information should appear on the screen when sending emails, deleting this property will cause information about the sending process to appear by default. <br>
```php
Mailer::init([
	'info' => [
		'debug' => 0,
		'host' => 'smtp.example',
		'port' => 0,
		'email' => "example@example.com",
		'user_name' => "example - user",
		'password' => "--example--",
		'encryption' => false // true for ssl, false for tls
	]
]);
```

The info property relates all kinds of user credentials for sending correct email.
```php
'info' => [
	'debug' => 0,
	'host' => 'smtp.example',
	'port' => 0,
	'email' => "example@example.com",
	'user_name' => "example - user",
	'password' => "--example--",
	'encryption' => false // true for ssl, false for tls
]
```

### 2. SEND EMAILS TO MULTIPLE ACCOUNTS
```php
$request = Mailer::sendGroup(
	Attach::newGroupAttach([
		['person1@example.com', 'person1'], // addAdress
		['person1@example.com', 'person2'], // addAdress
	]),
	Mailer::newGroupInfo(
		["example@example.com", 'example - user'], // addReplyTo
		null, // addCC
		null, // addBCC
		null, // addAttachment
		'example', // subject
		'example', // body
		'example' // alt body
	)
);

var_dump($request);
```

## Credits
[PHPMailer](https://github.com/PHPMailer/PHPMailer)

## License
Copyright © 2022 [MIT License](https://github.com/Sleon4/Lion-Mailer/blob/main/LICENSE)