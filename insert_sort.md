###  插入排序 php
```php
function insert_sort($arr) {
    $length = count($arr);

    for($i=1; $i < $length; $i++) {
        $tmp = $arr[$i];
        for($j = $i - 1; $j > 0 ; $j--) {
            if($tmp < $arr[$j]) {
                $arr[$j+1] = $arr[$j];
                $arr[$j] = $tmp;
            } else {
                break;
            }
        }
    }
    return $arr;
}

$arr = [
    2, 6, 8,7
];
print_r(insert_sort($arr));
```
