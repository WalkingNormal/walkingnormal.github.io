---
title: PHP 发送 raw 数据
date: 2019-02-22
categories:
tags:
---

> PHP 发送 `Content-type: application/json` 格式数据

```php
/**
 * 发送数据
 *
 * @param [string] $url 发送地址
 * @param [string|array] $data 发送数据
 * @return void
 */
public function https_request($url, $data = null)
{
    $headers = array("Content-type: application/json", "Accept: application/json", "Cache-Control: no-cache", "Pragma: no-cache","user-agent:User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36");
    $curl = curl_init();
    curl_setopt($curl, CURLOPT_URL, $url);
    curl_setopt($curl, CURLOPT_SSL_VERIFYPEER, FALSE);
    curl_setopt($curl, CURLOPT_SSL_VERIFYHOST, FALSE);
    if (!empty($data))
    {
        curl_setopt($curl, CURLOPT_POST, 1);
        curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
    }
    curl_setopt($curl, CURLOPT_HTTPHEADER, $headers);
    curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
    $output = curl_exec($curl);
    $http_code = curl_getinfo($curl, CURLINFO_HTTP_CODE);
    if($http_code >= 400)
    {
        $output = json_encode(array(
            'http_code' => $http_code,
        ));
    }
    curl_close($curl);
    return $output;
}
```
