## 集合(set)
- 不重复，但不保证顺序的数组
- 创建：**s = set()** or **s = {1, 2, 3}**
- 时间复杂度：
    - 访问：X(没有索引的概念，所以不存在访问，只能遍历)
    - 搜索：```2 in s```
        - **O(1)** (直接通过哈希函数，定位到key的内存地址)
        - **O(K)**（有哈希冲突）
    - 添加：```s.add(5)```不保证顺序
        - **O(1)**
        - **O(K)**（有哈希冲突）
    - 删除：**O(1)或者O(K)**（有哈希冲突）
        - ```s.remove(2)```如果不存在会报错
        - ```s.discard(x)```如果不存在不会报错
        - ```s.pop()```随机删除并返回
        - ```s.clear()```清空集合 → O(1)
    - 更新**O(len(iterable))**：```s.update([6, 7, 8])```
    - 长度**O(1)**：```len(s)```
    - 遍历**O(N)**：
    ```py
    for x in s:
    print(x)
    ```

### set练习题：
#### 217检查是否有重复的数字
```py
#我自己的解法
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        s = set()
        for num in nums:
            s.add(num)
        return (len(nums) != len(s))
        # 更优雅的写法,一行搞定
        # return len(nums) != len(set(nums))
```

```py
# 最高效的解法，时间复杂度有可能为0(1)
class Solution(object):
    def containsDuplicate(self, nums):
        s=set()
        for n in nums:
            if n in s:
                return True
            s.add(n)
        return False
```
#### 705
```py
class MyHashSet(object):

    def __init__(self):
        self.data = [False] * 1000001

    def add(self, key):
        """
        :type key: int
        :rtype: None
        """
        self.data[key] = True

    def remove(self, key):
        """
        :type key: int
        :rtype: None
        """
        self.data[key] = False

    def contains(self, key):
        """
        :type key: int
        :rtype: bool
        """
        return self.data[key]
```