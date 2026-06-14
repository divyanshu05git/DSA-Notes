
#Cycle Detection in Linked List

-Assign two pointers slow and fast initally pointing to head
-slow moves one step while fast moves two steps:
  when there is a cycle , slow and fast will keep moving in the cycle and will meet at a pointer(detecting cycle)
-if fast or slow becomes null , then no cycle 

## Floyd's Cycle Detection Algorithm

### Code

'''java
public class Solution {
    public boolean hasCycle(ListNode head) {
        if(head==null) return false;

        ListNode slow=head;
        ListNode fast=head;

        while(fast.next!=null && fast.next.next!=null){
            slow=slow.next;
            fast=fast.next.next;

            if(slow==fast) return true;
        }

        return false;
    }
}
'''
