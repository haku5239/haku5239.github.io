---
 title: strtoupper()和strtolower()方法带中文字符串乱码解决 
 date: 2021/05/14 13:36:24 
 tags: 
 - blog 
---


### strtoupper()和strtolower()方法带中文字符串乱码解决 

- 当有mbstring包时

  >可以使用`mb_convert_case(string str, int $mode, string|null $encodeing = null): string`方法进行转换
  >
  >`$mode参数可选值为MB_CASE_UPPER, MB_CASE_LOWER, MB_CASE_TITLE, MB_CASE_FOLD, MB_CASE_UPPER_SIMPLE, MB_CASE_LOWER_SIMPLE, MB_CASE_TITLE_SIMPLE, MB_CASE_FOLD_SIMPLE`
  >
  >其中**`MB_CASE_UPPER`**、**`MB_CASE_LOWER`**分别为转化成全大写和全小写

- 也可以自己封装一个方法，思路为将字符串切割为单字符的数组，判断字符的ACSII码值

  > 大写字母[A-Z]的ACSII值为65-90
  >
  > 小写字母[a-z]的ACSII值为97-122
  >
  > 大小写字母ACSII值差值为32

