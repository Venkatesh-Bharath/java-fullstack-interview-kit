

## **First Round: Pen and Paper (Coding Question)**  

### **Question 1:**  
Given an array, find the number of target element pairs whose sum equals the target value.  

#### **Example**  
**Input:**  
```  
arr = [1,3,4,5,1,5,0,-1]  
target = 4  
```  
**Pairs:** (1,3), (4,0), (5,-1) → **Output: 3**  

#### **Answer (Java)**
```java
import java.util.*;

public class TargetPairCount {
    public static int countPairs(int[] arr, int target) {
        Set<Integer> seen = new HashSet<>();
        int count = 0;
        for (int num : arr) {
            if (seen.contains(target - num)) {
                count++;
            }
            seen.add(num);
        }
        return count;
    }

    public static void main(String[] args) {
        int[] arr = {1, 3, 4, 5, 1, 5, 0, -1};
        int target = 4;
        System.out.println(countPairs(arr, target)); // Output: 3
    }
}
```

---

## **Second Round: Technical Interview**  

### **Question 2:**  
Given an array, replace each element with the **next largest element**. If no larger element exists, replace it with -1.  

#### **Example**  
**Input:** `[1,2,0,4,11,0,1]`  
**Output:** `[2,4,4,11,-1,1,-1]`  

#### **Answer (Java)**
```java
import java.util.*;

public class NextGreaterElement {
    public static int[] nextGreater(int[] arr) {
        int n = arr.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>();

        for (int i = n - 1; i >= 0; i--) {
            while (!stack.isEmpty() && stack.peek() <= arr[i]) {
                stack.pop();
            }
            result[i] = stack.isEmpty() ? -1 : stack.peek();
            stack.push(arr[i]);
        }
        return result;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 0, 4, 11, 0, 1};
        System.out.println(Arrays.toString(nextGreater(arr))); // Output: [2,4,4,11,-1,1,-1]
    }
}
```

### **Database Questions**  
1. **How can you optimize an SQL query for better performance?**  
   - Use **indexes** on frequently searched columns.  
   - Avoid `SELECT *` and fetch only required columns.  
   - Use **JOINs efficiently** and avoid unnecessary subqueries.  
   - Use **EXPLAIN PLAN** to analyze query execution.  

2. **When should you use NoSQL instead of SQL?**  
   - When working with **unstructured or semi-structured data**.  
   - When **scalability** is more important than **ACID compliance**.  
   - For real-time applications like chat apps and recommendation systems.  

3. **What are the best indexing strategies for improving database performance?**  
   - Use **B-Tree indexes** for range queries.  
   - Use **Hash indexes** for exact lookups.  
   - **Composite indexes** for multi-column searches.  

---

## **Third Round: Technical Interview**  

### **Question 3:**  
Given a list of strings, separate **palindromes** and **non-palindromes**, then **sort each group by length**.  

#### **Example**  
**Input:** `"hi oo how are your level comes"`  
**Output:**  
```  
Palindromes: [oo, level]  
Non-palindromes: [hi, how, comes, are your] (Sorted by length)  
```  

#### **Answer (Java - Single Stream Approach)**
```java
import java.util.*;
import java.util.stream.Collectors;

public class PalindromeSort {
    public static void main(String[] args) {
        String input = "hi oo how are your level comes";

        Map<String, List<String>> result = Arrays.stream(input.split(" "))
                .collect(Collectors.groupingBy(
                        word -> word.equals(new StringBuilder(word).reverse().toString()) ? "Palindromes" : "Non-Palindromes",
                        Collectors.collectingAndThen(
                                Collectors.toList(),
                                list -> list.stream()
                                        .sorted(Comparator.comparingInt(String::length))
                                        .collect(Collectors.toList())
                        )
                ));

        System.out.println(result);
    }
}
```

### **Database Question**  
- **Which Java Collection is best for this operation?**  
  **Answer:** `LinkedHashMap<String, List<String>>` (to maintain insertion order).  

---

## **Fourth Round: Managerial Interview**  

### **Question 4:**  
Why do we use `List` instead of `ArrayList` when declaring a variable?  
```java
List<Integer> ans = new ArrayList<>();
```
**Answer:**  
- `List<Integer>` is an **interface** that provides flexibility to switch implementations (`ArrayList`, `LinkedList`, etc.).  
- Helps in writing **loosely coupled** and **maintainable** code.  
- If later a `LinkedList` or `Vector` is needed, only the object needs to change, **not the variable type**.  

### **Behavioral Questions:**  
1. **What are your strengths and weaknesses?**  
   - Strengths: Problem-solving, adaptability, teamwork.  
   - Weaknesses: Perfectionism (but working on prioritization).  

2. **How do you learn new concepts?**  
   - Hands-on practice, online courses, and contributing to open-source projects.  

3. **Discussion about IBS Software projects.**  
   - Be prepared to discuss **what you know about IBS Software** and their work in the airline industry.  

---

## **Fifth Round: HR Interview**  

1. **What is your expected package?**  
   - Research the industry standard and **negotiate based on your experience**.  

2. **How do you keep up with new technologies?**  
   - Reading tech blogs, taking online courses, working on projects.  

3. **Tell me about your college life and how you got your first job.**  
   - Share an interesting story or highlight a key **learning experience**.  

---

### **Final Tips for the Interview**  
✔ **Write clean, efficient code** and be ready to explain it.  
✔ **Prepare database optimization strategies** (SQL vs NoSQL).  
✔ **Be confident in behavioral rounds** and talk about **real-life examples**.  
