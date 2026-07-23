# 1. Self Introduction with your Real-Time Project

## Answer

Hi, I'm Venkatesh, and I have around **5+ years of experience** as a Java Backend Developer specializing in **Java 8/17, Spring Boot, Spring WebFlux, Microservices, Kafka, REST APIs, Cassandra, PostgreSQL, Docker, Kubernetes, and CI/CD**.

Currently, I'm working on the **American Express MARS Platform**, which is a Microservices-based financial application responsible for managing customer accounts, payments, refunds, and financial obligations.

### My Responsibilities

- Develop REST APIs using Spring Boot and Spring WebFlux.
- Build Reactive APIs using Mono and Flux.
- Integrate downstream services using Spring WebClient.
- Publish and consume Kafka events.
- Write Unit Test cases using JUnit5 and Mockito.
- Resolve Production Issues.
- Optimize API performance.
- Deploy applications through Jenkins and Kubernetes.

### Achievement

One of my key achievements was reducing API response time from **2.5 seconds to 800 milliseconds** by implementing parallel API calls using WebClient and optimizing database queries.

---

# 2. How do you write Unit Test cases for Reactive Programming methods that return Mono and Flux?

## Answer

Reactive APIs are tested using:

- JUnit 5
- Mockito
- Reactor Test (StepVerifier)

StepVerifier is provided by **reactor-test** and is used to validate Mono and Flux.

### Maven Dependency

```xml
<dependency>
    <groupId>io.projectreactor</groupId>
    <artifactId>reactor-test</artifactId>
    <scope>test</scope>
</dependency>
```

### Service

```java
public Mono<String> getUser() {
    return Mono.just("Venkatesh");
}
```

### Unit Test

```java
@Test
void testGetUser() {

    StepVerifier.create(service.getUser())
            .expectNext("Venkatesh")
            .verifyComplete();

}
```

### Flux Example

```java
Flux<Integer> numbers = Flux.just(1,2,3);
```

```java
@Test
void testFlux(){

    StepVerifier.create(numbers)
            .expectNext(1)
            .expectNext(2)
            .expectNext(3)
            .verifyComplete();

}
```

### Real-Time

In our project, we use

- Mockito
- JUnit5
- StepVerifier

to validate Reactive APIs.

---

# 3. What are the biggest challenges you have faced while working with Microservices, and how did you overcome them?

## Answer

One major challenge was **high API response time**.

Our Customer Dashboard API was calling multiple downstream services sequentially.

```
Customer Service

↓

Account Service

↓

Rewards Service

↓

Transaction Service
```

Total response time was around **3 seconds**.

### Solution

We replaced sequential calls with **Spring WebClient** and **Mono.zip()**.

```java
Mono.zip(customer, account, reward)
```

All APIs were called in parallel.

### Result

- Response time reduced from **3 seconds to around 900 milliseconds**.
- Better scalability.
- Improved customer experience.

Another challenge was duplicate Kafka events.

We implemented **Idempotency** using a unique Transaction ID to prevent duplicate processing.

---

# 4. How do you implement logging in your Spring Boot Microservices? Which logging framework do you use?

## Answer

Spring Boot uses **SLF4J** with **Logback** as the default logging framework.

We create a logger using Lombok.

```java
@Slf4j
@Service
public class UserService {

}
```

Without Lombok

```java
private static final Logger log =
LoggerFactory.getLogger(UserService.class);
```

### Logging Levels

```java
log.info("User Created");

log.debug("Customer Request {}", request);

log.warn("Invalid Customer");

log.error("Database Connection Failed", ex);
```

### Best Practices

- Never log passwords.
- Log Correlation IDs.
- Log request and response time.
- Log exceptions with stack traces.

---

# 5. Which monitoring and observability tools have you used in your project, and how do you monitor application health and performance?

## Answer

In my project, we use

- Zipkin
- Spring Boot Actuator
- Prometheus
- Grafana
- Kibana (ELK)
- Splunk (depending on the project)

### What we monitor

- API Response Time
- CPU Usage
- Memory Usage
- Error Rate
- Kafka Consumer Lag
- Database Connections

### Example

Spring Boot Actuator

```
/actuator/health

/actuator/metrics

/actuator/prometheus
```

Grafana Dashboard

Shows

- Request Count
- Response Time
- JVM Memory
- Active Threads

---

# 6. How do you debug production issues in a Reactive Spring WebFlux application?

## Answer

Whenever a production issue occurs, I follow these steps.

### Step 1

Check application logs.

### Step 2

Verify response time in monitoring dashboards.

### Step 3

Check downstream services.

### Step 4

Check Kafka consumers.

### Step 5

Verify database queries.

### Step 6

Identify the Root Cause.

### Step 7

Deploy the fix.

### Real-Time Example

One API was taking **5 seconds**.

Investigation showed one downstream API was timing out.

We added

```java
.timeout(Duration.ofSeconds(2))
.retry(3)
.onErrorResume(...)
```

The API returned a fallback response instead of failing.

---

# 7. How do you trace and debug a request across multiple Microservices using distributed tracing tools like Zipkin or Spring Cloud Sleuth?

## Answer

When a request travels across multiple Microservices, debugging becomes difficult.

We use

- Spring Cloud Sleuth
- Zipkin

to trace the complete request.

### Flow

```
Client

↓

API Gateway

↓

Customer Service

↓

Account Service

↓

Rewards Service

↓

Notification Service
```

Sleuth automatically generates

- Trace ID
- Span ID

Example

```
Trace Id

8ab7d2...

Span Id

4df89...
```

Every Microservice logs the same Trace ID.

Zipkin displays the entire request flow.

### Benefits

- Easy debugging.
- Identify slow Microservices.
- Measure API latency.
- End-to-end request tracing.

### Real-Time Example

A customer API was taking **4 seconds**.

Using Zipkin, we found the delay was in the Rewards Service.

After optimizing that service, the total response time reduced to **900 milliseconds**.

## Interview Tip

If the interviewer asks,

**"How do you debug a request across 10 Microservices?"**

Answer:

"We use Spring Cloud Sleuth to generate Trace IDs and Zipkin to visualize the complete request flow. Using the Trace ID, we can identify exactly which Microservice is causing the delay or failure."
