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
かかった時間：30min

思考ログ
- Araiさんの解説と他の人の答えを見る
- なるほど次に行きなさいという.nextという操作を.next.nextに置き換えれば重複している要素を無視することになる

'''python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head:
            return head

        current = head

        while current.next:
            if current.val == current.next.val:
                current.next = current.next.next
            else:
                current = current.next
        return head
'''

# Step3
思考ログ
- 上のコードはcurrentにheadを代入してcurrentのnextを書き換えているのにいつの間にかheadも書き変わっていて不自然に感じる
- while文の条件を書き直せばもう少し自分にとってはわかりやすくはなった気がする? currentにheadというlistnodeを代入していて、headをwhile文で書き換えているので最終的に欲しいものはcurrentに入っていると思える

'''python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        current = head
        while head and head.next:
            if head.val == head.next.val:
                head.next = head.next.next
            else:
                head = head.next
        return current
'''
