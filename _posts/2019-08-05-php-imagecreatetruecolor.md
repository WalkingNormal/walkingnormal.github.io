---
title: 设备GPS 转高德坐标
date: 2019-08-02
categories:
tags: 
- 物联网
- 高德
---

> PHP 合成真彩色图片。

合成效果[![egFiqg.png](https://s2.ax1x.com/2019/08/05/egFiqg.png)](https://imgchr.com/i/egFiqg)

```php
$filename = 'aaa.png';
$QR       = './cb9sp-4hret.png'; //已经生成的原始二维码图
$im       = imagecreatefrompng($QR);
// $im = imagecreatefromjpeg($QR); // 从 jpeg 读取图片.微信返回的图片是 jpeg 格式
$QR_width = imagesx($im); //二维码图片宽度
//底部文字
$bottom_text_h = 40;
$bottom_text   = imagecreate($QR_width, $bottom_text_h);
$color = imagecolorallocate($bottom_text, 255, 255, 255);

$text_color = 255; // 字体颜色
$fonts = './msyhbd.ttc';
$str   = "设备编号 : 12345678";
$x     = 19;
imagettftext($bottom_text, 30, 0, $x, 34, $text_color, $fonts, $str);
//新建一个最终画布
$final = imagecreatetruecolor($QR_width, $QR_width + $bottom_text_h); // 新建一个真彩色图像
$color = imagecolorallocate($final, 255, 255, 255);

//合并画布
imagecopyresampled($final, $im, 0, 0, 0, 0, $QR_width,
    $QR_width, $QR_width, $QR_width);
imagecopyresampled($final, $bottom_text, 0, $QR_width, 0, 0, $QR_width,
    $bottom_text_h, $QR_width, $bottom_text_h);

imagepng($final, $filename);
imagedestroy($bottom_text);
imagedestroy($im);
imagedestroy($final);

```



