### 📌 Concept:

- A technique to **optimize subarray/substring problems**.
    
- Instead of recomputing for every window (brute force `O(n*k)`), we **reuse previous results** → reduces to `O(n)`.
    

---

### 📍 When to Use:

- Subarrays or substrings.
    
- Problems with **contiguous elements**.
    
- Common in:
    
    - Max/Min sum of `k` elements.
        
    - Longest substring with conditions.
        
    - Counting occurrences (anagrams, distinct chars).
        

---

### ⚡ Types of Sliding Window:

1. **Fixed Size Window** (k is given):
    
    - Example: Maximum sum subarray of size `k`.
        
    
    `int sum = 0, maxSum = 0; for(int i=0; i<k; i++) sum += arr[i]; maxSum = sum; for(int i=k; i<n; i++){     sum += arr[i] - arr[i-k];     maxSum = Math.max(maxSum, sum); }`
    
2. **Variable Size Window** (expand & shrink):
    
    - Window size is **not fixed**, depends on condition.
        
    - Example: Smallest subarray with sum ≥ target.
        
    
    `int l = 0, sum = 0, ans = n+1; for(int r=0; r<n; r++){     sum += arr[r];     while(sum >= target){         ans = Math.min(ans, r-l+1);         sum -= arr[l++];     } }`
    

---

### ⏱️ Complexity:

- Time: **O(n)**
    
- Space: **O(1)** (or `O(k)` if using map/set for characters)
    

---

### ⭐ Famous Problems:

- Max sum subarray of size `k` (fixed window)
    
- Minimum window substring (variable window)
    
- Longest substring without repeating characters
    
- Longest substring with at most `k` distinct characters
    
- Count occurrences of anagram in string
    

---

👉 **Key Idea**:

- **Expand** window → move `right` pointer.
    
- **Shrink** window → move `left` pointer until condition is valid.