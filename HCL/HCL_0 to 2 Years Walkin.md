# Online Assesment 
## 52 Questions = 50 MCQ 1 Code 1 SQL

1. **What is the output of the following pseudo-code?**  
   ```java
   class Animal {
       String sound() {
           return "Animal sound";
       }
   }

   class Dog extends Animal {
       String sound() {
           return "Bark";
       }
   }

   public class Main {
       public static void main(String[] args) {
           Animal obj = new Dog();
           System.out.println(obj.sound());
       }
   }
   ```
   a) Animal sound  
   b) Bark  
   c) Compile-time error  
   d) Runtime error  
   **Answer:** b) Bark  

---

2. **What happens if you call a static method on a subclass object?**  
   ```java
   class Parent {
       static void display() {
           System.out.println("Parent");
       }
   }

   class Child extends Parent {
       static void display() {
           System.out.println("Child");
       }
   }

   public class Main {
       public static void main(String[] args) {
           Parent obj = new Child();
           obj.display();
       }
   }
   ```
   a) Parent  
   b) Child  
   c) Compile-time error  
   d) Runtime error  
   **Answer:** a) Parent  

---

3. **How do you enforce a class to have certain methods in Java?**  
   ```java
   interface Vehicle {
       void start();
       void stop();
   }

   class Car implements Vehicle {
       // <missing_methods>
   }
   ```
   a) By inheriting from another class  
   b) By implementing an interface  
   c) By using a static method  
   d) By overriding methods  
   **Answer:** b) By implementing an interface  

---

4. **What is the output of this inheritance pseudo-code?**  
   ```java
   class A {
       int add(int x, int y) {
           return x + y;
       }
   }

   class B extends A {
       int add(int x, int y) {
           return x * y;
       }
   }

   public class Main {
       public static void main(String[] args) {
           A obj = new B();
           System.out.println(obj.add(2, 3));
       }
   }
   ```
   a) 5  
   b) 6  
   c) Compile-time error  
   d) Runtime error  
   **Answer:** a) 6  

---

5. **What is the purpose of using `super` in inheritance?**  
   ```java
   class Parent {
       Parent() {
           System.out.println("Parent Constructor");
       }
   }

   class Child extends Parent {
       Child() {
           super();
           System.out.println("Child Constructor");
       }
   }

   public class Main {
       public static void main(String[] args) {
           new Child();
       }
   }
   ```
   a) To call the parent's constructor  
   b) To override a method in the parent class  
   c) To access a private method in the parent class  
   d) None of the above  
   **Answer:** a) To call the parent's constructor  

---

6. **How do you filter a list of numbers to get even numbers only?**  
   ```java
   List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
   List<Integer> evens = numbers.stream()
       .<missing_code>
       .collect(Collectors.toList());
   ```
   a) filter(x -> x % 2 == 0)  
   b) map(x -> x % 2 == 0)  
   c) forEach(x -> x % 2 == 0)  
   d) None of the above  
   **Answer:** a) filter(x -> x % 2 == 0)  

---

7. **How do you sort a list of strings using streams?**  
   ```java
   List<String> names = Arrays.asList("Bob", "Alice", "Charlie");
   List<String> sortedNames = names.stream()
       .<missing_code>
       .collect(Collectors.toList());
   ```
   a) filter()  
   b) sorted()  
   c) collect()  
   d) map()  
   **Answer:** b) sorted()  

---

8. **How do you convert a list of integers into their squares?**  
   ```java
   List<Integer> numbers = Arrays.asList(1, 2, 3, 4);
   List<Integer> squares = numbers.stream()
       .<missing_code>
       .collect(Collectors.toList());
   ```
   a) map(x -> x * x)  
   b) filter(x -> x * x)  
   c) flatMap(x -> x * x)  
   d) None of the above  
   **Answer:** a) map(x -> x * x)  

---

9. **How do you group employees by department using streams?**  
   ```java
   Map<String, List<Employee>> grouped = employees.stream()
       .<missing_code>;
   ```
   a) collect(Collectors.groupingBy(Employee::getDepartment))  
   b) collect(Collectors.toMap(Employee::getDepartment))  
   c) groupBy(Employee::getDepartment)  
   d) None of the above  
   **Answer:** a) collect(Collectors.groupingBy(Employee::getDepartment))  

---

10. **How do you find the first element in a stream?**  
    ```java
    Optional<Integer> first = numbers.stream()
        .<missing_code>;
    ```
    a) findFirst()  
    b) findAny()  
    c) filter()  
    d) map()  
    **Answer:** a) findFirst()  

---

11. **What will be the output of the following code?**  
    ```java
    int x = 10, y = 20;
    int result = (x > y) ? x : y;
    System.out.println(result);
    ```
    a) 10  
    b) 20  
    c) Compile-time error  
    d) None of the above  
    **Answer:** b) 20  

---

12. **How do you check if a string starts with "Hello"?**  
    ```java
    String str = "Hello World";
    boolean result = str.<missing_code>("Hello");
    ```
    a) startsWith  
    b) endsWith  
    c) contains  
    d) equals  
    **Answer:** a) startsWith  

---

13. **What is the output of this pseudo-code?**  
    ```java
    class Test {
        static void display() {
            System.out.println("Static method in Test");
        }
    }

    public class Main {
        public static void main(String[] args) {
            Test obj = null;
            obj.display();
        }
    }
    ```
    a) Static method in Test  
    b) NullPointerException  
    c) Compile-time error  
    d) Runtime error  
    **Answer:** a) Static method in Test  

---

14. **How do you calculate the sum of all elements in a list using streams?**  
    ```java
    List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
    int sum = numbers.stream()
        .<missing_code>
        .orElse(0);
    ```
    a) reduce((a, b) -> a + b).get()  
    b) reduce(0, (a, b) -> a + b)  
    c) mapToInt(x -> x).sum()  
    d) None of the above  
    **Answer:** b) reduce(0, (a, b) -> a + b)  

---

15. **What happens if you override `equals` but not `hashCode`?**  
    ```java
    class Person {
        private String name;
        private int age;

        @Override
        public boolean equals(Object obj) {
            // custom logic here
        }
    }

    public static void main(String[] args) {
        HashSet<Person> set = new HashSet<>();
        set.add(new Person("Alice", 25));
        set.add(new Person("Alice", 25));
        System.out.println(set.size());
    }
    ```
    a) 1  
    b) 2  
    c) Compile-time error  
    d) Runtime error  
    **Answer:** b) 2  

---

16. **What is the purpose of the `final` keyword in Java?**  
    ```java
    final class Test {
        final int x = 10;

        final void display() {
            System.out.println("Final method");
        }
    }
    ```
    a) To prevent inheritance  
    b) To make a variable constant  
    c) To prevent method overriding  
    d) All of the above  
    **Answer:** d) All of the above  

---

17. **How do you find the maximum value in a list using streams?**  
    ```java
    List<Integer> numbers = Arrays.asList(10, 20, 30, 40, 50);
    Optional<Integer> max = numbers.stream()
        .<missing_code>;
    ```
    a) reduce(Integer::max)  
    b) max(Integer::compare)  
    c) mapToInt(x -> x).max()  
    d) Any of the above  
    **Answer:** d) Any of the above  

---

18. **What is the output of this method reference example?**  
    ```java
    class Test {
        void display(String msg) {
            System.out.println(msg);
        }
    }

    public class Main {
        public static void main(String[] args) {
            Test obj = new Test();
            Consumer<String> ref = obj::display;
            ref.accept("Hello World");
        }
    }
    ```
    a) Compile-time error  
    b) Hello World  
    c) NullPointerException  
    d) None of the above  
    **Answer:** b) Hello World  

---

19. **What is the purpose of the `Optional` class in Java?**  
    ```java
    Optional<String> opt = Optional.ofNullable(null);
    System.out.println(opt.orElse("Default Value"));
    ```
    a) To avoid null pointer exceptions  
    b) To simplify null checks  
    c) To provide default values when null  
    d) All of the above  
    **Answer:** d) All of the above  

---

20. **How do you create a custom functional interface in Java?**  
    ```java
    @FunctionalInterface
    interface Calculator {
        int calculate(int a, int b);
    }

    public class Main {
        public static void main(String[] args) {
            Calculator add = <missing_code>;
            System.out.println(add.calculate(10, 20));
        }
    }
    ```
    a) (x, y) -> x + y  
    b) new Calculator()  
    c) Calculator::calculate  
    d) None of the above  
    **Answer:** a) (x, y) -> x + y  

---

21. **How do you find duplicate elements in a list using streams?**  
    ```java
    List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 1, 3);
    Set<Integer> duplicates = numbers.stream()
        .<missing_code>
        .collect(Collectors.toSet());
    ```
    a) filter(x -> Collections.frequency(numbers, x) > 1)  
    b) groupBy(x -> x)  
    c) distinct()  
    d) None of the above  
    **Answer:** a) filter(x -> Collections.frequency(numbers, x) > 1)  

---

22. **What is the output of this method chaining example?**  
    ```java
    List<String> names = Arrays.asList("John", "Jane", "Jake");
    names.stream()
        .filter(name -> name.startsWith("J"))
        .map(String::toUpperCase)
        .forEach(System.out::println);
    ```
    a) JOHN JANE JAKE  
    b) Runtime error  
    c) Compile-time error  
    d) None of the above  
    **Answer:** a) JOHN JANE JAKE  

---

23. **What happens if a stream is reused?**  
    ```java
    Stream<String> stream = Stream.of("A", "B", "C");
    stream.forEach(System.out::println);
    stream.forEach(System.out::println);
    ```
    a) All elements printed twice  
    b) Stream reused without issues  
    c) IllegalStateException  
    d) None of the above  
    **Answer:** c) IllegalStateException  

---

24. **What is the output of the following?**  
    ```java
    Stream<Integer> numbers = Stream.iterate(1, n -> n + 1);
    numbers.limit(5)
        .forEach(System.out::println);
    ```
    a) 1 2 3 4 5  
    b) Infinite loop  
    c) Compile-time error  
    d) None of the above  
    **Answer:** a) 1 2 3 4 5  

---

25. **How do you concatenate two streams in Java?**  
    ```java
    Stream<Integer> s1 = Stream.of(1, 2, 3);
    Stream<Integer> s2 = Stream.of(4, 5, 6);
    Stream<Integer> combined = <missing_code>;
    ```
    a) Stream.concat(s1, s2)  
    b) s1.addAll(s2)  
    c) s1.merge(s2)  
    d) None of the above  
    **Answer:** a) Stream.concat(s1, s2)  

---

26. **What happens when an exception is thrown inside a stream pipeline?**  
    ```java
    Stream<Integer> numbers = Stream.of(1, 2, 0);
    numbers.map(x -> 10 / x)
        .forEach(System.out::println);
    ```
    a) All elements processed  
    b) ArithmeticException  
    c) Compile-time error  
    d) None of the above  
    **Answer:** b) ArithmeticException  

---

27. **How do you handle exceptions in streams?**  
    ```java
    List<Integer> numbers = Arrays.asList(1, 2, 0);
    List<Integer> results = numbers.stream()
        .<missing_code>
        .collect(Collectors.toList());
    ```
    a) try-catch inside lambda  
    b) Custom exception handler  
    c) Both a and b  
    d) None of the above  
    **Answer:** c) Both a and b  

---

28. **What is the difference between `map` and `flatMap`?**  
    ```java
    List<List<Integer>> numbers = Arrays.asList(
        Arrays.asList(1, 2, 3),
        Arrays.asList(4, 5, 6)
    );
    List<Integer> flat = numbers.stream()
        .flatMap(List::stream)
        .collect(Collectors.toList());
    ```
    a) `map` processes elements, `flatMap` flattens nested streams  
    b) Both are the same  
    c) Both flatten nested lists  
    d) None of the above  
    **Answer:** a) `map` processes elements, `flatMap` flattens nested streams

---

30. **Which of the following ensures a thread-safe Singleton class?**  
    ```java
    public class Singleton {
        private static Singleton instance;

        private Singleton() {}

        public static Singleton getInstance() {
            if (instance == null) {
                synchronized (Singleton.class) {
                    if (instance == null) {
                        instance = new Singleton();
                    }
                }
            }
            return instance;
        }
    }
    ```
    a) Use double-checked locking as shown in the code.  
    b) Use a synchronized method instead of a synchronized block.  
    c) Use an enum to implement Singleton.  
    d) All of the above.  
    **Answer:** d) All of the above.

---

31. **What is the output of this pseudo-code for a Singleton class?**  
    ```java
    public class Singleton {
        private static Singleton instance = new Singleton();

        private Singleton() {
            System.out.println("Constructor Called");
        }

        public static Singleton getInstance() {
            return instance;
        }
    }

    public class Main {
        public static void main(String[] args) {
            Singleton s1 = Singleton.getInstance();
            Singleton s2 = Singleton.getInstance();
            System.out.println(s1 == s2);
        }
    }
    ```
    a) Constructor Called  
       true  
    b) Constructor Called  
       Constructor Called  
       false  
    c) true  
    d) Compile-time error  
    **Answer:** a) Constructor Called  
               true 

---

31. **Given a table `Employee` with columns `id`, `name`, and `salary`, write a query to find the highest salary from the table.**

a) `SELECT MAX(salary) FROM Employee;`  
b) `SELECT salary FROM Employee ORDER BY salary DESC LIMIT 1;`  
c) `SELECT salary FROM Employee WHERE salary = (SELECT MAX(salary) FROM Employee);`  
d) All of the above  

**Answer:** d) All of the above  

---

32. **Given a table `Student` with a `marks` column, write a query to count the number of students who have grade 'A' (marks > 80), grade 'B' (marks > 70), grade 'C' (marks > 50), and grade 'F' (marks <= 50).**

a) 
```sql
SELECT COUNT(*) FROM Student WHERE marks > 80; -- Grade A
SELECT COUNT(*) FROM Student WHERE marks > 70 AND marks <= 80; -- Grade B
SELECT COUNT(*) FROM Student WHERE marks > 50 AND marks <= 70; -- Grade C
SELECT COUNT(*) FROM Student WHERE marks <= 50; -- Grade F
```
b) 
```sql
SELECT grade, COUNT(*) FROM Student GROUP BY grade;
```
c) 
```sql
SELECT COUNT(*) FROM Student WHERE marks > 80 AND marks <= 90; -- Grade B
```
d) 
```sql
SELECT marks FROM Student ORDER BY marks DESC;
```

**Answer:** a) 

---

33. **Given two tables, `Employee(id, name, department_id)` and `Department(id, name)`, write a query to list all employees with their department names.**

a) 
```sql
SELECT Employee.name, Department.name FROM Employee INNER JOIN Department ON Employee.department_id = Department.id;
```
b) 
```sql
SELECT Employee.name, Department.name FROM Employee LEFT JOIN Department ON Employee.department_id = Department.id;
```
c) 
```sql
SELECT Employee.name, Department.name FROM Employee JOIN Department ON Employee.department_id = Department.id;
```
d) All of the above  

**Answer:** d) All of the above  

---

34. **Write a query to count the number of employees in each department.**

a) 
```sql
SELECT department_id, COUNT(*) FROM Employee GROUP BY department_id;
```
b) 
```sql
SELECT COUNT(*) FROM Employee WHERE department_id = 1;
```
c) 
```sql
SELECT department_id, COUNT(*) FROM Employee HAVING COUNT(*) > 1;
```
d) 
```sql
SELECT department_id FROM Employee;
```

**Answer:** a) `SELECT department_id, COUNT(*) FROM Employee GROUP BY department_id;`  

---

35. **Write a query to increase the salary by 10% for all employees in department 2.**

a) 
```sql
UPDATE Employee SET salary = salary * 1.10 WHERE department_id = 2;
```
b) 
```sql
UPDATE Employee SET salary = salary + (salary * 0.10) WHERE department_id = 2;
```
c) 
```sql
UPDATE Employee SET salary = salary + 10 WHERE department_id = 2;
```
d) Both a) and b)  

**Answer:** d) Both a) and b)  

---

36. **Which CSS property is used to align items in a flex container along the cross-axis?**

a) `align-items`  
b) `justify-content`  
c) `align-self`  
d) `flex-direction`  

**Answer:** a) `align-items`  

---

37. **Which property is used to position an element relative to its normal position in CSS?**

a) `absolute`  
b) `relative`  
c) `fixed`  
d) `sticky`  

**Answer:** b) `relative`  

---

38. **Which of the following properties is used to set the margin between an element's border and its surroundings?**

a) `border`  
b) `padding`  
c) `margin`  
d) `content`  

**Answer:** c) `margin`  

---

39. **Which CSS rule is used for applying styles based on screen width?**

a) `@screen`  
b) `@media`  
c) `@viewport`  
d) `@responsive`  

**Answer:** b) `@media`  

---

40. **Which CSS property controls the stacking order of elements?**

a) `z-order`  
b) `z-index`  
c) `order`  
d) `stacking`  

**Answer:** b) `z-index`  

---

41. **Which HTML tag is used to create a table header?**

a) `<thead>`  
b) `<th>`  
c) `<tr>`  
d) `<table>`  

**Answer:** b) `<th>`  

---

42. **Which attribute is used to specify the destination of a hyperlink?**

a) `href`  
b) `src`  
c) `link`  
d) `target`  

**Answer:** a) `href`  

---

43. **Which element is used to define a form in HTML?**

a) `<form>`  
b) `<input>`  
c) `<textarea>`  
d) `<button>`  

**Answer:** a) `<form>`  

---

44. **Which tag is used to define an ordered list?**

a) `<ul>`  
b) `<li>`  
c) `<ol>`  
d) `<dl>`  

**Answer:** c) `<ol>`  

---

45. **Which attribute is used to provide an alternative text for an image in HTML?**

a) `alt`  
b) `title`  
c) `src`  
d) `desc`  

**Answer:** a) `alt`  

---

46. **Which of the following is the correct way to declare a function in JavaScript?**

a) `function myFunction() {}`  
b) `let myFunction() {}`  
c) `function = myFunction() {}`  
d) `myFunction() function {}`  

**Answer:** a) `function myFunction() {}`  

---

47. **How do you access the second element in an array `arr = [10, 20, 30]`?**

a) `arr[2]`  
b) `arr[1]`  
c) `arr(2)`  
d) `arr[3]`  

**Answer:** b) `arr[1]`  

---

48. **How do you access the `name` property of an object `person = {name: "John", age: 30}`?**

a) `person["name"]`  
b) `person.name`  
c) `person[name]`  
d) Both a) and b)  

**Answer:** d) Both a) and b)  

---

49. **Which method is used to attach an event listener to an element in JavaScript?**

a) `addEvent()`  
b) `attachEvent()`  
c) `addEventListener()`  
d) `bindEvent()`  

**Answer:** c) `addEventListener()`  

---
50. **Which JavaScript loop will print numbers from 1 to 5?**

a) 
```javascript
for (let i = 0; i <= 5; i++) {
    console.log(i);
}
```
b) 
```javascript
for (let i = 1; i < 5; i++) {
    console.log(i);
}
```
c) 
```javascript
while (i < 5) {
    console.log(i);
    i++;
}
```
d) All of the above  

**Answer:** d) All of the above  

---

### **SQL Query**
51. **Question:**  
A student table contains a `marks` column. Display the count of students in each grade:  
- `A`: Marks > 80  
- `B`: Marks > 70 and <= 80  
- `C`: Marks > 50 and <= 70  
- `F`: Marks <= 50  

**SQL Query:**
```sql
SELECT 
    CASE 
        WHEN marks > 80 THEN 'A'
        WHEN marks > 70 THEN 'B'
        WHEN marks > 50 THEN 'C'
        ELSE 'F'
    END AS Grade,
    COUNT(*) AS Count
FROM student
GROUP BY 
    CASE 
        WHEN marks > 80 THEN 'A'
        WHEN marks > 70 THEN 'B'
        WHEN marks > 50 THEN 'C'
        ELSE 'F'
    END;
```

---

### **Coding**
52. **Question:**  
Write a method to find the name with the highest score based on the input strings.  
- `L` = 1 point, `M` = 3 points, `H` = 5 points.  
Example: `findHighScore("LMM", "HHH")` should return `"shirly"` because `HHH` (15 points) is greater than `LMM` (7 points).

**Java Code:**
```java
public class HighScore {
    public static String findHighScore(String bob, String shirly) {
        int bobScore = calculateScore(bob);
        int shirlyScore = calculateScore(shirly);

        return bobScore > shirlyScore ? "bob" : "shirly";
    }

    private static int calculateScore(String input) {
        int score = 0;
        for (char ch : input.toCharArray()) {
            if (ch == 'L') score += 1;
            else if (ch == 'M') score += 3;
            else if (ch == 'H') score += 5;
        }
        return score;
    }

    public static void main(String[] args) {
        System.out.println(findHighScore("LMM", "HHH")); // Output: shirly
    }
}
```
# Technical Interview
