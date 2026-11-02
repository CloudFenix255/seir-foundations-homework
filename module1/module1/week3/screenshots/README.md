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
