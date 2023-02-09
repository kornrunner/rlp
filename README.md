# rlp [![Tests](https://github.com/kornrunner/rlp/actions/workflows/tests.yml/badge.svg?branch=master)](https://github.com/kornrunner/rlp/actions/workflows/tests.yml) [![Coverage Status](https://coveralls.io/repos/github/kornrunner/rlp/badge.svg?branch=master)](https://coveralls.io/github/kornrunner/rlp?branch=master) [![Latest Stable Version](https://poser.pugx.org/kornrunner/rlp/v/stable)](https://packagist.org/packages/kornrunner/rlp)

Recursive Length Prefix Encoding in PHP.

# Install

Set minimum stability to dev
```
composer require kornrunner/rlp
```

# Usage

RLP encode:

```php
use kornrunner\RLP\RLP;

$rlp = new RLP;
// c483646f67
$encoded = $rlp->encode(['dog']);

// 83646f67
$encoded = $rlp->encode('dog');
```

RLP decode:

```php
use kornrunner\RLP\RLP;
use kornrunner\RLP\Types\Str;

$rlp = new RLP;
$encoded = $rlp->encode(['dog']);

// only accept 0x prefixed hex string
$decoded = $rlp->decode('0x' . $encoded);

// show 646f67
echo $decoded[0];

// show dog
echo hex2bin($decoded[0]);

// or you can
echo Str::decodeHex($decoded[0]);
```

# API

### kornrunner\RLP\RLP

#### encode

Returns recursive length prefix encoding of given inputs.

`encode(mixed $inputs)`

Mixed inputs - array of string, integer or numeric string.

> Note: output is not zero prefixed.

###### Example

* Encode array of string.

```php
use kornrunner\RLP\RLP;

$rlp = new RLP;
$encoded = $rlp->encode(['kornrunner', 'ethereum', 'solidity']);
```

#### decode

Returns array recursive length prefix decoding of given data.

`decode(string $input)`

String input - recursive length prefix encoded string.

> Note: output is not zero prefixed.

###### Example

* Decode recursive length prefix encoded string.

```php
use kornrunner\RLP\RLP;
use kornrunner\RLP\Types\Str;

$rlp = new RLP;
$encoded = $rlp->encode(['kornrunner', 'ethereum', 'solidity']);
$decoded = $rlp->decode('0x' . $encoded);

// echo kornrunner
echo hex2bin($decoded[0]);

// echo ethereum
echo hex2bin($decoded[1]);

// echo solidity
echo hex2bin($decoded[2]);

// or you can
echo Str::decodeHex($decoded[0]);
echo Str::decodeHex($decoded[1]);
echo Str::decodeHex($decoded[2]);
```

# License

MIT
