# Daily Learning Log – 13 September 2025

## Topic: Heap Sort

### What I Explored Today
- Learned how **Heap Sort** works using the **heap data structure**.
- Heap Sort sorts an array by first building a **Max Heap** and then repeatedly extracting the largest element.

---

### Key Points / Notes

**Heapify:**  
- Start from index `n/2 - 1` (last non-leaf node).  
- **Why?** Leaves are already valid heaps, so no need to heapify them.

**Sorting Steps:**  
1. Swap the root (largest element) with the last element → last element is now sorted.  
2. Reduce heap size and heapify the root again.  
3. Repeat until the array is fully sorted.

**Time & Space Complexity:**  
- Time: `O(n log n)`  
- Space: `O(1)` (in-place)

---

### Code I Practiced

```cpp
#include <iostream>
#include <vector>
using namespace std;

void heapify(vector<int>& arr, int idx, int size) {
    int left = 2 * idx + 1;
    int right = 2 * idx + 2;
    int maxidx = idx;

    if (left < size && arr[left] > arr[maxidx]) {
        maxidx = left;
    }
    if (right < size && arr[right] > arr[maxidx]) {
        maxidx = right;
    }

    if (maxidx != idx) {
        swap(arr[maxidx], arr[idx]);
        heapify(arr, maxidx, size);
    }
}

void HeapSort(vector<int>& arr) {
    int n = arr.size();

    // Build max heap
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(arr, i, n);
    }

    // Extract elements one by one
    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]);
        heapify(arr, 0, i);
    }
}

int main() {
    vector<int> arr{1, 4, 2, 5, 3};
    HeapSort(arr);
    for (int val : arr) {
        cout << val << " ";
    }
}
```

### It was fun to explore this algorithm and see how the largest elements get placed one by one at the end.
### Understanding why we heapify from n/2 - 1 first really clarified how heap building works.