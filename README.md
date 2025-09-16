# unique-element-swapping-logic
Find the unique element in an array using swapping logic by Harsh Joshi
---
# Unique Element Detection Using Swapping Logic

## Introduction

This blog explains a simple yet powerful **swapping logic** to detect elements that appear an **odd number of times** in an array. The method is intuitive, easy to understand, and works efficiently in **linear time O(n)**.

---

## How the Logic Works

1. **Swap elements from both ends of the array** while counting each value’s occurrence.
2. **If the array has an odd length**, increment the middle element’s count, as it never gets swapped.
3. **After all swaps**, check which numbers have an odd count. These are the **unique elements** in the array.

---

## Example Walkthrough (Step-by-Step Tables)

### Test Case 1: `[2, 7, 7, 9, 2]`

| Step | Swap Pair | Array After Swap | swapCount Updates | Current swapCount |
| ---- | --------- | ---------------- | ----------------- | ----------------- |
| i=0  | (2, 2)    | \[2, 7, 7, 9, 2] | 2->2              | 2→2               |
| i=1  | (7, 9)    | \[2, 9, 7, 7, 2] | 7->1, 9->1        | 2→2,7→1,9→1       |
| mid  | (7)       | \[2, 9, 7, 7, 2] | 7->1              | 2→2,7→2,9→1       |

✅ **Unique element = 9**

---

### Test Case 2: `[2, 3, 4, 3, 2, 5]`

| Step | Swap Pair | Array After Swap    | swapCount Updates | Current swapCount |
| ---- | --------- | ------------------- | ----------------- | ----------------- |
| i=0  | (2, 5)    | \[5, 3, 4, 3, 2, 2] | 2->1,5->1         | 2→1,5→1           |
| i=1  | (3, 2)    | \[5, 2, 4, 3, 3, 2] | 3->1,2->1         | 2→2,3→1,5→1       |
| i=2  | (4, 3)    | \[5, 2, 3, 4, 3, 2] | 4->1,3->1         | 2→2,3→2,4→1,5→1   |

✅ **Unique elements = 4, 5**

---

## Code Implementation (Universal Version)

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>
using namespace std;

void findUnique(vector<int> arr) {
    int n = arr.size();
    unordered_map<int, int> swapCount;

    // Step 1: perform swapping and count swaps
    for (int i = 0; i < n / 2; i++) {
        int temp = arr[i];
        arr[i] = arr[n - i - 1];
        arr[n - i - 1] = temp;

        swapCount[arr[i]]++;
        swapCount[arr[n - i - 1]]++;
    }

    // Step 2: handle middle element if odd
    if (n % 2 == 1) {
        swapCount[arr[n / 2]]++;
    }

    // Debug: print array after swaps
    cout << "Array after swaps: ";
    for (int v : arr) cout << v << " ";
    cout << endl;

    // Debug: print swap counts
    cout << "Swap counts: ";
    for (auto &p : swapCount) {
        cout << p.first << "->" << p.second << " ";
    }
    cout << endl;

    // Step 3: detect unique elements
    vector<int> uniques;
    for (auto &p : swapCount) {
        if (p.second % 2 == 1) {
            uniques.push_back(p.first);
        }
    }

    // Step 4: print result
    if (uniques.empty()) {
        cout << "✅ No unique element (all paired)" << endl << endl;
    } else {
        cout << "✅ Unique elements = ";
        for (int u : uniques) cout << u << " ";
        cout << endl << endl;
    }
}

int main() {
    vector<int> arr1 = {2, 7, 7, 9, 2};
    vector<int> arr2 = {2, 3, 4, 3, 2, 5};
    vector<int> arr3 = {-2, -3, -2, -3, 9};
    vector<int> arr4 = {1000000, 2, 2, 1000000, 9};

    findUnique(arr1);
    findUnique(arr2);
    findUnique(arr3);
    findUnique(arr4);

    return 0;
}
```

---

## Strengths vs Limitations

**Strengths:**

* Easy to understand and explain step-by-step.
* Linear time complexity O(n).
* Universal version works with negative numbers, huge values, and multiple unique elements.
* Works even for empty arrays or single-element arrays.

**Limitations:**

* Original fixed-array version only works for non-negative numbers ≤ MAX.
* Original version only detects the first unique element if multiple exist.
* Order of unique elements in `unordered_map` output may not match array order.

---

## Credit & Author

This swapping logic for detecting unique elements was **originally discovered and implemented by Harsh Joshi**.
It demonstrates a simple yet effective approach to identifying odd-frequency elements in an array using swaps and counting.

Feel free to **share, study, and implement** this logic, but please give credit to the author when referencing or posting online.

---

