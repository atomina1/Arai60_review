#問題文
https://leetcode.com/problems/add-two-numbers/description/

# Step1

思考ログ：
- headから順々に足していって繰り上がりをちゃんと処理できればOKそう
- 桁数が一緒だったらもっと簡単になるけど当然問題の完全な回答ではない　だけど割と時間が経ってしまったので答えを見ることにする　Step1に書いてあるコードは完全に誤答なので無視してOKです
- 桁数が違う時にwhile l1 or l2でループをしてif l1 is not None..., if l2 is not None...みたいに3通りで場合わけをすることはできるけど

'''python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        ans = ListNode()
        head = ans
        while l1 and l2:
            head.next = ListNode(0)
            head = head.next
            temp = l1.val + l2.val
            if temp < 10:
                head.val += temp
            if temp >= 10:
                head.val += temp % 10
                l1.next.val += 1
            l1 = l1.next
            l2 = l2.next

        return ans.next
'''

# Step2

色んな人の回答を見る
思考ログ
- 上の回答だと1 + 99が [1,0] と [9,9]と渡されたとしても2桁目の処理をしているときにl1.nextがないのでエラーが出てしまう
- carryというパラメータを用意しておいて繰り上がりが発生していたらまたループを回すことにすればよい
- while l1 or l2としてその中でif l1, if l2と書くのは慣れた人には当たり前かもしれないけど割と綺麗に書けているので見ていて気持ちよかった
- いい問題だなと思った

'''python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        ans = ListNode()
        head = ans

        total = carry = 0

        while l1 or l2 or carry:
            total = carry

            head.next = ListNode()
            head = head.next
            if l1:
                total += l1.val
                l1 = l1.next
            if l2:
                total += l2.val
                l2 = l2.next
            num = total % 10
            carry = total // 10
            head.val = num

        return ans.next
'''

# Step3
思考ログ
- 
- 
'''python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        ans = ListNode()
        head = ans
        total = carry = 0

        while l1 or l2 or carry:
            total = carry
            if l1:
                total += l1.val
                l1 = l1.next
            if l2:
                total += l2.val
                l2 = l2.next
            carry = total // 10
            head.next = ListNode(total % 10)
            head = head.next
        return ans.next
'''
