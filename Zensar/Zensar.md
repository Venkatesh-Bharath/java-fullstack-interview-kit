---

# 📘 Zensar Interview Questions & Answers

---

## 1. Self Introduction (Project-Oriented)

I have around **4.5 years of experience as a Java Full Stack Developer**. Currently working on a **customer onboarding and transaction processing system**.

### Responsibilities:

* Developing REST & Reactive APIs using **Spring Boot & WebFlux**
* Handling high-volume traffic using **non-blocking architecture**
* Integrating **Kafka** for async communication
* Writing unit tests using **JUnit & Mockito**
* Frontend development using **ReactJS**

### Achievements:

* Improved API performance using reactive programming
* Implemented JWT-based authentication
* Optimized microservices communication

---

## 2. Reactive Programming (Mono vs Flux)

Reactive Programming is an **asynchronous, non-blocking approach**.

* **Mono** → 0 or 1 element
* **Flux** → 0 to N elements

---

## 3. Where do we use Mono?

Used when we expect a **single result**.

Examples:

* Get user by ID
* Login response
* Payment status

---

## 4. Real-Time Example for Mono

Fetching bank account balance returns only one value.

```java
public Mono<Double> getBalance(String accountId) {
    return webClient.get()
        .uri("/balance/" + accountId)
        .retrieve()
        .bodyToMono(Double.class);
}
```

---

## 5. API Calling using WebClient

```java
@Service
public class UserService {

    private final WebClient webClient;

    public UserService(WebClient.Builder builder) {
        this.webClient = builder.baseUrl("http://localhost:8081").build();
    }

    public Mono<String> getUser() {
        return webClient.get()
            .uri("/user")
            .retrieve()
            .bodyToMono(String.class)
            .onErrorReturn("Fallback User");
    }
}
```

---

## 6. How do you secure APIs?

* Spring Security
* JWT Authentication
* Role-based authorization
* HTTPS
* Input validation

---

## 7. JWT Authentication Workflow

1. User sends login credentials
2. Server validates credentials
3. JWT token generated
4. Token sent to client
5. Client sends token in header
6. Server validates token

👉 Validation done by **JWT Filter**

---

## 8. HTTP Status Codes

* 200 → OK
* 201 → Created
* 400 → Bad Request
* 401 → Unauthorized
* 403 → Forbidden
* 404 → Not Found
* 500 → Internal Server Error

---

## 9. Difference between 501 and 502

* **501 Not Implemented** → Server doesn’t support functionality
* **502 Bad Gateway** → Invalid response from upstream server

---

## 10. What is CORS?

CORS allows cross-origin requests.

Origin = protocol + host + port

---

## 11. CORS Configuration

```java
@Configuration
public class CorsConfig {
    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return registry -> registry.addMapping("/**")
            .allowedOrigins("*")
            .allowedMethods("*");
    }
}
```

---

## 12. Java 17 Features

* Records
* Sealed Classes
* Pattern Matching
* Text Blocks
* Enhanced Switch

---

## 13. Java 8 Supplier and Consumer

```java
Supplier<String> supplier = () -> "Hello";

Consumer<String> consumer = x -> System.out.println(x);
consumer.accept(supplier.get());
```

---

## 14. Method Reference

Short form of lambda.

```java
list.forEach(System.out::println);
```

Used for better readability and cleaner code.

---

## 15. CompletableFuture Example

```java
CompletableFuture.supplyAsync(() -> "Hello")
    .thenApply(String::toUpperCase)
    .thenAccept(System.out::println);
```

---

## 16. Executor Framework (Realtime)

Used for:

* Background jobs
* Async processing
* Email sending

---

## 17. Callable and Future

* Callable → returns value
* Future → holds result

```java
ExecutorService executor = Executors.newFixedThreadPool(1);
Future<Integer> future = executor.submit(() -> 10 + 20);
System.out.println(future.get());
```

---

## 18. Parallel Stream vs flatMap

* parallelStream → multi-threading
* flatMap → flatten nested collections

---

## 19. List of List of List → Single Stream

Yes, using multiple flatMap

```java
List<Integer> result = list.stream()
    .flatMap(List::stream)
    .flatMap(List::stream)
    .toList();
```

---

## 20. flatMap Example

```java
List<List<Integer>> list = List.of(
    List.of(1,2),
    List.of(3,4)
);

List<Integer> result = list.stream()
    .flatMap(Collection::stream)
    .toList();
```

---

## 21. HashSet vs TreeSet

| Operation | HashSet | TreeSet  |
| --------- | ------- | -------- |
| Insert    | O(1)    | O(log n) |
| Delete    | O(1)    | O(log n) |
| Search    | O(1)    | O(log n) |

HashSet → unordered
TreeSet → sorted

---

## 22. Composition vs Aggregation

* Composition → strong relationship (Car–Engine)
* Aggregation → weak relationship (School–Student)

---

## 23. Strengths and Weaknesses

Strengths:

* Problem solving
* Quick learner

Weakness:

* Sometimes focus too much on perfection

---

## 24. Why are you looking for a job change?

Looking for better growth, learning opportunities, and challenging work.

---

## 25. Builder vs Strategy Pattern

### Builder Pattern

```java
User user = User.builder()
    .name("Venkatesh")
    .age(25)
    .build();
```

---

### Strategy Pattern

```java
interface PaymentStrategy {
    void pay();
}

class UpiPayment implements PaymentStrategy {
    public void pay() {
        System.out.println("Paid using UPI");
    }
}
```

---
