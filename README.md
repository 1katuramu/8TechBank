# 8TechBank — Security Assessment

## BSE 4202: Software Security Practical Assignment

### Group BSE26-9 | Makerere University | May 2026

## Group Members

- Kitonsa Elvis - 20/U/7785/PS
- Katuramu Edgar - 22/U/21756/PS
- Asiimire Patricia - 21/U/19271/PS
- Kizito Daniel Jr. - 19/U/8282/EVE

## Project Structure

    8TechBank/
    ├── src/
    │   ├── vulnerable/     <- Deliberately vulnerable app (port 5000)
    │   ├── secure/         <- Fixed secure app (port 5001)
    │   └── requirements.txt
    ├── exploits/           <- CSRF attack proof-of-concept files
    ├── screenshots/        <- All evidence screenshots
    ├── report/             <- Security assessment report and documents
    ├── Dockerfile
    ├── docker-compose.yml
    └── README.md

## Setup Instructions

### Prerequisites

- Python 3.10 or higher
- pip

### Installation

    # Navigate to project folder
    cd 8TechBank

    # Create virtual environment
    python -m venv venv

    # Activate virtual environment (Windows)
    venv\Scripts\activate

    # Install dependencies
    pip install -r src/requirements.txt

### Running the Vulnerable App (Tasks 1 and 2)

    cd src/vulnerable
    python app.py
    # Visit http://127.0.0.1:5000

### Running the Secure App (Tasks 3 and 4)

    cd src/secure
    python app.py
    # Visit http://127.0.0.1:5001

## Test Credentials

| Username | Password    | Role  |
| -------- | ----------- | ----- |
| alice    | password123 | user  |
| bob      | qwerty456   | user  |
| admin    | admin123    | admin |

## Testing the API (Secure App Only)

Get a JWT token:

    Invoke-WebRequest -Uri "http://127.0.0.1:5001/api/auth/token" -Method POST -ContentType "application/json" -Body '{"username":"alice","password":"password123"}' | Select-Object -ExpandProperty Content

Access protected endpoint (replace TOKEN with actual token):

    Invoke-WebRequest -Uri "http://127.0.0.1:5001/api/account" -Method GET -Headers @{Authorization="Bearer TOKEN"} | Select-Object -ExpandProperty Content

Test rate limiting (run 6 times to trigger 429):

    Invoke-WebRequest -Uri "http://127.0.0.1:5001/api/auth/token" -Method POST -ContentType "application/json" -Body '{"username":"wrong","password":"wrong"}' | Select-Object -ExpandProperty Content

## Exploit Files

| File                             | Description                                        |
| -------------------------------- | -------------------------------------------------- |
| exploits/csrf_attack.html        | CSRF attack against vulnerable app (port 5000)     |
| exploits/csrf_attack_secure.html | CSRF attack attempt against secure app (port 5001) |

Open these files directly in Chrome while authenticated to demonstrate the attack.

## Ethical Notice

All exploit demonstrations were conducted exclusively against
the locally hosted 8TechBank application running on localhost.
No real systems were targeted. All testing complies with
Uganda's Computer Misuse Act, 2011.
