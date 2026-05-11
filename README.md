# Refund-Risk-Repository
Most tools focus on:  fraud detection payment authorization analytics after the fact  Very few focus specifically on:  “Will this customer probably refund this order even if the payment is legitimate?”
# Refund Risk API

A production-style FastAPI service that scores e-commerce orders for refund risk.

## Features
- API key authentication
- Order, customer, and product persistence
- Explainable refund-risk scoring
- Batch scoring
- Risk analytics
- Adjustable model weights
- SQLite by default, PostgreSQL-ready via SQLAlchemy

## Run locally

```bash
pip install -r requirements.txt
uvicorn app.main:app --reload
```

## Environment variables

- `APP_NAME` — app name
- `ENVIRONMENT` — development / production
- `DATABASE_URL` — defaults to `sqlite:///./refund_risk.db`
- `API_KEYS` — comma-separated list of accepted API keys
- `DEFAULT_HIGH_RISK_THRESHOLD` — default `0.75`
- `DEFAULT_MEDIUM_RISK_THRESHOLD` — default `0.45`

## Example auth

Send this header with every request:

```http
X-API-Key: dev-key-123
```

## Main endpoints

- `POST /v1/predict/refund-risk`
- `POST /v1/orders`
- `GET /v1/orders/{order_id}`
- `GET /v1/customers/{customer_id}/risk-profile`
- `GET /v1/products/{sku}/risk-trends`
- `POST /v1/batch/predict`
- `GET /v1/analytics/overview`
- `GET /health`

## Notes

This project uses a rule-based scoring engine with persistent weights and explanations.
It is designed to be easy to ship, extend, and replace later with a learned model.
