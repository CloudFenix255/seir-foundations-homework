Week 3 — COBOL lab evidence screenshots

## Run 1 — Manual Remediation and Verification

**Instance:** SEIR-Week3-Run1  
**Environment:** AWS EC2, Amazon Linux 2023

The Balerica Legacy Bank application did not initially deploy correctly through the automated installation. I completed the installation manually and verified that the COBOL banking application and FastAPI service were working.

During API testing, the account lookup endpoint returned HTTP 500 because the application did not have permission to access `/opt/balerica-bank/data/accounts.dat`.

I corrected the file ownership using:

`sudo chown ec2-user:ec2-user /opt/balerica-bank/data/accounts.dat`

After restarting FastAPI, I repeated the API tests.

### Verification Results

| Test | Result |
|---|---|
| COBOL account lookup | Passed |
| FastAPI startup | Passed |
| GET `/status` | HTTP 200 |
| GET `/accounts/100001` | HTTP 200 — Alice Johnson, ACTIVE, $5,000 |
| GET `/transactions` | HTTP 200 — no transactions recorded |

### Evidence

- [Run 1 API Status](Week3_Run1_API_Status.jpg)
- [Run 1 Account Lookup](Week3_Run1_Account_API.jpg)
- [Run 1 Transaction History](Week3_Run1_Transactions.jpg)

### What I Learned

This lab helped me understand how Linux file ownership and permissions can affect an application even when the service starts successfully. I also practiced troubleshooting API errors using HTTP response codes, Uvicorn logs, and command-line tests.
