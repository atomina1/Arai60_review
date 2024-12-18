#問題文
https://leetcode.com/problems/remove-duplicates-from-sorted-list/?envType=problem-list-v2&envId=xo2bgr0r

# Step1
かかった時間：5min

思考ログ：
- すでにソートされているリストなので最初から要素を見て前の要素と同じなら捨てる、違うなら残しておけば良い
- ただまだオブジェクトをよく理解してなくてどうやったらそんな操作ができるかわからない　普通のリストを返してもエラーが出るので他のコードを見る


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
