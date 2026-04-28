# Reverse Linked List II

## 🧩 Problem
Given the `head` of a singly linked list and two integers `left` and `right` (where `left <= right`), reverse the nodes from position `left` to `right`, and return the modified list.

---

## 🧠 Approach
- Use a **dummy node** to handle edge cases easily.
- Traverse to the node just before position `left`.
- Reverse the sublist using pointer manipulation.
- Reconnect the reversed portion back to the list.

---

## 🔁 Example

Input:
1 → 2 → 3 → 4 → 5, left = 2, right = 4

Output:
1 → 4 → 3 → 2 → 5

---

## 💻 Code (C++)
```cpp
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        if (!head || left == right) return head;

        ListNode* dummy = new ListNode(0);
        dummy->next = head;

        ListNode* prev = dummy;

        // Move prev to node before 'left'
        for (int i = 1; i < left; i++) {
            prev = prev->next;
        }

        ListNode* curr = prev->next;
        ListNode* nextNode = NULL;

        // Reverse sublist
        for (int i = 0; i < right - left; i++) {
            nextNode = curr->next;
            curr->next = nextNode->next;
            nextNode->next = prev->next;
            prev->next = nextNode;
        }

        return dummy->next;
    }
};
