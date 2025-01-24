## 1
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
## 2
```c
 ListNode* reverseList(ListNode* head) {
        ListNode* prev = nullptr;
        ListNode* curr = head;
        while(curr) {
            ListNode* next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
    
    int listLength(ListNode* head) {
        int result = 0;
        while(head) {
            head = head->next;
            result++;
        }
        return result;
    }
    bool isPalindrome(ListNode* head) {
        auto headCopy = head;
        auto l = listLength(head);
        
        for(size_t i = 0; i < l / 2; i++) {head = head->next;}
        if(l % 2 == 1) {
            head = head->next;
        }
        auto reversed = reverseList(head);
        for(size_t i = 0; i < l / 2; i++) {
            if(headCopy->val != reversed->val) {
                return false;
            }
            headCopy = headCopy->next, reversed = reversed->next
        }
        
        return true;
    }
```

## 3
```c
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* it1 = headA;
        ListNode* it2 = headB;
        while(it1 != it2)
        {
            it1 = it1 ? it1->next : headA;
            it2 = it2 ? it2->next : headB;
        }
        return it1;
    }
```
```c
int l(ListNode* head)
    {
        ListNode* it = head;
        int size = 0;
        while(it)
        {
            it = it->next;
            size++;
        }
        return size;
    }
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* it1 = headA;
        ListNode* it2 = headB;
        int size1 = l(it1), size2 = l(it2), size = 0;
        size = min(size1, size2);
        while(size1 != size)
        {
            size1--;
            it1 = it1->next;
        }
        while(size2 != size)
        {
            size2--;
            it2 = it2->next;
        }
        while(it1 && it2)
        {
            cout << "val1 " << it1->val <<  endl << "val2 " << it2->val << endl ;
            if(it1 == it2) break;
            it1 = it1->next;
            it2 = it2->next;
        }
        return it1;
    }
```
