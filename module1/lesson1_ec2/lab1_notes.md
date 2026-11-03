# SEIR Foundations — Lesson 1 Lab Notes

**Student:** Sid Owsley  
**Assignment:** Week 3 — EC2 and COBOL Banking  
**Environment:** AWS EC2, Amazon Linux 2023

## Initial Deployment Practice — November 2, 2026

**Instance ID:** i-0fce237d4cf96e52e  
**Status:** Initial deployment completed; qualification as one of the seven required lab runs has not been verified.

### What I Did

I launched an EC2 t3.micro instance and connected to it using SSH from Windows PowerShell. I worked through installing the Balerica Legacy Bank application, configuring Python FastAPI, and testing the COBOL banking programs.

The deployment required some troubleshooting because the application wasn't installed correctly during the initial setup.

### Problems I Encountered and How I Fixed Them

**1. Missing Legacy Bank application**

The `/opt/balerica-bank` directory wasn't available after the initial deployment. I manually cloned the SEIR Foundations repository and ran the installation script.

**2. SSH connection problems**

My SSH sessions disconnected while I was working. I learned how to reconnect to EC2 and restart the FastAPI application when necessary.

**3. FastAPI payment request error**

My initial payment request failed with HTTP 422 because of a JSON formatting problem. I corrected the request using Python and successfully submitted a payment.

### Commands I Used

Connect to EC2:

```bash
ssh -i "SEIR-Lab-Key.pem" ec2-user@<EC2-PUBLIC-IP>
```

Start FastAPI:

```bash
cd /opt/balerica-bank
source venv/bin/activate
uvicorn app.main:app --host 127.0.0.1 --port 8000
```

Test the account lookup:

```bash
./cobol/bin/account_lookup 100001
```

Check API status:

```bash
curl -s http://127.0.0.1:8000/status
```

View transactions:

```bash
curl -s http://127.0.0.1:8000/transactions
```

### Verification Results

- Successfully retrieved Alice Johnson's account information.
- Verified that the FastAPI service was online.
- Successfully processed a $25.00 payment.
- Confirmed the payment was POSTED and APPROVED.
- Verified the account balance was $4,975.00.
- Confirmed the transaction appeared in the transaction history.

An exact API response field I observed was:

```text
"core_banking":"GnuCOBOL"
```

### What I Learned

I learned more about connecting to EC2 using SSH, navigating Linux directories, troubleshooting installation problems, and managing a Python virtual environment.

I also gained a better understanding of how a COBOL banking application can communicate with a modern REST API.

## Mistakes I Made

- Initially used incorrect EC2 User Data.
- Assumed the application installation had completed successfully.
- Had trouble distinguishing between my local PowerShell terminal and my EC2 SSH session.
- Submitted a payment request with incorrectly formatted JSON.

## Commands I Now Know by Heart

- `pwd`
- `ls`
- `cd`
- `ssh`
- `git clone`
- `source venv/bin/activate`
- `uvicorn`
- `curl`

## Upcoming Lab Runs

The seven required manual deployments will be recorded separately with their actual instance IDs, screenshots, boot times, troubleshooting notes, and results.

## COBOL Practice

Return codes 0, 4, 8, and 12, along with fixed-width ledger decoding, will be documented after completing and verifying each test.

## COBOL Practice — November 3, 2026

**Instance ID:** `i-0fce237d4cf96e52e`  
**Environment:** Amazon Linux 2023  
**Working directory:** `/opt/balerica-bank`

### Return Code 0 — Successful Account Lookup

Command:
`./cobol/bin/account_lookup 100001`

Output:
```text
ACCOUNT=100001
NAME=Alice Johnson
STATUS=ACTIVE
BALANCE=4975.00
CURRENCY=USD
```

Exit code: `0`

### Return Code 4 — Account Not Found

Command:
`./cobol/bin/account_lookup 999999`

Output:
```text
ERROR=ACCOUNT NOT FOUND
```

Exit code: `4`

### Return Code 8 — Business Rejection

Command:
`./cobol/bin/payment_post TXN-SO-0008 100001 0.00 USD TEST-RC8`

Output:
```text
TXN=TXN-SO-0008
ACCOUNT=100001
AMOUNT=0.00
CURRENCY=USD
STATUS=REJECTED
REASON=AMOUNT MUST BE GREATER THAN ZERO
```

Exit code: `8`

The payment was rejected because the amount was zero. This confirmed that the COBOL application enforced its business rules.

### Return Code 12 — Environment Failure

Commands:
```bash
cd /tmp
/opt/balerica-bank/cobol/bin/account_lookup 100001
echo $?
```

Output:
```text
ERROR=CANNOT OPEN data/accounts.dat
FILE-STATUS=35
```

Exit code: `12`

The program couldn't locate the expected account data because I ran it from the wrong directory.

### Fixed-Width Ledger Decoding

I examined `data/accounts.dat` using Linux commands to identify the character positions of the account fields.

| Field | Positions | Value |
|---|---|---|
| Account number | 1–6 | 100001 |
| Account holder | 7–26 | Alice Johnson |
| Account status | 37–42 | ACTIVE |
| Balance | 45–56 | 000000497500 |

The account balance was stored as 497,500 cents, which equals **$4,975.00 USD**.

I used:

```bash
head -n 1 data/accounts.dat | cut -c45-56
```

And converted it into dollars using:

```bash
head -n 1 data/accounts.dat | cut -c45-56 | awk '{printf "$%.2f\n", $1/100}'
```

### What I Learned

I learned how COBOL uses return codes to distinguish between successful operations, missing accounts, business-rule violations, and environment problems. I also learned how to decode fixed-width ledger records using `cut -c`, including how to account for blank spaces within fields.

The rejected transaction `TXN-SO-0008` did not represent a successful payment. Alice Johnson's verified account balance remained $4,975.00 after the test.
