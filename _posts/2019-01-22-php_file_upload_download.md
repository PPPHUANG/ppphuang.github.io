---
layout: post
title: "php大文件上传下载"
date: 2019-01-22
description: "php大文件上传下载"
tag: php
---

#### 文件下载
```
<?php
//避免文件太大脚本超时
$file = './Penguins.jpg';
set_time_limit(0);
$file_display_name = basename($file);
$fsize = @filesize($file);
if (!empty($fsize)) {			
	$start = null ; 
	$end = $fsize - 1;
	if (isset($_SERVER['HTTP_RANGE']) && ($_SERVER['HTTP_RANGE'] != "") && preg_match("/^bytes=([0-9]+)-([0-9]*)$/i", $_SERVER['HTTP_RANGE'], $match) && ($match[1] < $fsize) && ($match[2] < $fsize)) {     
		$start = $match[1]; 
		if (!empty($match[2]))$end = $match[2];
	}
	header("Cache-control: public"); 
	header("Pragma: public"); 
	if ($start === null) {
		header("HTTP/1.1 200 OK");
		header("Content-Length: $fsize");
		header("Accept-Ranges: bytes");
	} else {  				
		header("HTTP/1.1 206 Partial Content");     
		header("Content-Length: " . ($end - $start + 1));     
		header("Content-Ranges: bytes " . $start . "-" . $end . "/" . $fsize); 
	}
	header("Content-Type: application/octet-stream"); 
	header("Content-Disposition: attachment; filename=" . urlencode ( $file_display_name ) );
	ob_clean();
	flush();
	$fp = fopen($file, "rb");
	fseek($fp,$start);
	$chunk = 8192;
	while(($nowNum = ftell($fp)) < $end){
		if($nowNum >= ($end - $chunk)){
			$chunk = $end - $nowNum + 1;
		}
		echo fread($fp, $chunk );
	}
	 
	fclose($fp);
	exit();
}else {
	header("HTTP/1.1 404 Not Found");
	header('Content-Type: text/html; charset=utf-8');
}
```
#### 上传

```
<?php
$file = './test.jpg';
$fsize = 0;
$start = 0;
$end = null ;
if (isset($_SERVER['HTTP_CONTENT_RANGES']) && ($_SERVER['HTTP_CONTENT_RANGES'] != "") && preg_match('/^bytes ([0-9]+)-([0-9]+)\/([0-9]+)$/i', $_SERVER['HTTP_CONTENT_RANGES'], $match) ) {
	$start = $match[1];
	if (!empty($match[2]))$end = $match[2];
	if (!empty($match[3]) && empty($filesize))$filesize = $match[3];
}
if (empty($filesize) && isset($_SERVER['CONTENT_LENGTH'])){
	$filesize = $_SERVER['CONTENT_LENGTH'];
}
$fp = fopen("php://input",'rb');
if(is_resource($fp))
{
	$fpu = fopen($file, "wb");
	if ($start > 0)
	fseek($fpu, $start);
	while($data = fread($fp, 8192))
	{
		if (!empty($data))
		fwrite($fpu, $data);
	}                
	fclose($fpu);
}
fclose($fp);
```
