---
title: Projects
icon: fas fa-code
order: 2
layout: single # Changed from 'default' or inferred to 'single' for Minimal Mistakes
---

# 🚀 Automation Projects

Each case study reflects real-world automation using scalable, CI/CD-integrated frameworks across healthcare, finance, and API platforms.

---

## 🩺 Cigna – Healthcare API & Kafka Automation

**🛠 Tech Stack:** Karate DSL, Pact, Cypress, GraphQL, Kafka, JUnit, Jenkins, AWS  
**📍 Domain:** Claims, Billing, Appointments (FHIR/HL7)

### 🔍 Highlights:
- Built 50+ Karate test suites for FHIR REST APIs with nested JSON assertions
- Kafka validation using Avro schemas + Karate retryUntil blocks
- GraphQL queries + mutation testing with Karate's built-in support
- Karate Mock Server + WireMock to simulate downstream failures
- Dynamic JWT generation with scenario outlines and reusable glue

### 🧪 Sample Karate Feature:
```gherkin
Feature: Validate patient API with token and JSONPath assertions

Background:
  * def token = call read('classpath:helpers/token.feature')
  * configure headers = { Authorization: 'Bearer ' + token }

Scenario: Verify active patient details
  Given url baseUrl + '/patient/12345'
  When method GET
  Then status 200
  And match response.name[0].family == 'Doe'
  And match response.active == true
📸 Allure dashboard with Jenkins nightly job integrations

💰 FHL Bank – Financial Microservices Testing
🛠 Tech Stack: Karate DSL, Pact, Cypress, Kafka, Avro, Docker, GitHub Actions
📍 Domain: Options Trading, Loan Processing

🔍 Highlights:

Full-stack UI + API testing for trade workflows using Cypress + Karate
Pact-based contract testing between internal and third-party microservices
Kafka topic testing with Avro schema validation and async polling
Executed parallel Dockerized tests across GitHub Actions runners
🧪 Pact Mock (JSON):

{
  "consumer": { "name": "TradeFrontend" },
  "provider": { "name": "LoanService" },
  "interactions": [
    {
      "description": "get loan details",
      "request": { "method": "GET", "path": "/loan/456" },
      "response": {
        "status": 200,
        "body": { "amount": 100000, "currency": "USD" }
      }
    }
  ]
}
📸 Cypress UI screenshot with DOM + API hook validations

🛠 Hybrid API Framework – Karate + Postman + Newman + Cucumber
🛠 Tech Stack: Karate, Postman, Newman, Java, Maven, OAuth2, Allure, Jenkins
📍 Domain: Generic REST/SOAP APIs, Auth, Contract Mocking

🔍 Highlights:

Karate for BDD-style API testing + token auth integration
Postman for manual/exploratory + Newman for CLI-based smoke
Reusable step definitions and global payload injections
Combined Allure + Newman reports for unified result analysis
🧪 Reusable Karate Java Function:

Java
* def getToken =
"""
function() {
  var res = karate.call('classpath:helpers/oauth2.feature');
  return res.token;
}
"""
* configure headers = { Authorization: 'Bearer ' + getToken() }
📸 Unified Allure report + HTML test result dashboard

✅ Key Outcomes:

Real-world automation applied to production microservices
CI/CD-integrated tests using Docker, GitHub Actions, Jenkins
Rich reporting, contract safety, mock-driven development
