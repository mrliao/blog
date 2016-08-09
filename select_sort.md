###  选择排序 php
```php
function select_sort($arr) {
    if (!is_array($arr) || empty($arr)) {
        return $arr;
    }
    $length = count($arr);
    for($i=0; $i < $length; $i++) {
        $p = $i;
        // 比较剩下的
        for($j=$i+1; $j < $length; $j++) {
            // 假若当前的节点大于下一个节点，那么最小的就是下一个节点的位置
            if($arr[$j] < $arr[$p]) {
                $p = $j;
            }
        }
        // 若位置不同需要交换，位置相同则不需要交换
        if($p != $i) {
            $tmp = $arr[$p];
            $arr[$p] = $arr[$i];
            $arr[$i] = $tmp;
        }
    }
    return $arr;
}
$arr = [
    8,3,5,1,10,12,11
];
print_r(select_sort($arr));
```
