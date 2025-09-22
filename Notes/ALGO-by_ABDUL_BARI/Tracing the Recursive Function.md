- The function **test(n)** prints n when n > 0 and then recursively calls **test(n‑1)**.
    
- Example with n = 3:
    

|   |   |   |
|---|---|---|
|Call order|Value printed|Next call|
|1st|3|test(2)|
|2nd|2|test(1)|
|3rd|1|test(0)|
|4th|— (no print)|stops|

- The recursion stops when n reaches **0** because the condition n > 0 fails.
    

---

## **⏱️ Time Analysis**

- **Work per call:** a single printf (or equivalent output) → **1 unit of time**.
    
- **Number of calls:** for input n, the function is invoked **n + 1** times (the extra call handles the base case n = 0).
    
- **Total time:**
    

[ T(n) = (n + 1) \times 1 = n + 1 ]

- **Complexity:**
    

> **Definition:** _Big‑O notation_ describes an upper bound on the growth rate of an algorithm.  
> The function runs in **O(n)** time (also Θ(n) and Ω(n) because the bound is tight).

---

## **📚 Formulating the Recurrence Relation**

- Let **T(n)** denote the running time of **test(n)**.
    
- Inside the function we have:
    
    1. A constant‑time check of the condition n > 0 → **c₁** (treated as 1).
        
    2. A constant‑time print → **c₂** (treated as 1).
        
    3. One recursive call **T(n‑1)**.
        
- Ignoring the negligible constant for the condition, the recurrence is:
    

[ T(n) = T(n-1) + 1 \quad \text{for } n > 0 ]

- **Base case:** when n = 0 the function does nothing but still counts as one constant‑time step, so
    

[ T(0) = 1 ]

---

## **🧩 Solving the Recurrence (Substitution / Back‑Substitution)**

1. **First expansion**  
    [ T(n) = T(n-1) + 1 ]
    
2. **Second expansion** (replace (T(n-1)))  
    [ T(n) = \bigl[T(n-2) + 1\bigr] + 1 = T(n-2) + 2 ]
    
3. **Third expansion**  
    [ T(n) = T(n-3) + 3 ]
    
4. **After k expansions**  
    [ T(n) = T(n-k) + k ]
    
5. **Choose k = n** (so that (n-k = 0))  
    [ T(n) = T(0) + n = 1 + n ]
    

- The closed‑form solution **T(n) = n + 1** matches the earlier direct counting.
    

> **Definition:** _Substitution method_ solves recurrences by repeatedly replacing the recurrence with itself until a pattern emerges, then applying the base case.

---

## **📊 Summary of Results**

|   |   |   |   |   |
|---|---|---|---|---|
|Input (n)|Calls made|Prints executed|Total time (T(n))|Asymptotic class|
|0|1|0|1|O(1)|
|1|2|1|2|O(n)|
|2|3|2|3|O(n)|
|3|4|3|4|O(n)|
|…|(n+1)|(n)|(n+1)|O(n)|

- The algorithm belongs to the **linear time class** (Θ(n)).