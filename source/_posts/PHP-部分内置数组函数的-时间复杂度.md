---
title: PHP 部分内置数组函数的 时间复杂度
urlname: Time-complexity-of-PHP-array-functions
date: 2018-11-01 15:22:19
tags:
- PHP
- Array
---
数组作为 PHP 的核心驱动力（我以为），PHP 内置了非常多的数组函数，几乎可以支持使用者超过 80% 的需要，但学习 PHP 有相当长的一段时间了，希望能够对于这门语言有更深入的了解，所以抽空整理了一份 PHP 内置数组函数时间复杂度的列表。会不定期更新补全。


<!--more-->

# isset

**时间复杂度**： O(1) - O(n)，但几乎是 O(1)

**理由**：PHP 的数组在 C 中是一个 HashTable，Hash 函数为 [DJBX33A][1]，以[拉链法][2]解决 Hash 冲突(根据源码，PHP7 之后似乎不再是，有问题可以留言评论)，理论上 isset 应该是 O(1) 的时间复杂度，但需要考虑有可能出现的 Hash 冲突。 

# array_key_exists

**时间复杂度**： O(1) - O(n)，但几乎是 O(1)

**理由**：同 isset

# in_array

**时间复杂度**： O(n)

**理由**：需要遍历整个 HashTable，推荐使用键来存储此类数据，时间复杂度可以提升到 O(1)

# array_search

**时间复杂度**： O(n)

**理由**：同 in_array

# array_push

**时间复杂度**： O( ∑ var_i, for all i )

**理由**：array_push 可以传入不定参数，所以时间复杂度也不定，但当只传入一个参数时，时间复杂度为 O(1)，PHP 的 HashTable 维护了一个指向数组最后一个元素的指针。

# array_pop

**时间复杂度**： O(1)

**理由**：array_pop PHP 的 HashTable 维护了一个指向数组第一个元素的指针。

# array_shift

**时间复杂度**： O(n)

**理由**：array_shift 操作数组之后，需要重新索引整个数组的键

# array_unshift

**时间复杂度**： O(n +  ∑ var_i, for all i )

**理由**：array_unshift 操作数组之后，需要重新索引整个数组的键，而且函数支持多个参数

# shuffle

**时间复杂度**： O(n)

**理由**：随机取数组的值

# array_rand

**时间复杂度**： O(n)

**理由**：同 shuffle ，随机取数组的值，线性轮询

# array_fill

**时间复杂度**： O(n)

**理由**：填充数组

# array_fill_keys

**时间复杂度**： O(n)

**理由**：填充数组

# range

**时间复杂度**： O(n)

**理由**：构建指定范围和跨度的数组

# array_splice

**时间复杂度**： O(offset + length)


# array_slice 

**时间复杂度**： O(offset + length) or O(n) if length = NULL

# array_keys 

**时间复杂度**：O(n)

# array_values

**时间复杂度**：O(n)

# array_reverse

**时间复杂度**：O(n)

# array_pad

**时间复杂度**：O(pad_size)

# array_flip

**时间复杂度**：O(n)

# array_sum

**时间复杂度**：O(n)

# array_product

**时间复杂度**：O(n)

# array_reduce

**时间复杂度**：O(n)

# array_filter

**时间复杂度**：O(n)

# array_map

**时间复杂度**：O(n)

# array_chunk

**时间复杂度**：O(n)

# array_combine

**时间复杂度**：O(n)









  [1]: http://www.nowamagic.net/academy/detail/3008095
  [2]: https://www.jianshu.com/p/4d3cb99d7580