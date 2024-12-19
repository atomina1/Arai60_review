#問題文
https://leetcode.com/problems/linked-list-cycle-ii/description/?envType=problem-list-v2&envId=xo2bgr0r

# Step1
かかった時間：30min

思考ログ：
- 以前サイクルがあるかどうかの判定を解いていたのでそこから導きたかった
- slowとfastが最初にぶつかった時、それぞれのポインタが動いた距離の差がサイクルの長さになるのでサイクルの長さー最初のリストの長さでサイクルの最初の位置はわかる
- だがlen(head)をするとエラーが出るので少し発想を変えないといけなかった　のでここで答えを見る


# Step2
かかった時間：30min

思考ログ
- フロイトのアルゴリズムだと言われているのを知る
- 最初のサイクルになってない部分の長さをk,サイクルの長さをmとするとぶつかった時点でslowはm、fastは2m動いているのでポインタたちはサイクル内のm-k番目のところにいる
- なので片方のポインタを始点に戻してまた両方のポインタを一つずつ動かしていくとk回動かしたところで二つの点はサイクルの最初に行くのでぶつかる

'''python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        fast = head
        slow = head

        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next

            if fast == slow:
                slow = head
                while slow != fast:
                    slow = slow.next
                    fast = fast.next
                return slow
        return None
'''

