---

title: "Projects"
layout: single
permalink: /projects/
author\_profile: true
---------------------

# 🚀 Corporate QA Automation Projects

A curated collection of advanced automation frameworks applied in real-world corporate settings. These projects demonstrate full-stack QA strategy across healthcare, fintech, and microservices domains, with CI/CD pipelines, mocking, contract testing, and hybrid validations using modern tools.

---

## 🩺 Cigna Healthcare – FHIR API Automation & Kafka Event Validation

**📍 Domain:** U.S. Healthcare (FHIR/HL7 Patient Records, Appointments, Billing)
**🛠 Tech Stack:** Karate DSL, OAuth2, GraphQL, Kafka + Avro, Pact, Jenkins, AWS

**🔍 Project Overview:**
Developed a robust automation framework for validating FHIR-compliant APIs with secure token-based authentication. Integrated real-time Kafka event stream validation using Avro schemas. Enhanced resilience through dynamic retry mechanisms and GraphQL query validation. Pact contracts were used for testing provider-consumer agreements in distributed systems.

**💡 Key Features:**

* OAuth2 token acquisition and reuse using JS glue logic in Karate
* Retry logic for polling asynchronous API responses
* GraphQL API testing for nested patient attributes
* Kafka consumer automation using Avro schema and Java interop
* Contract testing using Pact with regex and type-based matching rules

**🧪 Sample Snippet: Retry & Regex Assertions in Karate**

```gherkin
Scenario: Validate active status of patient 12345
  Given url config.baseUrl + '/fhir/Patient/12345'
  When method GET
  Then retry until response.active == true
  And match response.name[0].family == '#regex [A-Z][a-z]+'
  And match response.telecom[*].system contains 'email'
```

**🧪 Sample Snippet: GraphQL Query Execution**

```gherkin
Scenario: Query patient status using GraphQL
  Given url config.graphqlEndpoint
  And request
    """
    {
      patient(id: "12345") {
        name { family given }
        active
        gender
      }
    }
    """
  When method POST
  Then status 200
  And match response.data.patient.active == true
```

---

## 💰 FHL Bank – Financial Microservices Automation with Pact & Kafka

**📍 Domain:** Trade Finance, Loan Origination, Event-Driven Architecture
**🛠 Tech Stack:** Karate DSL, Pact, Cypress, Kafka + Avro, GitHub Actions, Docker

**🔍 Project Overview:**
Built enterprise-grade contract and event-driven tests for microservices in a financial platform handling loan approvals and trading events. Used Pact for contract negotiation, Kafka for asynchronous message validation, and Cypress for end-to-end UI + backend correlation.

**💡 Key Features:**

* Pact contract with provider states and schema matching
* Kafka Avro validation with Java-based schema readers
* Dockerized test containers for CI parallelism
* Cypress hybrid tests for UI and API interaction
* GitHub Actions pipeline integration

**🧪 Sample Pact Contract for LoanService**

```json
{
  "consumer": { "name": "LoanFrontend" },
  "provider": { "name": "LoanService" },
  "interactions": [
    {
      "description": "Get loan details by ID",
      "providerState": "Loan with ID 456 exists",
      "request": {
        "method": "GET",
        "path": "/loan/456"
      },
      "response": {
        "status": 200,
        "body": {
          "loanId": 456,
          "amount": 150000,
          "currency": "USD",
          "status": "APPROVED"
        },
        "matchingRules": {
          "$.amount": { "match": "type" },
          "$.currency": { "match": "regex", "regex": "^[A-Z]{3}$" }
        }
      }
    }
  ]
}
```

**🧪 Sample Kafka + Avro Test Logic**

```gherkin
Scenario: Wait for approved loan event
  * def schema = read('classpath:schemas/loan-avro-schema.avsc')
  * def kafka = Java.type('utils.KafkaConsumerUtils')
  * def message = call retry until kafka.readAvro('loan-events', schema) match { loanId: 456, status: 'APPROVED' }
  Then assert message.amount >= 100000
```

---

## 🌐 Enterprise API Framework – Karate + Postman + OAuth2 + Allure

**📍 Domain:** Generic REST/SOAP APIs, Authentication Systems
**🛠 Tech Stack:** Karate, Postman, Newman, Java, Maven, Allure Reports, Jenkins

**🔍 Project Overview:**
Designed a shared enterprise automation framework combining Karate's BDD-style scripting with Postman collections for manual exploration. Used Newman CLI for batch regression, and generated Allure reports for unified dashboarding. Token handling was modularized via JS-based glue scripts.

**💡 Key Features:**

* Token refresh function using `karate.callSingle()`
* Reusable header configuration across test suites
* Integration with Allure reporting and Jenkins for CI
* Mocked OAuth scenarios for negative test coverage

**🧪 Sample Token Fetch and Configuration**

```js
function() {
  var auth = karate.callSingle('classpath:auth/refresh-token.feature');
  if (!auth || !auth.token) {
    karate.fail("Token fetch failed.");
  }
  return 'Bearer ' + auth.token;
}
```

```gherkin
* configure headers = { Authorization: getToken() }
```

---

## 🖥️ Cypress UI + Backend API Synchronization

**📍 Domain:** Loan Origination Portal, Trade Approval Dashboards
**🛠 Tech Stack:** Cypress, Axios, Node.js, GitHub Actions

**🔍 Project Overview:**
Created a hybrid test suite that validated both UI DOM updates and backend API calls for financial workflows. Used Cypress intercepts to catch outgoing loan requests and assert server-side payload correctness alongside user-facing notifications.

**💡 Key Features:**

* UI event simulation (form submission, alerts)
* API request intercept and schema assertion
* DOM updates and dashboard validation in real-time
* Integrated into CI workflows for nightly runs

**🧪 Sample Cypress UI + API Validation**

```js
describe('Loan approval - UI + API validation', () => {
  it('submits loan request and verifies backend API + UI', () => {
    cy.loginAs('approver')
    cy.visit('/loans/new')

    cy.get('#loan-amount').type('100000')
    cy.get('#submit-btn').click()
    cy.contains('Loan submitted successfully')

    cy.intercept('POST', '/api/loan').as('loanPost')
    cy.wait('@loanPost').then((interception) => {
      expect(interception.response.statusCode).to.eq(201)
      expect(interception.response.body).to.have.property('loanId')
    })

    cy.visit('/loans/dashboard')
    cy.contains('100000').should('exist')
  })
})
```

---

## ✅ Strategic Outcomes

* **CI/CD Ready:** Dockerized tests triggered via GitHub Actions and Jenkins
* **Contract-Driven:** Pact and Avro-based validations ensure schema integrity
* **Real-World Coverage:** Hybrid automation covering API, UI, and event streams
* **Reusable Architecture:** OAuth, retry logic, GraphQL, and mocks modularized

> 🧠 These corporate projects reflect enterprise maturity in QA engineering, designed to impress SDET recruiters, engineering leads, and automation architects.
