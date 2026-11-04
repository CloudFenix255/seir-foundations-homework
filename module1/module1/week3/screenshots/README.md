# SEIR Foundations — Week 3: COBOL Bank Deployment

**Student:** Sid Owsley  
**Project:** SEIR Foundations  
**Environment:** AWS EC2 — Amazon Linux 2023

## Overview

For Week 3, I deployed the Balerica Legacy Bank application on an AWS EC2 instance and verified that the GnuCOBOL banking programs worked with the Python FastAPI application.

## Deployment

- Launched an EC2 t3.micro instance using an AWS launch template.
- Connected to the instance using SSH.
- Cloned the SEIR Foundations GitHub repository.
- Installed and tested the Legacy Bank COBOL application.
- Configured the Python virtual environment and started FastAPI using Uvicorn.

## Testing and Verification

I successfully completed the following tests:

1. COBOL account lookup for account 100001.
2. Verified that Alice Johnson's account was ACTIVE with a balance of $4,975.00 after the test payment.
3. Confirmed the FastAPI status endpoint was online.
4. Submitted a $25.00 USD payment using the FastAPI payment endpoint.
5. Verified that the payment was APPROVED and POSTED.
6. Retrieved the transaction history and confirmed the payment reference TXN0003.

## Evidence

Screenshots documenting the deployment and tests are included in this folder:

- Week3_LaunchTemplate.jpg
- Week3_instances.jpg
- week3_transaction.jpg
- Week3_AccountLookup.jpg
- Week3_API_Status.jpg
- Week3_TransactionHistory.jpg

## Conclusion

I successfully deployed the Legacy Bank application on AWS EC2 and verified that the COBOL programs and FastAPI endpoints were functioning together. The account lookup, API status, payment processing, and transaction history tests were completed successfully.


## Run 2 — Verification Results

I launched a second EC2 instance, SEIR-Week3-Run2, and verified the Balerica Legacy Bank application.

The FastAPI server initially stopped when my SSH connection was interrupted. I reconnected to EC2, restarted Uvicorn, and repeated the API tests.

| Test | Result |
| --- | --- |
| FastAPI `/status` | Passed — HTTP 200, API online |
| Account lookup `/accounts/100001` | Passed — Alice Johnson, ACTIVE, $4,975.00 |
| Transaction history `/transactions` | Passed — 1 POSTED transaction |
| Payment record | $25.00 USD, reference TXN0003 |

### Run 2 Evidence

[Run 2 Transaction History](Week3_Run2_TransactionHistory.jpg)

### What I Learned

I learned how to troubleshoot a FastAPI application on EC2, reconnect after an SSH connection was interrupted, restart Uvicorn, and verify API endpoints using curl.

## Week 3 — Final Verification (Runs 1–7)

I completed all seven deployment and verification runs for the Balerica Legacy Bank application on AWS EC2.

During the runs, I verified that:

- The FastAPI application was running and responding to requests.
- The GnuCOBOL banking application successfully retrieved account information.
- Account 100001 (Alice Johnson) was active with an initial balance of $5,000.00.
- A $25.00 USD payment was successfully processed with status POSTED and approval APPROVED.
- The account balance was updated to $4,975.00.
- The transaction history recorded the payment successfully.

For Run 7, the payment reference was `RUN7-TXN001`. I saved the API status, account lookup, and transaction history screenshots as evidence in the `screenshots` folder.

**Result:** All seven runs were completed successfully, and the verification screenshots were uploaded to GitHub.
