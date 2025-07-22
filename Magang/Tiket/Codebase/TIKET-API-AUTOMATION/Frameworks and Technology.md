## **Core Tech Stack & Frameworks**

### **1. Testing Frameworks**

- **TestNG** (v7.6.1) - Main testing framework for organizing and running tests
- **Rest Assured** (v5.3.2) - Primary framework for API testing and HTTP request/response handling
- **Hamcrest** (v2.1) - Assertion library for readable test assertions

### **2. Build & Dependency Management**

- **Maven** - Build tool and dependency management
- **Java 17** - Programming language version

### **3. Communication Protocols**

- **gRPC** - For microservice communication (you can see `IntegratorHotel.IntegratorHotel` and `rpcIntegratorGrpc` imports)
- **Protocol Buffers** - For data serialization (see `integratorHotel.proto` file)
- **REST APIs** - HTTP-based API communication

### **4. JSON Processing & Data Handling**

- **Jackson** (v2.14.0) - JSON serialization/deserialization (`ObjectMapper`)
- **Gson** (v2.9.0) - Alternative JSON processing
- **JSON Simple** - Basic JSON parsing
- **Apache POI** (v5.2.2) - Excel file processing for test data

### **5. Database Integration**

- **MongoDB Driver** (v3.12.14) - NoSQL database connectivity
- **Redis (Jedis)** (v2.8.1) - In-memory data structure store
- **MySQL** - Relational database (based on properties files)

### **6. Reporting & Logging**

- **ExtentReports** (v5.0.9) - Test reporting framework
- **Log4j2** (v2.17.2) - Logging framework
- **SLF4J** (v1.7.36) - Logging abstraction

### **7. Utility Libraries**

- **Apache Commons Lang3** (v3.11) - Utility methods
- **Google Guava** (v31.1-jre) - Collections and utilities
- **Lombok** (v1.18.24) - Reduces boilerplate code
- **JavaFaker** (v1.0.2) - Test data generation
- **Awaitility** - Asynchronous testing utilities

### **8. Web Testing (Optional)**

- **Selenium WebDriver** (v4.5.0) - Web browser automation
- **Appium** (v8.2.0) - Mobile testing

### **9. Google Services Integration**

- **Google Sheets API** - For external test data management
- **OAuth2** - Authentication