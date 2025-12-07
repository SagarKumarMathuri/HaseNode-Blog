---
title: "🚀 Linked List in JavaScript — The Ultimate Guide (With Code, Diagrams & Practice Questions)"
datePublished: Sun Dec 07 2025 10:57:59 GMT+0000 (Coordinated Universal Time)
cuid: cmivlzoa3000002l22xv7cbzi
slug: linked-list-in-javascript-the-ultimate-guide-with-code-diagrams-and-practice-questions
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1765105059792/b9102efe-6092-4a58-ae53-7f8cb4b08e53.png
tags: linked-list-in-javascript

---

When you step into **DSA for JavaScript**, one of the first interview-heavy data structures you meet is the **Linked List**.

Arrays are great…  
But Linked Lists?  
They give you **true dynamic memory**, **constant-time insertions**, and powerful pointer-based operations that appear in almost every FAANG interview.

In this Hasenode blog, we’ll break Linked Lists down in a **clean, visual, beginner-friendly** way.

---

# 🔥 What is a Linked List?

A **Linked List** is a linear data structure where elements are stored in **nodes**, and each node stores:

* `data`
    
* `next` reference pointing to the next node
    

```apache
[10 | next] → [20 | next] → [30 | null]
```

Unlike arrays:

| Feature | Array | Linked List |
| --- | --- | --- |
| Insert/Delete | ❌ O(n) | ✅ O(1) |
| Random Access | ✅ O(1) | ❌ O(n) |
| Memory | Contiguous | Dynamic |

---

# 🧱 Linked List Node Structure

```apache
class Node {
    constructor(data) {
        this.data = data;
        this.next = null;
    }
}
```

---

# 🛠️ Full Linked List Implementation in JavaScript

Here is a clean, interview-ready LinkedList class:

```apache
class LinkedList {
    constructor() {
        this.head = null;
        this.size = 0;
    }

    insertAtHead(data) {
        const newNode = new Node(data);
        newNode.next = this.head;
        this.head = newNode;
        this.size++;
    }

    insertAt(index, data) {
        if (index < 0 || index > this.size) return "Invalid Index";

        if (index === 0) return this.insertAtHead(data);

        let newNode = new Node(data);
        let temp = this.head;

        for (let i = 0; i < index - 1; i++) temp = temp.next;

        newNode.next = temp.next;
        temp.next = newNode;
        this.size++;
    }

    print() {
        let result = "";
        let temp = this.head;
        while (temp) {
            result += `${temp.data}->`;
            temp = temp.next;
        }
        return result;
    }

    removeAtHead() {
        if (this.isEmpty()) return "List is empty";

        this.head = this.head.next;
        this.size--;
    }

    removeElement(data) {
        if (this.isEmpty()) return "List is empty";

        let prev = null, current = this.head;

        while (current) {
            if (current.data === data) {
                if (prev === null) {
                    this.head = current.next;
                } else {
                    prev.next = current.next;
                }
                this.size--;
                return current.data;
            }
            prev = current;
            current = current.next;
        }
        return -1;
    }

    searchElement(data) {
        let curr = this.head;
        let index = 0;

        while (curr) {
            if (curr.data === data) return index;
            curr = curr.next;
            index++;
        }
        return -1;
    }

    middleNode() {
        let slow = this.head, fast = this.head;

        while (fast && fast.next) {
            fast = fast.next.next;
            slow = slow.next;
        }

        return slow;
    }

    reverse() {
        let prev = null, curr = this.head;

        while (curr) {
            let next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        this.head = prev;
    }

    isCycle() {
        let slow = this.head, fast = this.head;

        while (fast && fast.next) {
            fast = fast.next.next;
            slow = slow.next;
            if (slow === fast) return true;
        }
        return false;
    }

    isEmpty() {
        return this.size === 0;
    }
}
```

---

# 🧪 Example Usage

```apache
let list = new LinkedList();
list.insertAtHead(43);
list.insertAtHead(50);
list.insertAtHead(34);
list.insertAt(2, 46);

list.removeAtHead();
list.removeElement(46);

list.reverse();

console.log(list.isCycle());       // false
console.log(list.middleNode());    // 50
console.log(list.searchElement(50)); // 1
console.log(list.print());         // 43->50
```

---

# 🧠 Important Concepts in Linked Lists (Interview Gold)

### ✔ Slow & Fast Pointer

Used for:

* Find middle node
    
* Detect cycle
    
* Remove Nth node
    
* Reorder list
    

### ✔ Dummy Node Technique

Prevents edge-case errors in:

* Removing duplicates
    
* Merge lists
    
* Deleting nodes
    

### ✔ Reversing Pointers

Most Linked List questions eventually require using pointer manipulation instead of arrays.

---

# 📘 Linked List Practice Questions (LeetCode Based)

Below is the curated interview-heavy problem list:

## ✅ Beginner

1. **Middle of Linked List**
    
2. **Reverse Linked List**
    
3. **Merge Two Sorted Lists**
    
4. **Remove Duplicates from Sorted List I**
    

## 🟦 Intermediate

5. Remove Duplicates from Sorted List II
    
6. Linked List Cycle I
    
7. Linked List Cycle II
    
8. Intersection of Two Linked Lists
    
9. Next Greater Node in Linked List
    
10. Remove Zero Consecutive Nodes
    

## 🔥 Advanced (Must Know)

11. Reverse Linked List II
    
12. Odd Even Linked List
    
13. Swap Nodes in Pairs
    
14. Reorder List
    
15. Remove Nth Node from End
    
16. Merge K Sorted Lists
    

# ✅ **1\. Middle of Linked List**

**Logic:** Use slow–fast pointer.

```apache
var middleNode = function(head) {
    let slow = head, fast = head;
    while (fast && fast.next) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
};
```

---

# ✅ **2\. Reverse Linked List**

```apache
var reverseList = function(head) {
    let prev = null, curr = head;
    while (curr) {
        let next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
};
```

---

# ✅ **3\. Merge Two Sorted Lists**

```apache
var mergeTwoLists = function(l1, l2) {
    let dummy = new ListNode(-1);
    let temp = dummy;

    while (l1 && l2) {
        if (l1.val < l2.val) {
            temp.next = l1;
            l1 = l1.next;
        } else {
            temp.next = l2;
            l2 = l2.next;
        }
        temp = temp.next;
    }
    temp.next = l1 || l2;
    return dummy.next;
};
```

---

# ✅ **4\. Remove Duplicates from Sorted List I**

```apache
var deleteDuplicates = function(head) {
    let curr = head;
    while (curr && curr.next) {
        if (curr.val === curr.next.val) curr.next = curr.next.next;
        else curr = curr.next;
    }
    return head;
};
```

---

# ✅ **5\. Remove Duplicates from Sorted List II**

**Remove all nodes that have duplicates (keep only unique nodes).**

```apache
var deleteDuplicates = function(head) {
    let dummy = new ListNode(0, head);
    let prev = dummy;

    while (head) {
        if (head.next && head.val === head.next.val) {
            while (head.next && head.val === head.next.val) head = head.next;
            prev.next = head.next;
        } else {
            prev = prev.next;
        }
        head = head.next;
    }

    return dummy.next;
};
```

---

# ✅ **6\. Linked List Cycle I**

```apache
var hasCycle = function(head) {
    let slow = head, fast = head;
    while (fast && fast.next) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow === fast) return true;
    }
    return false;
};
```

---

# ✅ **7\. Linked List Cycle II (Find starting node)**

```apache
var detectCycle = function(head) {
    let slow = head, fast = head;

    while (fast && fast.next) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow === fast) break;
    }

    if (!fast || !fast.next) return null;

    fast = head;
    while (fast !== slow) {
        fast = fast.next;
        slow = slow.next;
    }
    return slow;
};
```

---

# ✅ **8\. Intersection of Two Linked Lists**

```apache
var getIntersectionNode = function(a, b) {
    let p1 = a, p2 = b;
    while (p1 !== p2) {
        p1 = p1 ? p1.next : b;
        p2 = p2 ? p2.next : a;
    }
    return p1;
};
```

---

# ✅ **9\. Next Greater Node in Linked List**

Use stack + array.

```apache
var nextLargerNodes = function(head) {
    let arr = [];
    while (head) {
        arr.push(head.val);
        head = head.next;
    }

    let res = Array(arr.length).fill(0);
    let stack = [];

    for (let i = 0; i < arr.length; i++) {
        while (stack.length && arr[i] > arr[stack[stack.length - 1]]) {
            res[stack.pop()] = arr[i];
        }
        stack.push(i);
    }
    return res;
};
```

---

# ✅ **10\. Remove Zero Consecutive Nodes from Linked List**

Sum groups between zeros.

```apache
var removeZeroSumSublists = function(head) {
    let dummy = new ListNode(0);
    dummy.next = head;
    let map = new Map();
    let sum = 0, curr = dummy;

    while (curr) {
        sum += curr.val;
        if (map.has(sum)) {
            let prev = map.get(sum).next;
            let tempSum = sum;
            while (prev !== curr) {
                tempSum += prev.val;
                map.delete(tempSum);
                prev = prev.next;
            }
            map.get(sum).next = curr.next;
        } else {
            map.set(sum, curr);
        }
        curr = curr.next;
    }
    return dummy.next;
};
```

---

# ✅ **11\. Reverse Linked List II (Reverse between left & right)**

```apache
var reverseBetween = function(head, left, right) {
    let dummy = new ListNode(0, head);
    let prev = dummy;

    for (let i = 0; i < left - 1; i++) prev = prev.next;

    let curr = prev.next;
    for (let i = 0; i < right - left; i++) {
        let next = curr.next;
        curr.next = next.next;
        next.next = prev.next;
        prev.next = next;
    }
    return dummy.next;
};
```

---

# ✅ **12\. Odd Even Linked List**

```apache
var oddEvenList = function(head) {
    if (!head) return head;

    let odd = head, even = head.next, evenHead = even;

    while (even && even.next) {
        odd.next = even.next;
        odd = odd.next;
        even.next = odd.next;
        even = even.next;
    }
    odd.next = evenHead;
    return head;
};
```

---

# ✅ **13\. Swap Nodes in Pairs**

```apache
var swapPairs = function(head) {
    let dummy = new ListNode(0, head);
    let curr = dummy;

    while (curr.next && curr.next.next) {
        let first = curr.next;
        let second = curr.next.next;

        first.next = second.next;
        second.next = first;
        curr.next = second;

        curr = curr.next.next;
    }
    return dummy.next;
};
```

---

# ✅ **14\. Reorder List**

(L1 → Ln → L2 → Ln-1 ...)

```apache
var reorderList = function(head) {
    if (!head || !head.next) return;

    // find middle
    let slow = head, fast = head;
    while (fast && fast.next) {
        fast = fast.next.next;
        slow = slow.next;
    }

    // reverse 2nd half
    let prev = null, curr = slow;
    while (curr) {
        let next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }

    // merge both halves
    let first = head, second = prev;

    while (second.next) {
        let tmp1 = first.next;
        let tmp2 = second.next;

        first.next = second;
        second.next = tmp1;

        first = tmp1;
        second = tmp2;
    }
};
```

---

# ✅ **15\. Remove Nth Node from End**

```apache
var removeNthFromEnd = function(head, n) {
    let dummy = new ListNode(0, head);
    let fast = dummy, slow = dummy;

    for (let i = 0; i <= n; i++) fast = fast.next;

    while (fast) {
        slow = slow.next;
        fast = fast.next;
    }

    slow.next = slow.next.next;
    return dummy.next;
};
```

---

# ✅ **16\. Merge K Sorted Lists**

Use the **min-heap** approach.

```apache
var mergeKLists = function(lists) {
    const heap = [];

    for (let node of lists) {
        if (node) heap.push(node);
    }

    heap.sort((a, b) => a.val - b.val);

    let dummy = new ListNode(0);
    let temp = dummy;

    while (heap.length) {
        let node = heap.shift();
        temp.next = node;
        temp = temp.next;

        if (node.next) {
            heap.push(node.next);
            heap.sort((a, b) => a.val - b.val);
        }
    }
    return dummy.next;
};
```

---

# 🎯 Conclusion

Linked Lists are not hard — they simply require **pointer thinking** instead of array thinking.  
Mastering these operations and problems above makes you interview-ready for **FAANG-level DSA**.