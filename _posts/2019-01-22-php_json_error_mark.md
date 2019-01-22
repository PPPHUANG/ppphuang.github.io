---
layout: post
title: "php json error"
date: 2017-08-24
description: "php json 错误检查"
tag: php
---
```
if($errorCode = json_last_error()){
	$error = '';
	if($errorCode == JSON_ERROR_NONE){
		$error = '没有错误发生';
		
	}elseif($errorCode == JSON_ERROR_DEPTH){
		$error = '到达了最大堆栈深度';
		
	}elseif($errorCode == JSON_ERROR_STATE_MISMATCH){
		$error = '无效或异常的 JSON';
		
	}elseif($errorCode == JSON_ERROR_CTRL_CHAR){
		$error = '控制字符错误，可能是编码不对';
		
	}elseif($errorCode == JSON_ERROR_SYNTAX){
		$error = '语法错误';
		
	}elseif($errorCode == JSON_ERROR_UTF8){
		$error = '异常的 UTF-8 字符，也许是因为不正确的编码。'; //最经常是遇到这个错误
		
	}elseif($errorCode == JSON_ERROR_RECURSION){
		$error = '被encode的数组存在互相引用的值';
		
	}elseif($errorCode == JSON_ERROR_INF_OR_NAN){
		$error = '被encode的数组存在NAN或INF的值';
		
	}elseif($errorCode == JSON_ERROR_UNSUPPORTED_TYPE){
		$error = '所传参数变量类型无法进行encode';
	}
	
	echo $error;
	
}else{
	echo $json;
}
```
