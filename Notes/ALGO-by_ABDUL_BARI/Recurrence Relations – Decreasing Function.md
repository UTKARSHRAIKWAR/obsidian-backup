> **Recurrence relation** – An equation that expresses the running time (T(n)) of an algorithm in terms of the running time on a smaller input size (e.g., (T(n-1))) plus the work done at the current level.

### **1️⃣ Deriving the Recurrence**

- The algorithm receives an integer **n**.
    
- It makes a **recursive call** with argument (n-1).
    
- Inside each call there is a **for‑loop** that iterates **n** times.
    

|   |   |
|---|---|
|Operation|Cost (units)|
|Loop condition check|1|
|Loop body (executed (n) times)|(n)|
|Recursive call (T(n-1))|(T(n-1))|
|**Total**|**(T(n) = T(n-1) + n)**|

_The constant terms (e.g., “+2”) are absorbed into Θ‑notation, so we write the recurrence as_

[ T(n) = T(n-1) + n \qquad (n > 0), \quad T(0) = 1 ]

### **2️⃣ Solving with the** **Recursion‑Tree** **Method**

1. **Level 0**: cost (n)
    
2. **Level 1**: cost (n-1) (from the recursive call)
    
3. **Level 2**: cost (n-2)
    
4. …
    
5. **Level (n)**: cost 0 (base case)
    

Summing the costs:

[ \sum_{i=0}^{n} i = \frac{n(n+1)}{2} ]

- Hence (T(n) = \frac{n(n+1)}{2} = \Theta(n^{2})).
    

### **3️⃣ Solving with** **Back‑Substitution / Induction**

|   |   |
|---|---|
|Substitution step|Expression|
|**0** (original)|(T(n) = T(n-1) + n)|
|**1**|(T(n) = T(n-2) + (n-1) + n)|
|**2**|(T(n) = T(n-3) + (n-2) + (n-1) + n)|
|**k**|(T(n) = T(n-k) + \displaystyle\sum_{j=0}^{k-1} (n-j))|

- Stop when (n-k = 0 \Rightarrow k = n).
    
- Substitute (k = n):
    

[ T(n) = T(0) + \sum_{j=0}^{n-1} (n-j) = 1 + \sum_{i=1}^{n} i ]

- The sum of the first (n) natural numbers is (\frac{n(n+1)}{2}).
    

[ \boxed{T(n) = \frac{n(n+1)}{2} = \Theta(n^{2})} ]

### **4️⃣ Key Concepts & Notations**

> **Θ‑notation** – Tight bound: (f(n) = \Theta(g(n))) means (c_1 g(n) \le f(n) \le c_2 g(n)) for some constants (c_1, c_2 > 0) and sufficiently large (n).

> **Recursion‑tree method** – Visualize each recursive call as a tree node; sum the work across all levels.

> **Back‑substitution (induction)** – Repeatedly replace (T(\cdot)) using the recurrence until a base case appears, then identify a pattern and prove it by induction.

### **5️⃣ Quick Reference Table**

|   |   |   |
|---|---|---|
|Method|Steps|Result|
|**Recursion tree**|List costs per level → sum arithmetic series|(\frac{n(n+1)}{2})|
|**Back substitution**|Expand (T(n)) repeatedly → reach (T(0)) → sum series|(\frac{n(n+1)}{2})|
|**Big‑Theta**|Drop lower‑order terms & constants|(\Theta(n^{2}))|

### **6️⃣ Practical Tips for Exams**

- **Identify** the loop count and recursive call size → write the recurrence.
    
- **Simplify** constant‑time parts using Θ‑notation before solving.
    
- **Choose** a solving technique you’re comfortable with (tree vs. substitution).
    
- **Verify** the final expression by checking base case (T(0)).