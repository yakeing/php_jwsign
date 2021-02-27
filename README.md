# Json Wed Sign (RSA)

This is a function wrapping through the `Openssl` to sign and validate the data, which ensures the integrity and security of the original data.

### Travis CI badge

[![Travis-ci](https://api.travis-ci.com/yakeing/php_jwsign.svg?branch=master)](https://travis-ci.com/yakeing/php_jwsign)

### codecov badge

[![codecov](https://codecov.io/gh/yakeing/php_jwsign/branch/master/graph/badge.svg)](https://codecov.io/gh/yakeing/php_jwsign)

### Github badge

[![Downloads](https://badging.now.sh/github/downloads/yakeing/php_jwsign?icon=github)](../../)
[![Size](https://badging.now.sh/github/size/yakeing/php_jwsign?icon=github)](src)
[![tag](https://badging.now.sh/github/tag/yakeing/php_jwsign?icon=github)](../../releases)
[![license](https://badging.now.sh/static/label/license/555/MPL-2.0/fe7d37?icon=github)](LICENSE)
[![languages](https://badging.now.sh/static/label/language/555/PHP/34abef?icon=github)](../../search?l=php)

### Installation

Use [Composer](https://getcomposer.org) to install the library.
Of course, You can go to [Packagist](https://packagist.org/packages/yakeing/php_jwsign) to view.

```

    $ composer require yakeing/php_jwsign

```

### JWSign init

```php

    $jwsign = new jwsign();
    $jwsign->SetPrivate($accesskey);

```

### Get Pubkey

```php

    $Pubkey = $jwsign->GetPubkey();

    var_dump($Pubkey);
    array(3) {
        ["pub"]=>string(451) "-----BEGIN PUBLIC KEY-----\nMIIBIjA....NjQIDAQA\n-----END PUBLIC KEY----"
        ["bits"]=>int(2048)
        ["kid"]=>string(43) "cjbdM-CeRfP...5BNYQuksIIgmk"
    }

```

### Sign Message

```php

    $Message = base64_encode('
        {
            "method":"pay",
            "charset":"utf-8",
            "version":"1.0",
            "token":"NAM...YgV"
        }
    ');

    $JsonStr = $jwsign->SignMessage($Message);

    var_dump($JsonStr);
    string(557) "{
        "message":"eyJtZXRiO...Z1YifQ==",
        "nonce":"MmlhaDE1MD...MTgwLjEwNDc1OTAw",
        "kid":"cjOdM-CORfPGa...j-0I5BNYQuksIIgmk",
        "sign":"hXvBULK2wSroVFZ...-HYHG7l8Epixikg"
        }"

```

### Pubkey Verify

```php

    $value = '{
        "message":"eyJtZXRiO...Z1YifQ==",
        "nonce":"MmlhaDE1MD...MTgwLjEwNDc1OTAw",
        "kid":"cjOdM-CORfPGa...j-0I5BNYQuksIIgmk"
        }';
    $sign = 'hXvBULK2wvSroVFZ...-HKbHGDYHG7l8Epixikg';
    $pub = '-----BEGIN PUBLIC KEY-----\nMIIBIjA....NjQIDAQA\n-----END PUBLIC KEY----';

    $Str = $jwsign->PubkeyVerify($value, $sign, $pub);

    var_dump($Str);
    bool(true)

```

### Get Message

```php

    $value = '{
        "message":"eyJtZXRiO...Z1YifQ==",
        "nonce":"MmlhaDE1MD...MTgwLjEwNDc1OTAw",
        "kid":"cjOdM-CORfPGa...j-0I5BNYQuksIIgmk"
        }';
    $Str = json_decode($value, true);

    var_dump(base64_decode($Str['message']));
    string(100) "{
            "method":"pay",
            "charset":"utf-8",
            "version":"1.0",
            "token":"NAM...YgV"
        }"

```

[Sponsor](https://github.com/yakeing/Documentation/blob/master/Sponsor/README.md)
---
If you've got value from any of the content which I have created, then I would very much appreciate your support by payment donate.

[![Sponsor](https://badging.now.sh/static/label/Sponsor/EA4AAA?icon=heart)](https://github.com/yakeing/Documentation/blob/master/Sponsor/README.md)

Author
---

weibo: [yakeing](https://weibo.com/yakeing)

twitter: [yakeing](https://twitter.com/yakeing)
