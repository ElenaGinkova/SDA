```c
    bool hasCycle(ListNode *head) {
        ListNode* fast = head;
        ListNode* slow = head;
        while(fast && slow && fast->next)
        {
           
            fast = fast->next->next;
            slow = slow->next;
             if(fast == slow) return true;
        }
        return false;
    }
```
или ако има невалидна стойност да се попълни за посесетени
