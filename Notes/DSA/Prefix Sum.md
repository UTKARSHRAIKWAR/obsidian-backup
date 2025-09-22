### 📌 Concept:

- A **prefix sum array** stores the cumulative sum of elements from the start up to a given index.
    
- Helps in answering **range sum queries in O(1)** after **O(n) preprocessing**.
    

---

### 📍 Formula:

If `arr[]` is the original array and `prefix[]` is the prefix sum array:

prefix[i]=arr[0]+arr[1]+...+arr[i]prefix[i] = arr[0] + arr[1] + ... + arr[i]prefix[i]=arr[0]+arr[1]+...+arr[i]

Range sum for **l to r**:

sum(l,r)=prefix[r]−prefix[l−1](l>0)sum(l, r) = prefix[r] - prefix[l-1] \quad (l > 0)sum(l,r)=prefix[r]−prefix[l−1](l>0)

If `l = 0`:

sum(0,r)=prefix[r]sum(0, r) = prefix[r]sum(0,r)=prefix[r]

---

### ⚡ Example:

`int arr[] = {2, 4, 6, 8, 10}; int n = arr.length; int prefix[] = new int[n];  // Build prefix array prefix[0] = arr[0]; for(int i=1; i<n; i++){     prefix[i] = prefix[i-1] + arr[i]; }  // Query sum from index 1 to 3 int l = 1, r = 3; int rangeSum = prefix[r] - (l > 0 ? prefix[l-1] : 0); // rangeSum = 4+6+8 = 18`

---

### ⭐ Applications:

1. **Range Sum Queries** – Sum of subarray in O(1).
    
2. **Equilibrium Index** – Where left sum = right sum.
    
3. **Subarray with given sum** (with hashing).
    
4. **2D Prefix Sum (Matrix)** – For fast sub-matrix sum queries.
    
    prefix[i][j]=matrix[i][j]+prefix[i−1][j]+prefix[i][j−1]−prefix[i−1][j−1]prefix[i][j] = matrix[i][j] + prefix[i-1][j] + prefix[i][j-1] - prefix[i-1][j-1]prefix[i][j]=matrix[i][j]+prefix[i−1][j]+prefix[i][j−1]−prefix[i−1][j−1]
5. **Difference Array Technique** – Efficient range updates.
    

---

### ⏱️ Complexity:

- Build prefix: **O(n)**
    
- Query sum: **O(1)**
    

---

👉 **Key Idea**: Pre-compute sums once → Answer range queries instantly.