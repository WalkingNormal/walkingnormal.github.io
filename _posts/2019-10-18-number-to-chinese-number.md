---
title: php 把阿拉伯数字转成拼音数字
date: 2019-10-18
categories:
tags: 
- PHP
- 数字转换
---
## 需求

在页面上展示排名信息，把 1/2/3/4/5.... 转成 一/二/三/四/五...

## 代码

```php
function ToChinaseNum($num)
{
   $char = array("零","一","二","三","四","五","六","七","八","九");
   $dw = array("","十","百","千","万","亿","兆");
   $retval = "";
   $proZero = false;
   for($i = 0;$i < strlen($num);$i++)
   {
      if($i > 0)    $temp = (int)(($num % pow (10,$i+1)) / pow (10,$i));
      else $temp = (int)($num % pow (10,1));

      if($proZero == true && $temp == 0) continue;

      if($temp == 0) $proZero = true;
      else $proZero = false;

      if($proZero)
      {
         if($retval == "") continue;
         $retval = $char[$temp].$retval;
      }
      else $retval = $char[$temp].$dw[$i].$retval;
   }
   if($retval == "一十") $retval = "十";
   return $retval;
}

echo ToChinaseNum(2); // 输出: 二
```
