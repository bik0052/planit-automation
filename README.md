# Planit Technical Assessment – Selenium + Maven (TestNG)

Automation for **Jupiter Toys** demo site using **Selenium 4**, **TestNG**, and **Page Object Model**.

## Tech
- Java 11+
- Maven
- Selenium 4 + TestNG
- WebDriverManager (auto driver)
- GitHub Actions + Jenkins pipelines (headless Chrome)

## Test cases
- **TC1:** Contact form – submit empty, verify errors, fill mandatory fields, verify errors cleared.
- **TC2:** Contact form – fill & submit, verify success message. (Executed 5 times)
- **TC3:** Shop/Cart – add *2 Stuffed Frog*, *5 Fluffy Bunny*, *3 Valentine Bear*; verify unit prices, subtotals and grand total.

## Project Structure
```
src/
  main/java/com/planit/pages/.. (Page Objects)
  main/java/com/planit/utils/DriverFactory.java, Money.java
  test/java/com/planit/tests/.. (TestNG tests)
  test/resources/testng.xml
```

## Local Run
1. Install **Java 11+** and **Maven** (`mvn -v`).
2. Install **Google Chrome**.
3. Run all tests (headless):
   ```bash
   mvn clean test -Dheadless=true
   ```
   Run headed (visible browser):
   ```bash
   mvn clean test -Dheadless=false
   ```
4. Reports: `target/surefire-reports/` (HTML summary and XML).

## GitHub Actions
Workflow at `.github/workflows/ci.yml` runs tests on push/PR, in headless Chrome and uploads surefire reports as an artifact.

## Jenkins
Use the included `Jenkinsfile`. It checks out code, runs `mvn clean test -Dheadless=true`, and archives surefire reports.

## Notes
- Base URL: `http://jupiter.cloud.planittesting.com`
- Page Objects prefer stable selectors (ids/text). Prices are read from Shop page and compared with Cart values.
