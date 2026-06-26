
## 1. Intuition
- **Goal:** Find a target or a boundary in logarithmic time.
- **Prerequisite:** Data must be sorted OR the "search space" must be monotonic (e.g., F, F, F, T, T, T).
- **Core Mechanism:** Discard half of the possibilities in every step.

## 2. Core Algorithms

### 2.1 Standard Binary Search
-  **When to use:** Exact match in sorted array.
-  **Complexity:** $O(\log n)$.
-  **Notes:** Handles standard lookups.

```cpp
int binarySearch(vector<int>& nums, int target) {
    int l = 0, r = nums.size() - 1;
    while (l <= r) {
        int mid = l + (r - l) / 2;
        if (nums[mid] == target) return mid;
        if (nums[mid] < target) l = mid + 1;
        else r = mid - 1;
    }
    return -1;
}
```

### 2.2 Binary Search on Answer Space (Min/Max)
-  **When to use:** Exact match in sorted array.
-  **Complexity:** $O(\log n)$.
-  **Notes:** Handles standard lookups.