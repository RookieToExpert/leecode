## stack(先进后出)
- 创建：stack = []
- 时间复杂度：
    - 访问**O(1)**：```stack[-1]``` (访问栈顶)
    - 搜索**O(1)**：```stack[-1]```
    - 插入**O(1)**：```stack.append(x)```(插入末尾)
    - 删除**O(1)**：```stack.pop()``` (删除并返回栈顶元素)
    - 添加**O(1)**：```stack.append(x)```(插入末尾)
    - 更新**O(1)**: ```stack[-1] = 99```
    - 遍历：
        ```py
        while stack:
        temp = stack.pop()
        print(temp)
        ```
### 栈练习题：
#### 20 有效括号
```py
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []

        for char in s:
            if char == '(' or char == '{' or char == '[':
                stack.append(char)
            elif not stack:
                return False
            else:
                if char == ')':
                    if stack.pop() != '(':
                        return False
                if char == '}':
                    if stack.pop() != '{':
                        return False
                if char == ']':
                    if stack.pop() != '[':
                        return False
        return not stack
```
#### 496
```py
class Solution(object):
    def nextGreaterElement(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        output = []
        stack = []
        for num in nums2:
            stack.append(num)

        for num in nums1:
            temp = []
            result = False
            max = -1
            while result != True:
                top = stack.pop()
                if top > num:
                    max = top
                elif top == num:
                    result = True
                temp.append(top)
            output.append(max)
            while len(temp) != 0:
                stack.append(temp.pop())
        return output
```
单栈版本：
```py
class Solution(object):
    def nextGreaterElement(self, nums1, nums2):
        stack = []
        next_greater = {}  # map number -> next greater

        for num in nums2:
            while stack and num > stack[-1]:
                prev = stack.pop()
                next_greater[prev] = num
            stack.append(num)

        # Remaining elements have no next greater
        for num in stack:
            next_greater[num] = -1

        # Build result for nums1
        return [next_greater[num] for num in nums1]
```