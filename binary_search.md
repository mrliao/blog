### 二分查找 PHP
```php
// 二分查找法，数组前提时拍好序的，排序可以使用bubble_sort,insert_sort, select_sort, quick_sort
function binary_search($arr, $find_val) {
    if( (!is_array($arr) || empty($arr))) {
        return 'can not find';
    }
    $left_index = 0;
    $right_index = count($arr) - 1;
    $middle_index = round($left_index + $right_index)/2;

    if($find_val > $arr[$middle_index]) {
        return  binary_search($arr, $find_val, $middle_index + 1, $right_index);
    } else if($find_val < $arr[$middle_index]) {
        return  binary_search($arr, $find_val, $left_index, $middle_index - 1);
    } else {
        return $find_val . ' is found at ' . $middle_index;
    }
}
```
