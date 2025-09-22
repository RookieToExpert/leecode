## Queue(先进先出)
- 创建Queue：q = deque()
- 时间复杂度(写非常快，读很慢)：
    - 访问**O(N)**：```q[1]```
    - 搜索**O(N)**：```3 in q```
    - 插入**O(1)**：```q.append(4)```
    - 删除**O(1)**：```x = q.popleft()```
    - 查看**O(1)**:```q[0]/q[-1]```
    - 大小**O(1)**：```len(q)```
    - 遍历**O(N)**：``for i in a``

### 队列练习题：
#### 993：最近请求次数
```py
class RecentCounter(object):

    def __init__(self):
        self.q = deque()

    def ping(self, t):
        """
        :type t: int
        :rtype: int
        """
        result = 0
        self.q.append(t)
        while len(self.q) > 0 and t - self.q[0] > 3000:
            self.q.popleft()
        return len(self.q)
```