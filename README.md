📜 API Testing with Playwright (Java)

# 🎭 Playwright API Testing with Java  

![Playwright Logo](https://playwright.dev/img/playwright-logo.svg)  

## 📖 Introduction  
This repository contains an **API Testing Framework** using [Microsoft Playwright](https://playwright.dev/java/) with **Java**.  
Playwright enables **fast, reliable, and cross-browser API testing** with built-in network request capabilities.  

---

## 🚀 Features  
✅ **REST API Testing (GET, POST, PUT, DELETE)**  
✅ **Request & Response Validations**  
✅ **JSON Schema Validation**  
✅ **Assertions with JUnit/TestNG**  
✅ **Authentication (OAuth, JWT, API Keys)**  
✅ **CI/CD Integration (GitHub Actions, Jenkins)**  
✅ **Allure & HTML Reporting**  

---

## 🛠️ Tech Stack  
- **Language:** Java (JDK 11+)  
- **Test Runner:** JUnit / TestNG  
- **Assertions:** JUnit Assertions  
- **HTTP Client:** Playwright APIRequestContext  
- **Build Tool:** Maven  
- **Reporting:** Allure / HTML Reports  
- **CI/CD:** GitHub Actions, Jenkins  

---

## 📂 Project Structure  
playwright-api-testing/ │-- src/ │ ├── test/ │ │ ├── GetUserTest.java # Sample GET API Test │ │ ├── PostUserTest.java # Sample POST API Test │ ├── main/ │ │ ├── utils/ # Utility Functions │ │ │ ├── ApiHelper.java # API Helper Methods │-- test-results/ # Test Reports │-- pom.xml # Maven Dependencies & Plugins │-- playwright.config.json # Playwright Configuration │-- README.md # Project Documentation


---

## 📦 Installation  
Make sure **Java 11+** and **Maven** are installed.  

1️⃣ Clone the Repository  
git clone https://github.com/yourusername/playwright-api-testing.git
cd playwright-api-testing

2️⃣ Install Dependencies
mvn clean install

3️⃣ Run API Tests
mvn test

📝 Sample GET API Test (src/test/GetUserTest.java)
import com.microsoft.playwright.*;
import com.microsoft.playwright.options.*;
import org.junit.jupiter.api.*;

public class GetUserTest {
    private static Playwright playwright;
    private static APIRequestContext request;

    @BeforeAll
    static void setup() {
        playwright = Playwright.create();
        request = playwright.request().newContext();
    }

    @Test
    void getUserDetails() {
        APIResponse response = request.get("https://jsonplaceholder.typicode.com/users/1");
        Assertions.assertEquals(200, response.status());
        System.out.println("Response Body: " + response.text());
    }

    @AfterAll
    static void teardown() {
        playwright.close();
    }
}

📝 Sample POST API Test (src/test/PostUserTest.java)
import com.microsoft.playwright.*;
import org.junit.jupiter.api.*;

import java.util.*;

public class PostUserTest {
    private static Playwright playwright;
    private static APIRequestContext request;

    @BeforeAll
    static void setup() {
        playwright = Playwright.create();
        request = playwright.request().newContext();
    }

    @Test
    void createUser() {
        Map<String, Object> requestBody = new HashMap<>();
        requestBody.put("name", "John Doe");
        requestBody.put("email", "johndoe@example.com");

        APIResponse response = request.post("https://jsonplaceholder.typicode.com/users",
                RequestOptions.create().setData(requestBody));

        Assertions.assertEquals(201, response.status());
        System.out.println("Response Body: " + response.text());
    }

    @AfterAll
    static void teardown() {
        playwright.close();
    }
}

⚙️ Playwright Configuration (playwright.config.json)
{
  "use": {
    "headless": true,
    "trace": "on-first-retry"
  }
}

📊 Test Reports & Tracing
1. Run tests with trace enabled:
mvn test -Dtrace=on

2. Open Test Report UI:
mvn allure:serve

🤖 CI/CD Integration
GitHub Actions Workflow (.github/workflows/playwright-api.yml)
name: Playwright API Tests (Java)

on:
  push:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Set up Java
        uses: actions/setup-java@v3
        with:
          distribution: 'temurin'
          java-version: '11'

      - name: Install Dependencies
        run: mvn clean install

      - name: Run Playwright API Tests
        run: mvn test

      - name: Upload Test Report
        uses: actions/upload-artifact@v3
        with:
          name: test-report
          path: target/surefire-reports/

📖 Documentation & Resources
Playwright for Java Official Docs
Maven Dependency for Playwright
JUnit 5 Documentation
Allure Reports for Playwright

💡 Contribution
Feel free to fork this repository and submit pull requests with improvements or additional test cases!

📜 License
This project is licensed under the MIT License.

🚀 Happy API Testing with Playwright & Java! 🎭
