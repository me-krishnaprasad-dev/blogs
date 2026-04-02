# Mastering the Two Heaps Pattern

## 1. Introduction: The Airport Dilemma
Imagine you’re managing a busy airport. Flights are constantly landing and taking off. You need to quickly find the next most important flight—perhaps an emergency landing (high priority) or a VIP departure. At the same time, new flights are constantly being added to the schedule. 

If you use a simple list, finding the highest-priority flight takes **O(n)** time because you have to scan everything. In a fast-paced environment, this is too slow.

**The Solution: Heaps.**
A Heap is a specialized tree-based data structure that allows us to:
1.  **Add** an element in $O(\log n)$.
2.  **Remove** the most "important" element in $O(\log n)$.
3.  **Peek** at the most "important" element in $O(1)$.

---

## 2. Heap Basics
A heap is a binary tree that follows the **Heap Property**:

| Type | Property | Priority |
| :--- | :--- | :--- |
| **Min Heap** | Each node is smaller than or equal to its children. | Root is the **Minimum** value. |
| **Max Heap** | Each node is greater than or equal to its children. | Root is the **Maximum** value. |

> **Note:** A **Priority Queue** is the abstract data type we use in programming (like Java) to implement this heap behavior.

---

## 3. Why *Two* Heaps?
While one heap gives us the smallest or largest element, some problems require us to divide data into two parts. The **Two Heaps Pattern** is typically used when we need to find a specific value (like a median) from a stream of data where elements are constantly being added.

### The Strategy:
We split the data into two halves:
1.  **A Max-Heap** to store the **smaller half** of the numbers.
2.  **A Min-Heap** to store the **larger half** of the numbers.

By doing this, the "middle" of our data is always sitting at the roots of the two heaps!

---

## 4. Implementation in Java
In Java, we use the `PriorityQueue` class. By default, it is a **Min-Heap**.

```java
import java.util.PriorityQueue;
import java.util.Collections;

public class HeapExample {
    public static void main(String[] args) {
        // 1. Min-Heap (Default)
        // Stores elements in ascending order (smallest at the top)
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        // 2. Max-Heap (Using Collections.reverseOrder())
        // Stores elements in descending order (largest at the top)
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

        // Common Operations:
        minHeap.add(10);      // O(log N)
        minHeap.poll();       // O(log N) - removes and returns root
        minHeap.peek();       // O(1) - looks at root without removing
    }
}
```

---

## 5. The "Two Heaps" Sub-Patterns
When solving LeetCode problems, look for these three common scenarios:

### Pattern A: Find the Median
*   **Goal:** Find the middle element of a dynamic data stream.
*   **Logic:** 
    *   `maxHeap` stores the left side, `minHeap` stores the right side.
    *   The median is either the top of the larger heap or the average of both tops.
*   **Balance Rule:** Ensure `maxHeap.size()` is equal to or one greater than `minHeap.size()`.

### Pattern B: Sliding Window Median
*   **Goal:** Find the median of all elements in every window of size `K`.
*   **Logic:** Same as finding the median, but you must also **remove** the element that slides out of the window from one of the heaps.

### Pattern C: Task Scheduling / IPO
*   **Goal:** Maximize profit or minimize time given constraints (like capital or deadlines).
*   **Logic:** 
    *   One heap to store "available" tasks (based on start time/capital).
    *   A second heap to store "profitable" tasks (based on reward/priority).

---

## 6. Time & Space Complexity
*   **Insert/Delete:** $O(\log n)$
*   **Find Median/Peek:** $O(1)$
*   **Space:** $O(n)$ to store $n$ elements in the heaps.

---

## 7. Problem Tracking List
*This is where I will document my progress with the Two Heaps pattern.*

| Problem # | Difficulty | Title | Key Learning |
| :--- | :--- | :--- | :--- |
| **LC 1942** | Medium | [The Number of the Smallest Unoccupied Chair](https://leetcode.com/problems/the-number-of-the-smallest-unoccupied-chair/solutions/7745668/smallest-unoccupied-chair-problem-using-l6kll) | *Two Heaps: one for available chairs and one for departure times.* |


---

### Tips for Success:
1.  **Always Balance:** After every insertion, check if one heap has $>1$ more element than the other. If so, move the root of the larger heap to the smaller one.
2.  **Handle Evens/Odds:** If the total number of elements is even, the median is the average of both roots. If odd, it's the root of the heap with more elements.
3.  **Data Types:** For LeetCode problems involving large numbers or averages, use `Double` or `Long` to avoid overflow!
