### 冒泡排序
```php
<?php
// bubble_sort
function bubble_sort($arr) {
    if(empty($arr)) {
        return $arr;
    }
    $length = count($arr);
    // kongzhi 冒泡次数
    for($i = 0; $i < $length; $i++) {
        // 冒出一个数，需要比较的次数
        for($k= 0; $k< $length-$i; $k++) {
            if(isset($arr[$k])  && isset($arr[$k+1]) && $arr[$k] > $arr[$k+1]) {
                $tmp = $arr[$k+1];
                $arr[$k+1] = $arr[$k];
                $arr[$k] = $tmp;
            }
        }
    }
    return $arr;
}

$arr = [
    1,43,23,45, 56, 13, 17
];
print_r(bubble_sort($arr));
```
