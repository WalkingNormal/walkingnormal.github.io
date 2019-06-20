---
title: 移除多维数组中的指定键名
date: 2019-06-20
categories:
tags: 
- PHP 
- array
---

> 利用回调函数删除多维数组中的指定键名。

数组示例.要删除数组中的 `parent_menu_id`

```php
$list = [
    [
        "id"             => 1,
        "name"           => "test",
        "parent_menu_id" => 0,
        "children"       => [
            [
                "id"             => 2,
                "name"           => "sun",
                "parent_menu_id" => 1,
            ],
            [
                "id"             => 3,
                "name"           => "2sun",
                "parent_menu_id" => 1,
                "children"       => [
                    [
                        "id"             => 4,
                        "name"           => "3sun",
                        "parent_menu_id" => 3,
                    ],
                ],
            ],
        ],
    ],

];
```

```php
/**
 * 删除多维数组中的指定键名
 *
 * @param [array] $arr 要处理的多维数组
 * @param [string] $children_key 子节点的键名
 * @param [string] $delkey 要删除的键名
 */
function delKey(&$arr, $children_key, $delkey) {
    foreach ($arr as &$value) {
        if (array_key_exists($children_key, $value)) {
            delKey($value[$children_key], $children_key, $delkey);
        }
        unset($value[$delkey]);
    }
}
```

使用示例
```php
delkey($list,"children","parent_menu_id");

print_r($list);
/*
Array
(
    [0] => Array
        (
            [id] => 1
            [name] => test
            [children] => Array
                (
                    [0] => Array
                        (
                            [id] => 2
                            [name] => sun
                        )

                    [1] => Array
                        (
                            [id] => 3
                            [name] => 2sun
                            [children] => Array
                                (
                                    [0] => Array
                                        (
                                            [id] => 4
                                            [name] => 3sun
                                        )

                                )

                        )

                )

        )

)
*/
```
