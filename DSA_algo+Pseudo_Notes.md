# Unit 1: Algorithms Reference Guide
*Resource: GeeksforGeeks*

---

## Part 1: Sorting Algorithms

### 1. Insertion Sort

**Logic:** Iteratively builds a sorted portion of the array by picking the next element and inserting it into its correct position.

**Algorithm:**
1. **Iterate:** Start from the second element (index 1) to the end of the array.
2. **Key:** Store the current element as the key.
3. **Compare:** Compare the key with the elements to its left (the sorted part).
4. **Shift:** While the element to the left is greater than the key, shift that element one position to the right.
5. **Insert:** Place the key into its correct sorted position.
6. **Repeat** until the entire array is sorted.

**Pseudocode:**
```
INSERTION-SORT(A):
  for i = 1 to length(A) - 1:
    key = A[i]
    j = i - 1
    while j >= 0 AND A[j] > key:
      A[j + 1] = A[j]
      j = j - 1
    A[j + 1] = key
```

---

### 2. Merge Sort

**Logic:** A recursive Divide and Conquer algorithm that divides the array into halves, sorts them, and then merges them.

**Algorithm:**
1. **Divide:** Find the middle point of the array: `mid = (left + right) / 2`.
2. **Conquer:** Recursively call mergeSort for the left half and the right half.
3. **Merge:**
   - Create two temporary subarrays (Left and Right).
   - Compare the smallest elements of each subarray.
   - Copy the smaller element into the original array.
   - Continue until all elements from both subarrays are placed back.
4. **Base Case:** The recursion stops when the array size is 1.

**Pseudocode:**
```
MERGE-SORT(A, left, right):
  if left < right:
    mid = (left + right) / 2
    MERGE-SORT(A, left, mid)
    MERGE-SORT(A, mid + 1, right)
    MERGE(A, left, mid, right)

MERGE(A, left, mid, right):
  n1 = mid - left + 1
  n2 = right - mid
  create arrays L[0..n1] and R[0..n2]

  for i = 0 to n1 - 1:
    L[i] = A[left + i]
  for j = 0 to n2 - 1:
    R[j] = A[mid + 1 + j]

  i = 0, j = 0, k = left
  while i < n1 AND j < n2:
    if L[i] <= R[j]:
      A[k] = L[i]
      i = i + 1
    else:
      A[k] = R[j]
      j = j + 1
    k = k + 1

  while i < n1:
    A[k] = L[i]
    i = i + 1
    k = k + 1

  while j < n2:
    A[k] = R[j]
    j = j + 1
    k = k + 1
```

---

### 3. Quick Sort

**Logic:** Picks a 'pivot' element and partitions the array around it so that smaller elements are on the left and larger ones are on the right.

**Algorithm:**
1. **Pivot Selection:** Pick an element as the pivot (e.g., the last element).
2. **Partitioning:**
   - Initialize an index `i` to track elements smaller than the pivot.
   - Traverse the array; if an element is smaller than the pivot, swap it with the element at index `i` and increment `i`.
   - Finally, swap the pivot into its correct position (at index `i`).
3. **Recurse:** Recursively apply the same logic to the sub-array on the left of the pivot and the sub-array on the right.

**Pseudocode:**
```
QUICK-SORT(A, low, high):
  if low < high:
    pivotIndex = PARTITION(A, low, high)
    QUICK-SORT(A, low, pivotIndex - 1)
    QUICK-SORT(A, pivotIndex + 1, high)

PARTITION(A, low, high):
  pivot = A[high]
  i = low - 1

  for j = low to high - 1:
    if A[j] < pivot:
      i = i + 1
      swap(A[i], A[j])

  swap(A[i + 1], A[high])
  return i + 1
```

---

### 4. Heap Sort

**Logic:** Uses a Binary Heap data structure to find the maximum (or minimum) element and move it to the end of the array.

**Algorithm:**
1. **Build Max-Heap:** Transform the input array into a Max-Heap (where the parent is always larger than its children).
2. **Extract Max:**
   - Swap the root (largest element) with the last element of the heap.
   - Decrease the heap size by 1.
3. **Heapify:** Call the heapify function on the new root to restore the Max-Heap property.
4. **Repeat** steps 2 and 3 until the heap size is 1.

**Pseudocode:**
```
HEAP-SORT(A):
  n = length(A)

  // Build Max-Heap
  for i = floor(n / 2) - 1 downto 0:
    HEAPIFY(A, n, i)

  // Extract elements one by one
  for i = n - 1 downto 1:
    swap(A[0], A[i])
    HEAPIFY(A, i, 0)

HEAPIFY(A, n, i):
  largest = i
  left    = 2 * i + 1
  right   = 2 * i + 2

  if left < n AND A[left] > A[largest]:
    largest = left
  if right < n AND A[right] > A[largest]:
    largest = right

  if largest != i:
    swap(A[i], A[largest])
    HEAPIFY(A, n, largest)
```

---

## Part 2: Tree-Based Data Structures

### 1. Binary Search Tree (BST)

**Insertion Algorithm:**
1. Start from the root.
2. If the new value is less than the current node, move to the left child.
3. If the new value is greater, move to the right child.
4. Repeat until a NULL spot is found and insert the node.

**Pseudocode (Insertion):**
```
BST-INSERT(root, value):
  if root == NULL:
    return NEW-NODE(value)
  if value < root.data:
    root.left = BST-INSERT(root.left, value)
  else if value > root.data:
    root.right = BST-INSERT(root.right, value)
  return root
```

**Deletion Algorithm:**
1. **Search:** Locate the node to delete.
2. **Case 1 (No child):** Simply remove the node.
3. **Case 2 (One child):** Replace the node with its child.
4. **Case 3 (Two children):** Find the **Inorder Successor** (smallest in the right subtree), replace the node's value with it, and delete the successor.

**Pseudocode (Deletion):**
```
BST-DELETE(root, value):
  if root == NULL:
    return NULL

  if value < root.data:
    root.left = BST-DELETE(root.left, value)
  else if value > root.data:
    root.right = BST-DELETE(root.right, value)
  else:
    // Case 1 & 2: No child or one child
    if root.left == NULL:
      return root.right
    else if root.right == NULL:
      return root.left

    // Case 3: Two children — find inorder successor
    successor = FIND-MIN(root.right)
    root.data = successor.data
    root.right = BST-DELETE(root.right, successor.data)

  return root

FIND-MIN(node):
  while node.left != NULL:
    node = node.left
  return node
```

---

### 2. AVL Tree (Self-Balancing)

**Insertion Algorithm:**
1. Perform standard BST insertion.
2. **Update Height:** Update the height of the current node.
3. **Check Balance:** Calculate Balance Factor (`BF = height(left) - height(right)`).
4. **Rotate:** If `BF > 1` or `BF < -1`, perform rotations:
   - **LL:** Right Rotation
   - **RR:** Left Rotation
   - **LR:** Left-Right Rotation
   - **RL:** Right-Left Rotation

**Pseudocode (Insertion):**
```
AVL-INSERT(root, value):
  // Step 1: Standard BST insert
  if root == NULL:
    return NEW-NODE(value)
  if value < root.data:
    root.left = AVL-INSERT(root.left, value)
  else if value > root.data:
    root.right = AVL-INSERT(root.right, value)
  else:
    return root  // Duplicates not allowed

  // Step 2: Update height
  root.height = 1 + MAX(HEIGHT(root.left), HEIGHT(root.right))

  // Step 3: Check balance factor
  BF = HEIGHT(root.left) - HEIGHT(root.right)

  // Step 4: Rotations
  if BF > 1 AND value < root.left.data:       // LL Case
    return RIGHT-ROTATE(root)
  if BF < -1 AND value > root.right.data:     // RR Case
    return LEFT-ROTATE(root)
  if BF > 1 AND value > root.left.data:       // LR Case
    root.left = LEFT-ROTATE(root.left)
    return RIGHT-ROTATE(root)
  if BF < -1 AND value < root.right.data:     // RL Case
    root.right = RIGHT-ROTATE(root.right)
    return LEFT-ROTATE(root)

  return root

RIGHT-ROTATE(z):
  y = z.left
  T3 = y.right
  y.right = z
  z.left = T3
  z.height = 1 + MAX(HEIGHT(z.left), HEIGHT(z.right))
  y.height = 1 + MAX(HEIGHT(y.left), HEIGHT(y.right))
  return y

LEFT-ROTATE(z):
  y = z.right
  T2 = y.left
  y.left = z
  z.right = T2
  z.height = 1 + MAX(HEIGHT(z.left), HEIGHT(z.right))
  y.height = 1 + MAX(HEIGHT(y.left), HEIGHT(y.right))
  return y
```

**Deletion Algorithm:**
1. Perform standard BST deletion.
2. Update heights and check Balance Factor for every node moving up to the root.
3. Perform necessary rotations to restore balance.

**Pseudocode (Deletion):**
```
AVL-DELETE(root, value):
  // Step 1: Standard BST delete
  if root == NULL:
    return NULL
  if value < root.data:
    root.left = AVL-DELETE(root.left, value)
  else if value > root.data:
    root.right = AVL-DELETE(root.right, value)
  else:
    if root.left == NULL OR root.right == NULL:
      root = root.left OR root.right
    else:
      successor = FIND-MIN(root.right)
      root.data = successor.data
      root.right = AVL-DELETE(root.right, successor.data)

  if root == NULL:
    return root

  // Step 2: Update height
  root.height = 1 + MAX(HEIGHT(root.left), HEIGHT(root.right))

  // Step 3: Rebalance
  BF = HEIGHT(root.left) - HEIGHT(root.right)

  if BF > 1 AND HEIGHT(root.left.left) >= HEIGHT(root.left.right):   // LL
    return RIGHT-ROTATE(root)
  if BF > 1 AND HEIGHT(root.left.left) < HEIGHT(root.left.right):    // LR
    root.left = LEFT-ROTATE(root.left)
    return RIGHT-ROTATE(root)
  if BF < -1 AND HEIGHT(root.right.right) >= HEIGHT(root.right.left): // RR
    return LEFT-ROTATE(root)
  if BF < -1 AND HEIGHT(root.right.right) < HEIGHT(root.right.left):  // RL
    root.right = RIGHT-ROTATE(root.right)
    return LEFT-ROTATE(root)

  return root
```

---

### 3. Heap (Min / Max)

**Insertion Algorithm:**
1. Add the new element to the bottom-rightmost spot (end of the array).
2. **Heapify-Up:** Compare with the parent; if the property is violated (e.g., child > parent in Max-Heap), swap them.
3. Repeat until the root is reached or the property is satisfied.

**Pseudocode (Insertion):**
```
HEAP-INSERT(A, value):
  append value to end of A
  i = length(A) - 1

  // Heapify-Up
  while i > 0:
    parent = floor((i - 1) / 2)
    if A[i] > A[parent]:        // For Max-Heap; flip for Min-Heap
      swap(A[i], A[parent])
      i = parent
    else:
      break
```

**Deletion Algorithm (Root):**
1. Replace the root with the last element in the heap.
2. Remove the last element.
3. **Heapify-Down:** Compare the new root with its children and swap with the larger (Max) or smaller (Min) child.
4. Repeat until the heap property is restored.

**Pseudocode (Deletion):**
```
HEAP-DELETE-ROOT(A):
  A[0] = A[length(A) - 1]
  remove last element of A
  n = length(A)

  // Heapify-Down
  i = 0
  while True:
    left  = 2 * i + 1
    right = 2 * i + 2
    largest = i

    if left < n AND A[left] > A[largest]:
      largest = left
    if right < n AND A[right] > A[largest]:
      largest = right

    if largest != i:
      swap(A[i], A[largest])
      i = largest
    else:
      break
```

---

## Part 3: Priority Queue using Heaps

**Logic:** A priority queue uses a Max-Heap (for highest priority) or Min-Heap (for lowest priority) to manage elements.

**Algorithms:**
1. **Insert (Enqueue):** Use the **Heap Insertion** algorithm (add to end, then Heapify-Up).
2. **Extract Max/Min (Dequeue):** Use the **Heap Deletion** algorithm (swap root with last, remove last, then Heapify-Down).
3. **Peek:** Simply return the root element of the heap (`O(1)`).

**Pseudocode:**
```
PQ-ENQUEUE(A, value):
  HEAP-INSERT(A, value)          // Add and Heapify-Up

PQ-DEQUEUE(A):
  if A is empty:
    return NULL
  max = A[0]
  HEAP-DELETE-ROOT(A)            // Swap, remove, and Heapify-Down
  return max

PQ-PEEK(A):
  if A is empty:
    return NULL
  return A[0]                    // Root is always max (or min)
```

---

## Complexity Summary

### Part 1: Sorting Algorithms

> Note: **Quick Sort** is often the fastest in practice despite its worst-case scenario, while **Merge Sort** provides the most consistency.

| Algorithm | Logic Style | Best Case | Worst Case | Space Complexity |
|---|---|---|---|---|
| **Insertion Sort** | Incremental / Sub-list | O(n) | O(n²) | O(1) |
| **Merge Sort** | Divide & Conquer | O(n log n) | O(n log n) | O(n) |
| **Quick Sort** | Partitioning | O(n log n) | O(n²) | O(log n) |
| **Heap Sort** | Selection / Tree-based | O(n log n) | O(n log n) | O(1) |

---

### Part 2: Tree-Based Data Structures

> Complexity refers to **Search, Insertion, and Deletion** operations.

| Structure | Logic Style | Best Case | Worst Case | Space Complexity |
|---|---|---|---|---|
| **BST** | Hierarchical / Ordered | O(log n) | O(n) — Skewed | O(n) |
| **AVL Tree** | Self-Balancing BST | O(log n) | O(log n) | O(n) |
| **Heap** | Complete Binary Tree | O(1) — FindMax/Min | O(log n) — Insert/Delete | O(n) |

---

### Part 3: Priority Queue (using Heaps)

> A Priority Queue is an abstract data type usually implemented with a Heap to ensure the highest (or lowest) priority item is always at the top.

| Operation | Logic Style | Average Case | Worst Case | Space Complexity |
|---|---|---|---|---|
| **Insertion** | Heapify-Up | O(1) | O(log n) | O(1) |
| **Deletion (Extract)** | Heapify-Down | O(log n) | O(log n) | O(1) |
| **Peek (Find Max/Min)** | Root Access | O(1) | O(1) | O(1) |