### 快速排序 php
```php
// 快速排序一般时找第一个元素或者最后一个元素
function quick_sort($arr) {
    if( !is_array($arr) || empty($arr) ) {
        return $arr;
    }
    $length = count($arr);
    $baseline = $arr[0];
    $left_arr = $right_arr = [];
    for($i=1; $i < $length; $i++) {
        if($arr[$i] > $baseline) {
            $right_arr[] = $arr[$i];
        } else {
            $left_arr[] = $arr[$i];
        }
    }
    $right_arr = quick_sort($right_arr);
    $left_arr = quick_sort($left_arr);
    return array_merge($left_arr, [$baseline], $right_arr);
}

$arr = [5, 6, 1, 3, 4, 2, 8, 10];
print_r(quick_sort($arr));
```
