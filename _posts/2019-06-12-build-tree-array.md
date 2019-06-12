---
title: PHP 创建树结构数据
date: 2019-06-12
categories:
tags: 
- PHP 
- Tree
---

`menu` 表结构示例

|  id   | parent_id |   name   |
| :---: | :-------: | :------: |
|   1   |     0     |   首页   |
|   2   |     0     | 个人中心 |
|   3   |     2     | 我的收藏 |
|   4   |     2     | 我的文章 |


需求数据示例

```php
$menu = [
  [
    "id"=>1,
    "name"=>"首页"
  ],
  [
    "id"=>2,
    "name"=>"个人中心",
    "children" => [
      [
        "id"=>3,
        "name"=>"我的收藏"
      ],
      [
        "id"=>4,
        "name"=>"我的文章"
      ]
    ]
  ]
  
]
```

函数如下:
```
/**
 * 创建树结构
 *
 * @param [array] $flat 分析数组
 * @param [string] $pidKey  父节点
 * @param [string] $idKey 索引
 * @return array 
 */
function buildTree($flat, $pidKey, $idKey = null)
{
    $grouped = array();
    foreach ($flat as $sub){
        $grouped[$sub[$pidKey]][] = $sub;
    }

    $fnBuilder = function($siblings) use (&$fnBuilder, $grouped, $idKey) {
        foreach ($siblings as $k => $sibling) {
            $id = $sibling[$idKey];
            if(isset($grouped[$id])) {
                $sibling['children'] = $fnBuilder($grouped[$id]);
            }
            $siblings[$k] = $sibling;
        }

        return $siblings;
    };

    $tree = $fnBuilder($grouped[0]);

    return $tree;
}
```

函数调用返回示例
```php
$data = DB::table('menu')->get(); // 返回数组
$result = buildTree($data,"parent_id","id");

print_r($result);
/*
array(
  array(
    "id"=>1,
    "parent_id"=>0,
    "name"=>"首页"
  ),
  array(
    "id"=>2,
    "parent_id"=>0,
    "name"=>"个人中心",
    "children"=>array(
      array(
        "id"=>3,
        "parent_id"=>2,
        "name"=>"我的收藏"
      ),
      array(
        "id"=>4,
        "parent_id"=>2,
        "name"=>"我的文章"
      )
    )
  )
)
*/
```


