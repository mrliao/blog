```php
final class Product {
    private static $_instance;

    public $mix;

    /**
     * Return self instance
     * @return self
     */
    public static function getInstance() {
        if(!( self::$_instance instanceof self )) {
            self::$_instance = new self();
        }
        return self::$_instance;
    }

    private function __construct() {

    }

    private function __clone() {

    }
}

$firstProduct = Product::getInstance();
$secondProduct = Product::getInstance();

$firstProduct->mix = 'test';
$secondProduct->mix = 'example';

print_r($firstProduct->mix);
print_r($secondProduct->mix);
```
