+++
Categories = ["python"]
Description = "python奇思妙解"
Tags = ["python3"]
title = "python3 sorted的用法"
comments = true
date = 2016-06-19T21:04:40Z
+++

---
* * *

## **例题：**

    先来看一个例题：
    给你一个其中包含不同的英文字母和标点符号的文本，你要找到其中出现最多的字母，返回的字母必须是小写形式，
    当检查最想要的字母时，不区分大小写，所以在你的搜索中 "A" == "a"。 请确保你不计算标点符号，数字和空格，只计算字母。
    如果你找到 两个或两个以上的具有相同的频率的字母， 返回那个先出现在字母表中的字母。 例如 -- “one”包含“o”，“n”，“e”每个字母一次，因此我们选择“e”。
    **输入:** 用于分析的文本 (str, unicode).
    **输出:** 最常见的字母的小写形式。
    **前提::**
    密码只包含ASCII码符号
    0 < len(text) ≤ 105

使用sorted的解法如下：

    def checkio(text):
        #filter out not-alphebet char
        if text.isalpha():  text = text.lower()
        else:  text = ''.join([x.lower() for x in text if x.isalpha()])
        #print(text)

        from collections import Counter
        str_count = Counter(text)
        #print(str_count)
        #sorted with two parameters, the first parameter is the count of every char,the second is alphabet
        str_sorted = sorted(Counter(text).items(), key=lambda k: (k[1],k[0]))
        #print(str_sorted)
        #get the most wanted chars
        most_wanted_letters = [item for item in str_sorted if item[1] == str_sorted[len(str_sorted) - 1][1]]
        return most_wanted_letters[0][0]

    if __name__ == '__main__':
        #These "asserts" using only for self-checking and not necessary for auto-testing
        assert checkio("Hello World!") == "l", "Hello test"
        assert checkio("How do you do?") == "o", "O is most wanted"
        assert checkio("One") == "e", "All letter only once."
        assert checkio("Oops!") == "o", "Don't forget about lower case."
        assert checkio("AAaooo!!!!") == "a", "Only letters."
        assert checkio("abe") == "a", "The First."
        print("Start the long test")
        assert checkio("a" * 9000 + "b" * 1000) == "a", "Long."
        print("The local tests are done.")

测试结果如下：
![the most wanted letter](http://o7ubfyghw.bkt.clouddn.com/checkio%20most%20wanted%20letter.jpg)

## **sorted的用法：**

分析解法的关键代码

    str_sorted = sorted(Counter(text).items(), key=lambda k: (k[1],k[0]))    增加print测试:
    #print(text)
    >>>checkio("Lorem ipsum dolor sit amet")
    loremipsumdolorsitamet
    <<< 'm'
    #print(str_sorted)
    >>>checkio("Lorem ipsum dolor sit amet")
    loremipsumdolorsitamet
    Counter({'m': 3, 'o': 3, 'i': 2, 'l': 2, 's': 2, 'e': 2, 't': 2, 'r': 2, 'd': 1, 'p': 1, 'a': 1, 'u': 1})
    <<< 'm'

这里sorted使用**两个关键字**进行排序：
先按照每个字母出现的次数k[1]进行排序，然后安装字母表顺序对测试text中的内容k[0]进行排序.

python3手册对sorted的用法描述如下：

    sorted(iterable[, key][, reverse])

    Return a new sorted list from the items in iterable.

    Has two optional arguments which must be specified as keyword arguments.

    key specifies a function of one argument that is used to extract a comparison key from each list element: key=str.lower. The default value is None (compare the elements directly).

    reverse is a boolean value. If set to True, then the list elements are sorted as if each comparison were reversed.

    Use functools.cmp_to_key() to convert an old-style cmp function to a key function.

    The built-in sorted() function is guaranteed to be stable. A sort is stable if it guarantees not to change the relative order of elements that compare equal — this is helpful for sorting in multiple passes (for example, sort by department, then by salary grade).

    For sorting examples and a brief sorting tutorial, see Sorting HOW TO.

sorted的第一个参数是一个迭代器，第二个参数是用来排序的key，第三个参数的排序数序：正序还是倒序
如：
第一个参数是迭代器

    >>> sorted([36, 5, -12, 9, -21])
    [-21, -12, 5, 9, 36]

第二个参数是用来排序的key

    >>> sorted([36, 5, -12, 9, -21], key=abs)
    [5, 9, -12, -21, 36]    key指定的函数将作用于list的每一个元素上，并根据key函数返回的结果进行排序。对比原始的list和经过key=abs处理过的list：
    list = [36, 5, -12, 9, -21]
    keys = [36, 5,  12, 9,  21]
    然后sorted()函数按照keys进行排序，并按照对应关系返回list相应的元素：
    keys排序结果 => [5, 9,  12,  21, 36]
    最终结果     ====> [5, 9, -12, -21, 36]

第三个参数决定正向还是反向排序：
要进行反向排序，不必改动key函数，可以传入第三个参数reverse=True：

    >>> sorted(['bob', 'about', 'Zoo', 'Credit'], key=str.lower, reverse=True)
    ['Zoo', 'Credit', 'bob', 'about']

**注：**例题解法来自 [https://checkio.org/user/penn201500/](https://checkio.org/user/penn201500/)
更优解法为：

    import string
    ​
    def checkio(text):
        """
        We iterate through latyn alphabet and count each letter in the text.
        Then 'max' selects the most frequent letter.
        For the case when we have several equal letter,
        'max' selects the first from they.
        """
        text = text.lower()
        return max(string.ascii_lowercase, key=text.count)

* * *

**参考：**

[廖雪峰官网 sorted方法](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014318230588782cac105d0d8a40c6b450a232748dc854000)

[checkio: most wanted letter](https://checkio.org/mission/most-wanted-letter/)

[sorted()函数](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014318230588782cac105d0d8a40c6b450a232748dc854000)

* * *

