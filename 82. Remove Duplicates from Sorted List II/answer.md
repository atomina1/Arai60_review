#問題文
https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/

# Step1

思考ログ：
- 安直に考えるなら前の問題でダブりがあるリンクリストからダブりをなくす方法を知っているので、ダブった数をリストに記録しておいてダブりをなくした後ダブった数を消せば良さそうではある
- しかしダブった数の分だけsingly listの要素を探してまた削除しないといけないからO(N^2)の計算量になってしまいよくない気がする
- しかも自分が書いたコードは[1,1]に対して[1]を返してWAになってしまうが時間も経ってしまったので諦める　コードはここに供養しておきます

'''python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        node = head
        doubled = []
        while head and head.next:
            if head.val != head.next.val:
                head = head.next
            else:
                head.next = head.next.next
                doubled.append(head.val)
            
        ans = node
        for num in doubled:
            temp = node
            while temp and temp.next:
                if temp.val == num:
                    temp.val = temp.next.val
                    temp.next = temp.next.next
                else:
                    temp = temp.next  

        return ans
'''

# Step2

思考ログ
- Araiさんの解説と他の人の答えを見る
- 重複が無くなるまでポインタを飛ばすというのは実装の仕方がよくわからなくて考えていなかったし先頭から重複が始まるケースは完全に考えていなかった
- ChatGPTも違うコード返すからおもしろい

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(0)
        dummy.next = head
        curr = dummy 

        while curr.next and curr.next.next:
            if curr.next.val == curr.next.next.val:
                running = curr.next
                num = running.val
                while running and running.val == num:
                    running = running.next
                curr.next = running
            else:
                curr = curr.next

        return dummy.next

# Step3
思考ログ
- 上のコードを再現しようとしたらwhile running and running.val == numのうちrunningを忘れてTLEになった 反省

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(-1, head)
        curr = dummy

        while dummy.next and dummy.next.next:
            if dummy.next.val != dummy.next.next.val:
                dummy = dummy.next
            else:
                remove = dummy.next.val
                while dummy.next and dummy.next.val == remove:
                    dummy.next = dummy.next.next
        return curr.next
