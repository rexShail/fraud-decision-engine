# Fraud Decision Engine

A real-time fraud detection and onboarding decision platform built with FastAPI.

Inspired by modern banking and fintech onboarding systems used for account opening, customer verification, fraud prevention, and risk assessment.

---

## Overview

Fraud Decision Engine evaluates customer onboarding requests and produces risk-based business decisions.

The platform combines:

- Business Rules
- Fraud Detection
- Risk Scoring
- Device Intelligence
- Velocity Checks
- Explainable Decisions
- Workflow Automation

The engine provides deterministic and transparent decisions suitable for regulated financial environments.

---

## Problem Statement

Banks and fintech companies face increasing fraud during customer onboarding.

Common threats include:

- Synthetic identities
- Identity theft
- Account takeover
- Device farms
- Velocity attacks
- Bonus abuse
- Multi-account fraud

Traditional onboarding systems rely on multiple independent checks.

This project centralizes those checks into a single decision platform.

---

## Architecture

                         +------------------+
                         | Customer Request |
                         +---------+--------+
                                   |
                                   v
                    +---------------------------+
                    | Risk Orchestration Engine |
                    +-----------+---------------+
                                |
            ---------------------------------------
            |            |           |            |
            v            v           v            v

      Device Risk   Identity    Velocity     Behavioral
       Service      Checks       Checks        Checks

            |            |           |            |
            ---------------------------------------
                                |
                                v

                    +--------------------+
                    | Scoring Engine     |
                    +----------+---------+
                               |
                               v

                    +--------------------+
                    | Decision Engine    |
                    +----------+---------+
                               |
               -------------------------------
               |             |               |
               v             v               v

            APPROVE       REVIEW          DECLINE

---

## Features

### Identity Verification

Validate:

- Name
- Email
- Phone
- Address
- SSN/PAN/Aadhaar (mock)

Supports integration simulation for:

- Socure
- Persona
- Experian
- LexisNexis

---

### Velocity Checks

Detect:

- Multiple applications from same user
- Multiple devices
- Multiple emails
- Multiple phone numbers
- Rapid application attempts

Examples:

- 5 applications within 24 hours
- 3 devices within 1 hour
- High-risk email reuse

---

### Device Intelligence

Analyze:

- Device Fingerprint
- Browser Signature
- Operating System
- Proxy Usage
- VPN Detection
- Emulator Detection

---

### Behavioral Analysis

Evaluate:

- Form completion speed
- Mouse movements
- Copy-paste frequency
- Application abandonment
- Suspicious navigation patterns

---

### Rules Engine

Business users can configure decision rules.

Example:

```json
{
  "rule_name": "high_risk_device",
  "conditions": [
    {
      "field": "device_risk_score",
      "operator": ">",
      "value": 80
    }
  ],
  "action": "DECLINE"
}
```

---

### Risk Scoring

Risk Score Range:

| Score | Decision |
|---------|----------|
| 0 - 30 | APPROVE |
| 31 - 70 | REVIEW |
| 71 - 100 | DECLINE |

Factors:

- Device Risk
- Identity Risk
- Behavioral Risk
- Velocity Risk
- Historical Fraud Signals

---

### Explainable Decisions

Every decision includes reasoning.

Example:

```json
{
  "decision": "REVIEW",
  "risk_score": 62,
  "reasons": [
    "Email used by multiple applications",
    "VPN detected",
    "High velocity activity"
  ]
}
```

---

## Tech Stack

### Backend

- FastAPI
- Python 3.12
- SQLAlchemy
- Pydantic

### Database

- PostgreSQL

### Caching

- Redis

### Infrastructure

- Docker
- Docker Compose

### Testing

- Pytest
- Locust

### Observability

- Prometheus
- Grafana

---

## API Endpoints

### Submit Application

```http
POST /applications
```

Request:

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@email.com",
  "phone": "9999999999",
  "device_id": "abc123",
  "ip_address": "10.0.0.1"
}
```

---

### Evaluate Application

```http
POST /applications/{id}/evaluate
```

---

### Retrieve Decision

```http
GET /applications/{id}/decision
```

---

### Rule Management

```http
GET /rules

POST /rules

PUT /rules/{rule_id}

DELETE /rules/{rule_id}
```

---

## Database Design

Tables:

- applications
- decisions
- fraud_signals
- rules
- devices
- customers
- velocity_events
- audit_logs

---

## Sample Workflow

1. Customer submits application
2. Device profile generated
3. Identity verification performed
4. Velocity checks executed
5. Business rules evaluated
6. Risk score calculated
7. Decision generated
8. Audit trail created

---

## Future Enhancements

### Machine Learning Risk Scoring

Implement:

- XGBoost
- LightGBM
- Random Forest

for predictive fraud detection.

### Event Driven Processing

Use:

- Kafka
- RabbitMQ

for real-time streaming decisions.

### Real-Time Monitoring

Support:

- Fraud Analytics Dashboard
- Operational Metrics
- Decision Analytics
- Alert Management

---

## Sample Decision Response

```json
{
  "application_id": "12345",
  "decision": "REVIEW",
  "risk_score": 68,
  "reasons": [
    "VPN Detected",
    "Email Reuse",
    "High Device Risk"
  ],
  "timestamp": "2026-11-20T15:00:00Z"
}
```

---

## Business Value

This project demonstrates:

- Fraud Prevention
- Fintech Engineering
- Decision Engines
- FastAPI Development
- System Design
- Risk Modeling
- Rules Engine Architecture
- Enterprise Software Patterns

---

## License

MIT
