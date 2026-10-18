# Automation Exercise Test Suite

An end-to-end QA automation project for the [Automation Exercise](https://automationexercise.com) practice site. It covers both **UI** and **API** testing in Python, uses the **Page Object Model**, runs in **GitHub Actions**, and is packaged with **Docker**.

## Tech Stack

| Area | Tools |
|---|---|
| Language | Python |
| Test framework | pytest |
| UI automation | Playwright |
| API testing | requests |
| Flaky test handling | pytest-rerunfailures, Playwright traces |
| CI | GitHub Actions |
| Containers | Docker |

## What's Covered

### UI tests: `tests/ui/`

- **Account:** register user, login, registration with an existing email (error case)
- **Products:** verify products, search, view category and brand products
- **Cart:** add to cart, add from recommended items, remove products from cart
- **Checkout and orders:** order while registering, register before checkout, login before checkout, verify the address on the checkout page, download invoice after order
- **Product reviews:** add a review on a product
- **Other pages:** contact form, subscription, scroll up and down

### API tests: `tests/api/`

- **Products:** list, search
- **Brands:** list
- **Account:** create and delete, get details, update
- **Login:** valid and invalid credentials

## Project Structure

```
automation_exercise/
├── .github/workflows/
│   └── tests.yml          # CI pipeline
├── api/                   # API client helpers (products, brands, login, account...)
├── pages/                 # Page Objects (cart, checkout, payment, login, register...)
├── tests/
│   ├── api/               # API tests
│   └── ui/                # UI tests
├── conftest.py            # Shared fixtures
├── pytest.ini             # pytest configuration
├── requirements.txt
├── Dockerfile
└── README.md
```

## Design Notes

- **Page Object Model.** Each page of the site has its own class in `pages/`, so locators and page actions live in one place and tests stay short and readable.
- **API helpers.** Request logic is separated into `api/`, and the tests in `tests/api/` only handle the calls and assertions.
- **Flaky test handling.** Failed tests are retried with `pytest-rerunfailures`, and Playwright traces are kept so a failure can be replayed and inspected.
- **End-to-end flows.** The checkout tests cover the full path from adding products to paying and downloading the invoice.

## Getting Started

### 1. Clone and install

```bash
git clone https://github.com/lovecraft409/automation_exercise.git
cd automation_exercise

python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

pip install -r requirements.txt
playwright install
```

### 2. Run the tests

Run everything:

```bash
pytest
```

Run one suite:

```bash
pytest tests/api
pytest tests/ui
```

Run the UI tests with a visible browser:

```bash
pytest tests/ui --headed
```

### 3. Run in Docker

```bash
docker build -t automation-exercise .
docker run --rm automation-exercise
```

## Continuous Integration

The workflow in `.github/workflows/tests.yml` installs dependencies, sets up Playwright, and runs the tests on every push, so a broken change is caught right away.

## Author

**lovecraft409**. Learning QA automation with a focus on Python, CI/CD, and containers.
