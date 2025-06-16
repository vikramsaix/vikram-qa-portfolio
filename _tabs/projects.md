---
title: "Projects"
layout: single
permalink: /projects/
author_profile: true
---

# 🚀 Automation Projects

Each case study reflects real-world automation using scalable, CI/CD-integrated frameworks across healthcare, finance, and API platforms.

---

## 🩺 Cigna – Healthcare API & Kafka Automation

**🛠 Tech Stack:** Karate DSL, Pact, Cypress, GraphQL, Kafka, JUnit, Jenkins, AWS  
**📍 Domain:** Claims, Billing, Appointments (FHIR/HL7)

**🔍 Highlights:**
- Built 50+ Karate test suites for FHIR REST APIs with nested JSON assertions
- Kafka validation using Avro schemas and `retryUntil` blocks
- GraphQL queries and mutation testing using Karate
- Karate Mock Server + WireMock for downstream simulations
- Dynamic JWT generation with reusable glue logic

**🧪 Sample Karate Feature:**

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
<!-- 📸 Allure dashboard with Jenkins nightly job integrations -->
💰 FHL Bank – Financial Microservices Testing

🛠 Tech Stack: Karate DSL, Pact, Cypress, Kafka, Avro, Docker, GitHub Actions
📍 Domain: Options Trading, Loan Processing

🔍 Highlights:

UI + API testing for trade workflows using Cypress + Karate
Pact contract testing between microservices
Kafka topic testing with Avro schema validation
Parallelized Dockerized tests via GitHub Actions
🧪 Pact JSON Contract:

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
<!-- 📸 Cypress UI screenshot with DOM + API hook validations -->
🧪 Hybrid API Framework – Karate + Postman + Newman + Cucumber

🛠 Tech Stack: Karate, Postman, Newman, Java, Maven, OAuth2, Allure, Jenkins
📍 Domain: Generic REST/SOAP APIs, Auth, Contract Mocking

🔍 Highlights:

Karate for BDD-style automation and token auth
Postman for manual testing, Newman for CLI regression
Shared step definitions and token handling
Allure + Newman reporting for unified test dashboards
🧪 Reusable Karate Function:

* def getToken =
"""
function() {
  var res = karate.call('classpath:helpers/oauth2.feature');
  return res.token;
}
"""
* configure headers = { Authorization: 'Bearer ' + getToken() }
<!-- 📸 Unified Allure report + HTML test result dashboard -->
✅ Key Outcomes:
Real-world automation applied to live microservices
CI/CD-integrated frameworks using Docker, Jenkins, GitHub Actions
Reporting, contract safety, and mock-driven testing at scale
