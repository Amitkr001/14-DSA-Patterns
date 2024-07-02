Sure! Here's a README file that includes the expanded content for the first two patterns. We will follow the same format for the remaining patterns.

```markdown
# 14 Coding Patterns To Master

This is a collection of coding patterns to help you solve some of the most common problems encountered in coding interviews. These 14 patterns condense 6 months of preparation into a concise guide that you can master in 1-2 weeks. These patterns cover a wide range of problems and will become familiar over time. Good luck!

Please feel free to comment if you got some value or find any errors!

## Table of Contents
1. Sliding Window
2. Two Pointers or Iterators
3. Fast and Slow Pointers
4. Merge Intervals
5. Cyclic Sort
6. In-place Reversal of a Linked List
7. Tree Breadth First Search
8. Tree Depth First Search
9. Two Heaps
10. Subsets
11. Modified Binary Search
12. Top K Elements
13. K-way Merge
14. Topological Sort

## 1. Sliding Window

### Explanation
The sliding window pattern is useful for problems involving arrays or strings where you need to find a subrange or contiguous subarray that meets certain criteria. This technique avoids the need for nested loops, reducing the time complexity to O(n).

### Template

```cpp
vector<int> slidingWindow(vector<int>& arr, int k) {
    vector<int> result;
    int windowSum = 0, windowStart = 0;
    for (int windowEnd = 0; windowEnd < arr.size(); windowEnd++) {
        windowSum += arr[windowEnd];  // add the next element
        if (windowEnd >= k - 1) {  // slide the window
            result.push_back(windowSum);
            windowSum -= arr[windowStart];
            windowStart++;
        }
    }
    return result;
}
```

### Questions

1. **Maximum Sum Subarray of Size K**: [LeetCode](https://leetcode.com/problems/maximum-sum-subarray-of-size-k)
2. **Smallest Subarray with a given sum**: [LeetCode](https://leetcode.com/problems/minimum-size-subarray-sum)
3. **Longest Substring with K Distinct Characters**: [LeetCode](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters)
4. **Fruits into Baskets**: [LeetCode](https://leetcode.com/problems/fruit-into-baskets)
5. **No-repeat Substring**: [LeetCode](https://leetcode.com/problems/longest-substring-without-repeating-characters)
6. **Longest Substring with Same Letters after Replacement**: [LeetCode](https://leetcode.com/problems/longest-repeating-character-replacement)
7. **Longest Subarray with Ones after Replacement**: [LeetCode](https://leetcode.com/problems/max-consecutive-ones-iii)
8. **Permutation in a String**: [LeetCode](https://leetcode.com/problems/permutation-in-string)
9. **String Anagrams**: [LeetCode](https://leetcode.com/problems/find-all-anagrams-in-a-string)
10. **Smallest Window containing Substring**: [LeetCode](https://leetcode.com/problems/minimum-window-substring)

### Example Solution

#### 1. Maximum Sum Subarray of Size K

```cpp
#include <iostream>
#include <vector>
using namespace std;

int maxSumSubarray(vector<int>& arr, int k) {
    int maxSum = 0, windowSum = 0;
    for (int i = 0; i < k; i++) {
        windowSum += arr[i];
    }
    maxSum = windowSum;
    for (int i = k; i < arr.size(); i++) {
        windowSum += arr[i] - arr[i - k];
        maxSum = max(maxSum, windowSum);
    }
    return maxSum;
}

int main() {
    vector<int> arr = {2, 1, 5, 1, 3, 2};
    int k = 3;
    cout << "Maximum sum of a subarray of size " << k << " is: " << maxSumSubarray(arr, k);
    return 0;
}
```

---

## 2. Two Pointers

### Explanation
The two pointers pattern is useful for problems involving sorted arrays or linked lists where you need to find pairs with a specific sum or move elements based on conditions.

### Template

```cpp
vector<int> twoPointers(vector<int>& arr, int target) {
    vector<int> result;
    int left = 0, right = arr.size() - 1;
    while (left < right) {
        int currentSum = arr[left] + arr[right];
        if (currentSum == target) {
            result.push_back(left);
            result.push_back(right);
            break;
        }
        if (currentSum < target) {
            left++;
        } else {
            right--;
        }
    }
    return result;
}
```

### Questions

1. **Pair with Target Sum**: [LeetCode](https://leetcode.com/problems/two-sum)
2. **Remove Duplicates**: [LeetCode](https://leetcode.com/problems/remove-duplicates-from-sorted-array)
3. **Squaring a Sorted Array**: [LeetCode](https://leetcode.com/problems/squares-of-a-sorted-array)
4. **Triplet Sum to Zero**: [LeetCode](https://leetcode.com/problems/3sum)
5. **Triplets with Smaller Sum**: [LeetCode](https://leetcode.com/problems/3sum-smaller)
6. **Subarrays with Product Less than a Target**: [LeetCode](https://leetcode.com/problems/subarray-product-less-than-k)
7. **Dutch National Flag Problem**: [LeetCode](https://leetcode.com/problems/sort-colors)
8. **4Sum**: [LeetCode](https://leetcode.com/problems/4sum)
9. **Backspace Compare**: [LeetCode](https://leetcode.com/problems/backspace-string-compare)
10. **Subsequence of another String**: [LeetCode](https://leetcode.com/problems/is-subsequence)

### Example Solution

#### 1. Pair with Target Sum

```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<int> pairWithTargetSum(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    while (left < right) {
        int currentSum = arr[left] + arr[right];
        if (currentSum == target) {
            return {left, right};
        }
        if (currentSum < target) {
            left++;
        } else {
            right--;
        }
    }
    return {-1, -1};
}

int main() {
    vector<int> arr = {1, 2, 3, 4, 6};
    int target = 6;
    vector<int> result = pairWithTargetSum(arr, target);
    cout << "Pair with target sum: [" << result[0] << ", " << result[1] << "]";
    return 0;
}
```

---

## 3. Fast and Slow Pointers

### Explanation
The fast and slow pointers pattern is useful for problems related to cyclic linked lists or arrays. This technique helps in detecting cycles, finding the middle of a linked list, etc.

### Template

```cpp
bool hasCycle(ListNode* head) {
    ListNode *slow = head, *fast = head;
    while (fast != nullptr && fast->next != nullptr) {
        fast = fast->next->next;
        slow = slow->next;
        if (fast == slow) return true;
    }
    return false;
}
```

### Questions

1. **Linked List Cycle**: [LeetCode](https://leetcode.com/problems/linked-list-cycle)
2. **Happy Number**: [LeetCode](https://leetcode.com/problems/happy-number)
3. **Middle of the Linked List**: [LeetCode](https://leetcode.com/problems/middle-of-the-linked-list)
4. **Palindrome Linked List**: [LeetCode](https://leetcode.com/problems/palindrome-linked-list)
5. **Cycle in Circular Array**: [LeetCode](https://leetcode.com/problems/circular-array-loop)
6. **Reorder List**: [LeetCode](https://leetcode.com/problems/reorder-list)
7. **Remove Nth Node From End of List**: [LeetCode](https://leetcode.com/problems/remove-nth-node-from-end-of-list)
8. **Find the Duplicate Number**: [LeetCode](https://leetcode.com/problems/find-the-duplicate-number)
9. **Linked List Cycle II**: [LeetCode](https://leetcode.com/problems/linked-list-cycle-ii)
10. **Intersection of Two Linked Lists**: [LeetCode](https://leetcode.com/problems/intersection-of-two-linked-lists)

### Example Solution

#### 1. Linked List Cycle

```cpp
#include <iostream>
using namespace std;

struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

bool hasCycle(ListNode *head) {
    ListNode *slow = head, *fast = head;
    while (fast != nullptr && fast->next != nullptr) {
        fast = fast->next->next;
        slow = slow->next;
        if (fast == slow) return true;
    }
    return false;
}

int main() {
    ListNode*

 head = new ListNode(3);
    head->next = new ListNode(2);
    head->next->next = new ListNode(0);
    head->next->next->next = new ListNode(-4);
    head->next->next->next->next = head->next; // creates a cycle

    cout << "Linked list has cycle: " << (hasCycle(head) ? "true" : "false");
    return 0;
}
```

---

Please review this structure and let me know if it works for you. We can continue with the remaining patterns in the same format.
```
