+++
Categories = ["python"]
Description = "python奇思妙解"
Tags = ["python3"]
title = "获取两个字符串中最长的公共字符串"
comments = true
date = 2016-06-26T21:04:40Z
+++


---

## **例题：**
longest common substring
获取两个字符串中最长的公共字符串
如：
如果s1='abcdefgh'，s2='cdefgh'; s1与s2的最长公共字符串'cd'

例子：
>s1='abcdefgh'，s2='cdefgh'
lcs(s1,s2) ==> 'cd'

## **解法：**


```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

def lcs(s1,s2):
    m = len(s1)
    n = len(s2)
    counter = [[0]*(n+1) for x in range(m+1)]
    longest = 0
    lcs_set = set()
    for i in range(1,m+1):
        for j in range(1,n+1):
            if s1[i-1] == s2[j-1]:
                c = counter[i-1][j-1] + 1
                counter[i][j] = c
                if c > longest:
                    lcs_set = set()
                    longest = c
                    lcs_set.add(s1[i-c:i])
                elif c == longest:
                    lcs_set.add(s1[i-c:i])
    return lcs_set


if __name__ == "__main__":
    assert lcs('academy', 'abracadabra') == {'acad'}
    assert lcs('ababc', 'abcdaba') == {'aba','abc'}
    assert lcs('abcdefgh', 'cdefgh') == {'cdefgh'}
    assert lcs('abcdefgh', '') == set()
    print('assert complete!')
```

运行结果：

```python
C:\Anaconda3\python.exe E:/python_projects/test.py
assert complete!

Process finished with exit code 0

```

## **解释：**
1. 创建一个二维矩阵counter用来记录最长相同字符串的长度
```python
m = len(S)
n = len(T)
counter = [[0]*(n+1) for x in range(m+1)]
```

![](http://o7ubfyghw.bkt.clouddn.com/python%20longest%20common%20substring%201.jpg)
2. 将s1中的每一个字符与s2中的每一个字符进行比较
```python
for i in range(m):
    for j in range(n):
        if S[i] == T[j]:
```
![](http://o7ubfyghw.bkt.clouddn.com/python%20longest%20common%20substring%202.jpg)
3. 如果s1的第i个字符和s2的第j个字符相同，则将矩阵counter[i+1][j+1]的值在counter[i][j]的基础上加1
```python
if S[i] == T[j]:
    c = counter[i][j] + 1
    counter[i+1][j+1] = c
```
![](http://o7ubfyghw.bkt.clouddn.com/python%20longest%20common%20substring%203.jpg)
4. 如果现在的最长substring比以前的substring长，更新longest和set为新substring；如果新的substring和以前的substring一样长，直接将新的substring加入到set中
```python
if c > longest:
     lcs_set = set()
     longest = c
     lcs_set.add(S[i-c+1:i+1])
elif c == longest:
     lcs_set.add(S[i-c+1:i+1])
```
![](http://o7ubfyghw.bkt.clouddn.com/python%20longest%20common%20substring%204.jpg)


## **寻找最长回文字符串**
上一篇博客[获取string中的最长回文字符串](http://blog.csdn.net/justheretobe/article/details/51761575)还可以使用寻找两个字符串最长公共substring的方法解答：
1. s1=‘给定字符串’
2. s2=‘给定字符串的反序’
3. 比较s1与s2, 获取两个字符串中最长的公共字符串，即为s1最长的回文字符串
代码：

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

def longest_palindrome (s):
    s1 = s
    s2 = s1[::-1]
    if len(s) == 1 : return 1
    elif len(s) == 0: return 0
    else:
      #get the longest common string between s1 and reversed s1
      m = [[0] * (1 + len(s2)) for i in range(1 + len(s1))]
      longest, x_longest = 0, 0
      for x in range(1, 1 + len(s1)):
        for y in range(1, 1 + len(s2)):
          if s1[x - 1] == s2[y - 1]:
            m[x][y] = m[x - 1][y - 1] + 1
            if m[x][y] > longest:
              longest = m[x][y]
              x_longest = x
          else:
              m[x][y] = 0

      #if the longest common string is palindrome, return its length, else return 1
      longest_string = s1[(x_longest-longest):x_longest]
      if longest_string == longest_string[::-1]: return longest
      else: return 1


if __name__ == "__main__":
    assert longest_palindrome('abcdab123454321') == 9
    assert longest_palindrome('ab') == 1
    assert longest_palindrome('aa') == 2
    assert longest_palindrome('') == 0
    assert longest_palindrome('abcdefba') == 1
    print('assert complete!')
```
运行结果：
```python
C:\Anaconda3\python.exe E:/python_projects/test.py
assert complete!

Process finished with exit code 0

```

更多longest_palindrome 解法，见：
https://www.codewars.com/kata/longest-palindrome/solutions/python


---
**Reference：**

[从给定string中找出至多只包含两个不同字符的最长substring](http://www.bogotobogo.com/python/python_solutions.php#longest_substring)

解释和主要代码来自：
[python_longest_common_substring_lcs_algorithm_generalized_suffix_tree](http://www.bogotobogo.com/python/python_longest_common_substring_lcs_algorithm_generalized_suffix_tree.php)

