# L1 Interview

## 1. Self Introduction with Real-Time Project

### Question
Tell me about yourself and explain your current real-time project.

### Answer

Hi, I'm Venkatesh, and I have around **5+ years of experience** as a Java Backend Developer. My primary expertise is in **Java 8/17, Spring Boot, Spring WebFlux, Microservices, Kafka, REST APIs, Cassandra, PostgreSQL, Docker, Kubernetes, and CI/CD**.

Currently, I'm working on the **American Express MARS Platform**, which is a Microservices-based financial application responsible for processing millions of customer transactions daily. The platform manages payment processing, account management, financial obligations, refunds, and customer profile services.

In my current role, I am responsible for:

- Developing REST APIs using Spring Boot and Spring WebFlux.
- Implementing Reactive Programming using Mono and Flux.
- Integrating multiple downstream microservices using WebClient.
- Publishing and consuming Kafka events.
- Writing Unit Test cases using JUnit5 and Mockito.
- Solving Production Issues.
- Performance optimization and code review.
- Deploying applications through Jenkins and Kubernetes.

One of my major contributions was reducing API response time from around **2.5 seconds to nearly 800 milliseconds** by implementing parallel API calls using WebClient and optimizing database queries.

---

## 2. Difference between Java 8 and Java 17

### Answer

Java 8 and Java 17 are both Long-Term Support (LTS) versions, but Java 17 provides many new language features, performance improvements, and security enhancements.

| Java 8 | Java 17 |
|---------|----------|
| Lambda Expressions | Improved Pattern Matching |
| Stream API | Records |
| Optional | Sealed Classes |
| Date & Time API | Text Blocks |
| Default Methods | Switch Expressions |
| Basic Garbage Collectors | Better G1, ZGC, Shenandoah |
| Less Secure | More Secure |

### Real-Time Example

Most legacy projects still run on Java 8.

New projects prefer Java 17 because of better performance and modern language features.

### Interview Tip

The interviewer usually asks:

> Why did your company migrate from Java 8 to Java 17?

Expected Answer:

- Better Performance
- LTS Support
- Better Garbage Collection
- Improved Security
- Cleaner Code using Records and Switch Expressions

---

## 3. Difference between flatMap() and concatMap()

### Answer

Both operators transform one object into another asynchronous Publisher.

The main difference is **ordering**.

### flatMap()

- Executes asynchronously.
- Multiple API calls happen in parallel.
- Faster.
- Order is NOT guaranteed.

### concatMap()

- Executes sequentially.
- Waits for one operation to finish before starting the next.
- Slower.
- Order is guaranteed.

### Code Example

```java
Flux.just(1,2,3)
.flatMap(i -> callAPI(i))
.subscribe(System.out::println);
```

Output order may be:

```
2
3
1
```

Using concatMap

```java
Flux.just(1,2,3)
.concatMap(i -> callAPI(i))
.subscribe(System.out::println);
```

Output

```
1
2
3
```

### Real-Time Example

Suppose you're sending payment requests.

If payment order matters,

Use

```
concatMap()
```

If you're calling Customer Service, Address Service, and Reward Service independently,

Use

```
flatMap()
```

because they can execute in parallel.

---

## 4. Explain Optional Class

### Answer

Optional is introduced in Java 8 to avoid **NullPointerException**.

Instead of returning null, we return an Optional object.

### Without Optional

```java
User user = repository.find(id);

System.out.println(user.getName());
```

If user is null

```
NullPointerException
```

### With Optional

```java
Optional<User> user = repository.findById(id);

String name = user
        .map(User::getName)
        .orElse("Guest");
```

### Important Methods

```java
of()

ofNullable()

empty()

isPresent()

ifPresent()

orElse()

orElseGet()

orElseThrow()
```

### Real-Time Example

Repository methods usually return

```java
Optional<User>
```

instead of

```java
User
```

This avoids unnecessary null checks.

---

## 5. What is Lambda Expression?

### Answer

Lambda Expression is a shorter way of implementing Functional Interfaces.

Before Java 8

```java
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello");
    }
};
```

Java 8

```java
Runnable r = () -> System.out.println("Hello");
```

### Syntax

```java
(parameters) -> expression
```

### Real-Time Usage

- Stream API
- Comparator
- Sorting
- Filtering
- Collection Processing

### Example

```java
employees.stream()
.filter(emp -> emp.getSalary()>50000)
.forEach(System.out::println);
```

---

## 6. Functional Interface

### Answer

A Functional Interface contains exactly **one abstract method**.

It may have multiple default and static methods.

### Example

```java
@FunctionalInterface
interface Calculator{

    int add(int a,int b);

}
```

### Built-in Functional Interfaces

- Predicate
- Consumer
- Supplier
- Function
- UnaryOperator
- BinaryOperator

### Real-Time Example

```java
Predicate<Integer> even = x -> x % 2 == 0;
```

```java
Consumer<String> print = System.out::println;
```

### Interview Question

Why Functional Interface?

Because Lambda Expressions can work only with Functional Interfaces.

---

## 7. Difference between Spring MVC, Spring Boot and Spring WebFlux

| Spring MVC | Spring Boot | Spring WebFlux |
|-------------|-------------|----------------|
| Framework | Framework | Reactive Framework |
| Blocking | Supports MVC/WebFlux | Non-Blocking |
| Servlet API | Auto Configuration | Netty/Event Loop |
| Thread per Request | Easy Configuration | Fewer Threads |
| Better for CRUD | Easy Development | High Concurrency |

### Real-Time Example

If your application receives

```
500 Requests/sec
```

Spring MVC works well.

If your application receives

```
100000 Requests/sec
```

WebFlux performs much better because it doesn't block threads.

---

## 8. Explain @SpringBootApplication

### Answer

@SpringBootApplication is a combination of three annotations.

```java
@Configuration

@EnableAutoConfiguration

@ComponentScan
```

### @Configuration

Creates Spring Beans.

### @EnableAutoConfiguration

Automatically configures Spring Boot.

### @ComponentScan

Scans Controllers, Services and Repositories.

### Example

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {

        SpringApplication.run(Application.class,args);

    }

}
```

---

## 9. How do you handle errors in Microservices?

### Answer

In Microservices we should never expose Java Exceptions directly.

We use

- Global Exception Handler
- Standard Error Response
- Proper HTTP Status Codes
- Logging
- Correlation ID
- Retry
- Circuit Breaker
- Fallback

### Example

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)

    public ResponseEntity<String> handle(Exception ex){

        return ResponseEntity
                .status(HttpStatus.INTERNAL_SERVER_ERROR)
                .body(ex.getMessage());

    }

}
```

### Real-Time

If Customer Service is down

Instead of failing

Return

```
Cached Data

OR

Fallback Response
```

using

```
Resilience4j
```

---

## 10. What is Spring WebFlux?

### Answer

Spring WebFlux is Spring's **Reactive Web Framework** introduced in Spring 5.

It supports

- Non-blocking
- Asynchronous
- Event-driven Programming

It is built on

```
Project Reactor
```

using

```
Mono

Flux
```

Instead of

```
Thread Per Request
```

WebFlux uses

```
Event Loop Model
```

which consumes fewer threads and handles many concurrent users efficiently.

### Example

```java
@GetMapping("/{id}")

public Mono<User> getUser(@PathVariable int id){

    return service.getUser(id);

}
```

### When should you use WebFlux?

- High Concurrent APIs
- Streaming APIs
- Chat Applications
- Notification Systems
- API Gateway
- External API Aggregation

### Interview Tip

If the interviewer asks:

**Why did your project choose WebFlux?**

Answer:

- High throughput
- Better scalability
- Non-blocking I/O
- Parallel API calls using WebClient
- Lower memory consumption
- Better response time for I/O-bound applications

# 11. Difference between Flux and Mono

## Question

What is the difference between Mono and Flux?

## Answer

Both **Mono** and **Flux** are Reactive Streams introduced by **Project Reactor**.

They represent asynchronous data streams.

- **Mono** → Emits **0 or 1** value.
- **Flux** → Emits **0 to N** values.

Think of them as:

```
Mono  -> One Result
Flux  -> Multiple Results
```

---

## Mono Example

```java
@GetMapping("/{id}")
public Mono<User> getUser(@PathVariable Long id) {
    return userService.getUser(id);
}
```

Output

```
{
   "id":1,
   "name":"John"
}
```

Only one object is returned.

---

## Flux Example

```java
@GetMapping
public Flux<User> getUsers() {
    return userService.getUsers();
}
```

Output

```
[
 {id:1},
 {id:2},
 {id:3}
]
```

Multiple records.

---

## Real-Time Example

Customer Details API

```
GET /customer/100
```

Return

```
Mono<Customer>
```

Customer List API

```
GET /customers
```

Return

```
Flux<Customer>
```

---

## Interview Tip

Whenever the interviewer asks

"When should we use Mono?"

Answer

When only one object is expected.

"When should we use Flux?"

Answer

When multiple objects or streams are expected.

---

# 12. What is Spring WebClient? If WebClient is not available, how will you call another Microservice?

## Answer

**WebClient** is Spring WebFlux's **non-blocking HTTP client**.

It is used to call external APIs asynchronously.

Unlike **RestTemplate**, WebClient doesn't block the thread while waiting for a response.

---

## WebClient Example

```java
WebClient webClient = WebClient.create();

Mono<User> response = webClient
        .get()
        .uri("http://user-service/users/1")
        .retrieve()
        .bodyToMono(User.class);
```

---

## Multiple Parallel Calls

```java
Mono<User> user = userClient.getUser();

Mono<Account> account = accountClient.getAccount();

return Mono.zip(user, account)
           .map(tuple -> new CustomerResponse(
                   tuple.getT1(),
                   tuple.getT2()));
```

Both APIs execute in parallel.

---

## If WebClient is not available?

Options

- RestTemplate
- OpenFeign Client
- HttpClient
- OkHttp

---

## RestTemplate Example

```java
RestTemplate restTemplate = new RestTemplate();

User user = restTemplate.getForObject(
        "http://user-service/users/1",
        User.class);
```

---

## Real-Time Example

Suppose Order Service needs

- Customer Service
- Payment Service
- Address Service

Instead of waiting one after another,

WebClient calls all services in parallel.

This reduces response time significantly.

---

# 13. How do you handle 10 Million Records in an API?

## Answer

Never return all records in one API response.

Use multiple optimization techniques.

---

## 1. Pagination

```sql
SELECT *
FROM customer
LIMIT 100 OFFSET 0;
```

---

## 2. Database Index

Create indexes on frequently searched columns.

```sql
CREATE INDEX idx_customer_name
ON customer(name);
```

---

## 3. Filtering

Instead of

```
GET /customers
```

Use

```
GET /customers?status=ACTIVE
```

---

## 4. Streaming Response

Instead of loading everything into memory

Use

```
Flux<Customer>
```

---

## 5. Compression

Enable GZIP Compression

```
server.compression.enabled=true
```

---

## 6. Cache Frequently Used Data

Use

- Redis
- Caffeine

---

## 7. Async Processing

Large reports

CSV Export

PDF Generation

should execute asynchronously.

---

## Real-Time Example

Our customer table contained more than **20 million records**.

We improved performance using

- Pagination
- Database Index
- Reactive Streaming
- Cassandra Partition Keys

Response time reduced from **8 seconds** to around **1.5 seconds**.

---

# 14. What is the Request and Response Time of APIs in your Project?

## Answer

Response time depends on API complexity.

Typical response times:

| API Type | Response Time |
|-----------|---------------|
| Simple CRUD | 100–200 ms |
| Database Query | 200–500 ms |
| External API Call | 500 ms–2 sec |
| Multiple Services | 1–3 sec |

---

## How did you improve performance?

- WebClient Parallel Calls
- Database Indexing
- Pagination
- Redis Cache
- Query Optimization
- Connection Pool Tuning

---

## Real-Time Example

Initially

```
2.8 Seconds
```

After optimization

```
800 ms
```

---

# 15. Have you worked on Unit Testing? Which Framework?

## Answer

Yes.

We use

- JUnit 5
- Mockito
- Spring Boot Test

---

## Mockito Example

```java
@Mock
UserRepository repository;

@InjectMocks
UserService service;
```

---

## Test Case

```java
@Test
void testGetUser() {

    when(repository.findById(1L))
            .thenReturn(Optional.of(new User()));

    User user = service.getUser(1L);

    assertNotNull(user);

}
```

---

## Why Unit Testing?

- Improves Code Quality
- Prevents Bugs
- Supports CI/CD
- Easier Refactoring

---

## Interview Tip

Mention

```
Mockito

verify()

when()

assertEquals()

assertThrows()
```

---

# 16. Which Databases have you worked with?

## Answer

I have worked with

- Cassandra
- PostgreSQL
- MySQL
- Oracle

---

## Cassandra

Used for

- Huge Data
- High Availability
- Distributed Systems

---

## PostgreSQL

Used for

- Transactional Data
- Financial Records

---

## MySQL

Used for

- CRUD Applications
- Reporting

---

## Oracle

Used in legacy enterprise applications.

---

## Real-Time Example

Customer Profile

```
PostgreSQL
```

Transaction Events

```
Cassandra
```

---

# 17. How do you implement Idempotency in Microservices?

## Answer

Idempotency ensures that multiple identical requests produce the same result.

---

## Example

Payment API

```
POST /payment
```

User clicks

```
Pay
```

3 times.

Without Idempotency

```
₹100

₹100

₹100
```

Three payments.

With Idempotency

Only one payment is processed.

---

## Implementation

Generate

```
Idempotency-Key
```

Store it in database.

If duplicate request arrives,

Return previous response.

---

## Sample Flow

```
Client

↓

Generate UUID

↓

Payment API

↓

Database Check

↓

Already Exists?

↓

Yes

↓

Return Existing Response
```

---

# 18. What is Event-Driven System?

## Answer

In Event Driven Architecture,

services communicate through events instead of direct API calls.

---

## Example

Order Created

↓

Kafka Topic

↓

Inventory Service

↓

Notification Service

↓

Payment Service

Each service works independently.

---

## Advantages

- Loose Coupling
- High Scalability
- Better Reliability
- Asynchronous Communication

---

## Real-Time Example

Customer updates address.

Customer Service publishes

```
CustomerUpdated
```

Kafka Event.

Other services consume it automatically.

---

# 19. Database contains millions of events. Fetch the latest 5 events.

## SQL

```sql
SELECT *
FROM event_table
ORDER BY created_date DESC
LIMIT 5;
```

---

## Optimization

- Create Index

```sql
CREATE INDEX idx_created_date
ON event_table(created_date);
```

---

## Why?

Sorting millions of rows without an index is expensive.

---

# 20. How is Message Ordering maintained in Kafka?

## Answer

Kafka guarantees ordering only

within a single partition.

Ordering is maintained using

```
Offset
```

Each message gets a unique offset.

Example

```
Partition-0

Offset

0

1

2

3

4
```

Consumer reads sequentially.

---

## Real-Time Example

Bank Transactions

For one customer,

all events should go to the same partition.

Partition Key

```
CustomerId
```

ensures ordering.

---

## Interview Tip

Question

Can Kafka guarantee ordering across multiple partitions?

Answer

**No.**

Kafka guarantees ordering only within the same partition.

# 21. If there are 3 Consumers, can they read partition messages in parallel without duplicates?

## Question

If a Kafka topic has multiple partitions and there are **3 consumers** in the same consumer group, can they process messages in parallel? How do you avoid duplicates?

---

## Answer

Yes.

Kafka allows multiple consumers within the **same Consumer Group** to read messages **in parallel**, but **one partition can be assigned to only one consumer** within that group.

Example:

```
Topic : Payment

Partitions

P0
P1
P2

Consumer Group

Consumer-1  --> P0

Consumer-2  --> P1

Consumer-3  --> P2
```

Each consumer processes its assigned partition independently.

---

## Will duplicate messages occur?

Normally, **No**.

However, duplicates may occur when:

- Consumer crashes after processing but before committing the offset.
- Producer retries sending the same message.
- Network failures cause retries.

---

## How do you avoid duplicates?

- Enable Idempotent Producer.
- Use unique Transaction IDs or Idempotency Keys.
- Commit offsets only after successful processing.
- Store processed event IDs in the database if required.

---

## Real-Time Example

In a payment application:

- Producer publishes a `PaymentCompleted` event.
- If the producer retries due to a timeout, the same event may be sent again.
- The consumer checks the Transaction ID before processing.
- If it already exists, the message is ignored.

---

## Interview Tip

**Question:** Can two consumers read the same partition simultaneously in the same consumer group?

**Answer:** No. Kafka assigns one partition to only one consumer within a consumer group.

---

# 22. Explain your Project Deployment Process.

## Answer

Our project follows an automated CI/CD pipeline.

Deployment Flow:

```
Developer

↓

Git Push

↓

Pull Request Review

↓

Merge to Main Branch

↓

Jenkins Pipeline

↓

Maven Build

↓

Unit Tests

↓

SonarQube Code Scan

↓

Docker Image Build

↓

Push Image to Artifact Repository

↓

Kubernetes Deployment

↓

Smoke Testing

↓

Production
```

---

## Deployment Steps

### Step 1

Developer pushes code to Git.

### Step 2

Jenkins pipeline is triggered automatically.

### Step 3

Maven compiles the application.

```bash
mvn clean install
```

### Step 4

JUnit and Mockito test cases are executed.

### Step 5

SonarQube checks:

- Bugs
- Vulnerabilities
- Code Coverage
- Code Smells

### Step 6

Docker Image is created.

```dockerfile
FROM eclipse-temurin:17

COPY target/app.jar app.jar

ENTRYPOINT ["java","-jar","app.jar"]
```

### Step 7

Docker image is pushed to the registry.

### Step 8

Kubernetes deploys the latest image.

### Step 9

Smoke testing is performed.

### Step 10

Application becomes available to users.

---

## Real-Time Example

Our deployments are fully automated.

Average deployment time:

**10–15 minutes**

Rollback can be completed within a few minutes if required.

---

# 23. Which CI/CD Pipeline or Tool are you using?

## Answer

In my project, we use:

- Git
- Jenkins
- Maven
- SonarQube
- Docker
- Kubernetes
- Nexus/Artifactory
- Helm (optional)
- ArgoCD (if applicable)

---

## Pipeline

```
Git

↓

Jenkins

↓

Maven Build

↓

JUnit

↓

SonarQube

↓

Docker

↓

Push Docker Image

↓

Kubernetes Deployment

↓

Health Check
```

---

## Benefits

- Automated deployment
- Faster releases
- Reduced manual effort
- Better quality
- Easy rollback

---

## Interview Tip

Mention:

- Build Pipeline
- Deployment Pipeline
- Rollback Strategy
- Blue-Green Deployment (if used)
- Canary Deployment (if used)

---

# 24. How do you solve Production Issues in Real Time?

## Answer

Whenever a production issue occurs, I follow a structured approach.

### Step 1

Understand the issue.

- API failure?
- Timeout?
- Performance issue?
- Database issue?

---

### Step 2

Check logs.

- Application Logs
- Kubernetes Logs
- Kafka Logs

---

### Step 3

Verify monitoring dashboards.

- CPU
- Memory
- Error Rate
- Response Time

---

### Step 4

Identify the Root Cause.

Common reasons:

- Database timeout
- Network issue
- External service failure
- Memory leak
- High CPU usage

---

### Step 5

Implement the fix.

Examples:

- Restart pod
- Increase timeout
- Optimize SQL query
- Fix code bug
- Scale Kubernetes pods

---

### Step 6

Deploy hotfix through CI/CD.

---

### Step 7

Prepare RCA (Root Cause Analysis) document.

Include:

- What happened?
- Root cause
- Resolution
- Preventive measures

---

## Real-Time Example

**Issue:** Customer Profile API was taking 5–6 seconds.

**Root Cause:** Missing database index caused a full table scan.

**Solution:**

- Added an index on the frequently searched column.
- Optimized the SQL query.
- Reduced response time from **5.8 seconds to 700 ms**.

---

# 25. What is Reactive Programming, and why did you use it in your project?

## Answer

Reactive Programming is an **asynchronous, non-blocking programming model** that efficiently handles many concurrent requests using a small number of threads.

Instead of waiting for one task to complete before starting another, the application continues processing other requests.

---

## Why did we use Reactive Programming?

- High concurrency
- Better scalability
- Non-blocking I/O
- Lower memory usage
- Better response time

---

## Real-Time Example

Our Customer Dashboard API called:

- Customer Service
- Account Service
- Rewards Service
- Transaction Service

Instead of calling them one by one, we called them in parallel using **WebClient** and combined the responses.

This reduced the API response time significantly.

---

# 26. Why did you choose Spring WebFlux instead of Spring MVC?

## Answer

Spring MVC follows a **blocking** model where one thread is allocated per request.

Spring WebFlux follows a **non-blocking** model using the Event Loop, allowing a small number of threads to handle many concurrent requests.

---

## Comparison

| Spring MVC | Spring WebFlux |
|------------|----------------|
| Blocking | Non-blocking |
| Thread per request | Event Loop |
| Tomcat | Netty |
| Best for CRUD | Best for High Concurrency |

---

## Real-Time Example

Our API aggregates responses from multiple downstream microservices.

Using WebFlux and WebClient, we executed these calls in parallel, reducing latency and improving throughput.

---

# 27. How do you call multiple downstream APIs in parallel using WebClient?

## Answer

Use **Mono.zip()** to execute independent API calls concurrently.

### Example

```java
Mono<Customer> customer = customerClient.getCustomer(id);

Mono<Account> account = accountClient.getAccount(id);

Mono<Reward> reward = rewardClient.getReward(id);

return Mono.zip(customer, account, reward)
        .map(tuple -> new CustomerResponse(
                tuple.getT1(),
                tuple.getT2(),
                tuple.getT3()
        ));
```

---

## Benefits

- Parallel execution
- Reduced response time
- Better resource utilization

---

## Real-Time Example

Instead of waiting:

- Customer API → 300 ms
- Account API → 300 ms
- Rewards API → 300 ms

Sequential calls would take ~900 ms.

With `Mono.zip()`, all calls run concurrently, reducing total response time to around **300–350 ms**.

---

# 28. How do you handle exceptions, retries, and fallback in Spring WebFlux?

## Answer

Project Reactor provides operators for robust error handling.

### Example

```java
return webClient.get()
        .uri("/customers")
        .retrieve()
        .bodyToMono(Customer.class)
        .timeout(Duration.ofSeconds(2))
        .retry(3)
        .onErrorResume(ex ->
                Mono.just(new Customer("Default Customer")));
```

---

## Explanation

- `timeout()` → Fails if the API takes too long.
- `retry()` → Retries failed requests.
- `onErrorResume()` → Returns a fallback response instead of failing.

---

## Real-Time Example

If the Rewards Service is unavailable, we return default reward information instead of failing the entire Customer Dashboard API.

---

# 29. What is Backpressure in Reactive Programming, and how does Project Reactor handle it?

## Answer

Backpressure is a mechanism that prevents a **fast producer** from overwhelming a **slow consumer**.

Instead of sending unlimited data, the consumer requests data at a rate it can process.

---

## Example

Without Backpressure:

```
Producer

↓

1 Million Events

↓

Consumer

↓

Memory Overflow
```

With Backpressure:

```
Producer

↓

100 Events

↓

Consumer Processes

↓

Requests Next 100 Events
```

---

## How does Project Reactor handle Backpressure?

Project Reactor implements the **Reactive Streams Specification**, allowing subscribers to control how many items they receive.

---

## Real-Time Example

Suppose Kafka publishes millions of events.

A slow consumer can request only a limited number of events at a time, preventing memory issues and ensuring stable processing.

---

# Interview Tips

- Always explain with a real-time project example.
- Mention performance improvements wherever possible.
- Explain why you chose a particular technology.
- Highlight scalability, resiliency, and fault tolerance.
- For Reactive Programming questions, emphasize **non-blocking I/O**, **parallel API calls**, and **better resource utilization**.
