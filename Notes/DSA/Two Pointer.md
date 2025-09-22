### 📌 Concept:

- Use **two indices (pointers)** to traverse data (usually arrays/strings).
    
- Helps **reduce time complexity** (often from `O(n²)` → `O(n)`).
    

---

### 📍 When to Use:

- Sorted arrays or strings.
    
- Searching for pairs/triplets.
    
- Sliding window problems.
    
- Removing duplicates / partitioning.
    

---

### ⚡ Common Patterns:

1. **Opposite Ends** (start + end):
    
    - Use when looking for a sum, product, or condition.
        
    - Example: _Pair with target sum in sorted array_.
        
    
    `int l = 0, r = n-1; while(l < r){     if(arr[l] + arr[r] == target) return true;     else if(arr[l] + arr[r] < target) l++;     else r--; }`
    
2. **Same Direction (Slow + Fast):**
    
    - One pointer moves fast, the other slow.
        
    - Example: _Remove duplicates, Linked List cycle detection_.
        
    
    `int i = 0; for(int j = 1; j < n; j++){     if(arr[i] != arr[j]){         i++;         arr[i] = arr[j];     } }`
    
3. **Sliding Window (variable size):**
    
    - Expand `right`, shrink `left` until condition is met.
        
    - Example: _Smallest substring / max sum subarray_.
        
    
    `int l = 0, sum = 0, ans = n+1; for(int r = 0; r < n; r++){     sum += arr[r];     while(sum >= target){         ans = Math.min(ans, r-l+1);         sum -= arr[l++];     } }`
    

---

### ⏱️ Time Complexity:

- Typically `O(n)` (since each element is processed at most once).
    

---

### ⭐ Famous Problems:

- Pair Sum / 3-Sum / 4-Sum
    
- Container With Most Water
    
- Trapping Rain Water
    
- Longest Substring Without Repeating Characters
    
- Remove Duplicates from Sorted Array
    
- Linked List Cycle Detection

# 📝 Two Pointer Approach

- **Definition**: Technique where two indices (pointers) are used to traverse an array/string efficiently.
    
- **When to Use**:
    
    - Searching pairs/triplets (e.g., sum problems).
        
    - Removing duplicates.
        
    - Problems on sorted arrays/strings.
        
- **Types**:
    
    1. **Opposite Ends** → One pointer at start, one at end.
        
        - Example: Find if array has pair with sum = target.
            
    2. **Same Direction** → Both pointers move forward.
        
        - Example: Remove duplicates, sliding window.
            
- **Time Complexity**: O(n) (instead of O(n²) brute force).
    
- **Pseudocode (Pair Sum)**:
    
    `left = 0, right = n-1 while left < right:     if arr[left] + arr[right] == target:         return True     elif arr[left] + arr[right] < target:         left++     else:         right--`