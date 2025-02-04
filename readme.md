This is a barcode generation package inspired by <https://github.com/tecnickcom/TCPDF>. Actually, I use that package's underline classes for generating barcodes. This package is just a wrapper of that package and adds compatibility with Laravel 5.

I used the following classes of that package.

- src/Stillzombie/Barcode/Datamatrix.php (include/barcodes/datamatrix.php)
- src/Stillzombie/Barcode/DNS1D.php (tcpdf_barcodes_1d.php)
- src/Stillzombie/Barcode/DNS2D.php (tcpdf_barcodes_2d.php)
- src/Stillzombie/Barcode/PDF417.php (include/barcodes/pdf417.php)
- src/Stillzombie/Barcode/QRcode.php (include/barcodes/qrcode.php)

[Read More on TCPDF website](http://www.tcpdf.org)

# This package is compatible with Laravel 5.2, 5.3 and 5.4 and Laravel 6.0

This package relies on [php-gd](http://php.net/manual/en/book.image.php) extension. So, make sure it is installed on your machine.

## Installation

Begin by installing this package through Composer. Just run following command to terminal-

```
composer require stillzombie/barcode
```

You can also edit your project's `composer.json` file to require `stillzombie/barcode`.

```
"require": {
    ...
    "stillzombie/barcode": "^5.3"
}
```

For Laravel 5.0 and 5.1 use this-

```
"require": {
    ...
    "stillzombie/barcode": "^5.1"
}
```

For Laravel 4.0, 4.1 and 4.2 use this-

```
"require": {
    ...
    "stillzombie/barcode": "^4.2"
}
```

Next, update Composer from the Terminal:

```
composer update
```

Once this operation completes, the final step is to add the service provider. Open `config/app.php`, and add a new item to the providers array.

```php
'providers' => [
    ...
    Stillzombie\Barcode\BarcodeServiceProvider::class,
    ...
]
```

For version 4.* add these lines on `app/config/app.php` file-

```php
'providers' => array(
    ...
    'Stillzombie\Barcode\BarcodeServiceProvider',
)
```

If you want to change Bar-code's settings (Store Path etc.), you need to publish its config file(s). For that you need to run in the terminal-

```
# Laravel 5.x
php artisan vendor:publish

# Laravel 4.x
php artisan config:publish stillzombie/barcode
```

Make sure you have write permission to the storage path. By default it sets to `/storage` folder.

Now add the alias.

```php
'aliases' => [
    ...
    'DNS1D' => Stillzombie\Barcode\Facades\DNS1DFacade::class,
    'DNS2D' => Stillzombie\Barcode\Facades\DNS2DFacade::class,
]
```

For version 4.2 alias will be like this-

```php
'aliases' => array(
    ...
    'DNS1D' => 'Stillzombie\Barcode\Facades\DNS1DFacade',
    'DNS2D' => 'Stillzombie\Barcode\Facades\DNS2DFacade',
)
```

Bar-code generator like Qr Code, PDF417, C39,C39+, C39E,C39E+, C93, S25,S25+, I25,I25+, C128,C128A,C128B,C128C, 2-Digits UPC-Based Extention, 5-Digits UPC-Based Extention, EAN 8,EAN 13, UPC-A,UPC-E, MSI (Variation of Plessey code)

generator in html, png embedded base64 code and SVG canvas

```php
echo DNS1D::getBarcodeSVG("4445645656", "PHARMA2T");
echo DNS1D::getBarcodeHTML("4445645656", "PHARMA2T");
echo '<img src="data:image/png,' . DNS1D::getBarcodePNG("4", "C39+") . '" alt="barcode"   />';
echo DNS1D::getBarcodePNGPath("4445645656", "PHARMA2T");
echo '<img src="data:image/png;base64,' . DNS1D::getBarcodePNG("4", "C39+") . '" alt="barcode"   />';
```

```php
echo DNS1D::getBarcodeSVG("4445645656", "C39");
echo DNS2D::getBarcodeHTML("4445645656", "QRCODE");
echo DNS2D::getBarcodePNGPath("4445645656", "PDF417");
echo DNS2D::getBarcodeSVG("4445645656", "DATAMATRIX");
echo '<img src="data:image/png;base64,' . DNS2D::getBarcodePNG("4", "PDF417") . '" alt="barcode"   />';
```

## Width and Height example

```php
echo DNS1D::getBarcodeSVG("4445645656", "PHARMA2T",3,33);
echo DNS1D::getBarcodeHTML("4445645656", "PHARMA2T",3,33);
echo '<img src="' . DNS1D::getBarcodePNG("4", "C39+",3,33) . '" alt="barcode"   />';
echo DNS1D::getBarcodePNGPath("4445645656", "PHARMA2T",3,33);
echo '<img src="data:image/png;base64,' . DNS1D::getBarcodePNG("4", "C39+",3,33) . '" alt="barcode"   />';
```

## Color

```php
echo DNS1D::getBarcodeSVG("4445645656", "PHARMA2T",3,33,"green");
echo DNS1D::getBarcodeHTML("4445645656", "PHARMA2T",3,33,"green");
echo '<img src="' . DNS1D::getBarcodePNG("4", "C39+",3,33,array(1,1,1)) . '" alt="barcode"   />';
echo DNS1D::getBarcodePNGPath("4445645656", "PHARMA2T",3,33,array(255,255,0));
echo '<img src="data:image/png;base64,' . DNS1D::getBarcodePNG("4", "C39+",3,33,array(1,1,1)) . '" alt="barcode"   />';
```

## Show Text

```php
echo DNS1D::getBarcodeSVG("4445645656", "PHARMA2T",3,33,"green", true);
echo DNS1D::getBarcodeHTML("4445645656", "PHARMA2T",3,33,"green", true);
echo '<img src="' . DNS1D::getBarcodePNG("4", "C39+",3,33,array(1,1,1), true) . '" alt="barcode"   />';
echo DNS1D::getBarcodePNGPath("4445645656", "PHARMA2T",3,33,array(255,255,0), true);
echo '<img src="data:image/png;base64,' . DNS1D::getBarcodePNG("4", "C39+",3,33,array(1,1,1), true) . '" alt="barcode"   />';
```

## 2D Barcodes

```php
echo DNS2D::getBarcodeHTML("4445645656", "QRCODE");
echo DNS2D::getBarcodePNGPath("4445645656", "PDF417");
echo DNS2D::getBarcodeSVG("4445645656", "DATAMATRIX");
```

## 1D Barcodes

```php
echo DNS1D::getBarcodeHTML("4445645656", "C39");
echo DNS1D::getBarcodeHTML("4445645656", "C39+");
echo DNS1D::getBarcodeHTML("4445645656", "C39E");
echo DNS1D::getBarcodeHTML("4445645656", "C39E+");
echo DNS1D::getBarcodeHTML("4445645656", "C93");
echo DNS1D::getBarcodeHTML("4445645656", "S25");
echo DNS1D::getBarcodeHTML("4445645656", "S25+");
echo DNS1D::getBarcodeHTML("4445645656", "I25");
echo DNS1D::getBarcodeHTML("4445645656", "I25+");
echo DNS1D::getBarcodeHTML("4445645656", "C128");
echo DNS1D::getBarcodeHTML("4445645656", "C128A");
echo DNS1D::getBarcodeHTML("4445645656", "C128B");
echo DNS1D::getBarcodeHTML("4445645656", "C128C");
echo DNS1D::getBarcodeHTML("44455656", "EAN2");
echo DNS1D::getBarcodeHTML("4445656", "EAN5");
echo DNS1D::getBarcodeHTML("4445", "EAN8");
echo DNS1D::getBarcodeHTML("4445", "EAN13");
echo DNS1D::getBarcodeHTML("4445645656", "UPCA");
echo DNS1D::getBarcodeHTML("4445645656", "UPCE");
echo DNS1D::getBarcodeHTML("4445645656", "MSI");
echo DNS1D::getBarcodeHTML("4445645656", "MSI+");
echo DNS1D::getBarcodeHTML("4445645656", "POSTNET");
echo DNS1D::getBarcodeHTML("4445645656", "PLANET");
echo DNS1D::getBarcodeHTML("4445645656", "RMS4CC");
echo DNS1D::getBarcodeHTML("4445645656", "KIX");
echo DNS1D::getBarcodeHTML("4445645656", "IMB");
echo DNS1D::getBarcodeHTML("4445645656", "CODABAR");
echo DNS1D::getBarcodeHTML("4445645656", "CODE11");
echo DNS1D::getBarcodeHTML("4445645656", "PHARMA");
echo DNS1D::getBarcodeHTML("4445645656", "PHARMA2T");
```

# Running without Laravel

You can use this library without using Laravel.

Example:

```
use \Stillzombie\Barcode\DNS1D;

$d = new DNS1D();
$d->setStorPath(__DIR__."/cache/");
echo $d->getBarcodeHTML("9780691147727", "EAN13");
```

## License

This package is published under `GNU LGPLv3` license and copyright to [Victor Casanas](http://stillzombie.im). Original Barcode generation classes were written by Nicola Asuni. The license agreement is on project's root.

License: GNU LGPLv3<br>
Package Author: [Victor Casanas](ing.vic.casanas@gmail.com)<br>
Original Barcode Class Author: [Nicola Asuni](http://www.tcpdf.org)<br>
Package Copyright: Victor Casanas<br>
Barcode Generation Class Copyright:<br>
Nicola Asuni<br>
Tecnick.com LTD<br>
www.tecnick.com
