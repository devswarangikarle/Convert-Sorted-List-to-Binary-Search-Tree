# Convert-Sorted-List-to-Binary-Search-Tree

Given the head of a singly linked list where elements are sorted in ascending order, convert it to a 
height-balanced binary search tree.


 class Solution:
    def sortedListToBST(self, head: Optional[ListNode]) -> Optional[TreeNode]:
        if not head:
            return None
        if not head.next:
            return TreeNode(head.val)

        slow = head
        fast = head
        prev = None

        # Finding the middle element
        while fast and fast.next:
            prev = slow
            slow = slow.next
            fast = fast.next.next

        # Create the root node with the middle element
        root = TreeNode(slow.val)

        # Disconnect the left part of the list
        if prev:
            prev.next = None

        # Recursively build left and right subtrees
        root.left = self.sortedListToBST(head)    # Left subtree
        root.right = self.sortedListToBST(slow.next)  # Right subtree

        return root
