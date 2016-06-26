+++
Categories = ["python"]
Description = "python奇思妙解"
Tags = ["python3"]
title = "获取string中的最长回文字符串"
comments = true
date = 2016-06-26T19:04:40Z
+++

---

## **例题**
获取string中的最长回文字符串

所谓回文字符串，即该字符串从左到右读和从右到左读是完全一样的。如“123454321”就是一个长度为9的回文字符串。
现要求使用python完成：对一个字符串s，找出其中为回文字符串的部分，并返回回文字符串的长度。规则为：
1. 如果s是1个字符，则长度为1，如“a”
2. 如果s为空“”，则长度为0
3. 如果s中有部分是回文字符串，返回最长回文字符串及其长度，如“aab”，最长回文字符串为“aa”，长度为2

例子：
>"a" -> 1 
"aab" -> 2  
"abcde" -> 1
"zzbaabcd" -> 4
"" -> 0

## **解法**
对该字符串的每个长度的组合都进行比较，如果是回文字符串，记录其长度。返回最长的回文字符串
```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

def longest_palindrome (s):
    longest = 0
    if s == '': return ''
    for left in range(len(s)):
        for right in range(len(s), left, -1):
            if s[left:right] in (s[left:right])[::-1]:
                #longest = max(right-left, longest)
                if (right-left)>longest:
                    longest = right-left
                    palindrome = s[left:right]
                    break
                else: break
    return palindrome

if __name__ == "__main__":
    assert longest_palindrome('abcdab123454321') == '123454321'
    assert len(longest_palindrome('abcdab123454321')) == 9
    assert longest_palindrome('ab') == 'a'
    assert len(longest_palindrome('ab')) == 1
    assert longest_palindrome('aa') == 'aa'
    assert len(longest_palindrome('aa')) == 2
    assert longest_palindrome('') == ''
    assert len(longest_palindrome('')) == 0
    assert longest_palindrome('abcdefba') == 'a'
    assert len(longest_palindrome('abcdefba')) == 1

    print('assert complete!')
```

运行结果：

```python
C:\Anaconda3\python.exe E:/python_projects/test.py
assert complete!

Process finished with exit code 0
```
